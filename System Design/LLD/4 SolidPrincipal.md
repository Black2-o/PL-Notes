# 04 — SOLID Design Principles
### S · O · L · I · D — Clean Code Rules Every Developer Must Know

> 📺 Sources:
> - [SOLID Design Principles | Complete Guide with Code Examples](https://www.youtube.com/watch?v=UsNl8kcU4UA)
> - [SOLID Design Principles | Part 2](https://www.youtube.com/watch?v=hU9koy6A2I0)

---

## 🧠 Why SOLID?

In a real-world project, thousands of classes exist. If they're tightly coupled and messy — like a house where electrical wires, internet cables, and pipes all run through one tangled bundle — then:

- Adding a new feature requires touching many classes → bugs creep in
- New engineers can't read or understand the code
- Debugging becomes a nightmare

**SOLID** is a set of 5 design principles by **Robert C. Martin (2000)** that, when followed, give you:

✅ Clean, readable code
✅ Maintainable architecture
✅ Easy to extend without breaking what's already working

```
S → Single Responsibility Principle  (SRP)
O → Open/Closed Principle             (OCP)
L → Liskov Substitution Principle     (LSP)
I → Interface Segregation Principle   (ISP)
D → Dependency Inversion Principle    (DIP)
```

> These are **principles**, not laws. There's always a trade-off with business logic. Follow them as much as possible — but real applications may need to bend them slightly.

---

## S — Single Responsibility Principle (SRP)

### Definition
> **A class should have only ONE reason to change.**
> A class should do only ONE thing.

### Real Life Analogy
A TV remote controls only the TV. If the same remote also controlled the fridge and AC, it would be a mess to maintain and fix.

### Problem (SRP Violated)

```
ShoppingCart
├── calculateTotalPrice()   ← cart logic ✅
├── printInvoice()          ← invoice logic ❌
└── saveToDatabase()        ← DB logic ❌
```

`ShoppingCart` is handling 3 different responsibilities. If DB logic changes → modify this class. If invoice format changes → modify this class. **Multiple reasons to change = SRP broken.**

### Solution (SRP Followed)

Break it into separate classes, each with one job:

```cpp
class ShoppingCart {
    vector<Product> products;
public:
    void addProduct(Product p);
    double calculateTotalPrice(); // ONLY this responsibility
};

class ShoppingCartPrinter {
    ShoppingCart* sc; // HAS-A ShoppingCart
public:
    void printInvoice();          // ONLY prints
};

class ShoppingCartStorage {
    ShoppingCart* sc;
public:
    void saveToDatabase();        // ONLY saves
};
```

Now each class has exactly **one reason to change**. ✅

> 🔑 **Key:** Use **Composition** heavily here. Separate classes hold references to each other (HAS-A).

---

## O — Open/Closed Principle (OCP)

### Definition
> **A class should be OPEN for extension, but CLOSED for modification.**

- **Open for extension** = You can add new behavior
- **Closed for modification** = You don't change the existing working code to do it

### Problem (OCP Violated)

You have a `DBStorage` class. Now you want to support MongoDB and FileStorage too.

❌ Wrong approach:
```cpp
class DBStorage {
    void saveToSQL()   { ... } // existing
    void saveToMongo() { ... } // new — you just modified the existing class!
    void saveToFile()  { ... } // new — modified again!
};
```

Every new feature means touching and risking the old code. **OCP is broken.**

### Solution (OCP Followed)

Use **Abstraction + Inheritance + Polymorphism**:

```cpp
// Abstract base (interface) — CLOSED for modification
class DBPersistence {
public:
    virtual void save() = 0; // only declared
};

// New feature? Make a NEW class — don't touch existing ones
class SaveToSQL : public DBPersistence {
public:
    void save() override { /* SQL logic */ }
};

class SaveToMongo : public DBPersistence {
public:
    void save() override { /* MongoDB logic */ }
};

class SaveToFile : public DBPersistence {
public:
    void save() override { /* File I/O logic */ }
};

// Tomorrow, Cassandra? Just add a new class:
class SaveToCassandra : public DBPersistence {
public:
    void save() override { /* Cassandra logic */ }
};
```

Old code is **never touched**. New features arrive as new classes. ✅

> 🔑 **Key:** Introduce an **abstract class / interface** as the boundary. Extend through inheritance, not modification.

---

## L — Liskov Substitution Principle (LSP)

### Definition
> **If B is a subclass of A, then objects of type A can be replaced with objects of type B — without breaking the client.**

In other words: **Child class should behave like the parent class.**

### The Classic Violation

```cpp
class Account {
public:
    virtual void deposit(int amount) { ... }
    virtual void withdraw(int amount) { ... }
};

class FixedTermAccount : public Account {
public:
    void deposit(int amount) override { ... }    // fine
    void withdraw(int amount) override {
        throw logic_error("Withdrawal not allowed!"); // ❌ breaks the contract!
    }
};
```

```cpp
// Client
for (Account* acc : accounts) {
    acc->deposit(100);
    acc->withdraw(50); // CRASHES for FixedTermAccount!
}
```

The client expected all accounts to support withdraw. `FixedTermAccount` broke that expectation → **LSP violated**.

### Solution

Restructure the hierarchy to reflect reality:

```cpp
class DepositOnlyAccount {      // base: only deposit
    virtual void deposit() = 0;
};

class WithdrawableAccount : public DepositOnlyAccount { // adds withdraw
    virtual void withdraw() = 0;
};

class SavingsAccount  : public WithdrawableAccount { ... };
class CurrentAccount  : public WithdrawableAccount { ... };
class FixedTermAccount: public DepositOnlyAccount  { ... }; // no withdraw
```

Now the client uses the right type:
```cpp
vector<WithdrawableAccount*> withdrawable = { savings, current };
vector<DepositOnlyAccount*>  depositOnly  = { fixed };
```

No surprises. No exceptions. ✅

### LSP Guidelines (3 Rules)

#### 1. Signature Rule
| Sub-rule | Rule |
|---|---|
| **Method Argument Rule** | Child's overridden method must accept the **same or broader** argument type than the parent |
| **Return Type Rule** | Child's overridden method must return the **same or narrower** type than the parent |
| **Exception Rule** | Child must not throw **new or broader** exceptions than the parent declared |

#### 2. Property Rule
| Sub-rule | Rule |
|---|---|
| **Class Invariant** | Child must **maintain** all constraints the parent declared (e.g., balance can never be negative) |
| **History Constraint** | Child must **not modify** immutable state the parent established. If a parent marks something `final`, child cannot override it |

#### 3. Method Rule
| Sub-rule | Rule |
|---|---|
| **Pre-condition** | Child can **weaken** (loosen) pre-conditions but **never strengthen** them |
| **Post-condition** | Child can **strengthen** (tighten) post-conditions but **never weaken** them |

**Pre-condition example:**
- Parent: `password.length >= 8`
- Child (Admin): `password.length >= 6` ✅ (weaker = acceptable)
- Child (Admin): `password.length >= 12` ❌ (stronger = breaks client)

**Post-condition example:**
- Parent: `after braking, car should slow down`
- Child (ElectricCar): `after braking, car slows down AND battery charges` ✅ (stronger = acceptable)
- Child: `after braking, nothing guaranteed` ❌ (weaker = breaks contract)

> 🔑 **Key:** "Child should behave like the parent — the client should never know the difference."

---

## I — Interface Segregation Principle (ISP)

### Definition
> **No class should be forced to implement methods it doesn't need.**
> Build **small, specific interfaces** instead of one large general-purpose one.

### Problem (ISP Violated)

```cpp
class Shape {
public:
    virtual double area()   = 0;
    virtual double volume() = 0; // 2D shapes DON'T have volume!
};

class Square : public Shape {
public:
    double area()   override { return side * side; }
    double volume() override { throw logic_error("Not applicable!"); } // ❌ forced
};

class Rectangle : public Shape {
    double area()   override { return l * w; }
    double volume() override { throw logic_error("Not applicable!"); } // ❌ forced
};
```

2D shapes are being **forced to implement** `volume()` which makes no sense for them. **ISP is broken.**

### Solution (ISP Followed)

Split into smaller, focused interfaces:

```cpp
class TwoDShape {
public:
    virtual double area() = 0;
};

class ThreeDShape : public TwoDShape {
public:
    virtual double volume() = 0; // 3D also has area (inherits) + volume
};

class Square    : public TwoDShape   { double area() override { ... } };
class Rectangle : public TwoDShape   { double area() override { ... } };
class Cube      : public ThreeDShape { double area() override { ... }; double volume() override { ... } };
```

Every class implements **only what it needs**. ✅

> 🔑 **Key:** "Many small interfaces are better than one fat interface." Split interfaces by behavior type.

---

## D — Dependency Inversion Principle (DIP)

### Definition
> **High-level modules should NOT depend on low-level modules.**
> **Both should depend on abstractions (interfaces).**

### High-Level vs Low-Level Modules

| Type | Meaning | Example |
|---|---|---|
| **High-Level** | Business logic | `UserService`, `OrderService` |
| **Low-Level** | Infrastructure/system | `MySQLDB`, `MongoDB`, `FileSystem` |

### Real Life Analogy
A CEO (high-level) doesn't talk directly to every developer (low-level). There's a Manager (abstraction/interface) in between. If developers change, the CEO doesn't care — they only talk to the Manager.

### Problem (DIP Violated)

```cpp
class UserService {
    MySQLDatabase* sqlDB;     // tightly coupled to low-level ❌
    MongoDB*       mongoDB;   // tightly coupled to low-level ❌

    void storeUserToSQL()   { sqlDB->saveToSQL(user); }
    void storeUserToMongo() { mongoDB->saveToMongo(user); }
};
```

If you switch from MongoDB to Cassandra → you must **open and modify** `UserService`. OCP is broken, classes are tightly coupled.

### Solution (DIP Followed)

Introduce an **abstraction layer** between high-level and low-level:

```cpp
// Abstraction (interface) — the "Manager"
class Database {
public:
    virtual void save(string user) = 0;
};

// Low-level implementations
class MySQLDatabase : public Database {
    void save(string user) override { /* SQL query */ }
};

class MongoDB : public Database {
    void save(string user) override { /* Mongo function */ }
};

class CassandraDB : public Database {
    void save(string user) override { /* Cassandra logic */ }
};

// High-level module — only talks to the abstraction
class UserService {
    Database* db; // depends on abstraction, NOT concrete class ✅

public:
    UserService(Database* db) : db(db) {} // Dependency Injection

    void storeUser(string user) {
        db->save(user); // doesn't care which DB it is
    }
};

// Usage:
UserService* service = new UserService(new MySQLDatabase()); // inject SQL
// OR
UserService* service = new UserService(new MongoDB());       // inject Mongo
// Tomorrow: new UserService(new CassandraDB()); — no changes to UserService!
```

> 🔑 **Key:** `UserService` doesn't know or care which database it's using. It just calls `db->save()`. The specific DB is **injected from outside** (Dependency Injection).

> 🔑 **Golden line:** *"If Open/Closed Principle is the target — Dependency Inversion Principle is the solution."*

---

## 🔑 Quick Recap

| Principle | One Line | Violation Sign | Fix |
|---|---|---|---|
| **SRP** | One class = one job | Class has too many methods doing unrelated things | Break into smaller, focused classes |
| **OCP** | Extend, don't modify | Adding a feature requires changing old classes | Use abstract class + inheritance for extensions |
| **LSP** | Child behaves like parent | Replacing parent with child crashes the client | Redesign hierarchy so substitution is safe |
| **ISP** | Small focused interfaces | Classes throw "not applicable" on methods they don't need | Split large interfaces into smaller ones |
| **DIP** | Depend on abstractions | High-level class directly creates low-level objects | Inject abstraction (interface) between them |

---

## 🧱 How They Connect

```
SRP  → Keep classes small and focused
OCP  → Use abstractions so old code never changes
LSP  → Make hierarchies substitutable
ISP  → Keep interfaces lean
DIP  → Wire everything through abstractions, not concretes
         ↑
         This is what makes OCP actually achievable
```

All 5 are **deeply intertwined**. Applying one often requires applying others. That's by design — they reinforce each other.