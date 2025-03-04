# Среда разработки

## Настройка проекта: Leiningen vs deps.edn

Для Java-разработчиков система сборки проекта - это как Maven или Gradle. В мире Clojure есть два основных инструмента: Leiningen и deps.edn.

### Leiningen
Leiningen (или просто "lein") - это классический и наиболее популярный инструмент. Он похож на Maven тем, что использует централизованный файл конфигурации `project.clj`, где описываются все зависимости и настройки проекта.

Пример `project.clj`:
```clojure
(defproject my-app "0.1.0-SNAPSHOT"
  :dependencies [[org.clojure/clojure "1.11.1"]]
  :main ^:skip-aot my-app.core)
```

### deps.edn
deps.edn - это более новый и минималистичный подход, встроенный непосредственно в Clojure. Он похож на Gradle Kotlin DSL тем, что конфигурация более гибкая и программируемая.

Пример `deps.edn`:
```clojure
{:deps {org.clojure/clojure {:mvn/version "1.11.1"}}
 :paths ["src" "resources"]}
```

## Подключение Java-библиотек

Одно из главных преимуществ Clojure - это полная совместимость с Java экосистемой. Вы можете использовать любые Java библиотеки так же легко, как и нативные Clojure библиотеки.

### Пример использования Java библиотеки:
```clojure
;; Импорт Java классов
(import java.time.LocalDateTime)

;; Использование Java методов
(def current-time (LocalDateTime/now))
```

В отличие от Kotlin, где вы используете Java классы напрямую, в Clojure есть специальный синтаксис для вызова Java методов:
- Статические методы: `(ClassName/staticMethod args)`
- Методы экземпляра: `(.methodName object args)`

## Отладка и профилирование

### Отладка
В отличие от традиционной отладки в IDE типа IntelliJ IDEA, в Clojure часто используется REPL-driven development. Это интерактивный подход, где вы можете:

1. Оценивать код на лету
2. Исследовать состояние программы в реальном времени
3. Модифицировать работающую программу без перезапуска

Для классической отладки доступны:
- Встроенный макрос `println`
- Продвинутый макрос `clojure.tools.trace`
- Интеграция с отладчиком IDE через плагины

### Профилирование
Для профилирования доступны как стандартные Java-инструменты (JProfiler, YourKit), так и специфичные для Clojure решения:

- `clj-async-profiler` - профилировщик на базе async-profiler
- `criterium` - библиотека для бенчмаркинга
- VisualVM с поддержкой Clojure

Пример использования criterium для бенчмаркинга:
```clojure
(require '[criterium.core :as c])

(c/bench (your-function args))
```

## Заключение

Несмотря на отличия от привычной Java/Kotlin среды, инструменты разработки Clojure предоставляют все необходимое для профессиональной разработки. Главное отличие - это акцент на интерактивную разработку через REPL, что может показаться необычным для Java-разработчиков, но становится мощным преимуществом при освоении.