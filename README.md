# TypeScript Style Guide

## A structured approach to writing TypeScript code

This guide is based on best practices for writing clean, maintainable, and scalable TypeScript code. It includes specific rules and conventions to follow when writing TypeScript in React projects.

## Introduction

### What
Consistency is key to maintaining a high-quality, scalable, and maintainable codebase. This TypeScript Style Guide enforces best practices using automated tools like ESLint, TypeScript, and Prettier, while also providing design and architectural conventions that developers should follow.

### Why
As projects grow, maintaining a uniform coding style and ensuring best practices become increasingly important. A well-defined style guide provides:

- A consistent codebase, reducing technical debt.
- Faster development cycles with fewer disputes over code style.
- Easier onboarding for new developers by minimizing learning curves.
- Improved readability and maintainability across the team.

### Disclaimer
Like any style guide, this one is opinionated and may not fit every project perfectly. Use it as a baseline and adapt it as necessary to fit your team’s needs while maintaining internal consistency.

### Requirements
This style guide assumes the use of:

- TypeScript v5 or later
- typescript-eslint with strict type-checking enabled
- Prettier for automatic formatting
- React for frontend conventions (though not required)

### TL;DR - Quick Best Practices
✅ Prefer const for immutability and readonly properties

✅ Use union types over enums when possible

✅ Avoid any and prefer unknown or proper type definitions

✅ Use PascalCase for components and camelCase for variables/functions

✅ Keep functions pure, stateless, and single-responsibility

✅ Follow consistent naming conventions across the codebase

✅ Prefer explicit return types for functions

By following these conventions, your TypeScript projects will be more predictable, efficient, and scalable. 🚀

---

## Table of Contents

1. [Basic Rules](#1-basic-rules)
2. [Type Annotations](#2-type-annotations)
3. [Interfaces vs. Types](#3-interfaces-vs-types)
4. [Class vs Functional Components](#4-class-vs-functional-components)
5. [Mixins](#5-mixins)
6. [Naming Conventions](#6-naming-conventions)
7. [Declarations & Alignment](#7-declarations--alignment)
8. [Quotes & Spacing](#8-quotes--spacing)
9. [Props & State](#9-props--state)
10. [Refs & Parentheses](#10-refs--parentheses)
11. [Tags & Methods](#11-tags--methods)
12. [Component Ordering](#12-component-ordering)
13. [Enums](#13-enums)


---

## 1. Basic Rules

- Use **TypeScript** syntax and avoid `any` unless absolutely necessary.
- Always define types for function parameters and return values.
- Enable **strict mode** in `tsconfig.json`.
- Use `const` and `let` instead of `var`.
- Prefer `readonly` for immutable object properties.
- Do not use `namespace`; use ES6 modules instead.
- Avoid non-null assertions (`!`), except when absolutely necessary.

---

## 2. Type Annotations

- Always specify types explicitly when the type is not inferred.
- Avoid redundant type annotations where TypeScript can infer them.

```ts
// Bad
let age: number = 25;

// Good
let age = 25; // TypeScript infers `number`
```

- Use `unknown` instead of `any` where applicable.
- Use `never` for functions that never return.

```ts
// Bad
function throwError(message: string): void {
  throw new Error(message);
}

// Good
function throwError(message: string): never {
  throw new Error(message);
}
```

---

## 3. Interfaces vs. Types

- Use `interface` for defining object shapes.
- Use `type` for unions, intersections, or primitive-based types.

```ts
// Bad
type User = {
  id: number;
  name: string;
};

// Good
interface User {
  id: number;
  name: string;
}
```

- Use `extends` for interface inheritance.

```ts
// Bad
type Admin = User & {
  role: "admin" | "super-admin";
};

// Good
interface Admin extends User {
  role: "admin" | "super-admin";
}
```

---

## 4. Class vs Functional Components

- Prefer **function components** over class components.
- Use `React.FC<T>` for defining functional components with props.

```tsx
// Bad
class UserProfile extends React.Component<{ name: string }> {
  render() {
    return <div>Hello, {this.props.name}</div>;
  }
}

// Good
const UserProfile: React.FC<{ name: string }> = ({ name }) => {
  return <div>Hello, {name}</div>;
};
```

- Use hooks instead of class-based lifecycle methods.

---

## 5. Mixins

- **Do not use mixins**.
- Prefer Higher-Order Components (HOCs) or custom hooks.

```ts
// Bad
const WithLogging = (Base: any) => class extends Base {
  log() {
    console.log("Logging...");
  }
};

// Good
function useLogging() {
  useEffect(() => {
    console.log("Logging...");
  }, []);
}
```

---

## 6. Naming Conventions

- Use **PascalCase** for components.
- Use **camelCase** for variables and functions.
- Use `T` prefix for generic type parameters.
- Use meaningful names.

```ts
// Bad
const x = "John";

// Good
const userName = "John";
```

---

## 7. Declarations & Alignment

- Use **single responsibility** per file.
- Use `export default` for components.
- Maintain **consistent indentation** and spacing.

---

## 8. Quotes & Spacing

- Use **single quotes** for JavaScript/TypeScript.
- Use **double quotes** for JSX attributes.
- Do not pad JSX curly braces.

---

## 9. Props & State

- Always use **interfaces** or **types** for props.
- Avoid `any`; prefer `unknown` when necessary.
- Use **defaultProps** or default function parameters for optional props.

---

## 10. Refs & Parentheses

- Use **ref callbacks** over string refs.
- Wrap JSX in parentheses when multiline.

---

## 11. Tags & Methods

- Use **self-closing tags** where applicable.
- Use **arrow functions** for event handlers.
- Bind event handlers in constructor if using class components.

---

## 12. Component Ordering

For class components, order methods as follows:

1. `static` properties and methods
2. Constructor
3. Lifecycle methods
4. Event handlers
5. Getter methods
6. Render method

---

## 13. Enums

Enums allow defining a set of named constants. Use them when a variable can take one of a few predefined values.

### Numeric Enums

```ts
enum Status {
  Pending,
  InProgress,
  Completed
}
```

### String Enums

```ts
enum Status {
  Pending = "Pending",
  InProgress = "InProgress",
  Completed = "Completed"
}
```

### Prefer Union Types

```ts
type Status = "Pending" | "InProgress" | "Completed";
```

---

## Conclusion

This style guide ensures your TypeScript code follows best practices while staying maintainable and scalable. Adhering to these conventions will improve consistency across projects and facilitate collaboration among developers.

