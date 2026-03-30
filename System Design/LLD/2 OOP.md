# 02 — Object Oriented Programming (OOP)
### All 4 Pillars: Abstraction · Encapsulation · Inheritance · Polymorphism

> 📺 Sources:
> - [OOPs Real-World Examples | Abstraction | Encapsulation](https://www.youtube.com/watch?v=QbGoqAgP_zg)
> - [Inheritance & Polymorphism in OOPs](https://www.youtube.com/watch?v=KGOEK0-XBIg)

---

## 🕰️ History of Programming (Why OOP Exists?)

Before OOP, programming went through 3 phases — each better than the last, but still not enough for large real-world apps.

| Era | Language Type | What It Did | Problems |
|---|---|---|---|
| 1st | **Machine Language** | Binary code (0s and 1s), direct CPU talk | Extremely error-prone, unreadable, not scalable |
| 2nd | **Assembly Language** | Used mnemonics (`MOV A, 61H`), closer to English | Still hardware-coupled, no loops/methods, low scalability |
| 3rd | **Procedural Programming** (e.g. C) | Introduced functions, loops, if-else blocks | Can't model real-world well, poor data security, not scalable for big apps |

> **The Problem with Procedural Programming:**
> Code is just a "recipe" — a list of instructions. It has no concept of real-world *objects* interacting. Building apps like Uber or Zomato with it would be a nightmare.

That's why we moved to → **Object Oriented Programming (OOP)** 🚀

---

## ❓ What is OOP?

OOP is a way to model the **real world in code**.

> In real life — everything is an **object** (you, a mic, a laptop, a car). Objects have **characteristics** (data) and **behaviors** (actions). They **interact** with each other.

OOP brings this same model into programming:

| Real World | OOP Term |
|---|---|
| Thing / Entity | **Object** |
| Properties / Attributes | **Characteristics** (Variables) |
| Actions / Functions | **Behaviors** (Methods) |
| Blueprint to create objects | **Class** |

```cpp
class Car {
    string brand;       // characteristic
    string model;       // characteristic
    bool isEngineOn;    // characteristic

    void startEngine(); // behavior
    void stopEngine();  // behavior
    void accelerate();  // behavior
};

Car* myCar = new Car(); // object created from blueprint
```

> 🏠 **Class = Blueprint. Object = The actual house built from that blueprint.**

---

## 🔴 The Procedural Problem (Story)

Imagine you have a `Car` with brand, model, isEngineOn and methods like start/stop/shiftGear.

In **procedural** style you'd write:
```c
string brand;
string model;
bool isEngineOn;
void startCar() { ... }
void stopCar() { ... }
```

Now add an **Owner** who owns the car. In procedural:
```c
string ownerName;
string ownerCarBrand; // duplicated!
string ownerCarModel; // duplicated!
```

Now imagine **100 cars** and **100 owners**. You'd have hundreds of loose variables floating everywhere with no connection to each other. No structure, no grouping, total chaos. This is why OOP was needed.

---

## 🏛️ The 4 Pillars of OOP

```
┌─────────────────────────────────────────┐
│              4 Pillars of OOP           │
│                                         │
│  Abstraction    │   Encapsulation       │
│  (Data Hiding)  │   (Data Security)     │
│─────────────────┼───────────────────────│
│  Inheritance    │   Polymorphism        │
│  (IS-A relation)│   (Many forms)        │
└─────────────────────────────────────────┘
```

---

## 1️⃣ Abstraction — *"Hide the unnecessary, show the necessary"*

### Real Life Example
When you drive a car:
- You turn the key → engine starts ✅
- You press the accelerator → car moves ✅
- Do you need to know **how the engine works inside**? ❌ NO.
- Do you need to know **how the gearbox works internally**? ❌ NO.

The car gives you an **interface** (steering, pedals, gear) to interact with it. The internal complexity is **hidden**.

Same with a TV — you use a remote. You don't need to know the internal wiring.

> **Definition:**
> Abstraction **hides unnecessary details** from the client (user of the object) and **shows only what is necessary**.

### In Code (C++)

We use `virtual` keyword to **declare** methods in a parent class without defining them. The child class is responsible for the definition (the actual implementation is hidden from the user).

```cpp
class Car {
public:
    virtual void startEngine() = 0;  // declared, not defined
    virtual void accelerate() = 0;   // child class will define HOW
    virtual void applyBrake() = 0;
};
```

The user just calls `myCar->accelerate()` — they don't care about the implementation inside. That's abstraction.

> 🔑 **Key Line:** Abstraction focuses on **WHAT** an object does, not **HOW** it does it.

---

## 2️⃣ Encapsulation — *"Protect your data"*

### Real Life Example
A car has a current speed. You (the driver) should be **able to see** the speed. But you should **not be able to directly set** the speed to 500 km/h without the engine running. There must be **controlled access**.

> **Definition:**
> Encapsulation bundles **data (characteristics) and methods (behaviors) together** in a class, AND **restricts direct access** to internal data using access modifiers (`private`, `public`, `protected`).

**Two things Encapsulation says:**
1. Bundle characteristics + behaviors together in a class ✅
2. Sensitive data should NOT be directly accessible from outside — use getters/setters ✅

### In Code (C++)

```cpp
class SportsCar {
private:
    string brand;
    string model;
    bool isEngineOn;
    int currentSpeed;   // private — cannot be changed directly
    string tire;        // private

public:
    // Behaviors remain PUBLIC — needed to interact with the object
    void startEngine() { isEngineOn = true; }
    void stopEngine()  { isEngineOn = false; currentSpeed = 0; }
    void accelerate(int speed) { currentSpeed += speed; }

    // GETTER — read only (no setter for speed = intended!)
    int getCurrentSpeed() { return this->currentSpeed; }

    // GETTER + SETTER — for tire (with validation possible)
    string getTire() { return this->tire; }
    void setTire(string t) {
        // Can add validation here before setting!
        // e.g., check if tire brand exists
        this->tire = t;
    }
};
```

### Why Getters/Setters over Public Variables?

```cpp
// ❌ BAD — direct access, no control
myCar.currentSpeed = 500; // anyone can set anything!

// ✅ GOOD — controlled access through setter
myCar.setTire("MRF"); // validation can happen inside setter
int speed = myCar.getCurrentSpeed(); // read only
```

With setters, you can **add validations** before data is set — e.g., check if the tire brand actually exists in the database. This control is what makes encapsulation powerful.

### Abstraction vs Encapsulation — Key Difference

| | Abstraction | Encapsulation |
|---|---|---|
| Focus | **Data Hiding** | **Data Security** |
| Concern | Hiding *how* things work | Protecting data from unauthorized access |
| Example | You don't see engine internals | You can't directly set speed to 500 |
| Tool | `virtual` functions, interfaces | `private` + getters/setters |

> Data hiding (abstraction) — even if someone sees it, it's OK.
> Data security (encapsulation) — if that data gets exposed outside, it's a **problem**.

---

## 3️⃣ Inheritance — *"IS-A Relationship"*

### Real Life Example

In real life, objects have **parent-child relationships**:
- A **ManualCar** IS-A **Car** ✅
- An **ElectricCar** IS-A **Car** ✅

Both share common properties of a Car, but each has its own **extra features**:

| Car (Parent) | ManualCar (Child) | ElectricCar (Child) |
|---|---|---|
| brand, model | + currentGear | + batteryPercentage |
| isEngineOn, currentSpeed | + shiftGear() | + chargeBattery() |
| startEngine() | inherits all Car stuff | inherits all Car stuff |
| stopEngine() | | |
| accelerate() | | |
| applyBrake() | | |

### In Code (C++)

```cpp
// PARENT CLASS
class Car {
protected:
    string brand;
    string model;
    bool isEngineOn;
    int currentSpeed;

public:
    Car(string b, string m) : brand(b), model(m), isEngineOn(false), currentSpeed(0) {}

    void startEngine() { isEngineOn = true; }
    void stopEngine()  { isEngineOn = false; currentSpeed = 0; }
    virtual void accelerate() = 0;   // child defines HOW
    virtual void applyBrake() = 0;
};

// CHILD CLASS 1 — inherits Car
class ManualCar : public Car {
private:
    int currentGear;

public:
    ManualCar(string b, string m) : Car(b, m), currentGear(1) {}

    void shiftGear(int gear) { currentGear = gear; } // extra feature

    void accelerate() override {
        currentSpeed += 20; // manual car accelerates differently
    }
    void applyBrake() override { currentSpeed -= 10; }
};

// CHILD CLASS 2 — inherits Car
class ElectricCar : public Car {
private:
    int batteryPercentage;

public:
    ElectricCar(string b, string m) : Car(b, m), batteryPercentage(100) {}

    void chargeBattery() { batteryPercentage = 100; } // extra feature

    void accelerate() override {
        currentSpeed += 15; // electric car accelerates differently
    }
    void applyBrake() override { currentSpeed -= 8; }
};
```

### Why `protected` in Parent Class?

- `private` → only accessible inside that class (child can't access)
- `protected` → accessible inside the class AND child classes ✅
- `public` → accessible everywhere

We use `protected` for characteristics so child classes can access them directly.

> 🔑 **Key:** Inheritance lets child classes **reuse** the parent's code + add their own extra features. No need to rewrite `startEngine()` for every car type.

---

## 4️⃣ Polymorphism — *"Many forms of the same thing"*

Polymorphism = one method name, **many different behaviors** depending on context.

**Two types:**

```
Polymorphism
├── Static Polymorphism  (Compile Time) → Method Overloading
└── Dynamic Polymorphism (Run Time)     → Method Overriding
```

---

### 🅰️ Static Polymorphism — Method Overloading

Same method name, **different parameters** in the **same class**.

Decided at **compile time**.

```cpp
class Car {
public:
    // Two accelerate() methods — same name, different parameters
    virtual void accelerate() {
        currentSpeed += 20; // accelerate by default amount
    }
    virtual void accelerate(int speed) {
        currentSpeed += speed; // accelerate by specific amount
    }
};
```

```cpp
myCar->accelerate();     // calls first version
myCar->accelerate(40);   // calls second version
```

> 🔑 The compiler decides which version to call based on the arguments at **compile time**.

---

### 🅱️ Dynamic Polymorphism — Method Overriding

Same method name, **different implementation** in **child class** vs **parent class**.

Decided at **run time**.

```cpp
// Parent declares virtual
class Car {
public:
    virtual void accelerate(int speed) {
        currentSpeed += speed;
    }
};

// Child OVERRIDES with its own behavior
class ManualCar : public Car {
public:
    void accelerate(int speed) override {
        currentSpeed += speed; // manual: adds full speed
        cout << "Manual car: Now at " << currentSpeed << " km/h" << endl;
    }
};

class ElectricCar : public Car {
public:
    void accelerate(int speed) override {
        currentSpeed += speed / 2; // electric: adds half speed (battery saving)
        cout << "Electric car: Now at " << currentSpeed << " km/h" << endl;
    }
};
```

```cpp
Car* car1 = new ManualCar("Toyota", "Corolla");
Car* car2 = new ElectricCar("Tesla", "Model 3");

car1->accelerate(40); // "Manual car: Now at 40 km/h"
car2->accelerate(40); // "Electric car: Now at 20 km/h"
```

Same method name `accelerate()`, same call — but **different output** based on the actual object type. This decision happens at **run time**.

> 🔑 `virtual` keyword in parent + `override` in child = Dynamic Polymorphism.

---

### Overloading vs Overriding — Quick Comparison

| | Method Overloading | Method Overriding |
|---|---|---|
| Type | Static Polymorphism | Dynamic Polymorphism |
| Where | Same class | Parent → Child class |
| Difference | Different parameters | Same signature, different implementation |
| Decided at | Compile time | Run time |
| Keyword | None needed | `virtual` + `override` |

---

## 🚗 Complete Example — All 4 Pillars Together

```cpp
class Car {                               // ABSTRACTION + ENCAPSULATION
protected:                                // ENCAPSULATION (protected = child access)
    string brand, model;
    bool isEngineOn;
    int currentSpeed;

public:
    Car(string b, string m) : brand(b), model(m), isEngineOn(false), currentSpeed(0) {}

    void startEngine() { isEngineOn = true; }
    void stopEngine()  { isEngineOn = false; currentSpeed = 0; }

    virtual void accelerate() = 0;        // ABSTRACTION (hide HOW)
    virtual void accelerate(int s) = 0;   // OVERLOADING (static polymorphism)
    virtual void applyBrake() = 0;
};

class ManualCar : public Car {            // INHERITANCE (IS-A Car)
    int currentGear;
public:
    ManualCar(string b, string m) : Car(b, m), currentGear(1) {}
    void shiftGear(int g) { currentGear = g; }

    void accelerate() override {          // OVERRIDING (dynamic polymorphism)
        currentSpeed += 20;
        cout << "Manual: " << currentSpeed << " km/h\n";
    }
    void accelerate(int s) override {
        currentSpeed += s;
        cout << "Manual: " << currentSpeed << " km/h\n";
    }
    void applyBrake() override { currentSpeed -= 10; }
};

class ElectricCar : public Car {          // INHERITANCE (IS-A Car)
    int batteryPercentage;
public:
    ElectricCar(string b, string m) : Car(b, m), batteryPercentage(100) {}
    void chargeBattery() { batteryPercentage = 100; }

    void accelerate() override {          // OVERRIDING — different behavior
        currentSpeed += 15;
        cout << "Electric: " << currentSpeed << " km/h\n";
    }
    void accelerate(int s) override {
        currentSpeed += s / 2;
        cout << "Electric: " << currentSpeed << " km/h\n";
    }
    void applyBrake() override { currentSpeed -= 8; }
};

int main() {
    Car* car1 = new ManualCar("Toyota", "Corolla");
    Car* car2 = new ElectricCar("Tesla", "Model 3");

    car1->startEngine();
    car1->accelerate();     // 20 km/h
    car1->accelerate(40);   // 60 km/h
    car1->applyBrake();
    car1->stopEngine();

    car2->startEngine();
    car2->accelerate();     // 15 km/h
    car2->accelerate(40);   // 15 + 20 = 35 km/h
    car2->applyBrake();
    car2->stopEngine();
}
```

> ✅ This single example demonstrates all 4 pillars of OOP.

---

## 🔑 Quick Recap Table

| Pillar | One Line | Key Tool | Focus |
|---|---|---|---|
| **Abstraction** | Hide *how*, show *what* | `virtual` / interfaces | Data Hiding |
| **Encapsulation** | Bundle + protect data | `private` + getters/setters | Data Security |
| **Inheritance** | Child IS-A Parent, reuse code | `: public ParentClass` | Code Reuse |
| **Polymorphism** | One name, many behaviors | Overloading + Overriding | Flexibility |

---

## 🏆 Golden Lines to Remember

> **Abstraction** → *"You drive the car. You don't need to know how the engine works."*

> **Encapsulation** → *"You can SEE the speedometer. You can't DIRECTLY set speed to 500."*

> **Inheritance** → *"ManualCar IS-A Car. ElectricCar IS-A Car."*

> **Polymorphism** → *"Same accelerate() call — Manual goes 20, Electric goes 15."*

---

## ⏭️ What's Next?

**Next Video → SOLID Principles** (or Design Patterns)

OOP gives us the building blocks. SOLID tells us the **rules** for using those blocks correctly to write clean, maintainable code.

---

## 📝 Homework (from the video)

> **Question:** What is **Operator Overloading** in C++?
> - Why does C++ support it?
> - Why do Java and Python **NOT** support operator overloading?