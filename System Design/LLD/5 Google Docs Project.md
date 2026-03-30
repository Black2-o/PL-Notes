# 05 — Real-World LLD: Document Editor (Google Docs)
### Applying OOP + SOLID to a Real Problem from Scratch

> 📺 Source: [Build Google Docs | A Real-World LLD Project](https://www.youtube.com/watch?v=MT9qZFGQXOU)

---

## 🎯 Problem Statement

Design a **Document Editor** (like Google Docs) that:
- Supports inserting **Text** and **Images** into a document
- Can **render** the document to show output
- Can **save** the document (to file or database)
- Is **scalable** — tomorrow should easily support Tables, Videos, NewLine, Bold, Fonts etc. without touching existing code

---

## 🧭 Design Approach: Bottom-Up

Two ways to approach any LLD problem:

| Approach | How it works |
|---|---|
| **Top-Down** | Start with the biggest/outermost object first, then drill into smaller ones |
| **Bottom-Up** | Build the smallest pieces first, then compose them into bigger classes |

We use **Bottom-Up** here. Most LLD interviews prefer this approach — build the atomic building blocks first, then wire them together.

---

## 🔴 Version 1 — The BAD Design

First instinct: dump everything into one `DocumentEditor` class.

```cpp
class DocumentEditor {
    vector<string> elements;       // text + image paths mixed together
    string renderedDocument;

public:
    void addText(string text)  { elements.push_back(text); }
    void addImage(string path) { elements.push_back(path); }

    string renderDocument() {
        if (!renderedDocument.empty()) return renderedDocument;
        string result = "";
        for (auto& el : elements) {
            // HACK: detect image by checking file extension
            if (el.size() > 4 && (el.substr(el.size()-4) == ".jpg"
                               || el.substr(el.size()-4) == ".png")) {
                result += "[Image: " + el + "]\n";
            } else {
                result += el + "\n";
            }
        }
        renderedDocument = result;
        return renderedDocument;
    }

    void saveToFile() {
        ofstream f("document.txt");
        if (f.is_open()) { f << renderDocument(); f.close(); }
    }
};
```

### Why this is BAD

| SOLID Principle | Status | Reason |
|---|---|---|
| **SRP** | ❌ | Handles adding, rendering, AND saving — 3 reasons to change |
| **OCP** | ❌ | Adding Video or Table element requires opening and modifying this class |
| **DIP** | ❌ | File I/O is hardcoded — tightly coupled to low-level details |

---

## ✅ Version 2 — The GOOD Design (Step by Step)

**Insight:** Break the single class into focused responsibilities.

```
Responsibilities to separate:
1. How each element renders itself      → DocumentElement hierarchy
2. Holding and managing the elements    → Document class
3. Saving to file or DB                 → Persistence hierarchy
4. The client-facing entry point        → DocumentEditor class
```

---

### Step 1 — DocumentElement Hierarchy

```cpp
// Abstract base — contract every element must fulfill
class DocumentElement {
public:
    virtual string render() = 0;
};

class TextElement : public DocumentElement {
    string text;
public:
    TextElement(string t) : text(t) {}
    string render() override { return text; }
};

class ImageElement : public DocumentElement {
    string imagePath;
public:
    ImageElement(string p) : imagePath(p) {}
    string render() override { return "[Image: " + imagePath + "]"; }
};

// Tomorrow, need NewLine? Just add a new class — zero existing code changes ✅
class NewLineElement : public DocumentElement {
public:
    string render() override { return "\n"; }
};
```

> **OCP in action:** Adding a new element type (Video, Table, Bold) = create a new subclass. Nothing else changes.

> **Polymorphism:** `el->render()` calls the right version at runtime depending on the actual object type.

---

### Step 2 — Document Class

```cpp
class Document {
    vector<DocumentElement*> elements; // 1-to-many with DocumentElement

public:
    void addElement(DocumentElement* el) {
        elements.push_back(el);
    }

    // Document delegates rendering to each element — it doesn't know HOW
    string render() {
        string result = "";
        for (auto& el : elements) {
            result += el->render() + "\n";
        }
        return result;
    }

    vector<DocumentElement*> getElements() { return elements; }
};
```

> **SRP:** Document only manages the list of elements and triggers their rendering. It does not know HOW to render text or images — that's each element's job.

> **Delegation:** Document loops over elements and calls `el->render()`. The element handles itself.

---

### Step 3 — Persistence Hierarchy

```cpp
// Abstract persistence — contract for any save strategy
class Persistence {
public:
    virtual void save(string content) = 0;
};

class SaveToFile : public Persistence {
public:
    void save(string content) override {
        ofstream f("document.txt");
        if (f.is_open()) { f << content; f.close(); }
        cout << "Saved to file\n";
    }
};

// Adding DB support = new class only, SaveToFile untouched ✅
class SaveToDB : public Persistence {
public:
    void save(string content) override {
        cout << "Saved to DB: " << content << "\n";
    }
};
```

> **OCP + DIP:** `DocumentEditor` depends only on the `Persistence` abstraction. Swap `SaveToFile` for `SaveToDB` or `SaveToCassandra` — the editor never knows or cares.

---

### Step 4 — DocumentEditor (Client-Facing Facade)

```cpp
class DocumentEditor {
    Document* doc;
    Persistence* db; // depends on ABSTRACTION, not concrete class ✅

public:
    DocumentEditor(Document* d, Persistence* p) : doc(d), db(p) {}

    void addText(string text) {
        doc->addElement(new TextElement(text)); // delegates to Document
    }

    void addImage(string path) {
        doc->addElement(new ImageElement(path)); // delegates to Document
    }

    string renderDocument() {
        return doc->render();                    // delegates to Document
    }

    void save() {
        db->save(renderDocument());              // delegates to Persistence
    }
};
```

> **SRP:** DocumentEditor is ONLY the entry point for the client. It holds references and delegates. It does nothing itself.

> **DIP:** `db` is `Persistence*` — not `SaveToFile*`. The actual object is injected from outside (Dependency Injection).

---

### Step 5 — Client Code

```cpp
int main() {
    Document* doc = new Document();
    Persistence* db = new SaveToFile(); // inject: swap to SaveToDB anytime

    DocumentEditor editor(doc, db);

    editor.addText("Hello World");
    editor.addImage("photo.jpg");
    editor.addText("This is a document editor.");

    cout << editor.renderDocument();
    editor.save();

    return 0;
}
```

The **client talks only to `DocumentEditor`**. It has zero knowledge of `Document`, `TextElement`, `ImageElement`, or `SaveToFile`. All complexity is hidden.

---

## 🔍 Bonus Principle: Principle of Least Knowledge

> **"A class should only talk to its immediate friends. Never to a friend's friend."**

This is a design principle (separate from SOLID) that says: only call methods on objects you directly own or were passed to you.

### Example — the problem it solves:

If a `DocumentRenderer` class existed that did this:
```cpp
// ❌ BAD — DocumentRenderer talks to Document's friend (DocumentElement)
auto elements = doc->getElements();
for (auto& el : elements) el->render(); // friend's friend
```

`DocumentRenderer` now knows about `DocumentElement` too — that's extra coupling.

The fix: put the render loop inside `Document` itself.

```cpp
// ✅ GOOD — DocumentEditor only talks to its direct friend (Document)
string result = doc->render(); // Document handles its own elements internally
```

```
❌ Bad:  DocumentEditor → doc.getElements() → el.render()   (friend of friend)
✅ Good: DocumentEditor → doc.render()                       (direct friend only)
```

---

## 📐 Final Architecture Summary

```
«abstract»
DocumentElement ──────────── render(): string
      ▲
      ├── TextElement          (text → returns text)
      ├── ImageElement         (path → returns [Image: path])
      └── NewLineElement       (returns \n)

Document
  - elements: List<DocumentElement*>   ◆── DocumentElement (1..*)
  + addElement()
  + render()   ← loops elements, calls el->render() via polymorphism

«abstract»
Persistence ─────────────── save(content): void
      ▲
      ├── SaveToFile
      └── SaveToDB

DocumentEditor
  - doc: Document*       ◇── Document
  - db: Persistence*     ◇── Persistence
  + addText()
  + addImage()
  + renderDocument()
  + save()

Client ──────────────────► DocumentEditor only
```

---

## ✅ SOLID Check on Final Design

| Principle | Status | Evidence |
|---|---|---|
| **SRP** | ✅ | DocumentElement renders, Document manages list, Persistence saves, Editor is interface |
| **OCP** | ✅ | New element/storage type = new class added, nothing existing touched |
| **LSP** | ✅ | Any `DocumentElement*` subclass substitutes safely wherever the base is expected |
| **ISP** | ✅ | `DocumentElement` has only `render()`, `Persistence` has only `save()` — lean contracts |
| **DIP** | ✅ | Editor depends on `Document` and `Persistence` abstractions, not concrete classes |

---

## 🔑 Key Takeaways

| Concept | Remember This |
|---|---|
| **Bottom-Up approach** | Build atomic pieces first, then compose them |
| **Each element renders itself** | `el->render()` — polymorphism takes care of which one |
| **Document delegates** | Loops and calls `render()`, doesn't know HOW each element renders |
| **Persistence abstraction** | Editor never touches SaveToFile directly — inject and swap freely |
| **Client talks only to Editor** | All internal complexity is hidden behind DocumentEditor |
| **Principle of Least Knowledge** | Talk only to direct friends, not friends-of-friends |
| **No perfect LLD** | Always a trade-off — justify your design, stay open to discussion |