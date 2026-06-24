---
slug: 'variables'
title: 'Урок 4. Переменные и типы данных'
date: 2024-01-15
description: 'Изучаем var, final, const и базовые типы.'
tags: ['TypeScript', 'Основы']
---

Переменные в TypeScript — это основа любого приложения. Они хранят данные, которые могут меняться или оставаться неизменными. TypeScript добавляет к JavaScript статическую типизацию: вы явно указываете типы данных, и компилятор помогает избежать ошибок.

## `var`, `let` и `const`

В TypeScript доступны те же декларации переменных, что и в JavaScript:

- `var` — устаревшая форма, имеет функциональную область видимости и может вызывать неожиданные эффекты;
- `let` — современный способ объявлять изменяемые переменные с блочной областью видимости;
- `const` — объявляет константу, значение которой нельзя переназначить.

Пример:

```ts
var version = '1.0';
let count = 0;
const appName = 'Svelte App';

count += 1;
// appName = 'New Name'; // Ошибка: нельзя переназначить const
```

В большинстве случаев используйте `const` по умолчанию, а `let` — когда значение действительно должно меняться.

## Типы данных

TypeScript поддерживает основные примитивы и структурированные типы.

### `string`

```ts
let title: string = 'Привет, TypeScript';
```

### `number`

```ts
let age: number = 25;
let price: number = 199.99;
```

### `boolean`

```ts
let isActive: boolean = true;
let isAdmin: boolean = false;
```

### `string[]` и `number[]`

```ts
let tags: string[] = ['svelte', 'typescript', 'web'];
let scores: number[] = [10, 20, 30];
```

### Кортеж (`tuple`)

Кортежи фиксируют длину массива и типы элементов:

```ts
let user: [number, string] = [1, 'Алексей'];
```

### `enum`

Перечисления удобны для набора именованных констант:

```ts
enum Role {
  Admin,
  Editor,
  Viewer,
}

let currentRole: Role = Role.Editor;
```

### Тип `any`

Тип `any` отключает проверку типов и нужен только для совместимости:

```ts
let value: any = 'строка';
value = 123;
```

Использование `any` не рекомендуется, если можно указать конкретный тип.

## Типы с объединением и пересечением

### Объединение (`union`)

```ts
let id: string | number;
id = 'abc';
id = 42;
```

### Пересечение (`intersection`)

```ts
type User = {
  name: string;
};

type Admin = User & {
  role: string;
};

let admin: Admin = {
  name: 'Мария',
  role: 'admin',
};
```

## Когда использовать `let` и `const`

- `const` — когда значение не должно переназначаться. Это основной вариант для большинства переменных.
- `let` — когда значение должно изменяться, например счетчик, флаг или результат вычисления.
- `var` — используется редко, только если нужно сохранить обратную совместимость с очень старым кодом.

```ts
const maxUsers: number = 100;
let currentUsers: number = 0;

function addUser() {
  if (currentUsers < maxUsers) {
    currentUsers += 1;
  }
}
```

## Пример применения типов

```ts
interface Product {
  id: number;
  name: string;
  price: number;
  inStock: boolean;
}

const product: Product = {
  id: 1,
  name: 'Футболка',
  price: 1299,
  inStock: true,
};

let productNames: string[] = [product.name];
```

TypeScript делает код надежнее: ошибки типа обнаруживаются ещё на этапе компиляции, а не в браузере.

## Заключение

Переменные и типы — это ключ к понятному и безопасному коду. Хорошая практика: использовать `const` по умолчанию, объявлять типы для объектов и массивов, и избегать `any`, если можно определить точный тип.
