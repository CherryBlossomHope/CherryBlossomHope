## any 和 unknown 的区别

- `any` 类型：
  any 类型是 TypeScript 中的 一种特殊类型，它允许你在编译阶段绕过类型检查。当你声明一个变量为 any 类型时，TypeScript 编译器将不会对它的操作进行类型检查。
  any 类型可以被赋值为任何类型的值，也可以赋值给任何类型的变量。
  使用 any 类型相当于是在告诉 TypeScript：“我相信这个变量的类型，你不需要进行检查。”这可能会导致运行时错误，因为类型错误可能在编译阶段被忽略。

- `unknown` 类型：
  unknown 类型是 TypeScript 3.0 中引入的一种新类型，它是对 any 类型的一个更安全的选择。unknown 类型表示一个未知类型的值。
  与 any 类型不同，unknown 类型的变量不能直接进行任何操作，除非你先进行某种类型的检查（例如使用类型断言或类型守卫）。
  unknown 类型可以被认为是“类型安全的 any”，因为它迫使你在使用它之前先确认类型。

## type 和 interface 的区别

在 TypeScript 中，`type` 和 `interface` 都是用来定义类型的，但它们在使用方式和某些特性上有所不同。以下是一些主要的区别：

1. **定义方式**:
   
   - `type` 用于定义非联合类型或非交叉类型的别名。
   - `interface` 用于定义对象类型，可以扩展或继承其他接口。

2. **扩展和继承**:
   
   - `interface` 可以通过 `extends` 关键字扩展其他接口或接口的集合（多个接口）。
   - `type` 不能直接扩展其他类型，但可以通过交叉类型（`&`）实现类似的效果。

3. **合并声明**:
   
   - TypeScript 允许相同名称的 `interface` 声明合并。这意味着你可以定义多个同名接口，TypeScript 会将它们合并为一个接口。
   - `type` 不支持声明合并。如果你尝试定义两个相同名称的 `type`，将会导致编译错误。

4. **表达式类型**:
   
   - `type` 可以定义任何类型的别名，包括基本类型、联合类型、交叉类型、元组类型等。
   - `interface` 仅限于定义对象类型。

5. **匿名类型**:
   
   - `type` 常用于定义匿名类型或复杂的联合/交叉类型。
   - `interface` 通常用于定义具有明确名称和意图的类型。

6. **类型查询**:
   
   - `type` 不能用于类型查询。你不能在类型查询中使用 `typeof` 来获取一个 `type` 的类型。
   - `interface` 可以用于类型查询，你可以使用 `typeof` 来获取一个 `interface` 的类型。

7. **实现（implements）**:
   
   - 类可以使用 `implements` 关键字来实现 `interface`，表明该类符合接口定义的契约。
   - `type` 不能被类实现。

8. **扩展原始类型**:
   
   - `type` 可以用来扩展原始类型，例如为字符串添加新的属性。
   - `interface` 不能直接扩展原始类型。

9. **动态类型**:
   
   - `type` 可以使用泛型和条件类型来创建更动态的类型。
   - `interface` 通常用于静态类型的定义。

10. **工具类型**:
    
    - `type` 通常用于创建工具类型，如 `Partial`、`Readonly`、`Pick` 等。
    
    - `interface` 不常用于创建工具类型。

## 装饰器

## 高级类型

TypeScript 中的高级类型提供了一种强大的方式来表示复杂的数据结构或操作类型。以下是一些常见的高级类型：

1. **交叉类型 (Intersection Types)**:
   交叉类型允许你将多个类型合并成一个类型，从而这个类型将拥有所有合并类型的特性。使用 `&` 操作符定义交叉类型。
   
   ```typescript
   type Person = {
     name: string;
   };
   
   type Employee = {
     empId: number;
   };
   
   type PersonEmployee = Person & Employee;
   
   const personEmployee: PersonEmployee = {
     name: "John",
     empId: 123,
   };
   ```

2. **联合类型 (Union Types)**:
   联合类型允许你定义一个值可以是几种类型之一的类型。使用 `|` 操作符定义联合类型。
   
   ```typescript
   function formatValue(value: string | number): string {
     return typeof value === "string" ? value : value.toString();
   }
   ```

3. **泛型 (Generics)**:
   泛型允许你在定义函数、接口或类的时候，不预先指定具体的类型，而是在使用的时候再指定类型。这样可以创建可重用的组件。
   
   ```typescript
   function identity<T>(arg: T): T {
     return arg;
   }
   
   let output = identity<string>("myString");
   ```

4. **索引签名 (Index Signatures)**:
   当你想一个对象可以接受任意数量的属性，并且你不想为每个属性都定义一个具体的类型时，可以使用索引签名。
   
   ```typescript
   interface StringArray {
     [index: number]: string;
   }
   
   let myArray: StringArray = ["Bob", "Fred"];
   let myStr: string = myArray[0];
   ```

5. **映射类型 (Mapped Types)**:
   映射类型基于一个已存在的类型创建一个新类型。例如，你可以使用 `Partial` 或 `Readonly` 映射类型来将一个类型的所有属性变为可选或只读。
   
   ```typescript
   type ReadOnly<T> = {
     readonly [P in keyof T]: T[P];
   };
   
   interface Person {
     name: string;
     age: number;
   }
   
   const readOnlyPerson: ReadOnly<Person> = {
     name: "Alice",
     age: 30,
   };
   
   // readOnlyPerson.name = "Bob"; // Error: Cannot assign to 'name' because it is a read-only property.
   ```

6. **条件类型 (Conditional Types)**:
   条件类型是基于条件表达式来决定类型的类型。它们通常用于高级的类型编程和泛型函数中。
   
   ```typescript
   type TypeName<T> = T extends string
     ? "string"
     : T extends number
     ? "number"
     : T extends boolean
     ? "boolean"
     : T extends undefined
     ? "undefined"
     : T extends Function
     ? "function"
     : "object";
   
   type T0 = TypeName<string>; // "string"
   type T1 = TypeName<string[]>; // "object"
   ```

7. **推断类型 (Inference Types)**:
   TypeScript 提供了多种方式来进行类型推断，例如 `ReturnType` 用于获取函数返回类型，`Parameter` 用于获取函数参数类型。
   
   ```typescript
   function add(a: number, b: number) {
     return a + b;
   }
   
   type Num = ReturnType<typeof add>; // Num 类型为 number
   ```

8. **模板字面量类型 (Template Literal Types)**:
   模板字面量类型允许你基于字符串字面量创建新的类型，这在处理联合类型和映射类型时非常有用。
   
   ```typescript
   type EventNames = "click" | "scroll" | "mousemove";
   type Listener = `${EventNames}Handler`;
   
   function handleEvent(eventName: EventNames, handler: Listener) {
     // ...
   }
   
   handleEvent("click", "clickHandler"); // 正确
   handleEvent("scroll", "clickHandler"); // 错误
   ```
   
   这些高级类型为 TypeScript 提供了强大的类型操作能力，使得类型系统更加灵活和表达力强。在实际开发中，合理使用这些高级类型可以帮助你编写更安全、更可维护的代码。
