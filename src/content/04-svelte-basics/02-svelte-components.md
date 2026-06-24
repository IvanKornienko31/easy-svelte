---
slug: 'svelte-components'
title: 'Урок 10. Основы верстки'
date: 2024-02-02
description: 'Компоненты, layout и стили в Svelte.'
tags: ['Svelte', 'Layout']
---

Компоненты — это строительные блоки интерфейса в Svelte. Каждый компонент описывает часть страницы: шаблон, стили и логику в одном файле `.svelte`.

## Что такое компонент

Компонент — это файл, который может содержать:

- блок `<script>` с логикой и переменными;
- разметку HTML с синтаксисом Svelte;
- блок `<style>` для стилей, привязанных к компоненту.

Пример простого компонента:

```svelte
<script lang="ts">
  export let title: string = 'Заголовок';
</script>

<section>
  <h2>{title}</h2>
  <p>Это базовый компонент Svelte.</p>
</section>

<style>
  section {
    padding: 1rem;
    border: 1px solid #ddd;
    border-radius: 0.75rem;
  }

  h2 {
    margin-bottom: 0.5rem;
  }
</style>
```

## Переиспользование компонентов

Компонент можно импортировать в другой файл:

```svelte
<script lang="ts">
  import Card from './Card.svelte';
</script>

<main>
  <Card title="Пользователь" />
  <Card title="Список" />
</main>
```

## Props и данные

`export let` позволяет передавать свойства из родителя в дочерний компонент.

```svelte
<script lang="ts">
  export let name: string;
  export let age: number;
</script>

<p>Имя: {name}</p><p>Возраст: {age}</p>
```

## Слоты

Слоты позволяют передавать содержимое внутрь компонента:

```svelte
<!-- Card.svelte -->
<div class="card">
  <slot />
</div>

<style>
  .card {
    padding: 1rem;
    background: #fff;
    border: 1px solid #ccc;
    border-radius: 1rem;
  }
</style>
```

```svelte
<!-- App.svelte -->
<Card>
  <h3>Текст внутри слота</h3>
  <p>Это содержимое передано в компонент.</p>
</Card>
```

## События и взаимодействие компонентов

Можно отправлять события от дочернего компонента родителю.

```svelte
<!-- Counter.svelte -->
<script lang="ts">
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();
  let count = 0;

  function increment() {
    count += 1;
    dispatch('update', { count });
  }
</script>

<button on:click={increment}>Нажми: {count}</button>
```

```svelte
<!-- App.svelte -->
<script lang="ts">
  import Counter from './Counter.svelte';

  let currentCount = 0;

  function handleUpdate(event: CustomEvent<{ count: number }>) {
    currentCount = event.detail.count;
  }
</script>

<Counter on:update={handleUpdate} /><p>Текущий счёт: {currentCount}</p>
```

## Layout и структура

Svelte не навязывает жесткую структуру. Вы можете создавать компоненты для навигации, заголовка, страницы и карточек.

Пример простого layout-компонента:

```svelte
<nav>
  <a href="/">Главная</a>
  <a href="/about">О проекте</a>
</nav>

<style>
  nav {
    display: flex;
    gap: 1rem;
    padding: 1rem;
    background: #f0f0f0;
  }

  a {
    color: #333;
    text-decoration: none;
  }
</style>
```

## Стилизация компонентов

Svelte поддерживает встроенные стили, которые по умолчанию локальны для компонента. Это удобно, потому что стили не «протекают» наружу.

```svelte
<style>
  button {
    background: #ff3e00;
    color: white;
    border: none;
    padding: 0.75rem 1rem;
    border-radius: 0.5rem;
  }
</style>
```

Для глобальных стилей используйте `:global()`:

```svelte
<style>
  :global(body) {
    margin: 0;
    font-family: system-ui, sans-serif;
  }
</style>
```

## Использование CSS-фреймворков

Можно подключать Tailwind, Bootstrap или любые другие стили. Важно, что вы всё равно сохраняете преимущества компонентов Svelte.

## Итог

В Svelte компоненты — это удобный способ организовать интерфейс. Они поддерживают props, события, слоты и стили, а также легко комбинируются в общей структуре приложения. С помощью компонентов вы быстро строите понятный и поддерживаемый интерфейс.
