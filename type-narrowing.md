# Type Narrowing in TypeScript

## Introduction

Type narrowing makes a broad type more specific after checking a value. It helps safely handle variables with multiple possible types.

## Detailed Explanation

**1. `typeof`**

Checks primitive types such as strings and numbers. Inside the `if` block, TypeScript treats `value` as a `string`, and after it returns, `value` is a `number`.

```ts
function format(value: string | number): string {
  if (typeof value === "string") {
    return value.toLowerCase();
  }
  return value.toFixed(2);
}
```

**2. `instanceof`**

Checks whether an object belongs to a particular class. This also works with built-in classes such as `Date`.

```ts
class Dog {
  bark(): string { return "Woof!"; }
}

function describe(value: Dog | Date): string {
  if (value instanceof Dog) return value.bark();
  return value.toDateString();
}
```

**3. `in` operator**

Checks whether an object contains a specific property. It is useful for unions of object types where each member has different properties.

```ts
type Admin = { permissions: string[] };
type Guest = { visitCode: string };

function identify(user: Admin | Guest): string {
  if ("permissions" in user) return "Admin";
  return "Guest";
}
```

These checks help TypeScript identify the correct type before accessing its properties or methods.

## Conclusion

Use `typeof` for primitive types, `instanceof` for class instances, and `in` for object properties. Type narrowing makes TypeScript code safer and easier to understand. Without it, the compiler would reject calls like `toLowerCase()` on a union type, since not every member supports them.