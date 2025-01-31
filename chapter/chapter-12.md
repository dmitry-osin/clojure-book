# Библиотеки и фреймворки

## Веб-разработка: Ring и Compojure

Если вы знакомы с Spring Framework в Java, то понимание Ring и Compojure будет довольно простым. Ring - это базовый веб-фреймворк для Clojure, который можно сравнить с сервлетами в Java. Он обрабатывает HTTP-запросы и ответы в самой простой форме.

Compojure - это маршрутизатор, построенный поверх Ring. Он похож на Spring MVC, но с более функциональным подходом. Вот простой пример:

```clojure
(ns myapp.core
  (:require [compojure.core :refer :all]
            [ring.adapter.jetty :as jetty]))

(defroutes app-routes
  (GET "/" [] "Привет, мир!")
  (GET "/users/:id" [id] (str "Пользователь " id))
  (POST "/users" request 
    (str "Создание пользователя: " (:body request))))
```

В отличие от Spring, где мы используем аннотации и классы, здесь маршруты определяются как функции, что соответствует функциональной парадигме Clojure.

## Работа с данными

### clojure.data.json

Работа с JSON в Clojure очень похожа на работу с Jackson в Java, но синтаксис более лаконичный:

```clojure
(require '[clojure.data.json :as json])

;; Преобразование в JSON
(json/write-str {:name "Иван" :age 25})
;; => "{\"name\":\"Иван\",\"age\":25}"

;; Парсинг JSON
(json/read-str "{\"name\":\"Иван\",\"age\":25}")
;; => {"name" "Иван", "age" 25}
```

### JDBC-интеграция

Работа с базами данных через JDBC в Clojure очень похожа на Java, но с функциональным подходом:

```clojure
(require '[clojure.java.jdbc :as jdbc])

(def db-spec
  {:dbtype "postgresql"
   :dbname "mydb"
   :user "user"
   :password "password"})

(jdbc/query db-spec ["SELECT * FROM users WHERE age > ?" 18])
```

В отличие от JPA или MyBatis, здесь мы работаем с данными напрямую через SQL, но с удобными функциональными обертками.

## Асинхронное программирование: core.async

core.async - это библиотека для асинхронного программирования в Clojure. Если вы знакомы с корутинами в Kotlin, то концепция похожа, но реализация более функциональная:

```clojure
(require '[clojure.core.async :refer [chan go >! <!]])

(let [c (chan)]  ; создаем канал
  (go  ; запускаем асинхронный блок
    (>! c "привет")  ; отправляем значение в канал
    (println "отправлено"))
  (go
    (println "получено:" (<! c))))  ; читаем из канала
```

Основные отличия от привычного подхода в Java/Kotlin:
- Вместо Future/Promise используются каналы
- Нет явных колбэков
- Код выглядит синхронным, но выполняется асинхронно
- Более явная работа с потоками данных

Эти библиотеки показывают, как функциональный подход Clojure может сделать код более лаконичным и выразительным, даже если вы привыкли к объектно-ориентированному стилю Java или Kotlin.
