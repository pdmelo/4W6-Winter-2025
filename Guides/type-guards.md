# Type Guards

**JavaScript** is inherently dynamic, meaning variables can hold different types at runtime. **TypeScript** adds static typing for better code safety and maintainability. However, this static typing can sometimes be overly cautious, especially with dynamic data or complex checks. Type guards, type narrowing, and type assertions bridge this gap. Type guards help TypeScript understand type changes based on your code’s logic, while type narrowing refines types automatically. Type assertions, used cautiously, let you override TypeScript’s type checks when necessary, giving you more control over how TypeScript interprets your code. Overall, these mechanisms allow you to write safer, more predictable TypeScript code that leverages the strengths of both static and dynamic typing.

## Type Guards

- **Purpose:** Type guards are how you tell TypeScript, “Hey, I know more about the type of this variable than you do!” They let you safely check the type of a variable at runtime to refine its type within a specific code block.
- How They Work: Type guards typically involve checks like:
  - **`typeof`:** Checking if a value is a primitive type (`typeof value === 'string'`)
  - **`instanceof`:** Checking if an object is an instance of a class (`value instanceof Date`)
  - **Custom type guard functions:** You can define functions that return a boolean using the `parameter is Type` syntax for more complex checks.

### Example

```ts
function isString(value: unknown): value is string {  
    return typeof value === "string";
}
function doSomething(value: unknown) { 
    if (isString(value)) {    
        // TypeScript knows 'value' is a string inside this block    
        console.log(value.toUpperCase());  
    }
}
```



>[!note]
>**unknown vs any**
>
>In TypeScript, `unknown` is like a type-safe version of `any`. `unknown` requires you to check the type of a variable before using it, making your code less prone to unexpected runtime errors.

Essentially, it’s a function that returns a boolean, but it also has a special return type signature that informs TypeScript’s type checker about the type of variable if the guard returns `true`. This is why, while the function itself technically returns a boolean, its return type is expressed differently to leverage TypeScript’s type narrowing capabilities.

### Example

```ts
function isDatabaseError(error: unknown): error is DatabaseError {

  return typeof error.code === "string";

}
```

- **Parameter Type (`unknown`)**: The function takes a parameter `error` of type `unknown`. This is because, in a `catch` block, we don’t know the type of the caught error in advance.
- **Return Type (`error is DatabaseError`)**: This is the special syntax used for type guards. The return type `error is DatabaseError` tells TypeScript that if this function returns `true`, then the `error` object can be treated as an instance of `DatabaseError` in the scope where this type guard is used.
- **Function Logic**: Inside the function, we check whether `error.code` is a string. If this condition is true, we assume `error` is a `DatabaseError` and return `true`. Otherwise, the function returns `false`.
- **Effect of the Type Guard**: When you use this function in an `if` statement, TypeScript understands that within the `if` block, the variable has the type `DatabaseError`.

Here’s an example of how it’s used:

```ts
if (isDatabaseError(error)) {

  // Inside this block, TypeScript treats 'error' as a 'DatabaseError'

  console.error(error.code); // This is safe to access

}
```

In this example, when `isDatabaseError(error)` returns `true`, TypeScript *narrows* the type of `error` to `DatabaseError` within the `if` block, allowing you to safely access properties like `error.code` and `error.message` that are defined on the `DatabaseError` type.



## Type Narrowing

- **Purpose:** Type narrowing is the *process* by which TypeScript leverages your code’s logic to automatically deduce a more specific type for a variable.
- **How It Works:** TypeScript analyzes your code, especially control flow like `if` statements and type guards, to figure out the potential types of a variable within sections of code.

### Example (from above)

- Inside the `if (isString(value)) { ... }` block, TypeScript has *narrowed* the type of `value` from `unknown` to `string`.

## Type Assertions

- **Purpose:** Type assertions are a way to override TypeScript’s type inference, essentially saying “Trust me, I know what I’m doing!”
- How They Work:
  - **Angle brackets:** `<string>value`
  - **`as` keyword:** `value as string`
- **Use with Caution:** Type assertions suppress TypeScript’s type checking. If you’re wrong about the type you assert, you could introduce runtime errors that TypeScript would normally catch for you.

### Example

```ts
const someValue = document.getElementById("someId"); // someValue is an HTMLElement (or null)
// Not ideal, but sometimes necessary
const inputElement = someValue as HTMLInputElement;
```

## Key Points

- Type **guards** protect your code and lead to type narrowing. They are the preferred approach for refining types.
- Type **narrowing** is the mechanism TypeScript uses to update its understanding of types based on your code.
- Type **assertions** are a sometimes-necessary escape hatch, but they should generally be used as a last resort after carefully considering other options.