---
slug: 'control-flow'
title: 'Урок 6. Управляющие конструкции'
date: 2024-01-17
description: 'If, else, switch и циклы.'
tags: ['TypeScript', 'Logic']
---

Управляющие конструкции позволяют выбирать ветки выполнения и повторять действия. В TypeScript эти конструкции работают как в JavaScript, но с преимуществом строгой типизации и проверкой выражений.

## `if`, `else if`, `else`

Самый распространённый способ ветвления — условный оператор `if`.

```ts
const score: number = 78;

if (score >= 90) {
 console.log('Отлично');
} else if (score >= 75) {
 console.log('Хорошо');
} else {
 console.log('Нужно подтянуть');
}
```

TypeScript подробно проверяет переменные в условии. Например, можно использовать `typeof`:

```ts
function describeValue(value: string | number) {
 if (typeof value === 'string') {
  console.log(`Строка длиной ${value.length}`);
 } else {
  console.log(`Число: ${value}`);
 }
}
```

## Тернарный оператор

Короткая форма `if` — тернарный оператор:

```ts
const isActive: boolean = true;
const status = isActive ? 'активен' : 'не активен';
console.log(status);
```

## `switch`

`switch` удобен, когда нужно сравнить одно значение с несколькими вариантами.

```ts
const color: string = 'blue';

switch (color) {
  case 'red':
    console.log('Красный');
    break;
  case 'blue':
    console.log('Синий');
    break;
  case 'green':
    console.log('Зелёный');
    break;
 default:
  console.log('Неизвестный цвет');
}
```

### `switch` с перечислениями

```ts
enum Direction {
  Up = 'up',
  Down = 'down',
  Left = 'left',
  Right = 'right'
}

function handleDirection(dir: Direction) {
  switch (dir) {
    case Direction.Up:
      console.log('Вверх');
      break;
    case Direction.Down:
      console.log('Вниз');
      break;
    default:
      console.log('Другой');
 }
}
```

## Цикл `for`

Цикл `for` используется для повторения блока кода фиксированное количество раз.

```ts
for (let i = 0; i < 5; i += 1) {
  console.log(`Итерация ${i}`);
}
```

### `for...of`

Для перебора массивов удобен `for...of`:

```ts
const fruits: string[] = ['яблоко', 'банан', 'киви'];

for (const fruit of fruits) {
  console.log(fruit);
}
```

### `for...in`

`for...in` проходит по ключам объекта:

```ts
const user = { name: 'Олег', age: 30 };
for (const key in user) {
  console.log(`${key}: ${user[key as keyof typeof user]}`);
}
```

## Цикл `while`

Цикл `while` выполняется, пока условие истинно.

```ts
let n: number = 3;
while (n > 0) {
  console.log(n);
  n -= 1;
}
```

## Цикл `do...while`

В `do...while` тело выполняется хотя бы один раз.

```ts
let count: number = 0;
do {
  console.log('Выполнение тела');
  count += 1;
} while (count < 2);
```

## Пример вложенных условий и циклов

```ts
const users = [
  { name: 'Аня', age: 22 },
  { name: 'Борис', age: 17 },
  { name: 'Виктор', age: 34 }
];

for (const user of users) {
  if (user.age >= 18) {
    console.log(`${user.name} — взрослый`);
  } else {
    console.log(`${user.name} — ещё нет`);
  }
}
```

## Сужение типов

TypeScript умеет сузить типы в условиях:

```ts
function printValue(value: string | null) {
  if (value === null) {
    console.log('Нет значения');
  } else {
    console.log(value.toUpperCase());
  }
}
```

## Советы

- Используйте `if`/`else` для простых условий.
- Используйте `switch` для множества возможных значений одного выражения.
- Предпочитайте `for...of` для массивов.
- Убедитесь, что цикл завершится, чтобы избежать бесконечного выполнения.

## Итог

Управляющие конструкции позволяют гибко управлять логикой. Благодаря строгой типизации TypeScript вы получаете понятные и безопасные условия, а также возможность ловить ошибки на этапе компиляции.
