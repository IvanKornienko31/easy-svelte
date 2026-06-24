---
slug: 'classes'
title: 'Урок 7. Классы и объекты'
date: 2024-01-20
description: 'Основы ООП в TypeScript.'
tags: ['TypeScript', 'ООП']
---

Классы помогают моделировать объекты реального мира. В TypeScript они выглядят как в JavaScript, но с поддержкой типов, модификаторов доступа и интерфейсов.

## Объявление класса

```ts
class User {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet(): string {
    return `Привет, меня зовут ${this.name}`;
  }
}

const user = new User('Анна', 27);
console.log(user.greet());
```

## Упрощённый синтаксис конструктора

В TypeScript можно объявить свойства прямо в параметрах конструктора:

```ts
class Product {
  constructor(
    public id: number,
    public name: string,
    private price: number
  ) {}

  getInfo(): string {
    return `${this.name} стоит ${this.price} руб.`;
  }
}

const product = new Product(1, 'Книга', 499);
console.log(product.getInfo());
```

## Модификаторы доступа

- `public` — открытый доступ (по умолчанию);
- `private` — доступ только внутри класса;
- `protected` — доступ внутри класса и его наследников.

```ts
class Counter {
  private value: number = 0;

  increment(): void {
    this.value += 1;
  }

  getValue(): number {
    return this.value;
  }
}
```

## Интерфейсы и классы

Интерфейсы описывают структуру объекта:

```ts
interface Point {
  x: number;
  y: number;
}

class Location implements Point {
  constructor(
    public x: number,
    public y: number
  ) {}
}

const location = new Location(10, 20);
```

## Наследование

Класс может наследовать другой класс, расширяя его поведение.

```ts
class Animal {
  constructor(public name: string) {}

  speak(): string {
    return `${this.name} издаёт звук`;
  }
}

class Dog extends Animal {
  speak(): string {
    return `${this.name} говорит: Гав!`;
  }
}

const dog = new Dog('Шарик');
console.log(dog.speak());
```

## Абстрактные классы

Абстрактный класс задаёт общую структуру, но не может быть создан напрямую.

```ts
abstract class Shape {
  constructor(public color: string) {}

  abstract area(): number;
}

class Rectangle extends Shape {
  constructor(
    color: string,
    public width: number,
    public height: number
  ) {
    super(color);
  }

  area(): number {
    return this.width * this.height;
  }
}

const rect = new Rectangle('blue', 5, 10);
console.log(rect.area());
```

## Полиморфизм

Полиморфизм означает, что разные классы могут иметь общий интерфейс.

```ts
class Cat extends Animal {
  speak(): string {
    return `${this.name} говорит: Мяу`;
  }
}

const animals: Animal[] = [new Dog('Шарик'), new Cat('Мурка')];
animals.forEach((animal) => console.log(animal.speak()));
```

## Пример объекта с методами

```ts
class Cart {
  private items: string[] = [];

  add(item: string): void {
    this.items.push(item);
  }

  list(): string {
    return this.items.join(', ');
  }
}

const cart = new Cart();
cart.add('Футболка');
cart.add('Блокнот');
console.log(cart.list());
```

## Заключение

TypeScript делает классы более надёжными: типы и модификаторы доступа предотвращают ошибки, а интерфейсы и наследование помогают организовать код. Классы — удобный инструмент для создания сложных объектов и структуры приложения.
