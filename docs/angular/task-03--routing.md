---
title: "Задание: Routing"
sidebar_label: 💻 Routing
---

Реализовать Layout и [Routing](https://angular.io/guide/router-tutorial).

1. [ ] Компонент `Dashboard` позволяет выбрать список задач для просмотра. Доступен всегда
2. [ ] Страница `TodoListPage` отображает задачи конкретного списка, выбранного в `Dashboard`
3. [ ] Страница `TodayTasksPage` отображает невыполненные задачи назначенные на сегодня или дату в прошлом

:::note
Компонент `TodayTasksPage` может содержать задачи из разных списков. Поэтому, для каждой задачи надо выводить название списка, и сделать его ссылкой на страницу `TodoListPage`. 
:::

## Routes

1. [ ] `/today` -- показываем компонент страницы `TodayTasksPage`
2. [ ] `/todo-list/:id` -- показываем компонент страницы `TodoListPage`, выводим информацию про список с id `:id` используя [Route Parameters](https://angular.io/guide/router-tutorial-toh#route-parameters)

## Route params subscription

Если при смене пути новый "ведет" к то-му же компоненту, он уже не будет повторно инитиализирован. И компонент "не узнает", что путь поменялся и надо получить новый список задач. Поэтому, в компоненте вывода всех задач по `id` списка (путь `/todo-list/:id`) надо подписаться на смену параметров пути. 

```typescript title="todo-list-page.component.ts"
class TodoListPageComponent {

    tasks: Task[] = [];

    constructor(
        private route: ActivatedRoute, 
        private taskService: TaskService,
    ) {
        this.route.params.pipe(
            switchMap(params => this.taskService.getTasksByListId(params.id))
        ).subscribe(listTasks => this.tasks = listTasks);
    }
}
```
