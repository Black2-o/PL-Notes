# 03 — UML Diagrams
### Class Diagrams & Sequence Diagrams with Real Examples

> 📺 Source: [What is UML Diagrams | Class & Sequence Diagrams](https://www.youtube.com/watch?v=nPJyyO9pb5s)

---

## ❓ What is UML?

You have an idea for an application in your head. Now you need to explain it to your teammate. Two ways:
1. Write long boring paragraphs describing every component → hard to understand
2. **Draw a diagram** → visual, intuitive, everyone gets it instantly

**UML (Unified Modeling Language)** = a standard way to draw diagrams that show how an application is structured and how its components interact.

> UML expresses: what components exist, how they are connected, and how they communicate with each other.

---

## 📐 Types of UML Diagrams

UML has **14 diagrams** split into 2 categories. But you only need **2** for LLD.

```
UML Diagrams (14 total)
├── Structural (Static) → Shows WHAT the app looks like
│   └── ✅ Class Diagram         ← YOU NEED THIS
│
└── Behavioral (Dynamic) → Shows HOW components interact
    └── ✅ Sequence Diagram      ← YOU NEED THIS
```

| Type | Also Called | Shows |
|---|---|---|
| **Class Diagram** | Static Diagram | Which classes exist + how they connect |
| **Sequence Diagram** | Dynamic Diagram | How objects send messages to each other over time |

> The other 12 UML diagrams are use-case specific — rarely needed in LLD interviews or real projects.

---

## 📦 Part 1: Class Diagram

A Class Diagram shows:
1. **The structure of each class** (name, variables, methods, access modifiers)
2. **The associations between classes** (how they are connected)

---

### 🔷 How to Represent a Class

A class is drawn as a **rectangle divided into 3 sections**:

```
┌──────────────────────────────────┐
│  «abstract» (only if abstract)   │
│           ClassName              │  ← Section 1: Class Name
├──────────────────────────────────┤
│  accessMod  varName  : DataType  │  ← Section 2: Variables (Characteristics)
│  accessMod  varName  : DataType  │
├──────────────────────────────────┤
│  accessMod  method() : RetType   │  ← Section 3: Methods (Behaviors)
│  accessMod  method() : RetType   │
└──────────────────────────────────┘
```

**Access Modifier Symbols:**

| Symbol | Modifier | Who Can Access |
|---|---|---|
| `+` | Public | Everywhere |
| `#` | Protected | Inside class + child classes |
| `-` | Private | Only inside the class |

**Abstract vs Concrete:**
- Write `«abstract»` above class name → has virtual/unimplemented methods
- Nothing written → Concrete class (all methods are defined)

### Example — Car Class

```
┌────────────────────────────────┐
│           «abstract»           │
│              Car               │
├────────────────────────────────┤
│  - brand    : String           │
│  - model    : String           │
│  - engineCC : int              │
├────────────────────────────────┤
│  + startEngine() : void        │
│  + stopEngine()  : void        │
│  + accelerate()  : void        │
│  + applyBrake()  : void        │
└────────────────────────────────┘
```

> Variable format is reversed from code: `varName : DataType` (not `DataType varName`)

---

### 🔗 Associations (How Classes Connect)

```
Associations
├── Class Association  → Inheritance  (IS-A relationship)
└── Object Association → Composition  (HAS-A relationship)
    ├── Simple Association  (weakest)
    ├── Aggregation         (medium)
    └── Composition         (strongest)
```

---

#### 1. Inheritance — IS-A Relationship

**Cow IS-A Animal. ManualCar IS-A Car.**

Drawn with a **closed (filled) arrowhead** pointing child → parent.

```
      Car
       ▲
       │  ← closed arrow = inheritance
    ───┴───
   /         \
ManualCar   ElectricCar
```

> **IS-A Test:** Can you say "Child IS-A Parent"? → Use Inheritance.

---

#### 2. Composition — HAS-A Relationship

All three sub-types follow HAS-A. They differ only in how tightly coupled the objects are.

| Type | Strength | Key Idea | Can parts exist alone? | Arrow |
|---|---|---|---|---|
| Simple Association | Weakest | Two objects loosely related | Yes | `──→` Open arrow |
| Aggregation | Medium | Container object holds others | Yes, independently | `──◇` Open diamond |
| Composition | Strongest | Parts cannot exist without the whole | No | `──◆` Filled diamond |

**Simple Association** — Arjun lives in a House
```
Arjun ──────────→ House
```
> Arjun HAS-A house. Both exist independently.

**Aggregation** — Room contains Sofa, Bed, Chair
```
Sofa  ◇──→ Room
Bed   ◇──→ Room
Chair ◇──→ Room
```
> Room HAS-A Sofa. A sofa **can exist without** the room (you can move it out).

**Composition** — Chair is made of Arms, Seat, Wheels
```
Arms   ◆──→ Chair
Seat   ◆──→ Chair
Wheels ◆──→ Chair
```
> Chair HAS-A Arms. Arms **cannot exist** without the chair.

> 💡 **Thin line between Aggregation and Composition:** It's often **subjective**. Example — can a Menu exist without a Restaurant? If yes → Aggregation. If no → Composition. No single right answer, depends on your design.

---

#### Composition in Code (C++)

```cpp
class A {
public:
    void methodOne() { /* ... */ }
};

class B {
private:
    A* a;  // B HAS-A reference to A
public:
    B() { a = new A(); }

    void methodTwo() { /* ... */ }

    void useA() {
        a->methodOne(); // access A's method through the stored reference
    }
};

int main() {
    B* b = new B();
    b->methodTwo();     // B's own method
    b->useA();          // indirectly calls A's method
}
```

> In composition, you store a **reference** to the other class inside your class. You **cannot** call `b->methodOne()` directly — you go through the reference. Composition is used **more than inheritance** in LLD.

---

### Arrow Summary — Class Diagram

| Relationship | Arrow | Example |
|---|---|---|
| Inheritance | `──▷` Closed arrowhead | ManualCar → Car |
| Simple Association | `──→` Open arrowhead | Arjun → House |
| Aggregation | `──◇` Open diamond | Sofa → Room |
| Composition | `──◆` Filled diamond | Arms → Chair |

---

## ⏱️ Part 2: Sequence Diagram

A Sequence Diagram shows **how objects communicate with each other** over time for a specific **use case** (one flow/scenario).

> Each use case gets its own sequence diagram. You only draw one flow at a time — never the entire application at once.

---

### 🧩 Components of a Sequence Diagram

**1. Objects** — simple labeled boxes placed at the top

```
[User]   [ATM]   [Transaction]   [Account]   [CashDispenser]
```

**2. Lifeline** — dashed vertical line below each object
- Shows how long the object **exists** in the application
- Objects created mid-flow start their lifeline mid-diagram

**3. Activation Bar** — thin solid rectangle on top of the lifeline
- Shows when the object is **actively** processing (sending/receiving messages)
- Inactive object = cannot send or receive

**4. Messages** — horizontal arrows between objects

| Type | Arrow | Meaning |
|---|---|---|
| Synchronous | `──▶` Closed arrow | Send and **wait** for response |
| Synchronous Response | `- - →` Dashed line | Return value back |
| Asynchronous | `──>` Open arrow | Send and **don't wait** |
| Create | `──→ «create»` | Instantiate a new object |
| Destroy | `X` on lifeline | Object is destroyed/goes out of scope |
| Lost | Arrow with filled dot at end | Receiver unavailable |
| Found | Arrow with filled dot at start | Sender unknown |

**Synchronous vs Asynchronous:**
- **Synchronous** — send one message, wait for response, then send the next
- **Asynchronous** — fire messages one after another without waiting

---

### 📋 How to Draw a Sequence Diagram — 3 Steps

**Step 1: Define the Use Case**
Write the flow in plain English — what happens step by step.

**Step 2: Identify the Objects**
Which entities are involved in this flow?

**Step 3: Draw the Diagram**
Place objects at top → draw lifelines → add activation bars → connect with messages.

---

### 🏧 Real Example — ATM Cash Withdrawal

**Use Case:** User goes to ATM, enters account number + amount, gets cash.

**Objects:** User, ATM, Transaction, Account, CashDispenser

**Flow (plain English):**
1. User sends `withdraw(amount, accountNo)` to ATM
2. ATM **creates** a new Transaction object
3. Transaction sends `checkAmount(amount)` to Account
4. Account returns `true` (sufficient funds exist)
5. Transaction is **destroyed** (its job is done)
6. ATM sends `withdrawCash(amount)` to CashDispenser
7. CashDispenser returns the cash to ATM
8. ATM returns the cash to User — all objects deactivate

**Sequence Diagram (text representation):**

```
User        ATM         Transaction     Account     CashDispenser
 │           │               │             │              │
 █───withdraw(amt, accNo)───→│             │              │
 │           █               │             │              │
 │           │──«create»─────→             │              │
 │           │               █             │              │
 │           │               │─checkAmount(amt)──────────→│
 │           │               │             █              │
 │           │               │←─ ─ ─true─ ─│             │
 │           │               █             │              │
 │           │←─ ─ ─true─ ─ │             │              │
 │           │              [X] destroyed  │              │
 │           │─withdrawCash(amt)────────────────────────→ │
 │           │               │             │              █
 │           │←─ ─ ─cash─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─  │
 █←─ ─cash─ │               │             │              │
 │           │               │             │              │
(all deactivate — flow complete)
```

**Key observations:**
- User and ATM are active throughout the entire flow
- Transaction is created mid-flow (`«create»`) and destroyed (`X`) once done
- CashDispenser only activates when actually dispensing cash
- All messages are synchronous (each step waits for response)

---

### 🔖 Extra Sequence Diagram Terms

| Term | What it Means |
|---|---|
| `alt` | If-Else block (e.g., funds available vs not) |
| `opt` | If-only block (no else) |
| `loop` | Repeating block (for/while loop) |

> These are rarely used — most diagrams show only the **happy flow** (everything goes well).

---

## 🔑 Quick Recap

### Class Diagram — Cheat Sheet

| Element | How to Draw |
|---|---|
| Class box | Rectangle, 3 sections: Name / Variables / Methods |
| Abstract class | `«abstract»` above class name |
| Public | `+` before variable/method |
| Protected | `#` before variable/method |
| Private | `-` before variable/method |
| Inheritance | Closed arrow child → parent |
| Simple Association | Open arrow |
| Aggregation | Open diamond |
| Composition | Filled diamond |

### Sequence Diagram — Cheat Sheet

| Element | What it Represents |
|---|---|
| Object box | An entity in the flow |
| Dashed vertical line | Lifeline (how long it exists) |
| Thin rectangle on line | Activation bar (when it's active) |
| Closed arrow | Synchronous message |
| Dashed return arrow | Response |
| Open arrow | Asynchronous message |
| `«create»` arrow | New object instantiated |
| `X` on lifeline | Object destroyed |

---

## 🏆 Golden Rules to Remember

> **IS-A → Inheritance. HAS-A → Composition.**

> **Aggregation:** parts can exist independently. **Composition:** parts cannot exist without the whole.

> **Sequence Diagram:** one diagram per use case. Show objects, lifelines, activation bars, and messages in the order they happen.

> **Composition is used MORE than Inheritance in real LLD.**

---

## 🏋️ Practice Exercise (from video)

Draw a **Class Diagram** for this scenario:
- A `Car` class (abstract) with 3-4 variables and 3-4 methods
- `ManualCar` (inherits Car) → extra method: `changeGear()`
- `ElectricCar` (inherits Car) → extra method: `chargeBattery()`

Think about:
- Which association type connects ManualCar/ElectricCar to Car?
- What arrow do you draw?
- Which access modifiers do you use on Car's variables vs methods?