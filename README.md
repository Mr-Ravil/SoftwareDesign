# Лабораторные по курсу Software Design

## Лабораторная 1. [LRUCache](Lab1-LRUCache)

Цель: получить практический опыт применения динамических проверок в коде (assertions).

Необходимо реализовать структуры данных LRUCache на хешмапе и двусвязном списке. При реализации необходимо самостоятельно продумать возможные проверки pre/post-условий и инвариантов класса. Придуманные проверки необходимо добавить в код реализации в виде assertions. Класс необходимо покрыть тестами.

Указания:
+	использовать LinkedHashMap напрямую нельзя


## Лабораторная 4. [ToDoList](Lab4-ToDoList)

Цель: получить практический опыт применения паттерна MVC (Model-View-Controller).
Напишите небольшое веб-приложение для работы со списками дел. Приложение должно позволять:
+ Просматривать списки дел и дела в них
+ добавлять/удалять списки дел
+ добавлять дела
+ отмечать дела, как выполненные

Рекомендации:
+ использовать spring mvc
+ использовать средства spring-framework для DI (dependency injection)

Пример, который был рассмотрен на лекции:
https://github.com/akirakozov/software-design/tree/master/java/mvc


## Лабораторная 5. [DrawGraph](Lab5-DrawGraph)

Цель: получить практический опыт применения структурного паттерна bridge.
Необходимо реализовать простой визуализатор графов, используя два различных графических API. Способ визуализации графа можно выбрать самостоятельно (например, рисовать вершины по кругу). Приложение должно поддерживать две реализации графов: на списках ребер и матрице смежностей. Каркас классов:

```java
public abstract class Graph {
    
    /**
     * Bridge to drawing api
     */
    private DrawingApi drawingApi;
    
    public Graph(DrawingApi drawingApi) { 
        this.drawingApi = drawingApi;   
    }    
    
    public abstract void drawGraph();
}

public interface DrawingApi { 
    long getDrawingAreaWidth(); 
    long getDrawingAreaHeight(); 
    void drawCircle(...); 
    void drawLine(...);
}
```

Примечания:
+	выбор API и реализации графа должны задаваться через аргументы командной строки при запуске приложения;
+	каркас классов можно менять (добавлять новые поля/методы, параметры методов и тд);
+	в качестве drawing api можно использовать java.awt и javafx (примеры: https://github.com/akirakozov/software-design/tree/master/java/graphics/);
+	можно использовать любой язык и любые api для рисования (главное, чтобы они были принципиально разные).


## Лабораторная 6. [Calculator](Lab6-Calculator)

Цель: получить практический опыт применения паттернов поведения visitor и state.

Необходимо реализовать калькулятор, который умеет преобразовывать простые арифметические выражения в обратную польскую
запись (ОПЗ) и вычислять их. Пример выражения:

```
(23 + 10) * 5 – 3 * (32 + 5) * (10 – 4 * 5) + 8 / 2.
```

Выражение может содержать скобки, пробельные символы, цифры и 4 операции: ``+, -, *, /``.


## Лабораторная 8. [Clock](Lab8-Clock)

Цель: получить практический опыт применения паттерна Clock при реализации тестов.

Необходимо реализовать интерфейс EventsStatistic, который считает события, происходящие в системе. Реализация должна хранить статистику ровно за последний час и подсчитывать, сколько событий каждого типа произошло в минуту. 

Интерфейс EventsStatistic:

```java
public interface EventsStatistic {
    void incEvent(String name);    
    ... getEventStatisticByName(String name);    
    ... getAllEventStatistic();
    void printStatistic();
}
```

+ ``incEvent(String name)`` - инкрементит число событий name;
+ ``getEventStatisticByName(String name)`` - выдает rpm (request per minute) события name за последний час;
+ ``getAllEventStatistic()`` - выдает rpm всех произошедших событий за прошедший час;
+ ``printStatistic()`` - выводит в консоль rpm всех произошедших событий;

Реализацию EventsStatistic необходимо покрыть тестами, используя паттерн Clock, рассмотренный на лекции. Тесты не должны использовать sleep'ы и должны выполняться быстро.
