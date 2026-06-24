---
slug: 'inheritance'
title: 'Урок 8. Наследование и полиморфизм'
date: 2024-01-21
description: 'Расширение классов и переопределение методов.'
tags: ['TypeScript', 'ООП']
---

Наследование — один из ключевых механизмов объектно-ориентированного программирования. В TypeScript классы могут расширять другие классы, переопределять методы и работать через общий интерфейс.

## Расширение класса с помощью `extends`

Вы можете создать базовый класс и сделать от него более специфичный класс:

```ts
class Person {
  constructor(
    public name: string,
    public age: number
  ) {}

  describe(): string {
    return `${this.name}, ${this.age} лет`;
  }
}

class Employee extends Person {
  constructor(
    name: string,
    age: number,
    public position: string
  ) {
    super(name, age);
  }

  describe(): string {
    return `${super.describe()} — ${this.position}`;
  }
}

const employee = new Employee('Ольга', 28, 'дизайнер');
console.log(employee.describe());
```

## Использование `super`

Ключевое слово `super` позволяет вызвать методы или конструктор базового класса.

```ts
class Vehicle {
  constructor(public brand: string) {}

  getInfo(): string {
    return `Марка: ${this.brand}`;
  }
}

class Car extends Vehicle {
  constructor(
    brand: string,
    public model: string
  ) {
    super(brand);
  }

  getInfo(): string {
    return `${super.getInfo()}, модель ${this.model}`;
  }
}
```

## Полиморфизм

Полиморфизм означает, что объекты разных классов можно обрабатывать единообразно, если они наследуются от одного базового класса или реализуют общий интерфейс.

```ts
function printDescription(item: Person) {
  console.log(item.describe());
}

const person = new Person('Дима', 34);
const manager = new Employee('Лена', 30, 'менеджер');

printDescription(person);
printDescription(manager);
```

## Наследование с интерфейсами

Интерфейсы описывают набор методов, который могут реализовать разные классы:

```ts
interface Drawable {
  draw(): void;
}

class Circle implements Drawable {
  constructor(private radius: number) {}

  draw(): void {
    console.log(`Рисуем круг радиуса ${this.radius}`);
  }
}

class Square implements Drawable {
  constructor(private size: number) {}

  draw(): void {
    console.log(`Рисуем квадрат со стороной ${this.size}`);
  }
}

const shapes: Drawable[] = [new Circle(5), new Square(10)];
shapes.forEach((shape) => shape.draw());
```

## Защищенные и приватные члены

Наследование работает с `protected` членами:

```ts
class Account {
  protected balance: number;

  constructor(balance: number) {
    this.balance = balance;
  }
}

class SavingsAccount extends Account {
  deposit(amount: number) {
    this.balance += amount;
  }
}
```

При этом `private` члены недоступны в потомках.

## Переопределение методов

Класс-потомок может изменить поведение метода базового класса:

```ts
class Printer {
  print(): void {
    console.log('Печать документа');
  }
}

class ColorPrinter extends Printer {
  print(): void {
    console.log('Печать цветного документа');
  }
}
```

## Абстрактные классы и наследование

Абстрактный класс задаёт шаблон, который должен реализовать потомок.

```ts
abstract class EmployeeBase {
  constructor(public name: string) {}

  abstract getSalary(): number;
}

class FullTimeEmployee extends EmployeeBase {
  constructor(
    name: string,
    private salary: number
  ) {
    super(name);
  }

  getSalary(): number {
    return this.salary;
  }
}
```

## Пример с несколькими классами

```ts
class Animal {
  constructor(public name: string) {}

  speak(): string {
    return `${this.name} издаёт звук`;
  }
}

class Dog extends Animal {
  speak(): string {
    return `${this.name} гавкает`;
  }
}

class Cat extends Animal {
  speak(): string {
    return `${this.name} мяукает`;
  }
}

const animals: Animal[] = [new Dog('Тузик'), new Cat('Мурка')];
animals.forEach((animal) => console.log(animal.speak()));
```

## Заключение

Наследование и полиморфизм позволяют строить гибкие архитектуры. TypeScript помогает правильно описать отношения между классами и гарантировать, что методы реализованы корректно. Это делает код понятнее и проще для поддержки.
