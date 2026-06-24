---
slug: 'setup'
title: 'Урок 3. Установка TypeScript и Svelte'
date: 2024-01-12
description: 'Пошаговая инструкция по установке SDK.'
tags: ['Setup', 'TypeScript', 'Svelte']
---

Для разработки на Svelte с TypeScript вам понадобится современная версия Node.js и пакетный менеджер. Это базовое окружение позволит запускать сборку, устанавливать зависимости и пользоваться инструментами для работы с Svelte.

## Шаг 1. Установка Node.js

Sначала установите Node.js версии 18 или выше. Это можно сделать несколькими способами:

- Скачав официальный установщик с сайта nodejs.org.
- Через пакетный менеджер, если он уже установлен на вашей системе.
- Через Docker, если вы предпочитаете контейнеры.

После установки проверьте версии:

```bash
node -v
npm -v
```

Если вы используете `pnpm` или `yarn`, установите их дополнительно:

```bash
npm install -g pnpm
npm install -g yarn
```

## Шаг 2. Редактор кода

Для комфортной работы с Svelte рекомендуются следующие редакторы:

- Visual Studio Code + расширение `Svelte` и `Svelte for VS Code`;
- Zed с плагином Svelte;
- WebStorm / IntelliJ IDEA с плагином Svelte.

В VS Code дополнительно полезны расширения:

- `ESLint`;
- `Prettier`;
- `TypeScript`.

## Шаг 3. Создание проекта

Самый простой способ создать проект на Svelte + TypeScript — использовать шаблон Vite.

```bash
npm create vite@latest my-svelte-app -- --template svelte-ts
cd my-svelte-app
npm install
```

Если вы предпочитаете `pnpm`:

```bash
pnpm create vite my-svelte-app -- --template svelte-ts
cd my-svelte-app
pnpm install
```

Или с `yarn`:

```bash
yarn create vite my-svelte-app --template svelte-ts
cd my-svelte-app
yarn
```

Для SvelteKit команда будет такой:

```bash
npx sv create svelte@latest my-sveltekit-app
```

При выборе SvelteKit укажите, что хотите добавить поддержку TypeScript.

## Шаг 4. Запуск проекта

Запустите локальный сервер разработки:

```bash
npm run dev -- --host
```

После этого откройте адрес, который покажет терминал, обычно `http://localhost:5173`.

## Шаг 5. TypeScript и `tsc`

В проекте `tsconfig.json` уже настроен TypeScript. Дополнительно можно установить компилятор глобально, если хотите проверять файлы вне проекта:

```bash
npm install -g typescript
```

Флаги `tsc`:

- `tsc --noEmit` — проверяет типы без генерации кода;
- `tsc --watch` — отслеживает изменения в файлах;
- `tsc --project ./tsconfig.json` — использует конкретный файл конфигурации.

## Шаг 6. Работа с зависимостями

В Svelte-проекте часто устанавливают пакеты с любыми UI-библиотеками или утилитами. Пример:

```bash
npm install axios
npm install -D eslint prettier
```

Если вы хотите писать стили в Svelte, можно дополнительно поставить:

```bash
npm install -D stylelint
```

## Полезные советы

- Не забудьте настроить `.gitignore` для `node_modules`, `dist`, `.svelte-kit`.
- При использовании VS Code включите автоматическое форматирование и линтинг.
- Проверяйте конфигурацию `tsconfig.json`, если хотите строгую типизацию.

## Пример проверки сборки

```bash
npm run build
```

Если сборка проходит, значит проект настроен правильно.

## Итог

Теперь у вас есть рабочее окружение для разработки на TypeScript + Svelte. Один раз установив Node.js и редактор, вы можете быстро создавать новые проекты, использовать шаблоны и настраивать TypeScript под свои задачи.
