# LLD (Low Level Design) — Answer Bank

---

**Q: What are the SOLID principles?**

**Short:** Single Responsibility, Open-Closed, Liskov Substitution, Interface Segregation, Dependency Inversion.

**Detailed:**
- **S** — Single Responsibility: A class should have only one reason to change.
- **O** — Open-Closed: Open for extension, closed for modification. Add new behavior via subclassing/composition, not editing existing code.
- **L** — Liskov Substitution: A subclass must be usable wherever the parent is used without breaking the program.
- **I** — Interface Segregation: Don't force a class to implement methods it doesn't need. Split fat interfaces.
- **D** — Dependency Inversion: Depend on abstractions (interfaces), not concrete classes. High-level modules shouldn't depend on low-level ones.

---

**Q: How do you make a Singleton thread-safe?**

**Short:** Use double-checked locking with `volatile`, or use an enum (simplest, Java), or initialize eagerly.

**Detailed:**
```java
// Double-checked locking (Java)
public class Singleton {
    private static volatile Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}

// Enum Singleton — simplest, thread-safe, handles serialization
public enum Singleton { INSTANCE; }
```

---

**Q: When should you use Factory Pattern vs Builder Pattern?**

**Short:** Factory = create one of several related types (hides which class). Builder = construct a complex object step by step (same class, many configurations).

**Detailed:**
```javascript
// Factory — returns different types based on input
class ShapeFactory {
  static create(type) {
    if (type === "circle") return new Circle();
    if (type === "square") return new Square();
  }
}

// Builder — constructs complex object with optional parts
class UserBuilder {
  setName(n) { this.name = n; return this; }
  setEmail(e) { this.email = e; return this; }
  setRole(r) { this.role = r; return this; }
  build() { return new User(this.name, this.email, this.role); }
}
const user = new UserBuilder().setName("Abhishek").setRole("admin").build();
```

---

**Q: What is the difference between Proxy and Adapter pattern?**

**Short:** Proxy controls access to the same interface. Adapter converts one interface to another (incompatible interfaces).

**Detailed:**
- **Proxy:** Same interface as the real object. Adds behavior: lazy loading, caching, access control, logging. Client doesn't know it's talking to a proxy.
- **Adapter:** Different interfaces. Wraps an existing class with a new interface expected by the client — like a plug adapter.

```javascript
// Proxy — same interface, adds caching
class CachedDB {
  constructor(db) { this.db = db; this.cache = {}; }
  query(sql) {
    if (this.cache[sql]) return this.cache[sql];
    return this.cache[sql] = this.db.query(sql);
  }
}

// Adapter — converts interface
class OldPaymentAPI { charge(cents) { ... } }
class PaymentAdapter {
  pay(dollars) { this.old.charge(dollars * 100); } // adapts dollars → cents
}
```

---

**Q: When should you use Decorator instead of Inheritance?**

**Short:** Use Decorator when you need to add behavior combinations at runtime without creating a class explosion.

**Detailed:**
```javascript
// Inheritance approach needs: PlainCoffee, MilkCoffee, SugarCoffee, MilkAndSugarCoffee...
// Decorator approach:
class Coffee { cost() { return 10; } }
class Milk {
  constructor(coffee) { this.coffee = coffee; }
  cost() { return this.coffee.cost() + 2; }
}
class Sugar {
  constructor(coffee) { this.coffee = coffee; }
  cost() { return this.coffee.cost() + 1; }
}

const myDrink = new Sugar(new Milk(new Coffee()));
myDrink.cost(); // 13
```
Use inheritance for "is-a" relationships. Use Decorator for "has-a" or behavior extensions.

---

**Q: How does Strategy Pattern remove if-else conditions?**

**Short:** Extract each algorithm into its own class implementing a common interface. Swap strategies at runtime instead of branching.

**Detailed:**
```javascript
// Without Strategy — messy
function process(type, data) {
  if (type === "credit") { /* credit logic */ }
  else if (type === "upi") { /* UPI logic */ }
  else if (type === "paypal") { /* PayPal logic */ }
}

// With Strategy
class CreditStrategy { pay(amount) { /* credit logic */ } }
class UPIStrategy { pay(amount) { /* UPI logic */ } }

class PaymentProcessor {
  constructor(strategy) { this.strategy = strategy; }
  process(amount) { this.strategy.pay(amount); }
}

const processor = new PaymentProcessor(new UPIStrategy());
processor.process(500);
```

---

**Q: What is the difference between Observer and Pub-Sub?**

**Short:** Observer = direct coupling (subject knows its observers). Pub-Sub = decoupled via event bus (publisher doesn't know subscribers).

**Detailed:**
- **Observer:** Subject maintains list of Observer objects. Notifies directly. Same process, tight coupling.
- **Pub-Sub:** Publisher emits events to a channel. Subscribers listen on that channel. No direct reference. Allows cross-process, cross-service communication (e.g., Redis Pub/Sub, Kafka).

```javascript
// Observer — direct
class EventEmitter {
  on(event, handler) { this.listeners[event].push(handler); }
  emit(event, data) { this.listeners[event].forEach(h => h(data)); }
}

// Pub-Sub — decoupled via message broker
kafka.publish("user.created", { id: 1 });  // publisher doesn't know who listens
kafka.subscribe("user.created", handler);   // subscriber doesn't know who published
```

---

**Q: How would you design a Parking Lot (LLD interview question)?**

**Short:** Identify entities → define interfaces → apply patterns (Factory for vehicle types, Strategy for pricing, Observer for availability, Singleton for the lot).

**Detailed:**
```
Entities: ParkingLot, Level, ParkingSpot, Vehicle, Ticket, PricingStrategy

Classes:
- ParkingLot (Singleton) — manages levels
- Level — has N spots, tracks availability
- ParkingSpot — type (compact/large/handicapped), occupied status
- Vehicle (abstract) — Car, Motorcycle, Bus (different sizes)
- Ticket — vehicleId, spotId, entryTime
- PricingStrategy (interface) — HourlyPricing, FlatRatePricing

Flow: vehicle arrives → ParkingLot.findSpot(vehicleType) → assign spot → issue Ticket
      vehicle exits → calculate fee via PricingStrategy → free spot
```
Show class diagram + key methods. Explain which patterns you used and why.

---

**Q: How would you implement Undo/Redo using Command Pattern?**

**Short:** Encapsulate each operation as a Command object with `execute()` and `undo()`. Maintain an undo stack and redo stack.

**Detailed:**
```javascript
class TextEditor {
  constructor() { this.text = ""; this.history = []; this.future = []; }

  execute(command) {
    command.execute();
    this.history.push(command);
    this.future = []; // clear redo stack
  }

  undo() {
    const cmd = this.history.pop();
    cmd?.undo();
    this.future.push(cmd);
  }

  redo() {
    const cmd = this.future.pop();
    cmd?.execute();
    this.history.push(cmd);
  }
}

class InsertCommand {
  constructor(editor, text) { this.editor = editor; this.text = text; }
  execute() { this.editor.text += this.text; }
  undo() { this.editor.text = this.editor.text.slice(0, -this.text.length); }
}
```

---

## Links
- [[Study Plan/LLD]] — topic list
- [[Study Plan/Answer Bank/README]] — all answer files
