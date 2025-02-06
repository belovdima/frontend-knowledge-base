# 🚀 Типизация в TypeScript

TypeScript добавляет **строгую статическую типизацию** в JavaScript, что помогает **избегать ошибок** на этапе написания кода.

<div align="center">

![image](https://github.com/user-attachments/assets/e390e196-7624-4b03-9d65-9191ef2a954e)

</div>

---

# 📌 Основные правила типизации

## 🔹 1. Типизация переменных

### ✅ **Синтаксис**
```typescript
let переменная: тип = значение;
```

### 🛠 **Примеры**
```typescript
let age: number = 30;
let username: string = "John";
let isAdmin: boolean = true;
```

📌 **Ошибка при присвоении неверного типа:**
```typescript
age = "thirty"; // ❌ Ошибка: "string" не может быть присвоен "number"
```

---

## 🔹 2. Типизация массивов

### ✅ **Синтаксис**
```typescript
let массив: тип[];
// или
let массив: Array<тип>;
```

### 🛠 **Примеры**
```typescript
let numbers: number[] = [1, 2, 3, 4, 5];
let names: string[] = ["Alice", "Bob", "Charlie"];
let flags: boolean[] = [true, false, true];
```

📌 **Альтернативный вариант записи:**
```typescript
let numbers: Array<number> = [1, 2, 3];
```

---

## 🔹 3. Типизация кортежей (Tuple)

Кортеж (tuple) — массив **с фиксированной длиной и разными типами элементов**.

### ✅ **Синтаксис**
```typescript
let кортеж: [тип1, тип2, ...];
```

### 🛠 **Примеры**
```typescript
let person: [string, number, boolean] = ["Alice", 30, true];
```

📌 **Ошибка при изменении структуры:**
```typescript
person.push("extra"); // ❌ Ошибка: Кортеж фиксированной длины
```

---

## 🔹 4. Типизация объектов

### ✅ **Синтаксис**
```typescript
let объект: { ключ: тип; ключ2: тип; };
```

### 🛠 **Пример**
```typescript
let user: { name: string; age: number; isAdmin: boolean } = {
  name: "John",
  age: 25,
  isAdmin: false,
};
```

📌 **Опциональные свойства (`?`)**
```typescript
let user: { name: string; age?: number } = { name: "Alice" };
```

---

## 🔹 5. Типизация функций

### ✅ **Синтаксис**
```typescript
function имя(параметр: тип, параметр2: тип): тип_возвращаемого_значения { }
```

### 🛠 **Пример**
```typescript
function sum(a: number, b: number): number {
  return a + b;
}
```

📌 **Опциональные параметры (`?`)**
```typescript
function greet(name: string, age?: number): void {
  console.log(`Hello, ${name}`);
}
```

📌 **Функция без `return` (тип `void`)**
```typescript
function logMessage(message: string): void {
  console.log(message);
}
```

📌 **Функция, которая никогда не завершает выполнение (`never`)**
```typescript
function throwError(message: string): never {
  throw new Error(message);
}
```

---

## 🔹 6. Типы `any`, `unknown`, `never`

### ✅ **`any` (отключает проверку типов)**
```typescript
let value: any = "Hello";
value = 42;
value = true; 
```
📌 Использование `any` **снижает безопасность кода**.

### ✅ **`unknown` (строгая альтернатива `any`)**
```typescript
let value: unknown = "Hello";
value = 42;

if (typeof value === "string") {
  console.log(value.toUpperCase()); // ✅ TypeScript не ругается
}
```

### ✅ **`never` (функция, которая никогда не завершает выполнение)**
```typescript
function throwError(message: string): never {
  throw new Error(message);
}
```

---

## 🔹 7. Типы `type` и `interface`

### ✅ **Синтаксис `type`**
```typescript
type ИмяТипа = { ключ: тип; ключ2: тип; };
```

### 🛠 **Пример**
```typescript
type User = {
  name: string;
  age: number;
};

const user: User = { name: "Alice", age: 30 };
```

### ✅ **Синтаксис `interface`**
```typescript
interface ИмяИнтерфейса {
  ключ: тип;
  ключ2: тип;
}
```

### 🛠 **Пример**
```typescript
interface User {
  name: string;
  age: number;
}

const user: User = { name: "Bob", age: 40 };
```

📌 **Расширение интерфейсов (`extends`)**
```typescript
interface Employee extends User {
  role: string;
}

const employee: Employee = { name: "Bob", age: 40, role: "Manager" };
```

---

## 🔹 8. Пересечение и объединение типов

### ✅ **Пересечение (`&`)**
```typescript
type Person = { name: string };
type Worker = { job: string };

type Employee = Person & Worker;

const bob: Employee = { name: "Bob", job: "Developer" };
```

### ✅ **Объединение (`|`)**
```typescript
let id: number | string;
id = 42; // ✅
id = "42"; // ✅
id = true; // ❌ Ошибка
```

---

## 🔹 9. Типизация классов

### ✅ **Синтаксис**
```typescript
class ИмяКласса {
  переменная: тип;
  constructor(параметр: тип) {}
  метод(): тип_возвращаемого_значения {}
}
```

### 🛠 **Пример**
```typescript
class User {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet(): string {
    return `Hello, my name is ${this.name}`;
  }
}

const user = new User("Alice", 30);
console.log(user.greet());
```

📌 **Модификаторы доступа**
```typescript
class Car {
  private brand: string;
  protected speed: number;
  public color: string;

  constructor(brand: string, speed: number, color: string) {
    this.brand = brand;
    this.speed = speed;
    this.color = color;
  }
}

const car = new Car("Tesla", 200, "Red");
car.color = "Blue"; // ✅ Можно изменить
// car.brand = "BMW"; // ❌ Ошибка: private
// car.speed = 300; // ❌ Ошибка: protected
```

---

## ✅ Итоги

✔ **TypeScript добавляет строгую типизацию в JavaScript**  
✔ **Типизировать можно переменные, массивы, объекты, функции, классы**  
✔ **Использование `interface` и `type` помогает структурировать код**  
✔ **Модификаторы `public`, `private`, `protected` управляют доступом в классах**  
✔ **Типы `any`, `unknown`, `never` помогают контролировать значения**  
