# Реальные примеры

## Миграция Java-кода на Clojure

Представьте, что у вас есть Java-приложение, и вы хотите постепенно перейти на Clojure. Это возможно благодаря тому, что Clojure работает на JVM и может легко взаимодействовать с Java-кодом.

Давайте рассмотрим простой пример. У нас есть Java-класс для обработки заказов:

```java
public class OrderProcessor {
    public double calculateTotal(List<Order> orders) {
        return orders.stream()
                    .mapToDouble(order -> order.getPrice() * order.getQuantity())
                    .sum();
    }
}
```

В Clojure тот же код будет выглядеть так:

```clojure
(defn calculate-total [orders]
  (reduce + (map #(* (:price %) (:quantity %)) orders)))
```

Преимущества перехода на Clojure:
- Код становится более лаконичным
- Неизменяемые структуры данных по умолчанию
- Более простая работа с многопоточностью
- REPL-driven development для быстрой разработки

## Параллельные вычисления

В Java для параллельной обработки данных часто используется ExecutorService:

```java
ExecutorService executor = Executors.newFixedThreadPool(4);
List<Future<Integer>> futures = new ArrayList<>();

for (Task task : tasks) {
    Future<Integer> future = executor.submit(() -> processTask(task));
    futures.add(future);
}

// Ожидание результатов
for (Future<Integer> future : futures) {
    results.add(future.get());
}
```

В Clojure та же задача решается проще благодаря встроенным примитивам для параллельных вычислений:

```clojure
(def results 
  (pmap process-task tasks))
```

Преимущества Clojure для параллельных вычислений:
- Неизменяемость данных снижает риски race conditions
- Встроенные примитивы для параллельной обработки (pmap, future, agent)
- Более простой код без явного управления потоками
- Транзакционная память (STM) для безопасного изменения состояния

## Создание DSL (предметно-ориентированного языка)

DSL - это специализированный язык для решения задач в конкретной предметной области. В Java создание DSL обычно требует много шаблонного кода:

```java
Order order = new OrderBuilder()
    .addProduct("Laptop")
    .setQuantity(2)
    .setPrice(1000.0)
    .setShippingAddress("123 Main St")
    .build();
```

Clojure, благодаря своей гибкости и макросам, позволяет создавать более естественные DSL:

```clojure
(def order
  (order
    (product "Laptop")
    (quantity 2)
    (price 1000.0)
    (shipping "123 Main St")))
```

Преимущества создания DSL на Clojure:
- Макросы позволяют расширять сам язык
- Более чистый и понятный синтаксис
- Меньше шаблонного кода
- Возможность создавать декларативные DSL

### Заключение

Эти примеры показывают, как Clojure может улучшить существующий Java-код, сделав его более кратким, понятным и надёжным. При этом переход может быть постепенным, так как Clojure отлично интегрируется с существующим Java-кодом.