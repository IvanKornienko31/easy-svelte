---
slug: 'runes-intro'
title: 'Урок 9. Введение в руны'
date: 2024-02-01
description: 'Работа с текстом и символами в Svelte.'
tags: ['Svelte', 'Руны']
---

В Svelte «руны» можно понимать как любые символы и строки, которые используются для отображения текста и специальных символов. Важно понимать, как работать с Unicode, emoji и escape-последовательностями, чтобы интерфейс выглядел правильно на всех языках.

## Что такое Unicode и руны

Unicode — это стандарт, который позволяет кодировать символы из разных письменных систем. В JavaScript и TypeScript строки поддерживают Unicode, а Svelte выводит их напрямую в шаблоне.

Пример простого текста:

```svelte
<script lang="ts">
  const greeting: string = 'Привет, мир!';
</script>

<p>{greeting}</p>
```

## Специальные символы и escape-последовательности

Можно использовать Unicode-escapes:

```ts
const heart: string = '\u2764';
const smile: string = '\u{1F600}';
```

В Svelte это может выглядеть так:

```svelte
<script lang="ts">
  const heart = '\u2764';
  const smile = '\u{1F600}';
</script>

<p>{heart} Люблю Svelte {smile}</p>
```

## Эмодзи и символы из других языков

Emoji можно вставлять напрямую в строку:

```ts
const emoji: string = '🚀';
const cyrillic: string = 'Привет';
const japanese: string = 'こんにちは';
```

Пример компонента:

```svelte
<script lang="ts">
  const title = 'Работа с символами';
  const emoji = '✨';
</script>

<h1>{emoji} {title}</h1><p>{cyrillic} / {japanese}</p>
```

## Функции для работы с символами

TypeScript поддерживает методы строк, которые помогают работать с рунами:

```ts
const text = 'Svelte 🔥';
console.log(text.length); // длина строки
console.log(text.charCodeAt(6));
console.log(String.fromCodePoint(0x1f525));
```

В Svelte можно использовать это так:

```svelte
<script lang="ts">
 const text = 'Svelte 🔥';
 const code = String.fromCodePoint(0x1f60a);
</script>

<p>Текст: {text}</p><p>Смайлик по коду: {code}</p>
```

## Интернационализация и локализация

Для поддержки разных языков важно хранить строки отдельно от логики. В Svelte это можно сделать через объект с переводами:

```svelte
<script lang="ts">
  const translations = {
    ru: 'Здравствуйте',
    en: 'Hello',
    jp: 'こんにちは'
  };

  let locale: 'ru' | 'en' | 'jp' = 'ru';

  function changeLocale(newLocale: 'ru' | 'en' | 'jp') {
    locale = newLocale;
  }
</script>

<select bind:value={locale}>
  <option value="ru">Русский</option>
  <option value="en">English</option>
  <option value="jp">日本語</option>
</select>

<p>{translations[locale]}</p>
```

## Пользовательские метки и символы

Можно хранить символы как данные и выводить их динамически:

```svelte
<script lang="ts">
  const runes: string[] = ['⚡', '🔥', '🌟', '✨'];
</script>

<ul>
  {#each runes as rune}
    <li>{rune}</li>
  {/each}
</ul>
```

## Заключение

Работа с текстом и символами в Svelte простая: вы используете обычные строки, а компилятор быстро превращает их в DOM. Unicode, emoji и локализация работают из коробки, важно лишь правильно определять кодировку и типы. Такие «руны» делают приложение выразительным и удобным для пользователей по всему миру.
