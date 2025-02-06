# 📚 JavaScript: Полный Гид

## 📖 Оглавление

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
<!-- Здесь можно описать различия между `let`, `const` и `var`, их область видимости и особенности использования. -->

### <a id="data-types"></a>📌 Типы данных: `string`, `number`, `boolean`, `null`, `undefined`, `object`, `symbol`, `bigint`
<!-- Здесь можно рассказать о примитивных и сложных типах данных в JavaScript. -->

### <a id="type-conversion"></a>📌 Преобразование типов (явное и неявное)
<!-- Здесь можно объяснить, как работает приведение типов в JavaScript. -->

---

## 🔄 Область видимости, контекст и замыкания

### <a id="closures-scope"></a>📌 Замыкания и область видимости: `var` vs `let` vs `const`, `function scope`, `block scope`
<!-- Здесь можно объяснить, что такое область видимости, как работают переменные в разных контекстах и что такое замыкание. -->

### <a id="this-context"></a>📌 Работа с `this`: глобальный контекст, `bind`, `call`, `apply`
<!-- Здесь можно объяснить, как работает `this` в разных ситуациях, а также разобрать `bind`, `call`, `apply`. -->

---

## ⚡ Асинхронность в JavaScript

### <a id="callbacks-promises"></a>📌 Колбэки и `Promise`
<!-- Здесь можно объяснить, что такое колбэки, какие у них проблемы и как промисы их решают. -->

### <a id="async-await"></a>📌 `async/await`
<!-- Здесь можно разобрать, как `async/await` упрощает работу с асинхронным кодом. -->

### <a id="error-handling"></a>📌 Обработка ошибок: `try/catch`, `.catch()`
<!-- Здесь можно объяснить, как правильно обрабатывать ошибки в асинхронном коде. -->

---

## 🏗 Работа с массивами и объектами

### <a id="array-methods"></a>📌 Методы массивов: `map`, `filter`, `reduce`, `forEach`, `some`, `every`
<!-- Здесь можно разобрать основные методы массивов и их применение. -->

### <a id="destructuring"></a>📌 Деструктуризация объектов и массивов
<!-- Здесь можно объяснить, как работает деструктуризация в JavaScript. -->

### <a id="spread-rest"></a>📌 Операторы `spread` и `rest`
<!-- Здесь можно разобрать разницу между `spread` и `rest`, а также их применение. -->

### <a id="sets-maps"></a>📌 Работа с `Set`, `Map`, `WeakSet`, `WeakMap`
<!-- Здесь можно рассказать, чем отличаются `Set` и `Map`, а также `WeakSet` и `WeakMap`. -->

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
