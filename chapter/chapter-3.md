# Функциональное программирование для Java-разработчиков

## Чистые функции и побочные эффекты

Представьте себе функцию как черный ящик, который получает входные данные и возвращает результат. Чистая функция - это функция, которая:
1. При одинаковых входных данных всегда возвращает одинаковый результат
2. Не имеет побочных эффектов (не изменяет состояние программы за пределами своей области видимости)

Пример нечистой функции в Java:
```java
class UserService {
    private List<User> users = new ArrayList<>();
    
    public void addUser(User user) {  // Нечистая функция
        users.add(user);              // Изменяет состояние списка users
        sendEmail(user);              // Побочный эффект - отправка email
    }
}
```

Пример чистой функции:
```java
class UserService {
    public User createUser(String name, String email) {  // Чистая функция
        return new User(name, email);  // Просто создает и возвращает новый объект
    }
}
```

## Неизменяемость данных (Immutability)

В функциональном программировании данные после создания не должны изменяться. Это помогает избежать множества ошибок и упрощает понимание кода.

В Java мы привыкли работать с изменяемыми объектами:
```java
// Традиционный подход в Java
public class User {
    private String name;
    public void setName(String name) { this.name = name; }
}

// Функциональный подход
public final class User {
    private final String name;
    public User(String name) { this.name = name; }
    // Вместо изменения создаем новый объект
    public User withName(String newName) {
        return new User(newName);
    }
}
```

В Kotlin неизменяемость поддерживается на уровне языка через `data class` и ключевое слово `val`:
```kotlin
data class User(val name: String)  // Неизменяемый класс
```

## Функции высшего порядка

Функции высшего порядка - это функции, которые могут принимать другие функции как параметры или возвращать их. В Java 8+ это реализуется через функциональные интерфейсы и лямбда-выражения.

Рассмотрим три основные функции высшего порядка:

### map
Преобразует каждый элемент коллекции:
```java
// Java Stream API
List<String> names = users.stream()
    .map(user -> user.getName())
    .collect(Collectors.toList());

// Kotlin
val names = users.map { it.name }
```

### filter
Фильтрует элементы по определенному условию:
```java
// Java Stream API
List<User> adults = users.stream()
    .filter(user -> user.getAge() >= 18)
    .collect(Collectors.toList());

// Kotlin
val adults = users.filter { it.age >= 18 }
```

### reduce
Сворачивает коллекцию в единственное значение:
```java
// Java Stream API
int totalAge = users.stream()
    .map(User::getAge)
    .reduce(0, (sum, age) -> sum + age);

// Kotlin
val totalAge = users.map { it.age }.reduce { sum, age -> sum + age }
```

Эти концепции функционального программирования помогают писать более надежный и понятный код, уменьшают количество потенциальных ошибок и упрощают тестирование. Хотя Java и Kotlin не являются чисто функциональными языками, они предоставляют инструменты для применения функционального подхода там, где это имеет смысл.
