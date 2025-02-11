# 📖 Оглавление

### 🟢 Основы JavaScript
- [`let`, `const`, `var` – в чём разница?](#variables)
- [Типы данных: `string`, `number`, `boolean`, `null`, `undefined`, `object`, `symbol`, `bigint`](#data-types)
- [Преобразование типов (явное и неявное)](#type-conversion)

### 🔄 Область видимости, контекст и замыкания
- [Замыкания и область видимости: `var` vs `let` vs `const`, `function scope`, `block scope`](#closures-scope)
- [Работа с `this`: глобальный контекст, `bind`, `call`, `apply`](#this-context)

### ⚡ Асинхронность в JavaScript
- [Колбэки и `Promise`](#callbacks-promises)
- [`async/await`](#async-await)
- [Обработка ошибок: `try/catch`, `.catch()`](#error-handling)

### 🏗 Работа с массивами и объектами
- [Методы массивов: `map`, `filter`, `reduce`, `forEach`, `some`, `every`](#array-methods)
- [Деструктуризация объектов и массивов](#destructuring)
- [Операторы `spread` и `rest`](#spread-rest)
- [Работа с `Set`, `Map`, `WeakSet`, `WeakMap`](#sets-maps)

### 🖥 Работа с DOM
- [Методы работы с DOM: `querySelector`, `getElementById`, `innerHTML`, `textContent`](#dom-methods)
- [Добавление и удаление элементов](#dom-manipulation)
- [Всплытие и погружение событий (`Event Bubbling` & `Capturing`)](#event-bubbling)

### 🌐 Работа с API и HTTP
- [`fetch()`, `axios`](#fetch-axios)
- [HTTP-методы: `GET`, `POST`, `PUT`, `DELETE`](#http-methods)
- [`CORS`](#cors)

### 🧩 Алгоритмы и структуры данных
- [Массивы и объекты](#arrays-objects)
- [Стек (`Stack`) и очередь (`Queue`)](#stack-queue)
- [Хэш-таблицы (`объекты {}` и `Map`)](#hash-tables)
- [Деревья (`DOM` – это дерево)](#trees)
- [Поиск (`linear search`, `binary search`)](#search)
- [Сортировки: `bubble sort`, `selection sort`, `merge sort`, `quick sort`](#sorting)
- [Рекурсия](#recursion)
- [Работа с графами](#graphs)

### 🛠 Разбор задач по JavaScript
- [Разворот строки/массива](#reverse-string-array)
- [Поиск дубликатов в массиве](#duplicate-search)
- [Поиск второго по величине числа в массиве](#second-largest)
- [Подсчёт количества уникальных элементов](#unique-count)
- [Проверка анаграмм](#anagram-check)

---

## 🟢 Основы JavaScript

### <a id="variables"></a>📌 `let`, `const`, `var` – в чём разница?

#### 📌 Кратко:
1. **`var`** – имеет **функциональную область видимости** (function scope), поднимается (hoisting) и инициализируется `undefined`.
2. **`let`** – имеет **блочную область видимости** (block scope), поднимается, но **не инициализируется** (`ReferenceError` при обращении до объявления).
3. **`const`** – аналогичен `let`, но **не позволяет переназначать значение**.

---

### 📌 Подробно:

### 🔹 `var`: функциональная область видимости и поднятие (hoisting)
Переменные, объявленные с `var`, доступны **внутри всей функции**, в которой они объявлены.

```javascript
function getDate() {
  var date = new Date();
  return date;
}

console.log(getDate()); // ✅ Выведет дату
console.log(date); // ❌ ReferenceError: date is not defined
```

**Hoisting (`поднятие`)**  
Переменные `var` поднимаются в начало своей области видимости и инициализируются `undefined`:

```javascript
console.log(a); // undefined
var a = 10;
console.log(a); // 10
```

---

### 🔹 `let`: блочная область видимости и отсутствие инициализации
Переменные, объявленные с `let`, доступны **только в том блоке `{}`**, где они объявлены.

```javascript
if (true) {
  let message = "Hello";
}
console.log(message); // ❌ ReferenceError
```

Также `let` поднимается, но **не инициализируется**:

```javascript
console.log(b); // ❌ ReferenceError: Cannot access 'b' before initialization
let b = 20;
```

---

### 🔹 `const`: нельзя переназначать значение
Переменная `const` должна быть инициализирована при объявлении и **не может быть переназначена**.

```javascript
const PI = 3.14;
PI = 3.1415; // ❌ TypeError: Assignment to constant variable.
```

Однако **свойства объектов, объявленных через `const`, можно изменять**:

```javascript
const user = { name: "Alice" };
user.name = "Bob"; // ✅ Работает
user = {}; // ❌ TypeError: Assignment to constant variable.
```

---

### 🔹 Сравнение `var`, `let`, `const`

| Особенность        | `var`                          | `let`                           | `const`                           |
|-------------------|-----------------------------|--------------------------------|---------------------------------|
| **Область видимости** | Функциональная (`function scope`) | Блочная (`block scope`)        | Блочная (`block scope`)         |
| **Поднимается?**   | Да (`undefined`)             | Да, но без инициализации       | Да, но без инициализации        |
| **Можно переназначить?** | Да                           | Да                              | ❌ Нет (но можно менять свойства объектов) |
| **Можно объявлять без значения?** | Да | Да | ❌ Нет (нужно сразу инициализировать) |

**Вывод:**  
- `var` стоит избегать, так как он не ограничивается блоками `{}`.  
- `let` – лучший вариант для изменяемых переменных.  
- `const` – для значений, которые не должны изменяться (но можно менять свойства объектов).

---
***
___

### <a id="data-types"></a>📌 Типы данных: `string`, `number`, `boolean`, `null`, `undefined`, `object`, `symbol`, `bigint`

JavaScript имеет **8 встроенных типов данных**, которые делятся на **примитивные** и **непримитивные** (объектные).

---

### 🔹 Примитивные и непримитивные типы

| Тип данных  | Примитивный? | Описание | Проверка типа |
|------------|-------------|----------|--------------|
| `null`     | ✅ Да       | Отсутствие значения, "пустота". Специальное значение. | `console.log(value === null); // true` |
| `undefined`| ✅ Да       | Значение переменной, которой не присвоено значение. | `console.log(typeof value); // 'undefined'` |
| `boolean`  | ✅ Да       | Логический тип (`true` или `false`). | `console.log(typeof value); // 'boolean'` |
| `number`   | ✅ Да       | Числа (`42`, `3.14`, `Infinity`, `NaN`). | `console.log(typeof value); // 'number'` |
| `string`   | ✅ Да       | Строки (`'Hello'`, `"World"`). | `console.log(typeof value); // 'string'` |
| `symbol`   | ✅ Да       | Уникальные идентификаторы (`Symbol('id')`). | `console.log(typeof value); // 'symbol'` |
| `bigint`   | ✅ Да       | Числа **больше 2^53-1**, например `BigInt(9007199254740991)`. | `console.log(typeof value); // 'bigint'` |
| `object`   | ❌ Нет      | Коллекция данных (`{}`, `[]`, `new Date()`, `function`). | `console.log(typeof value); // 'object'` (но `null` тоже!) |

---

### 🔥 Дополнительная информация

#### 🟢 `null` и `undefined`
- `null` – это **намеренное отсутствие значения**.
- `undefined` – это **отсутствие значения по умолчанию** (переменная объявлена, но не инициализирована).

```javascript
let a; // undefined
let b = null; // null
console.log(a, b); // undefined null
```

#### 🟢 `number`: особенности чисел
- JavaScript использует **IEEE 754** (числа с плавающей запятой).
- `NaN` (Not a Number) – специальное значение для "нечисловых" операций.

```javascript
console.log(0.1 + 0.2); // 0.30000000000000004 (проблема с точностью)
console.log(Number.MAX_SAFE_INTEGER); // 9007199254740991
console.log(Number.isNaN(NaN)); // true
```

#### 🟢 `bigint`: числа сверх `2^53-1`
```javascript
let big = 9007199254740991n;
console.log(big + 1n); // 9007199254740992n
console.log(typeof big); // 'bigint'
```

#### 🟢 `symbol`: уникальные идентификаторы
```javascript
const id1 = Symbol("id");
const id2 = Symbol("id");
console.log(id1 === id2); // false (всегда уникальны)
console.log(typeof id1); // 'symbol'
```

#### 🟢 `object`: хранит сложные структуры данных
```javascript
let user = { name: "Alice", age: 25 };
console.log(user.name); // Alice
console.log(typeof user); // 'object'
```

⚠️ **Особенность:** `typeof null === 'object'` – историческая ошибка в JS.

### **Вывод:**
- **Примитивы хранятся в памяти как значения.**
- **Объекты хранятся как ссылки в памяти.**

---
***
___

### <a id="type-conversion"></a>📌 Преобразование типов (явное и неявное)

Преобразование типов в JavaScript бывает:
- **Явное** – когда преобразование выполняется вручную с помощью функций (`String()`, `Number()`, `Boolean()`)
- **Неявное** – когда приведение происходит автоматически (например, при конкатенации строки и числа)

Примеры:
```javascript
String(123);   // "123" (Явное)
123 + "";      // "123" (Неявное)
```

---

### 🔹 Приведение к **строке**
**При преобразовании в `string` большинство значений становятся их текстовым представлением.**

| Значение      | `String(value)` | Неявное (`value + ""`) |
|--------------|----------------|------------------------|
| `null`       | `"null"`        | `"null"`              |
| `undefined`  | `"undefined"`   | `"undefined"`         |
| `true`       | `"true"`        | `"true"`              |
| `false`      | `"false"`       | `"false"`             |
| `1`          | `"1"`           | `"1"`                 |
| `NaN`        | `"NaN"`         | `"NaN"`               |
| `1000 * 9e10` | `"9e+12"`      | `"9e+12"`             |
| `{}`         | `"[object Object]"` | `"[object Object]"` |
| `{name: "Ivan"}` | `"[object Object]"` | `"[object Object]"` |
| `[]`         | `""`            | `""`                  |
| `[1,2,3]`    | `"1,2,3"`       | `"1,2,3"`             |

⚠️ **Особенность**:  
- **Объект** `{}` превращается в `"[object Object]"`.
- **Пустой массив `[]`** превращается в `""` (пустую строку).
- **Массив `[1,2,3]`** превращается в строку `"1,2,3"`.

---

### 🔹 Приведение к **числу**
**При преобразовании в `number` используются логика и правила обработки строк, массивов и объектов.**

| Значение     | `Number(value)` |
|-------------|----------------|
| `null`      | `0`            |
| `undefined` | `NaN`          |
| `true`      | `1`            |
| `false`     | `0`            |
| `1`         | `1`            |
| `NaN`       | `NaN`          |
| `1000 * 9e10` | `9e+12`      |
| `{}`        | `NaN`          |
| `{name: "Ivan"}` | `NaN`     |
| `[]`        | `0`            |
| `[1,2,3]`   | `NaN`          |
| `"Ivan"`    | `NaN`          |
| `"0"`       | `0`            |
| `"123"`     | `123`          |

⚠️ **Особенности**:
- `Number(null) → 0`
- `Number(undefined) → NaN`
- **Пустой массив `[]`** превращается в `0`, но `[1,2,3]` – в `NaN`.

---

### 🔹 Приведение к **логическому типу**
**Всё, кроме `"пустых"` значений, является `true`.**

| Значение     | `Boolean(value)` | Истинность |
|-------------|----------------|------------|
| `null`      | `false`        | ❌ Ложное  |
| `undefined` | `false`        | ❌ Ложное  |
| `NaN`       | `false`        | ❌ Ложное  |
| `0`         | `false`        | ❌ Ложное  |
| `-0`        | `false`        | ❌ Ложное  |
| `""`        | `false`        | ❌ Ложное  |
| `false`     | `false`        | ❌ Ложное  |
| `true`      | `true`         | ✅ Истинное |
| `1`         | `true`         | ✅ Истинное |
| `-1`        | `true`         | ✅ Истинное |
| `1000 * 9e10` | `true`       | ✅ Истинное |
| `{}`        | `true`         | ✅ Истинное |
| `{name: "Ivan"}` | `true`     | ✅ Истинное |
| `[]`        | `true`         | ✅ Истинное |
| `[1,2,3]`   | `true`         | ✅ Истинное |
| `() => {}`  | `true`         | ✅ Истинное |
| `"Ivan"`    | `true`         | ✅ Истинное |
| `"0"`       | `true`         | ✅ Истинное |

⚠️ **Особенности**:
- **Пустой массив `[]` → `true`**
- **Пустой объект `{}` → `true`**
- **Строка `"0"` → `true`** (даже если это `"0"`!)

---

### 📌 Итоги
- **`String(value)`** – превращает в строку (`""`, `"null"`, `"1,2,3"`, `"[object Object]"`).
- **`Number(value)`** – превращает в число (`0`, `NaN`, `1`, `123`, `9e+12`).
- **`Boolean(value)`** – определяет "истинность" (`false` только у `"пустых"` значений).

🔥 **Запомнить важные моменты:**
- `null → 0` при `Number()`, но `false` при `Boolean()`
- `undefined → NaN`
- `[] → ""` при `String()`, `0` при `Number()`, но `true` при `Boolean()`
- `{}` всегда `true`, но `NaN` при `Number()`
- `"0"` – `true`, `0` – `false` при `Boolean()`
- `Symbol()` нельзя привести к `string` и `number`

---
***
___

## 🔄 Область видимости, контекст и замыкания

### <a id="closures-scope"></a>📌 Замыкания

🔹 **Лексическое окружение** – это объект, содержащий переменные текущей области и ссылку на родительское окружение.  
🔹 **Функции "помнят" окружение, в котором были созданы.**  

### 🧠 Что такое замыкание?
> **Замыкание** – это способность функции **запоминать** лексическое окружение и обращаться к нему даже после завершения работы внешней функции.

### 🛠 Пример замыкания:
```javascript
const x = 1;
const logToConsole = function () {
  console.log(x);
};
logToConsole(); // 1
```
📌 **Функция `logToConsole` запомнила `x` из глобального окружения – это и есть замыкание.**  

---
***
___

### <a id="this-context"></a>📌 Работа с `this`: глобальный контекст, `bind`, `call`, `apply`

`this` – это ключевое слово, которое ссылается на объект, в контексте которого оно используется.  
Контекст зависит не от места объявления функции, а от способа её вызова.

---

## 📌 Что такое `this` и как оно работает?

Если у нас есть объект `person`, и мы хотим обратиться к его свойству `name`, мы можем написать `this.name`, но **только если мы находимся в контексте объекта `person`**.

```javascript
const person = {
    name: "Dima",
    home: "Birulevo",
    statement: function () {
        console.log(`Hi, my name is ${this.name}, I live in ${this.home}`);
    },
};

person.statement(); // "Hi, my name is Dima, I live in Birulevo"
```
📌 **Здесь `this` ссылается на сам объект `person`, так как функция `statement` вызывается через него.**

---

## ❌ Ошибки при работе с `this`

Рассмотрим ошибку, которая часто встречается у новичков:

```javascript
const person1 = {
    name: "Dima",
    home: "Birulevo",
    statement: function () {
        console.log(`Hi, my name is ${name}, I live in ${home}`); // ❌ Ошибка!
    },
};

person1.statement();
```
📌 **Почему ошибка?**  
Переменные `name` и `home` здесь **не определены** – JavaScript ожидает, что они будут объявлены в той же области видимости.  
Но вместо этого они принадлежат объекту, и к ним нужно обращаться через `this`:

```javascript
const person1 = {
    name: "Dima",
    home: "Birulevo",
    statement: function () {
        console.log(`Hi, my name is ${this.name}, I live in ${this.home}`);
    },
};

person1.statement(); // "Hi, my name is Dima, I live in Birulevo"
```
📌 **Теперь всё работает правильно, так как `this.name` и `this.home` берут значения из объекта `person1`.**

---

## 📌 `this` в обычных функциях

Теперь попробуем передать объект в обычную функцию и вызовем её:

```javascript
const person2 = {
    name: "Dasha",
    home: "Mytischi",
};

function WhoAmI() {
    console.log(`I am ${this.name}, and I live in ${this.home}`);
}

WhoAmI(); // "I am undefined, and I live in undefined"
```
📌 **Что пошло не так?**  
`WhoAmI()` – это обычный вызов функции, а значит, `this` внутри неё **не ссылается** на `person2`, а **указывает на глобальный объект** (`window` в браузере или `undefined` в strict mode).

### 🔹 Как исправить?  
Использовать `.call()`, `.apply()` или `.bind()`, чтобы **принудительно задать контекст `this`**.

---

## 📌 Управление `this` с помощью `call()`, `apply()`, `bind()`

### 1️⃣ `call()`
```javascript
const person = { name: "Dasha", home: "Mytischi" };

function WhoAmI() {
    console.log(`I am ${this.name}, and I live in ${this.home}`);
}

WhoAmI.call(person); // "I am Dasha, and I live in Mytischi"
```
📌 `WhoAmI.call(person)` говорит: "Вызови `WhoAmI`, но `this` внутри неё теперь ссылается на `person`".


---

### 2️⃣ `apply()`
`apply()` работает аналогично `call()`, но принимает аргументы в виде массива:

```javascript
function greet(greeting, emoji) {
    console.log(`${greeting}, I am ${this.name} ${emoji}`);
}

greet.apply(person, ["Hello", "😊"]); 
// "Hello, I am Dasha 😊"
```
📌 **Разница между `call` и `apply` – в передаче аргументов:**
```javascript
call(thisArg, arg1, arg2, ...)
apply(thisArg, [arg1, arg2, ...])
```

---

### 3️⃣ `bind()`
`bind()` **не вызывает функцию сразу**, а **создаёт новую функцию** с привязанным `this`:

```javascript
const boundWhoAmI = WhoAmI.bind(person);
boundWhoAmI(); // "I am Dasha, and I live in Mytischi"
```
📌 **Теперь `boundWhoAmI()` всегда будет выполняться с `this`, равным `person`**.

---

## 📌 `this` в стрелочных функциях

Стрелочные функции ведут себя **по-другому**:  
Они **не имеют собственного `this`**, а **берут его из родительского контекста**.

```javascript
const person3 = {
    name: "Alex",
    home: "Moscow",
    statement: () => {
        console.log(`Hi, my name is ${this.name}, I live in ${this.home}`);
    },
};

person3.statement(); // "Hi, my name is undefined, I live in undefined"
```
📌 **Почему?**  
Так как стрелочная функция не имеет своего `this`, она ищет его **в родительском окружении**, а там `this` – это глобальный объект.

✅ **Использование стрелочной функции внутри обычной позволяет сохранить `this`:**
```javascript
const obj = {
    count: 0,
    increment: function () {
        setTimeout(() => {
            this.count++;
            console.log(this.count);
        }, 1000);
    },
};

obj.increment(); // `this` остаётся ссылкой на obj
```
📌 **Так как стрелочная функция внутри `setTimeout()` берёт `this` из `increment()`, оно остаётся `obj`.**

---

## 📌 `this` в обработчиках событий

В обработчиках событий `this` **указывает на элемент, на котором произошло событие**:

```javascript
const button = document.querySelector("button");

button.addEventListener("click", function () {
    console.log(this); // `this` – сам элемент `button`
});
```
📌 **Если использовать стрелочную функцию, `this` будет взято из внешнего контекста:**
```javascript
button.addEventListener("click", () => {
    console.log(this); // `this` – глобальный объект (window)
});
```
⚠ **Осторожно!**  
Если стрелочная функция объявлена внутри объекта и передана как обработчик события, `this` не будет ссылаться на объект.

---

## ✅ Итоги

✔ **`this` зависит от способа вызова функции, а не от её объявления.**  
✔ **В глобальном контексте (`window` в браузере, `global` в Node.js).**  
✔ **В методах объекта `this` указывает на сам объект.**  
✔ **В обычных функциях `this` – `window` или `undefined` в strict mode.**  
✔ **Стрелочные функции не имеют своего `this`, а используют внешний контекст.**  
✔ **Использование `call()`, `apply()`, `bind()` позволяет принудительно задать `this`.**

---
***
___

## ⚡ Асинхронность в JavaScript

### <a id="callbacks-promises"></a>📌 Колбэки и `Promise`

### 🌀 Колбэки (Callback)  
**Колбэк** — функция, передаваемая в другую функцию и вызываемая позже.

```javascript
setTimeout(() => console.log('Hello!'), 5000);
```
📌 Колбэк выполняется через 5 сек.  

❌ **Callback Hell**: Вложенные колбэки делают код нечитаемым.  
**Решение** 👉 **Промисы**.

---

### 🔹 Промисы (Promise)  
**Promise** — объект, представляющий асинхронную операцию с состояниями:  
🟡 `pending` | ✅ `fulfilled` | ❌ `rejected`.

```javascript
function request(url) {
  return new Promise((resolve) => resolve('Ответ с сервера'));
}

request('/api/data').then(console.log);
```
📌 Код стал **плоским**, можно цепочкой вызывать `.then()`.

---
***
___

### <a id="async-await"></a>📌 `async/await`

### ⚡ `async/await` – удобный синтаксис  
`async` делает функцию асинхронной, `await` ждёт выполнения промиса.

```javascript
async function loadPosts() {
  const response = await fetch('/api/posts/');
  return await response.json();
}

loadPosts().then(console.log);
```
📌 **Читается легче, чем `.then()`**.

---
***
___

### <a id="error-handling"></a>📌 Обработка ошибок: `try/catch`, `.catch()`

🔥 **Обработка ошибок через `try/catch`**
```javascript
async function loadPosts() {
  try {
    const response = await fetch('/api/posts/');
    return await response.json();
  } catch (e) {
    console.log('Ошибка:', e);
  }
}
```
✅ Удобно **ловить ошибки** и **отлаживать код**.

---
***
___

## 🏗 Работа с массивами и объектами

### <a id="array-methods"></a>📌 Методы массивов: `map`, `filter`, `reduce`, `forEach`, `some`, `every`

###🔥 **Методы массивов: `map`, `filter`, `reduce`, `forEach`, `some`, `every`**

Все они работают **по одинаковому принципу**:  
1️⃣ **Перебирают массив**  
2️⃣ **Передают каждый элемент в функцию**  
3️⃣ **Делают что-то с этими элементами**  

---

## **1️⃣ `map()` – создаёт новый массив**
📌 **Берёт каждый элемент, изменяет его и возвращает новый массив.**

### ✅ **Простой пример**: Умножаем все числа на 2
```javascript
const numbers = [1, 2, 3, 4, 5];

const doubled = numbers.map(function(num) {
    return num * 2;
});

console.log(doubled); // [2, 4, 6, 8, 10]
```
📌 **Как это работает?**  
1️⃣ `num = 1 → 1 * 2 = 2`  
2️⃣ `num = 2 → 2 * 2 = 4`  
3️⃣ `num = 3 → 3 * 2 = 6`  
… и так далее.

✅ **Запись стрелочной функцией (то же самое, но короче):**
```javascript
const doubled = numbers.map(num => num * 2);
```

---

## **2️⃣ `filter()` – отбирает элементы**
📌 **Оставляет только те элементы, которые соответствуют условию.**

### ✅ **Пример**: Оставляем только чётные числа
```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const evenNumbers = numbers.filter(function(num) {
    return num % 2 === 0; // Оставляем только те, которые делятся на 2
});

console.log(evenNumbers); // [2, 4, 6]
```
✅ **Запись стрелочной функцией**:
```javascript
const evenNumbers = numbers.filter(num => num % 2 === 0);
```

---

## **3️⃣ `reduce()` – сворачивает массив в одно значение**
📌 **Проходит по всему массиву и накапливает значение.**

### ✅ **Пример**: Считаем сумму всех чисел
```javascript
const numbers = [1, 2, 3, 4, 5];

const sum = numbers.reduce(function(acc, num) {
    return acc + num;
}, 0);

console.log(sum); // 15
```
📌 **Как это работает?**  
1️⃣ `acc = 0, num = 1 → 0 + 1 = 1`  
2️⃣ `acc = 1, num = 2 → 1 + 2 = 3`  
3️⃣ `acc = 3, num = 3 → 3 + 3 = 6`  
… и так далее.

✅ **Запись стрелочной функцией**:
```javascript
const sum = numbers.reduce((acc, num) => acc + num, 0);
```

---

## **4️⃣ `forEach()` – просто перебирает элементы**
📌 **Ничего не возвращает, просто выполняет действие.**

### ✅ **Пример**: Выводим каждый элемент в консоль
```javascript
const numbers = [1, 2, 3];

numbers.forEach(function(num) {
    console.log(num);
});
```
📌 **Выведет:**
```
1
2
3
```
✅ **Стрелочная функция**:
```javascript
numbers.forEach(num => console.log(num));
```

---

## **5️⃣ `some()` – проверяет, есть ли **хотя бы один** элемент, соответствующий условию**
📌 **Если хотя бы один подходит → `true`, иначе → `false`.**

### ✅ **Пример**: Есть ли в массиве чётные числа?
```javascript
const numbers = [1, 3, 5, 8];

const hasEven = numbers.some(function(num) {
    return num % 2 === 0;
});

console.log(hasEven); // true (8 - чётное)
```
✅ **Стрелочная запись**:
```javascript
const hasEven = numbers.some(num => num % 2 === 0);
```

---

## **6️⃣ `every()` – проверяет, соответствуют ли **все** элементы условию**
📌 **Если ВСЕ соответствуют → `true`, иначе → `false`.**

### ✅ **Пример**: Все ли числа положительные?
```javascript
const numbers = [1, 3, 5, 8];

const allPositive = numbers.every(function(num) {
    return num > 0;
});

console.log(allPositive); // true (все > 0)
```
✅ **Стрелочная запись**:
```javascript
const allPositive = numbers.every(num => num > 0);
```

---

## 🎯 **Итоговая таблица**

| Метод        | Возвращает | Описание |
|-------------|-----------|-----------|
| `map()`     | Новый массив | Преобразует каждый элемент |
| `filter()`  | Новый массив | Оставляет только нужные элементы |
| `reduce()`  | Одно значение | Накапливает результат |
| `forEach()` | `undefined` | Просто выполняет код для каждого элемента |
| `some()`    | `true` / `false` | Есть ли **хотя бы один** подходящий элемент? |
| `every()`   | `true` / `false` | **Все** ли элементы соответствуют условию? |

---

## 🔥 **Вывод**
- `map` и `filter` **создают новые массивы**.  
- `reduce` **накапливает результат**.  
- `forEach` **просто перебирает**, но **ничего не возвращает**.  
- `some` и `every` **проверяют соответствие условию**.

---
***
___

### <a id="destructuring"></a>📌 Деструктуризация объектов и массивов

🔹 **Деструктуризация** — это удобный синтаксис, который упрощает **извлечение данных** из объектов и массивов, избавляя от повторяющихся обращений к их свойствам или элементам.

---

### 🟢 **Деструктуризация объектов**
Допустим, у нас есть объект `person`, содержащий имя и возраст:
```javascript
const person = { name: "Александр", age: 37 };
```
**Без деструктуризации:**
```javascript
const name = person.name;
const age = person.age;
console.log(name, age); // "Александр", 37
```
📌 **Вместо этого можно записать короче:**
```javascript
const { name, age } = person;
console.log(name, age); // "Александр", 37
```
**🎯 Задача:** Получить свойства объекта и задать значения по умолчанию.
```javascript
const point = { x: 120, y: 30 };
const { x, y, color = "black" } = point;

console.log(x, y); // 120, 30
console.log(color); // black (значение по умолчанию)
```

**🎯 Деструктуризация с переименованием полей**
```javascript
const shape = { "name.ru": "квадрат", "color-str": "black" };
const { "name.ru": name, "color-str": color } = shape;

console.log(name, color); // "квадрат", "black"
```
📌 **Переименование полезно, если свойство содержит спецсимволы или конфликтует с переменной.**

---

### 🔵 **Деструктуризация массивов**
**Пример с массивом:**
```javascript
const planets = ["Меркурий", "Венера", "Земля", "Марс"];
```
**Без деструктуризации:**
```javascript
const first = planets[0];
const second = planets[1];
const third = planets[2];
console.log(first, second, third); // "Меркурий", "Венера", "Земля"
```
📌 **С деструктуризацией:**
```javascript
const [first, second, third] = planets;
console.log(first, second, third); // "Меркурий", "Венера", "Земля"
```

📌 **Пропуск ненужных элементов:**
```javascript
const animals = ["🐱", "🐴", "🦆", "🐶", "🐸", "🐹"];
const [cat, , , dog] = animals; // Пропускаем "🐴", "🦆"
console.log(cat, dog); // "🐱", "🐶"
```

📌 **Получение оставшихся элементов с помощью `rest`-оператора:**
```javascript
const [firstAnimal, secondAnimal, ...rest] = animals;
console.log(firstAnimal, secondAnimal); // "🐱", "🐴"
console.log(rest); // ["🦆", "🐶", "🐸", "🐹"]
```

---
***
___

## <a id="spread-rest"></a>📌 Операторы `spread` и `rest`

🔹 **Оператор `rest` (`...`)** позволяет собрать оставшиеся элементы **в массив** или свойства **в объект**.  
🔹 **Оператор `spread` (`...`)** используется для **распаковки** массива или объекта.

---

### 🔥 `rest`-оператор (`...`) в объектах
Допустим, у нас есть объект с несколькими свойствами:
```javascript
const point = { x: 120, y: 30, color: "blue", opacity: 0.4 };
```
**Извлекаем часть данных, а остальные сохраняем в новый объект:**
```javascript
const { color, opacity, ...restPoint } = point;
console.log(restPoint); // { x: 120, y: 30 }
```
📌 **Можно удобно создавать новые объекты, исключая ненужные свойства.**

---

### 🔥 `rest`-оператор (`...`) в массивах
**Соберём оставшиеся элементы в новый массив:**
```javascript
const numbers = [2, 4, 8, 16, 32, 64];
const [elem0, , elem2, ...restNumbers] = numbers;

console.log(elem0, elem2); // 2, 8
console.log(restNumbers); // [16, 32, 64]
```
📌 **Rest-оператор (`...`) всегда ставится в конце!**
```javascript
const [elem0, ...restNumbers, lastElem] = numbers; // ❌ Ошибка!
```

---

### 🔥 `spread`-оператор (`...`) в массивах
**Распаковка массива в новый массив:**
```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const mergedArr = [...arr1, ...arr2];

console.log(mergedArr); // [1, 2, 3, 4, 5, 6]
```
📌 **Можно клонировать массив без изменения оригинала:**
```javascript
const copyArr = [...arr1];
console.log(copyArr); // [1, 2, 3]
```

---

### 🔥 `spread`-оператор (`...`) в объектах
**Объединение объектов:**
```javascript
const user = { name: "Иван", age: 30 };
const additionalInfo = { city: "Москва", job: "Разработчик" };

const mergedUser = { ...user, ...additionalInfo };
console.log(mergedUser);
// { name: "Иван", age: 30, city: "Москва", job: "Разработчик" }
```
📌 **Можно добавлять или перезаписывать свойства при объединении:**
```javascript
const updatedUser = { ...user, age: 31, job: "Программист" };
console.log(updatedUser);
// { name: "Иван", age: 31, job: "Программист" }
```

---

## 📌 Применение в функциях

### 🔥 Использование `rest` для параметров функции
**Передача неопределённого количества аргументов:**
```javascript
function sum(...numbers) {
  return numbers.reduce((acc, num) => acc + num, 0);
}

console.log(sum(1, 2, 3, 4, 5)); // 15
```
📌 **Все переданные аргументы собираются в массив `numbers`.**

---

### 🔥 Использование `spread` для передачи аргументов
```javascript
const values = [10, 20, 30];
console.log(Math.max(...values)); // 30
```
📌 **`spread` распаковывает массив в аргументы функции.**

---

## 📌 Деструктуризация в функциях

### 🔥 Упрощение обработки объектов в функциях
**Обычный способ:**
```javascript
function greet(user) {
  console.log(`Привет, ${user.name}!`);
}
greet({ name: "Анна", age: 25 });
```
📌 **Можно передавать объект и сразу деструктурировать его:**
```javascript
function greet({ name }) {
  console.log(`Привет, ${name}!`);
}
greet({ name: "Анна", age: 25 });
```

---

### 📌 Итоги
✅ **Деструктуризация** делает код чище и удобнее.  
✅ **`spread`-оператор (`...`)** распаковывает массивы и объекты.  
✅ **`rest`-оператор (`...`)** собирает оставшиеся элементы в массив или объект.  
✅ **Деструктуризация часто используется в функциях и методах массивов.**  
✅ **Можно передавать параметры в `filter()`, `map()` и другие методы удобнее.**

---
***
___

### <a id="sets-maps"></a>📌 Работа с `Set`, `Map`, `WeakSet`, `WeakMap`

### <a id="sets"></a>📌 Работа с `Set`

#### 🔹 Что такое `Set`?
**`Set` (множество)** — это структура данных, предназначенная для хранения **уникальных значений** любого типа.  
В отличие от массивов, элементы `Set` **не индексируются**, то есть нельзя получить элемент по индексу.

📌 **Основные особенности `Set`:**
- Хранит **только уникальные значения**.
- Может содержать **значения любого типа** (числа, строки, объекты и др.).
- Гарантирует **порядок добавления** элементов.

---

## 🔹 **Методы `Set`**
| Метод | Описание |
|--------|-------------|
| `add(value)` | Добавляет элемент в `Set` |
| `delete(value)` | Удаляет элемент |
| `has(value)` | Проверяет, есть ли элемент в `Set` |
| `clear()` | Полностью очищает `Set` |
| `forEach(callback)` | Выполняет функцию для каждого элемента |
| `size` | Возвращает количество элементов |

---

## 🔹 **Примеры работы с `Set`**
### 📌 Создание множества и добавление элементов
```javascript
const uniqueIds = new Set();

uniqueIds.add(123);
uniqueIds.add(456);
uniqueIds.add(111);
uniqueIds.add(123); // Дубликаты игнорируются

console.log(uniqueIds.size); // 3
```

---

### 📌 Проверка наличия элемента
```javascript
console.log(uniqueIds.has(111)); // true
console.log(uniqueIds.has(999)); // false
```

---

### 📌 Удаление элемента
```javascript
uniqueIds.delete(111);
console.log(uniqueIds.size); // 2
```

---

### 📌 Очистка множества
```javascript
uniqueIds.clear();
console.log(uniqueIds.size); // 0
```

---

## 🔹 **Как получить уникальные значения из массива?**
```javascript
const numbers = [1, 2, 3, 4, 5, 4, 5, 1, 1];
const uniqueValuesArr = [...new Set(numbers)];

console.log(uniqueValuesArr); // [1, 2, 3, 4, 5]
```
📌 **Это удобный способ очистить массив от дубликатов.**

---

## 🔹 **Как перебрать элементы `Set`?**
Так как `Set` **не индексируется**, нельзя получить элементы по `set[0]`.  
Но можно обойти `Set` через `forEach()` или `for...of`:

### ✅ `forEach()`:
```javascript
const filled = new Set([1, 2, 3, "hello"]);

filled.forEach((value) => {
  console.log(value);
});
// 1
// 2
// 3
// "hello"
```

### ✅ `for...of`:
```javascript
for (let value of filled) {
  console.log(value);
}
// 1
// 2
// 3
// "hello"
```

📌 **Элементы перебираются в порядке их добавления.**

---

## 🔹 **Особенности `Set` с объектами**
`Set` использует **строгое сравнение (`===`)**, но объекты в JavaScript сравниваются **по ссылке**, а не по значению.

### ❌ Два одинаковых объекта – это разные сущности:
```javascript
const obj1 = { size: "L", color: "white" };
const obj2 = { size: "L", color: "white" };

console.log(obj1 === obj2); // false
```

### ❌ Добавление двух объектов с одинаковыми значениями:
```javascript
const closet = new Set();
closet.add(obj1);
closet.add(obj2);

console.log(closet.size); // 2 (разные объекты, разные ссылки)
```
📌 **Даже если два объекта выглядят одинаково, они хранятся как разные элементы, потому что у них разные ссылки в памяти.**

---

## 📌 Итоги
✅ **`Set` – это коллекция уникальных значений**.  
✅ **Поддерживает методы для добавления, удаления и проверки элементов**.  
✅ **Позволяет перебирать элементы через `forEach()` и `for...of`**.  
✅ **Можно использовать `Set` для получения массива уникальных значений**.  
✅ **Работает с примитивами и объектами, но объекты сравниваются по ссылке**.  

---

### 🔹 Что такое `Map`?
**`Map`** — это коллекция для хранения данных в виде **пар [ключ → значение]**, где:
- **Ключ** может быть любого типа (в отличие от объектов, где ключи — только строки или символы).
- **Значение** хранится по уникальному ключу и извлекается с помощью этого ключа.

📌 **Основные особенности `Map`:**
- **Позволяет использовать любые типы данных в качестве ключей** (числа, строки, объекты, функции и т. д.).
- **Гарантирует порядок добавления элементов**.
- **Более эффективен для частых операций добавления/удаления ключей** по сравнению с обычными объектами.

---

## 🔹 **Методы `Map`**
| Метод | Описание |
|--------|-------------|
| `set(key, value)` | Добавляет пару `[ключ → значение]` в `Map` |
| `get(key)` | Возвращает значение по ключу (если нет, `undefined`) |
| `has(key)` | Проверяет, есть ли ключ в `Map` |
| `delete(key)` | Удаляет элемент по ключу |
| `clear()` | Полностью очищает `Map` |
| `size` | Возвращает количество пар в `Map` |
| `keys()` | Возвращает итератор по ключам |
| `values()` | Возвращает итератор по значениям |
| `entries()` | Возвращает итератор по `[ключ, значение]` |
| `forEach(callback)` | Перебирает `Map` (как у массива) |

---

## 🔹 **Примеры работы с `Map`**
### 📌 Создание `Map` и добавление элементов
```javascript
const someData = new Map();

someData.set("1", "Значение под строковым ключом 1");
someData.set(1, "Значение под числовым ключом 1");
someData.set(true, "Значение под булевым ключом true");

console.log(someData.size); // 3
```
📌 `Map` различает **строковые и числовые ключи**, даже если они выглядят одинаково.

---

### 📌 Получение значений по ключу
```javascript
console.log(someData.get(1));   // "Значение под числовым ключом 1"
console.log(someData.get("1")); // "Значение под строковым ключом 1"
console.log(someData.has(true)); // true
```
📌 Если ключ отсутствует, `get()` вернёт `undefined`.

---

### 📌 Удаление элементов и очистка `Map`
```javascript
someData.delete(1);
console.log(someData.size); // 2

someData.clear();
console.log(someData.size); // 0
```

---

## 🔹 **Создание `Map` с начальными значениями**
Можно сразу передать массив `[ключ, значение]`:
```javascript
const map = new Map([
  ["js", "JavaScript"],
  ["css", "Cascading Style Sheets"]
]);

console.log(map.size); // 2
console.log(map.get("js")); // "JavaScript"
```

---

## 🔹 **Перебор `Map`**
### ✅ Используем `for...of`
```javascript
const map = new Map([
  ["html", "HTML"],
  ["css", "CSS"],
  ["js", "JavaScript"]
]);

for (let [key, value] of map) {
  console.log(`${key} — ${value}`);
}
// html — HTML
// css — CSS
// js — JavaScript
```

### ✅ Используем `forEach()`
```javascript
map.forEach((value, key) => {
  console.log(`${key} — ${value}`);
});
```
📌 **При переборе `Map` порядок элементов сохраняется таким, каким они были добавлены.**

---

## 🔹 **Отличия `Map` от обычных объектов**
| Особенность | `Object` | `Map` |
|------------|---------|------|
| Ключи | Только `string` или `symbol` | Любой тип (`object`, `function`, `NaN`, `null`, `undefined`, `number`, `boolean`, `string`) |
| Порядок элементов | Не гарантирован | Гарантирован |
| Размер | `Object.keys(obj).length` | `map.size` |
| Перебор | `for...in`, `Object.keys()` | `for...of`, `map.keys()`, `map.values()` |
| Производительность | Медленнее при частом добавлении/удалении | Быстрее при частом добавлении/удалении |

### 📌 Пример: `Object` хранит ключи только как строки
```javascript
const obj = {
  1: "String",
  "2": "Number",
  true: "Bool"
};

console.log(Object.keys(obj)); // [ '1', '2', 'true' ]
```

### 📌 `Map` поддерживает ключи любого типа:
```javascript
const func = (name) => `Привет, ${name}`;
const objKey = { foo: "bar" };

const map = new Map();
map.set(func, "значение func");
map.set(objKey, "значение object");
map.set(undefined, "значение undefined");
map.set(NaN, "значение NaN");
map.set(null, "значение null");

console.log(map.get(func)); // "значение func"
console.log(map.get(objKey)); // "значение object"
console.log(map.get(undefined)); // "значение undefined"
console.log(map.get(NaN)); // "значение NaN"
console.log(map.get(null)); // "значение null"
```

📌 **Такое невозможно в `Object`, потому что `func` и `objKey` были бы преобразованы в строки `[object Object]`.**

---

## 📌 Итоги
✅ **`Map` – это коллекция пар [ключ → значение]**.  
✅ **Позволяет использовать в качестве ключей любые значения**.  
✅ **Методы `set()`, `get()`, `has()`, `delete()`, `clear()` для управления коллекцией**.  
✅ **Сохраняет порядок элементов**.  
✅ **Более удобен для динамических структур данных, чем `Object`**.  


---

### 🔹 Что такое `WeakSet`?
**`WeakSet`** — это коллекция, **в которой можно хранить только объекты**. Он похож на `Set`, но обладает важными особенностями:

1️⃣ **Только объекты** – в отличие от `Set`, `WeakSet` принимает только объекты (или незарегистрированные `Symbol`).  
2️⃣ **Слабые ссылки** – объекты в `WeakSet` **не предотвращают их удаление** сборщиком мусора.  
3️⃣ **Нет перебора элементов** – в `WeakSet` нет методов для получения всех элементов (`size`, `forEach()`, `values()` и т. д.).  

📌 **`WeakSet` полезен для хранения объектов, которые могут исчезнуть из памяти**, например, при отслеживании DOM-элементов.

---

## 🔹 Отличия `WeakSet` от `Set`
| Особенность | `Set` | `WeakSet` |
|------------|------|------------|
| Какие значения можно хранить | Любые (`number`, `string`, `object`, `boolean`) | Только **объекты** |
| Слабые ссылки (удаление из памяти) | ❌ **Нет** (объект остаётся в `Set`) | ✅ **Да** (удаляется при отсутствии других ссылок) |
| Перебор элементов (`forEach`, `for...of`) | ✅ **Да** | ❌ **Нет** |
| Узнать размер коллекции (`size`) | ✅ **Да** | ❌ **Нет** |
| Доступ к элементам (`values()`, `keys()`, `entries()`) | ✅ **Да** | ❌ **Нет** |

📌 `WeakSet` позволяет **автоматически «забывать» объекты**, если на них больше нет ссылок. Это помогает **избегать утечек памяти**.

---

## 🔹 **Методы `WeakSet`**
| Метод | Описание |
|--------|-------------|
| `add(obj)` | Добавляет объект в `WeakSet` |
| `has(obj)` | Проверяет, есть ли объект в `WeakSet` |
| `delete(obj)` | Удаляет объект из `WeakSet` |

⚠ **Нет методов для получения элементов!** (`size`, `values()`, `entries()`, `forEach()` и т. д.)

---

## 🔹 **Примеры работы с `WeakSet`**
### 📌 Создание `WeakSet` и добавление объектов
```javascript
const ws = new WeakSet();

const obj1 = { name: "Alice" };
const obj2 = { name: "Bob" };

ws.add(obj1);
ws.add(obj2);

console.log(ws.has(obj1)); // true
console.log(ws.has({ name: "Alice" })); // false (новый объект)
```
📌 **В `WeakSet` добавляются только объекты**. Простые значения (`number`, `string`, `boolean`) **нельзя добавить**.

---

### 📌 Удаление объекта из `WeakSet`
```javascript
ws.delete(obj1);
console.log(ws.has(obj1)); // false (объект удалён)
```

---

### 📌 Автоматическое удаление объекта (слабые ссылки)
```javascript
let user = { name: "Charlie" };
const users = new WeakSet();

users.add(user);

console.log(users.has(user)); // true

user = null; // Теперь объект больше нигде не используется
// В какой-то момент объект будет удалён из памяти автоматически
```
📌 **Объект исчезнет из `WeakSet`, когда на него не останется ссылок**.

---

## 🔹 **Когда использовать `WeakSet`?**
### ✅ **Отслеживание DOM-элементов**
Если DOM-элемент удаляется, он автоматически исчезает из `WeakSet`, предотвращая утечки памяти.

```javascript
const elements = new WeakSet();

let div = document.createElement("div");
elements.add(div);

console.log(elements.has(div)); // true

div.remove(); // Элемент удалён из DOM
div = null; // Теперь на него нет ссылок, и он будет удалён из памяти
```

📌 **В `Set` удалённый элемент остался бы навсегда!**  

---

## 📌 Итоги
✅ **`WeakSet` – это коллекция объектов** (примитивы добавить нельзя).  
✅ **Объекты автоматически удаляются, если на них нет ссылок** (слабые ссылки).  
✅ **Нет методов перебора, нет свойства `size`**.  
✅ **Полезен для временного хранения объектов, чтобы избежать утечек памяти**.  

`WeakSet` – полезный инструмент для ситуаций, когда объекты должны **исчезать автоматически**. 


---

## 🖥 Работа с DOM

### <a id="dom-methods"></a>📌 Методы работы с DOM: `querySelector`, `getElementById`, `innerHTML`, `textContent`
<!-- Здесь можно разобрать основные методы работы с DOM. -->

### <a id="dom-manipulation"></a>📌 Добавление и удаление элементов
<!-- Здесь можно объяснить, как динамически добавлять и удалять элементы в DOM. -->

### <a id="event-bubbling"></a>📌 Всплытие и погружение событий (`Event Bubbling` & `Capturing`)
<!-- Здесь можно разобрать механику всплытия и погружения событий в JavaScript. -->

---

## 🌐 Работа с API и HTTP

### <a id="fetch-axios"></a>📌 `fetch()`, `axios`
<!-- Здесь можно объяснить, как работать с API с помощью `fetch()` и `axios`. -->

### <a id="http-methods"></a>📌 HTTP-методы: `GET`, `POST`, `PUT`, `DELETE`
<!-- Здесь можно рассказать о базовых HTTP-методах и их использовании. -->

### <a id="cors"></a>📌 `CORS`
<!-- Здесь можно объяснить, что такое `CORS` и как решать проблемы, связанные с ним. -->

---

## 🧩 Алгоритмы и структуры данных

### <a id="arrays-objects"></a>📌 Массивы и объекты
<!-- Здесь можно разобрать основные структуры данных в JavaScript. -->

### <a id="stack-queue"></a>📌 Стек (`Stack`) и очередь (`Queue`)
<!-- Здесь можно объяснить, как работают стек и очередь, привести примеры использования. -->

### <a id="search"></a>📌 Поиск (`linear search`, `binary search`)
<!-- Здесь можно разобрать алгоритмы линейного и бинарного поиска. -->

---

## 🛠 Разбор задач по JavaScript

### <a id="reverse-string-array"></a>📌 Разворот строки/массива
<!-- Здесь можно разобрать задачу на разворот строки или массива. -->

### <a id="duplicate-search"></a>📌 Поиск дубликатов в массиве
<!-- Здесь можно разобрать задачу на поиск повторяющихся элементов в массиве. -->

### <a id="anagram-check"></a>📌 Проверка анаграмм
<!-- Здесь можно разобрать алгоритм проверки, являются ли две строки анаграммами. -->
