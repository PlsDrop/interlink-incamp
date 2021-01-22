---
id: encapsulation
title: Инкапсуляция в Java на примере связанного списка
sidebar_label: 💻 Инкапсуляция
---

Рассмотрим инкапсуляцию в Java реализуя простой [связанный список](/data-structures.md#linked-list).

:::note Связанный список
Разбор структуры связанного списка и его сравнение с масивом есть в общем разделе [Структуры данных](/data-structures.md).
:::

## Добавление элементов

В первом видео мы создаем класс `LinkedList` в виде структуры с публичными полями. Этот подход раскрывает детали реализации списка. Таким образом пользователь класса (тоже разработчик, а точнее его код) может случайно "поломать его внутренности". К примеру, обнулить ссылку на голову списка, но оставить прежним значение количества элементов. 

Для устранения этой проблемы мы делаем поля списка приватными а функции работы с ним заменяем методами. Таким образом применяем принцип инкапсуляции - скрываем детали реализации от пользователей класса и защищаем его от некоректного доступа извне. 

[Добавление элементов в список](https://youtu.be/PpA0AeeU3sM)

```java title="src/oop/linkedlist/LinkedList.java"
package oop.linkedlist;

import java.util.function.Consumer;

public class LinkedList {
    private ListNode head;
    private ListNode tail;
    private int size;

    static class ListNode {
        String value;
        ListNode nextNode;

        public ListNode(String value) {
            this.value = value;
        }
    }

    public String getFirst() {
        return head.value;
    }

    public int getSize() {
        return size;
    }

    void addItem(String value) {
        ListNode newNode = new ListNode(value);
        if (tail == null) { // empty list
            head = newNode;
        } else { // has at least one element
            tail.nextNode = newNode;
        }
        size++;
        tail = newNode;
    }
}
```

## Последовательный доступ к элементам

Мы сокрыли доступ к голове списка, но нам надо как-то проходить по его элементам. Для этого мы реализуем метод `forEach` и будем передавать в него функциональный интерфейс `Consumer` (потребитель). Реализовав интерфейс потребителя мы как раз и опишем тот код, который хотим выполнять над каждым элементом (использовать, потреблять этот элемент). 

[Последовательный проход списка](https://youtu.be/hBMgjuO_8bo)

```java {4-8} title="src/oop/linkedlist/LinkedList.java"
public class LinkedList {
    //...

    public void forEach(Consumer<String> consumer) {
        for (ListNode node = head; node != null; node = node.nextNode) {
            consumer.accept(node.value);
        }
    }
}
```

:::note Функциональные интерфейсы
[Consumer](https://docs.oracle.com/javase/8/docs/api/java/util/function/Consumer.html) -- это интерфейс из семейства функциональных интерфейсов в Java. Вот еще несколько из них:
- [Supplier](https://docs.oracle.com/javase/8/docs/api/java/util/function/Supplier.html) -- возвращает значения (поставляет)
- [Function](https://docs.oracle.com/javase/8/docs/api/java/util/function/Function.html) -- принимает параметр одного типа, и возвращает результат того-же или другого типа
- [Predicate](https://docs.oracle.com/javase/8/docs/api/java/util/function/Predicate.html) -- выполняет логическую проверку над параметром и возвращает ее результат, `true` или `false`
:::

:::tip Iterator
Более удобным и гибким способом доступа к элементам является использование итераторов. Реализовав для нашего списка интерфейсы [Itarable](https://docs.oracle.com/javase/8/docs/api/java/lang/Iterable.html) и [Iterator](https://docs.oracle.com/javase/8/docs/api/java/util/Iterator.html) мы получим :
- уже готовую реализацию метода `forEach`
- возможность использовать наш список в _foreach_ цикле 
```java
for(Integer item : items) { sum += item; }
```
::: 

## 💻 Практика

Дополнить API связанного списка реализовав следующие методы. На каждый метод реализовать хотя-бы один юнит-тест. 

- [ ] Удаление элемента из списка
- [ ] Вставку элемента в начало списка
- [ ] Вставку элемента в конец списка
- [ ] Замену значения элемента по индексу
