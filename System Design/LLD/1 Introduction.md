# 01 — Introduction to System Design (LLD Focus)

> 📺 Source: [Introduction To System Design — Aditya](https://www.youtube.com/watch?v=AK0hu0Zxua4)
> 🎯 Playlist: LLD Series by Aditya (Code Army)

---

## 🧠 Why Learn LLD?

You've done DSA. You can solve LeetCode problems. But that's not enough.

> **Real-world applications** like Swiggy, Zomato, Ola, Uber — they don't just need algorithms. They need **well-structured, scalable code** that can handle **millions of users** at once.

To build those kinds of apps — or to get into **top companies / startups** — you **must** know LLD.

LLD is also required to:
- Understand HLD (High Level Design) deeply
- Contribute to open source projects
- Work effectively in real company codebases

---

## ❓ What is LLD?

**LLD = Low Level Design**

DSA gives you tools (algorithms, data structures) to solve **isolated problems**.
LLD is about using **those DSA tools** to build a **complete, structured application**.

> 💡 Simple Formula:
> **DSA solution(s) + Structure + Design → LLD (Complete Application)**

### DSA vs LLD — Key Difference

| | DSA | LLD |
|---|---|---|
| Focus | Solving a single isolated problem | Building a complete application |
| Example | Binary Search, Merge Sort | Ride booking system, Parking lot |
| Output | Algorithm / Function | Classes, Objects, Full codebase |
| Scope | Narrow | Broad |

---

## 📖 The Story: Anurag vs Maurya

Two friends join a company called **QuickRide** (like Ola/Uber).
- **Anurag** → Great at DSA, but knows **zero LLD**
- **Maurya** → Great at DSA **+** knows LLD well

Their manager asks: *"Build the QuickRide app. Find the problems and solve them."*

---

### 🔴 Anurag's Approach (DSA only — No LLD)

Anurag hears "application" and immediately thinks in algorithms.

He identifies the core problem:
> *"I need to take a user from Source → Destination. So I need to find the shortest path."*

He models the city as a **Graph**:
- **Intersections** = Nodes
- **Roads** = Edges

He applies **Dijkstra's Algorithm** → finds the shortest path. ✅

Then the manager says: *"Now assign a rider to the user."*

Anurag thinks again. He sees it as a **matching problem**. He writes a `findNearestRider()` function — raw, standalone code.

**The Problem:**
- His code is not reusable
- Everything is written as isolated functions
- If tomorrow Zomato needs a similar delivery assignment feature, Anurag's code **cannot be reused** without major changes
- His code has **no structure**

---

### 🟢 Maurya's Approach (DSA + LLD)

Maurya also identifies the same DSA problems (Graph + Matching).

But instead of writing raw functions, Maurya **thinks in structure first**:

He asks:
- What are the **entities** in this system? → User, Rider, Trip, Location
- What are the **behaviors** of each entity?
- How should these entities **interact** with each other?

He creates **classes**:

```cpp
class User {
    string name;
    Location source;
    Location destination;
};

class Rider {
    string name;
    Location currentLocation;
    bool isAvailable;
};

class Trip {
    User user;
    Rider rider;
    void assignRider();
    void calculateFare();
};
```

He writes a `RiderMatchingAlgorithm` class — so clean and modular that it can be **plugged into any other app** (Swiggy, Blinkit, Amazon delivery) with minimal changes.

**The Result:**
- Code is **reusable** 🔁
- Code is **maintainable** 🛠️
- Code is **scalable** 📈
- Any algorithm can be **swapped out** without breaking the whole system

---

## 🎯 What Does LLD Focus On?

### 1. ♻️ Reusability
Write code so that a module (e.g., RiderMatchingAlgorithm) can be **taken out of one application and plugged into another** with minimal changes.

> Same rider-matching logic works for Ola, Swiggy, Blinkit, Amazon Delivery — only the data changes, not the core algorithm.

### 2. 🧱 Structure / Code Design
Decide **how the code is organized**:
- What classes exist?
- What are the relationships between them?
- Who talks to whom?

This is done using **OOP concepts** (which we'll cover next in this series).

### 3. 📐 Class Diagrams
In LLD interviews, you draw **Class Diagrams** — not system architecture diagrams (that's HLD).

---

## ❌ What is NOT LLD? (HLD vs LLD)

A lot of people confuse **HLD** and **LLD**. Here's the clear difference:

| | HLD (High Level Design) | LLD (Low Level Design) |
|---|---|---|
| Full Name | High Level Design | Low Level Design |
| Focus | System Architecture | Code Structure |
| Asks | Which DB? Which server? How to scale? | Which classes? Which methods? How do objects interact? |
| Output | System Design Diagram | Class Diagram + Code |
| Code Written? | Almost none | Yes, actual code |
| Example Topics | Load balancing, SQL vs NoSQL, Server scaling, Cost optimization | OOP, Design Patterns, SOLID principles |

### HLD Focuses On:
- **Tech Stack** → Java Spring Boot? Node.js?
- **Database Choice** → SQL or NoSQL?
- **Server Scaling** → How to handle traffic spikes?
- **Cost Optimization** → Don't waste server resources

### LLD Focuses On:
- **Code structure** → Classes, Objects, Interfaces
- **Design Patterns** → Singleton, Factory, Observer...
- **SOLID Principles** → Writing clean, maintainable code

---

## 🔺 The Big Picture: DSA + LLD + HLD

All three together build a complete application:

```
┌─────────────────────────────────────────────┐
│              APPLICATION                    │
│                                             │
│  ┌─────────┐  ┌─────────┐  ┌─────────────┐ │
│  │   DSA   │  │   LLD   │  │     HLD     │ │
│  │         │  │         │  │             │ │
│  │ Brain   │  │Skeleton │  │ Architecture│ │
│  │ (Logic) │  │(Structure│  │ (Infra)    │ │
│  └─────────┘  └─────────┘  └─────────────┘ │
└─────────────────────────────────────────────┘
```

| Layer | Role |
|---|---|
| **DSA** | The **brain** — algorithms and logic |
| **LLD** | The **skeleton** — structure and design of code |
| **HLD** | The **infrastructure** — servers, databases, scaling |

---

## 🏆 The Golden Line (Memorize This!)

> ### *"If DSA is the brain of an application — LLD is the skeleton."*

This one line explains everything:
- Without a brain (DSA), the app has no intelligence
- Without a skeleton (LLD), the app has no structure and cannot stand
- Both are needed to build something that works **and** scales

---

## 📋 Series Prerequisites

- ✅ You know **C++** (all source code in this series is C++)
- ✅ Java source code will also be provided alongside
- ✅ Beginner friendly — starts from scratch
- ✅ Full notes + GitHub repo provided

---

## ⏭️ What's Next?

**Next Video → Pillars of OOP (Object Oriented Programming)**

Even if you already know OOP — **don't skip it**. This series covers OOP from a design perspective, not just syntax. You'll likely learn something new.

---

## 🔑 Quick Recap

| Concept | Remember This |
|---|---|
| LLD | Building a complete, structured app using DSA |
| DSA | Tool used inside LLD to solve isolated problems |
| HLD | System architecture — infra, DB, scaling |
| Reusability | Code that can be plugged into any app with minimal change |
| LLD Interview | You draw Class Diagrams + write actual code |
| HLD Interview | You draw System Architecture Diagrams, almost no code |
| Golden Quote | DSA = Brain, LLD = Skeleton |