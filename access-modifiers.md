# Access Modifiers in TypeScript OOP

## Introduction

Access modifiers control how class properties and methods can be accessed. TypeScript provides `public`, `private`, `protected`, and `readonly`.

## Detailed Explanation

- **public:** Accessible from anywhere.
- **private:** Accessible only inside its declaring class.
- **protected:** Accessible inside the class and its subclasses.
- **readonly:** Prevents reassignment after initialization.

These modifiers are checked only at compile time. Once the code is compiled to JavaScript, the keywords disappear, so they help catch mistakes early rather than enforcing runtime security.

```ts
class Employee {
  public role: string;
  private salary: number;
  protected name: string;

  constructor(name: string, salary: number, role: string) {
    this.name = name;
    this.salary = salary;
    this.role = role;
  }

  public getSalary(): number {
    return this.salary;
  }
}

class Manager extends Employee {
  describe(): string {
    return `${this.name} is a ${this.role}`;
  }
}
```

Here, `Manager` can access `name` because it is protected. However, it cannot directly access `salary` because it is private. If `Manager` tried to read `this.salary`, the compiler would report an error, so the value is only available through the public `getSalary()` method.

Example of readonly:

```ts
class Product {
  constructor(public readonly id: number) {}
}
```

The `id` can be read but cannot be reassigned after construction.

## Conclusion

Access modifiers improve encapsulation and organization in object-oriented programming. Use them to control visibility and prevent unwanted changes to class properties. Choosing the narrowest access level that works keeps your classes easier to maintain.