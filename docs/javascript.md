# 🚀 Замыкание в JavaScript

Чтобы понять, что такое **замыкание**, необходимо сначала разобраться с **лексическим окружением**.

---

## 📌 Лексическое окружение

Лексическое окружение — это **невидимый объект**, который присутствует у любого блока, скрипта или функции в JavaScript. Оно состоит из двух частей:

🔹 **Объект переменных** – содержит все переменные, определённые в текущей области видимости.  
🔹 **Ссылка на родительское окружение** – позволяет функции обращаться к переменным внешней области видимости.

<div align="center">
  <img width="400" alt="Лексическое окружение" src="https://github.com/user-attachments/assets/99f1a6c0-096e-4700-9110-6a59382b8888" />
</div>

---

## 🔍 Примеры работы лексического окружения

### 🛠 Пример 1: Простая функция

```javascript
const x = 1;
const logToConsole = function () {
  const i = 'Hi';
  console.log(i);
};

logToConsole(); // "Hi"
```

### 🧐 Разбор примера

📌 **Глобальное окружение:**  
   - Содержит переменные `x` и `logToConsole`.  
   - Ссылка на родительское окружение = `null`.

📌 **Локальное окружение (при вызове `logToConsole`)**:  
   - Создаётся переменная `i` со значением `"Hi"`.  
   - Окружение имеет ссылку на глобальное.

<div align="center">
  <img src="https://github.com/user-attachments/assets/99f1a6c0-096e-4700-9110-6a59382b8888" alt="Лексическое окружение" width="400px" />
</div>

> ⚠️ **Важно!**  
> Локальное окружение создаётся **только при вызове функции**.

---

## ⏳ Порядок выполнения кода

🔹 **Создаётся глобальное окружение.**  
🔹 **В глобальном окружении появляется переменная `x = 1`.**  
🔹 **Определяется функция `logToConsole`.**  
🔹 **При вызове `logToConsole` создаётся новое окружение.**  
🔹 **Внутри `logToConsole` создаётся переменная `i`.**  
🔹 **Выводится `console.log(i)`.**  
🔹 **Локальное окружение уничтожается.**

---

## 🎨 Визуализация

<div align="center">
<img src="https://github.com/user-attachments/assets/ff1b03d1-2da7-4df7-93d6-4196c127e972" alt="Визуальное представление" width="400px" />
</div>

---

# 🔄 Замыкание

Теперь разберёмся, что такое **замыкание**.

### 🧠 Определение

> **Замыкание** — это способность функции в JavaScript **запоминать** лексическое окружение, в котором она была создана, и обращаться к нему даже после завершения работы внешней функции.

---

## 🛠 Пример 2: Функция с замыканием

Изменим наш предыдущий код, чтобы продемонстрировать **замыкание**.

```javascript
const x = 1;
const logToConsole = function () {
  console.log(x);
};

logToConsole(); // 1
```

---

### 🧐 Разбор кода

1️⃣ **Создаётся глобальное окружение.**  
2️⃣ **В глобальном окружении создаётся переменная `x = 1`.**  
3️⃣ **Определяется функция `logToConsole`.**  
4️⃣ **При вызове `logToConsole` создаётся локальное окружение.**  
5️⃣ **Выполняется `console.log(x)`.**  
6️⃣ **Функция не находит `x` в своём окружении и обращается к глобальному.**  
7️⃣ **Выводит `1`.**  

📌 **Функция "запомнила" своё окружение и может к нему обращаться — это и есть замыкание.**

---

## 🎨 Визуализация замыкания

<div align="center">
<img src="https://github.com/user-attachments/assets/f0c40793-e4e5-4e45-8c98-91f418cc5595" alt="Визуальное представление" width="400px" />
</div>

---

## ✅ Итоги

🔹 **Лексическое окружение** – это объект, хранящий переменные и ссылку на родительское окружение.  
🔹 **Функции в JS "помнят" окружение, в котором были созданы.**  
🔹 **Замыкание позволяет функциям обращаться к переменным из внешнего окружения даже после завершения работы этой области.**  
🔹 **Это важно при работе с колбэками, обработчиками событий и модульными системами.**

---

Вот улучшенная версия раздела **"Наследование в JavaScript"** с более понятной структурой, выделенными ключевыми моментами и пояснениями.

---

# 🚀 Наследование в JavaScript

**Наследование** — это механизм, который позволяет одному классу (дочернему) **унаследовать** свойства и методы другого класса (родительского). Это помогает **избежать дублирования кода** и организовать структуру классов.

## 📌 Основы наследования

В JavaScript наследование реализуется с помощью ключевого слова `extends`. Дочерний класс получает доступ ко всем **свойствам и методам** родительского класса.

### 🛠 Пример 1: Базовый класс и его наследники

Создадим **родительский класс** `Animal`, который содержит:
- Свойство `alive` (указывает, что животное живо).
- Методы `eat()` и `sleep()` (действия, доступные для всех животных).

```javascript
class Animal {
  alive = true;
  
  eat() {
    console.log(`This ${this.name} is eating`);
  }

  sleep() {
    console.log(`This ${this.name} is sleeping`);
  }
}
```

Теперь создадим **два дочерних класса** `Rabbit` и `Fish`, которые будут наследовать `Animal`.

```javascript
class Rabbit extends Animal {
  name = "rabbit";
}

class Fish extends Animal {
  name = "fish";
}
```

Создадим экземпляры этих классов:

```javascript
const rabbit = new Rabbit();
const fish = new Fish();
```

Проверим, что дочерние классы унаследовали свойства и методы родительского класса:

```javascript
console.log(rabbit.alive); // true
fish.eat();  // This fish is eating
```

---

## 🎯 Добавление собственных методов в дочерний класс

Хотя `Rabbit` и `Fish` унаследовали методы `eat()` и `sleep()`, мы можем **добавлять им уникальные методы**.

### 🛠 Пример 2: Дополнительный метод у дочернего класса

Добавим метод `run()` только для класса `Rabbit`, а `Fish` оставим без изменений.

```javascript
class Rabbit extends Animal {
  name = "rabbit";

  run() {
    console.log(`This ${this.name} is running`);
  }
}
```

Теперь `Rabbit` сможет **использовать** метод `run()`, но `Fish` — нет.

```javascript
rabbit.run();  // This rabbit is running
fish.run();    // ❌ TypeError: fish.run is not a function
```

> 📌 **Важно!**  
> Класс `Fish` **не наследует метод `run()`**, так как он был добавлен **только** в `Rabbit`.

---

## 🔄 Переопределение методов родительского класса

Если дочерний класс **должен изменять поведение родительского метода**, можно его **переопределить**.

### 🛠 Пример 3: Изменяем метод `eat()` в классе `Fish`

Добавим уникальную реализацию метода `eat()` для `Fish`, сделав так, чтобы рыба **ела под водой**.

```javascript
class Fish extends Animal {
  name = "fish";

  eat() {
    console.log(`This ${this.name} is eating underwater`);
  }
}
```

Теперь при вызове `eat()` у `Fish`, будет использоваться новая версия метода:

```javascript
rabbit.eat();  // This rabbit is eating
fish.eat();    // This fish is eating underwater
```
## ✅ Итоги

🔹 **Наследование** позволяет избежать дублирования кода, расширяя функциональность классов.  
🔹 **Ключевое слово `extends`** используется для создания дочерних классов.  
🔹 **Методы можно переопределять**, изменяя их логику в дочерних классах.  

---

# ⚡ `super` в JavaScript

`super` — ключевое слово, используемое для вызова **конструктора** или **методов родительского класса**. Оно **очень похоже на** `this`, но имеет одно ключевое отличие:

- **`this`** относится к **текущему объекту**.
- **`super`** относится к **родительскому классу (superclass)**.

---

## 📌 Наследование и необходимость `super`

Рассмотрим базовый класс `Animal`, от которого будут наследоваться `Rabbit`, `Fish` и `Hawk`.

### 🛠 Пример 1: Создаём классы, но пока без конструктора

```javascript
class Animal {}

class Rabbit extends Animal {}
class Fish extends Animal {}
class Hawk extends Animal {}
```

Пока всё работает, ошибок нет. Однако если мы **добавим конструктор в родительский класс**, дочерние классы **перестанут наследовать его автоматически**.

---

## 🔥 ReferenceError: "Must call super() before using this"

Добавим **пустой конструктор** в родительский класс:

```javascript
class Animal {
    constructor() {}
}
```

Теперь попробуем создать конструкторы в дочерних классах:

```javascript
class Rabbit extends Animal {
    constructor(name, age, runSpeed) {
        this.name = name;
        this.age = age;
        this.runSpeed = runSpeed;
    }
}

class Fish extends Animal {
    constructor(name, age, swimSpeed) {
        this.name = name;
        this.age = age;
        this.swimSpeed = swimSpeed;
    }
}

class Hawk extends Animal {
    constructor(name, age, flySpeed) {
        this.name = name;
        this.age = age;
        this.flySpeed = flySpeed;
    }
}
```

Теперь попробуем создать объекты:

```javascript
const rabbit = new Rabbit("Rabbit", 1, 11);
const fish = new Fish("Fish", 2, 5);
const hawk = new Hawk("Hawk", 2, 25);
```

❌ **Ошибка:**  
```
ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor.
```

📌 **Почему?**  
JavaScript **не позволяет** использовать `this` в конструкторе дочернего класса, пока **не вызван конструктор родительского класса**.

🔹 Решение: **Добавить `super()` в дочерние конструкторы.**

---

## ✅ Использование `super()` в конструкторах

Добавим `super()` в каждый дочерний класс:

```javascript
class Rabbit extends Animal {
    constructor(name, age, runSpeed) {
        super(); // ✅ Вызов конструктора родителя
        this.name = name;
        this.age = age;
        this.runSpeed = runSpeed;
    }
}

class Fish extends Animal {
    constructor(name, age, swimSpeed) {
        super();
        this.name = name;
        this.age = age;
        this.swimSpeed = swimSpeed;
    }
}

class Hawk extends Animal {
    constructor(name, age, flySpeed) {
        super();
        this.name = name;
        this.age = age;
        this.flySpeed = flySpeed;
    }
}
```

Теперь программа **работает без ошибок**.

---

## 🎯 Оптимизация с `super()`

Посмотрите, **какой код повторяется** в дочерних классах:

```javascript
this.name = name;
this.age = age;
```

Вместо того чтобы дублировать его, **перенесём эту логику в родительский класс**:

### 🛠 Пример 2: Выносим общие свойства в `super()`

```javascript
class Animal {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
}

class Rabbit extends Animal {
    constructor(name, age, runSpeed) {
        super(name, age); // ✅ Передаём в родительский класс
        this.runSpeed = runSpeed;
    }
}

class Fish extends Animal {
    constructor(name, age, swimSpeed) {
        super(name, age);
        this.swimSpeed = swimSpeed;
    }
}

class Hawk extends Animal {
    constructor(name, age, flySpeed) {
        super(name, age);
        this.flySpeed = flySpeed;
    }
}
```

Теперь конструкторы дочерних классов стали **чище и понятнее**.

📌 **Вывод:**  
🔹 `super()` **должен быть вызван перед использованием `this`**.  
🔹 Можно передавать **аргументы в `super()`**, чтобы избежать дублирования кода.  
🔹 Теперь каждый дочерний класс **наследует свойства `name` и `age`** из `Animal`.

---

## 🚀 `super` для вызова методов родителя

С `super` можно **вызывать методы** родительского класса.

### 🛠 Пример 3: Используем метод родителя в дочернем классе

Добавим метод `move(speed)` в `Animal`, который будет выводить скорость животного:

```javascript
class Animal {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    move(speed) {
        console.log(`Скорость ${this.name} равна ${speed} км/ч`);
    }
}
```

Теперь **используем этот метод в дочернем классе** `Rabbit`:

```javascript
class Rabbit extends Animal {
    constructor(name, age, runSpeed) {
        super(name, age);
        this.runSpeed = runSpeed;
    }

    run() {
        super.move(this.runSpeed); // ✅ Вызываем родительский метод
    }
}
```

Создадим объект `Rabbit` и вызовем его метод `run()`:

```javascript
const rabbit = new Rabbit("Rabbit", 2, 11);
rabbit.run();
```

🖥 **Вывод в консоли:**  
```
Скорость Rabbit равна 11 км/ч
```

📌 **Как это работает?**  
1️⃣ `super.move(this.runSpeed);` вызывает метод `move()` родителя.  
2️⃣ `move(speed)` получает `this.runSpeed` из `Rabbit`.  
3️⃣ В консоли появляется корректное сообщение.

🔹 **Преимущество `super` —** можно **добавлять новую логику**, но при этом использовать код родительского класса.

---

## ✅ Итоги

🔹 **`super()` используется в конструкторах** для вызова родительского конструктора.  
🔹 **Общие свойства можно выносить в родителя**, чтобы избежать дублирования кода.  
🔹 **`super.method()` вызывает методы родителя**, что позволяет переиспользовать код.  
🔹 **Вызов `super()` обязателен перед `this` в конструкторах дочерних классов.**  
