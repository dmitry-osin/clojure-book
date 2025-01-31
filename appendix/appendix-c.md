# Глоссарий терминов (FP vs OOP)

## Чистые функции (Pure Functions)
В функциональном программировании чистая функция - это функция, которая:
1. При одинаковых входных данных всегда возвращает одинаковый результат
2. Не имеет побочных эффектов (не изменяет состояние программы)

Пример на Kotlin:
```kotlin
// Чистая функция
fun add(a: Int, b: Int): Int = a + b

// Нечистая функция
var total = 0
fun addToTotal(value: Int) {
    total += value // Имеет побочный эффект - изменяет внешнюю переменную
}
```

## Иммутабельность (Immutability)
В ООП мы часто изменяем состояние объектов. В FP данные неизменяемы (иммутабельны). Вместо изменения существующих данных, мы создаем новые объекты с обновленными значениями.

Пример на Kotlin:
```kotlin
// ООП подход
class MutablePerson {
    var name: String
    var age: Int
    
    fun celebrateBirthday() {
        age++ // Мутация состояния
    }
}

// FP подход
data class Person(val name: String, val age: Int) {
    fun celebrateBirthday() = copy(age = age + 1) // Создание нового объекта
}
```

## Функции высшего порядка (Higher-Order Functions)
Это функции, которые могут принимать другие функции как параметры или возвращать функции. В Java 8+ и Kotlin это реализовано через лямбда-выражения.

```kotlin
// Пример функции высшего порядка
fun processNumbers(numbers: List<Int>, transform: (Int) -> Int): List<Int> {
    return numbers.map(transform)
}

// Использование
val numbers = listOf(1, 2, 3)
val doubled = processNumbers(numbers) { it * 2 } // [2, 4, 6]
```

## Рекурсия vs Циклы
В FP предпочтительно использовать рекурсию вместо циклов для итеративных операций.

```kotlin
// Императивный подход (ООП)
fun factorial(n: Int): Int {
    var result = 1
    for (i in 1..n) {
        result *= i
    }
    return result
}

// Функциональный подход (рекурсия)
fun factorialFP(n: Int): Int = 
    if (n <= 1) 1 else n * factorialFP(n - 1)
```

## Функции как значения первого класса
В FP функции являются "гражданами первого класса" - их можно присваивать переменным, передавать как параметры и возвращать из других функций.

```kotlin
val sum: (Int, Int) -> Int = { a, b -> a + b }
val multiply: (Int, Int) -> Int = { a, b -> a * b }

fun calculate(a: Int, b: Int, operation: (Int, Int) -> Int): Int {
    return operation(a, b)
}
```

## Композиция функций
В FP мы создаем сложные функции путем комбинирования простых функций.

```kotlin
fun addOne(x: Int) = x + 1
fun double(x: Int) = x * 2

// Композиция функций
val addOneThenDouble: (Int) -> Int = { x -> double(addOne(x)) }
// или с использованием оператора композиции
val composed = ::addOne andThen ::double
```

## Монады
Монады - это паттерн проектирования в FP, который помогает работать с цепочками вычислений и обрабатывать ошибки. В Kotlin примером монады является `Optional` или `Result`.

```kotlin
// Пример использования монады Result
fun divide(a: Int, b: Int): Result<Double> =
    if (b == 0) Result.failure(ArithmeticException("Division by zero"))
    else Result.success(a.toDouble() / b)

// Цепочка вычислений
divide(10, 2)
    .map { it * 2 }
    .getOrDefault(0.0)
```

## Функторы
Функтор - это контейнер данных, который определяет, как применить функцию к значению внутри контейнера. В Kotlin примерами функторов являются `List`, `Set`, `Map`.

```kotlin
val numbers = listOf(1, 2, 3)
// List является функтором, так как мы можем применить 
// функцию преобразования к каждому элементу
val doubled = numbers.map { it * 2 } // [2, 4, 6]
```