1// Differences Between interface and type in TypeScript
In TypeScript, both interface and type can be used to define the shape of an object, but they have some key differences and specific use cases.

Extending and Implementing:
Interfaces are mainly designed for defining the structure of objects and are often used when creating classes. You can extend one interface from another using the extends keyword, and classes can also implement interfaces.

ts
Copy
Edit
interface Person {
  name: string;
}

interface Employee extends Person {
  jobTitle: string;
}
While types can also be extended using intersections (&), the syntax is a bit different and not specifically designed for classes.

Union and Intersection Types:
The type keyword is more flexible when working with complex types like unions or intersections. For example:

ts
Copy
Edit
type Status = "success" | "error" | "loading";
Interfaces can’t do this — they’re not designed for union types.

Merging:
One unique thing about interfaces is that they support declaration merging. That means if you declare the same interface twice, TypeScript will automatically merge their properties.

ts
Copy
Edit
interface Animal {
  name: string;
}

interface Animal {
  age: number;
}

// Animal is now: { name: string; age: number }
Types don’t allow this — if you try to define the same type twice, you’ll get an error.

Performance:
For performance reasons, TypeScript internally treats interfaces a bit differently and more efficiently in large codebases. This rarely matters, but it's another subtle difference.

In short:
Use interface when you’re working with object shapes or defining contracts for classes. Use type when you need unions, intersections, or more complex type expressions.

2// What is keyof in TypeScript?
The keyof keyword is a powerful tool in TypeScript that lets you get a union of the property names (keys) of a given type or interface.

Why use it?
It’s super useful when you want to write generic or reusable code that can safely reference the keys of an object without hardcoding them.

Example:

ts
Copy
Edit
interface User {
  id: number;
  name: string;
  email: string;
}

type UserKeys = keyof User; // "id" | "name" | "email"
So UserKeys is now a type that can only be one of those three strings — "id", "name", or "email".

You can also use it in functions:

ts
Copy
Edit
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user: User = { id: 1, name: "Alice", email: "alice@example.com" };

const userName = getProperty(user, "name"); // "Alice"
This helps TypeScript understand exactly what you’re doing and gives you strong type safety.
