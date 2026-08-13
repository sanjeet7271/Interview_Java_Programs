# Java Method Overriding — Output-Based Interview Questions

## Question 1 — Basic Overriding

```java
class Parent {
    void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {
    @Override
    void display() {
        System.out.println("Child");
    }
}

public class Test {
    public static void main(String[] args) {

        Parent obj = new Child();
        obj.display();
    }
}
```

### What is the output?

**Answer:**

```text
Child
```

### Why?

The reference type is `Parent`, but the actual object is `Child`.

```text
Reference → Parent
Object    → Child
```

For overridden instance methods, Java uses the **runtime object type**.

---

# Question 2 — Parent Reference and Parent Object

```java
class Parent {
    void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {
    @Override
    void display() {
        System.out.println("Child");
    }
}

public class Test {
    public static void main(String[] args) {

        Parent obj = new Parent();
        obj.display();
    }
}
```

### Output?

```text
Parent
```

Because the actual object is `Parent`.

---

# Question 3 — Child Reference and Child Object

```java
class Parent {
    void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {
    @Override
    void display() {
        System.out.println("Child");
    }
}

public class Test {
    public static void main(String[] args) {

        Child obj = new Child();
        obj.display();
    }
}
```

### Output?

```text
Child
```

---

# Question 4 — Three-Level Inheritance

```java
class A {
    void show() {
        System.out.println("A");
    }
}

class B extends A {
    @Override
    void show() {
        System.out.println("B");
    }
}

class C extends B {
    @Override
    void show() {
        System.out.println("C");
    }
}

public class Test {
    public static void main(String[] args) {

        A obj = new C();
        obj.show();
    }
}
```

### Output?

```text
C
```

### Why?

Runtime object:

```text
new C()
```

Therefore Java selects the most-derived override.

---

# Question 5 — `super` with Overriding

```java
class Parent {

    void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    @Override
    void display() {

        System.out.println("Child");
        super.display();
    }
}

public class Test {

    public static void main(String[] args) {

        Parent obj = new Child();
        obj.display();
    }
}
```

### Output?

```text
Child
Parent
```

### Why?

First:

```java
System.out.println("Child");
```

Then:

```java
super.display();
```

explicitly calls the parent implementation.

---

# Question 6 — Static Method Trick

This is **very important**.

```java
class Parent {

    static void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    static void display() {
        System.out.println("Child");
    }
}

public class Test {

    public static void main(String[] args) {

        Parent obj = new Child();

        obj.display();
    }
}
```

### Output?

```text
Parent
```

### Why?

Static methods are **not overridden**.

They are **hidden**.

Static method resolution is based on the **reference type**.

```text
Reference type = Parent
Therefore → Parent.display()
```

---

# Question 7 — Static Method with Child Reference

```java
class Parent {

    static void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    static void display() {
        System.out.println("Child");
    }
}

public class Test {

    public static void main(String[] args) {

        Child obj = new Child();

        obj.display();
    }
}
```

### Output?

```text
Child
```

Because the reference type is `Child`.

---

# Question 8 — Static + Instance Method

```java
class Parent {

    static void display() {
        System.out.println("Parent Static");
    }

    void show() {
        System.out.println("Parent Instance");
    }
}

class Child extends Parent {

    static void display() {
        System.out.println("Child Static");
    }

    @Override
    void show() {
        System.out.println("Child Instance");
    }
}

public class Test {

    public static void main(String[] args) {

        Parent obj = new Child();

        obj.display();
        obj.show();
    }
}
```

### Output?

```text
Parent Static
Child Instance
```

### Important rule

```text
static method    → reference type
instance method  → runtime object
```

---

# Question 9 — Field Hiding vs Method Overriding

Very common interview question.

```java
class Parent {

    int value = 10;

    void display() {
        System.out.println("Parent Method");
    }
}

class Child extends Parent {

    int value = 20;

    @Override
    void display() {
        System.out.println("Child Method");
    }
}

public class Test {

    public static void main(String[] args) {

        Parent obj = new Child();

        System.out.println(obj.value);
        obj.display();
    }
}
```

### Output?

```text
10
Child Method
```

### Why?

Fields are resolved using the **reference type**.

Methods are resolved using the **runtime object**.

```text
Field  → Parent.value
Method → Child.display()
```

---

# Question 10 — Private Method

```java
class Parent {

    private void display() {
        System.out.println("Parent");
    }

    void call() {
        display();
    }
}

class Child extends Parent {

    private void display() {
        System.out.println("Child");
    }
}

public class Test {

    public static void main(String[] args) {

        Parent obj = new Child();

        obj.call();
    }
}
```

### Output?

```text
Parent
```

### Why?

The private method in `Parent` is not overridden by `Child`.

`Parent.call()` calls `Parent.display()`.

---

# Question 11 — Final Method

```java
class Parent {

    final void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    void test() {
        System.out.println("Child");
    }
}

public class Test {

    public static void main(String[] args) {

        Parent obj = new Child();

        obj.display();
    }
}
```

### Output?

```text
Parent
```

A `final` method cannot be overridden.

---

# Question 12 — Constructor + Overriding

This is a favorite tricky question.

```java
class Parent {

    Parent() {
        display();
    }

    void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    Child() {
        System.out.println("Child Constructor");
    }

    @Override
    void display() {
        System.out.println("Child");
    }
}

public class Test {

    public static void main(String[] args) {

        new Child();
    }
}
```

### Output?

```text
Child
Child Constructor
```

### Why?

When `new Child()` is executed:

```text
Child constructor
      ↓
Parent constructor
      ↓
Parent constructor calls display()
      ↓
Runtime polymorphism
      ↓
Child.display()
```

So even though the parent constructor is executing, the overridden method in `Child` is called.

### Important warning

Calling overridable methods from constructors is generally discouraged because the child object's initialization may not yet be complete.

---

# Question 13 — Multi-Level Constructor + Overriding

```java
class A {

    A() {
        show();
    }

    void show() {
        System.out.println("A");
    }
}

class B extends A {

    @Override
    void show() {
        System.out.println("B");
    }
}

class C extends B {

    @Override
    void show() {
        System.out.println("C");
    }
}

public class Test {

    public static void main(String[] args) {

        new C();
    }
}
```

### Output?

```text
C
```

The runtime object is `C`, so `C.show()` is invoked.

---

# Question 14 — Overriding with `super`

```java
class A {

    void display() {
        System.out.println("A");
    }
}

class B extends A {

    @Override
    void display() {
        System.out.println("B");
        super.display();
    }
}

class C extends B {

    @Override
    void display() {
        System.out.println("C");
        super.display();
    }
}

public class Test {

    public static void main(String[] args) {

        A obj = new C();

        obj.display();
    }
}
```

### Output?

```text
C
B
A
```

### Execution:

```text
C.display()
   ↓
super.display()
   ↓
B.display()
   ↓
super.display()
   ↓
A.display()
```

---

# Question 15 — Overriding + Overloading

This is a **very important senior-level question**.

```java
class Parent {

    void display(int x) {
        System.out.println("Parent int");
    }

    void display(String x) {
        System.out.println("Parent String");
    }
}

class Child extends Parent {

    @Override
    void display(int x) {
        System.out.println("Child int");
    }
}

public class Test {

    public static void main(String[] args) {

        Parent obj = new Child();

        obj.display(10);
        obj.display("Java");
    }
}
```

### Output?

```text
Child int
Parent String
```

### Why?

`display(int)` is overridden.

`display(String)` is inherited because Child didn't override it.

---

# Question 16 — Overloading in Child

```java
class Parent {

    void display(int x) {
        System.out.println("Parent int");
    }
}

class Child extends Parent {

    @Override
    void display(int x) {
        System.out.println("Child int");
    }

    void display(String x) {
        System.out.println("Child String");
    }
}

public class Test {

    public static void main(String[] args) {

        Parent obj = new Child();

        obj.display(10);
        obj.display("Java");
    }
}
```

Will this compile?

### Answer:

**No.**

The reference type is:

```java
Parent obj
```

Parent doesn't have:

```java
display(String)
```

Therefore:

```java
obj.display("Java");
```

causes a compilation error.

This demonstrates:

> **Overload resolution is performed using the reference/compile-time type.**

---

# Question 17 — Covariant Return Type

```java
class Animal {
}

class Dog extends Animal {
}

class Parent {

    Animal getAnimal() {
        System.out.println("Parent");
        return new Animal();
    }
}

class Child extends Parent {

    @Override
    Dog getAnimal() {
        System.out.println("Child");
        return new Dog();
    }
}

public class Test {

    public static void main(String[] args) {

        Parent obj = new Child();

        Animal animal = obj.getAnimal();
    }
}
```

### Output?

```text
Child
```

`Dog` is a subtype of `Animal`, so the covariant return type is valid.

---

# Question 18 — Exception and Overriding

```java
class Parent {

    void display() throws IOException {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    @Override
    void display() throws FileNotFoundException {
        System.out.println("Child");
    }
}
```

Does this compile?

### Answer:

**Yes.**

Because:

```text
FileNotFoundException
        ↓
IOException
```

The child throws a narrower checked exception.

---

# Question 19 — Broader Exception

```java
class Parent {

    void display() throws IOException {
    }
}

class Child extends Parent {

    @Override
    void display() throws Exception {
    }
}
```

Does it compile?

### Answer:

**No.**

`Exception` is broader than `IOException`.

An overriding method cannot throw a broader checked exception.

---

# Question 20 — Most Important Output Question

```java
class Parent {

    int x = 10;

    void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    int x = 20;

    @Override
    void display() {
        System.out.println("Child");
    }
}

public class Test {

    public static void main(String[] args) {

        Parent obj = new Child();

        System.out.println(obj.x);
        obj.display();
    }
}
```

### Output?

```text
10
Child
```

### Memorize this rule:

> **Variables/fields → reference type**

> **Overridden instance methods → runtime object**

---

# Question 21 — Casting

```java
class Parent {

    void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    @Override
    void display() {
        System.out.println("Child");
    }
}

public class Test {

    public static void main(String[] args) {

        Parent obj = new Child();

        obj.display();

        ((Child) obj).display();
    }
}
```

### Output?

```text
Child
Child
```

Both calls invoke `Child.display()`.

---

# Question 22 — Parent Method Using `super`

```java
class Parent {

    void display() {
        System.out.println("Parent");
    }
}

class Child extends Parent {

    @Override
    void display() {
        System.out.println("Child");
    }

    void test() {
        super.display();
    }
}

public class Test {

    public static void main(String[] args) {

        Child obj = new Child();

        obj.test();
    }
}
```

### Output?

```text
Parent
```

`super` explicitly bypasses the child's override and invokes the parent's implementation.

---

# Question 23 — Static + Instance + Field

This is an excellent interview question.

```java
class Parent {

    static int x = 10;
    int y = 20;

    static void display() {
        System.out.println("Parent Static");
    }

    void show() {
        System.out.println("Parent Instance");
    }
}

class Child extends Parent {

    static int x = 100;
    int y = 200;

    static void display() {
        System.out.println("Child Static");
    }

    @Override
    void show() {
        System.out.println("Child Instance");
    }
}

public class Test {

    public static void main(String[] args) {

        Parent obj = new Child();

        System.out.println(obj.x);
        System.out.println(obj.y);

        obj.display();
        obj.show();
    }
}
```

### Output:

```text
10
20
Parent Static
Child Instance
```

### Remember:

```text
static field       → reference type
instance field     → reference type
static method      → reference type
overridden method  → runtime object
```

---

# Question 24 — Interface Overriding

```java
interface Animal {

    default void sound() {
        System.out.println("Animal");
    }
}

class Dog implements Animal {

    @Override
    public void sound() {
        System.out.println("Dog");
    }
}

public class Test {

    public static void main(String[] args) {

        Animal animal = new Dog();

        animal.sound();
    }
}
```

### Output?

```text
Dog
```

The class implementation overrides the interface's default method.

---

# Question 25 — Parent Class Reference with Interface

```java
interface Animal {

    void sound();
}

class Dog implements Animal {

    @Override
    public void sound() {
        System.out.println("Dog");
    }
}

public class Test {

    public static void main(String[] args) {

        Animal animal = new Dog();

        animal.sound();
    }
}
```

### Output?

```text
Dog
```

This is also runtime polymorphism.

---

# 🔥 10 Rules You Should Memorize for Interviews

```text
1. Instance method overriding → runtime polymorphism

2. Reference type determines what methods are accessible.

3. Runtime object determines which overridden instance method executes.

4. Static methods are hidden, not overridden.

5. Private methods are not overridden.

6. Final methods cannot be overridden.

7. Constructors cannot be overridden.

8. Fields are hidden, not overridden.

9. Overriding method cannot reduce access visibility.

10. Overriding method cannot throw a broader checked exception.
```

## Most important interview formula

```text
Parent obj = new Child();

obj.method();
```

If `method()` is a **normal instance method and overridden**:

```text
→ Child method
```

If `method()` is **static**:

```text
→ Parent method
```

If `method` is a **field**:

```text
→ Parent field
```
