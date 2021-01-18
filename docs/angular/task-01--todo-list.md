---
title: "Задание: Компоненты TodoList"
sidebar_label: 💻 Компоненты TodoList
---

Реализовать интерфейс управления списком задач разделив его на компоненты. 

![схема компонентов](taks-01--todolist-components.svg)

:::note Date pipe
Для преобразования и форматирования данных перед выводам в HTML используется механизм [pipe-ов](https://angular.io/guide/pipes). Сродни пайпов в Unix-like системах, они принимают данные в одном виде, обрабатывают и возвращают в результат. К примеру, для форматирования даты используется [DatePipe](https://angular.io/api/common/DatePipe). 
```html
<span>{{ deadline | date:'short' }}</span>
```
:::
