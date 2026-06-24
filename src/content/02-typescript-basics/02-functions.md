---
slug: 'functions'
title: 'Урок 5. Функции в TypeScript'
date: 2024-01-16
description: 'Синтаксис функций, стрелочные функции.'
tags: ['TypeScript', 'Функции']
---

Функции — базовый элемент любой программы. В TypeScript функции объявляются так же, как и в JavaScript, но с дополнительными типами для параметров и возвращаемого значения.

## Обычная функция

```ts
function sum(a: number, b: number): number {
  return a + b;
}

const result = sum(5, 10);
console.log(result); // 15
```

Здесь `a` и `b` объявлены как `number`, а функция возвращает `number`.

## Функции с необязательными параметрами

Если параметр не обязателен, добавьте знак `?`:

```ts
function greet(name: string, title?: string): string {
  return title ? `Привет, ${title} ${name}` : `Привет, ${name}`;
}

console.log(greet('Ирина'));
console.log(greet('Ирина', 'доктор'));
```

## Значения по умолчанию

```ts
function createMessage(text: string, prefix: string = 'Info'): string {
  return `[${prefix}] ${text}`;
}

console.log(createMessage('Система запущена'));
console.log(createMessage('Ошибка', 'Warning'));
```

## Стрелочные функции

Стрелочные функции короче и часто используются для передачи как callback:

```ts
const multiply = (a: number, b: number): number => a * b;
console.log(multiply(4, 6));
```

Если тело функции больше одной строки, используйте фигурные скобки:

```ts
const formatUser = (name: string, age: number): string => {
  return `${name}, ${age} лет`;
};
```

## Анонимные функции и присвоение переменным

Функции могут быть присвоены переменным, а затем вызываться по имени переменной:

```ts
const logMessage = function (message: string): void {
  console.log(message);
};

logMessage('Привет из функции');
```

## Типы функций

Вы можете явно описать тип функции:

```ts
type Calculator = (a: number, b: number) => number;

const subtract: Calculator = (a, b) => a - b;
console.log(subtract(10, 4));
```

## Функции как аргументы

Функции можно передавать другим функциям:

```ts
function applyOperation(a: number, b: number, operation: Calculator): number {
 return operation(a, b);
}

console.log(applyOperation(7, 3, subtract));
console.log(applyOperation(7, 3, multiply));
```

## Функции с возвратом `void`

Если функция ничего не возвращает, используйте `void`:

```ts
function printUser(name: string): void {
  console.log(`Пользователь: ${name}`);
}
```

## Функции с обобщениями (generics)

Обобщения позволяют писать универсальные функции:

```ts
function identity<T>(value: T): T {
  return value;
}

const str = identity<string>('Svelte');
const num = identity<number>(42);
```

## Callback-функции

```ts
function fetchData(url: string, callback: (data: string) => void): void {
  // Моделируем асинхронную загрузку
  setTimeout(() => {
    callback(`Данные с ${url}`);
  }, 500);
}

fetchData('https://api.example.com', (data) => {
  console.log(data);
});
```

## Заключение

Функции в TypeScript — это тот же JavaScript, но с типами. Типизация параметров и возвращаемого значения помогает избежать ошибок и делает код предсказуемым. Стрелочные функции, анонимные функции и generics позволяют писать гибкий и безопасный код.
