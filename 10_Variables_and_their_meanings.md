# Variables and their meanings

Before:
```java
int resultSum;
// code
result = sum(firstOperand, secondOperand);
```    
After: инициализация переменной result в месте её объявления перед использованием.
```java
int resultSum = sum(firstOperand, secondOperand)
// code
```
---

Before:
```java
User user;
// code
user = userService.getUserById(id);
```
After: переменная объявлена как final(часто используемая) и инициализирована перед первым использованием.
```java
final User user = userService.getUserById(id);
```
---

Before:
```java
public class UserConstants {
    public static int MIN_ALLOWED_AGE;

    static {
      MIN_ALLOWED_AGE = 18;
    }
}
```
After: использование final для константы MIN_ALLOWED_AGE и инициализация её при объявлении.
```java
public class Constants {
    public static final int MIN_ALLOWED_AGE = 18;
}
```
---

Before:
```java
public class ConnectionSettings {
    private int timeoutMs;
    private int retryCount;

    public void defaultInitialize() {
      timeoutMs = 5000;
      retryCount = 3;
    }
    // code
}
```
After: использование final для полей класса и их инициализация в конструкторе.
```java
public class ConnectionSettings {
    private final int timeout;
    private final int retryCount;

    public ConnectionSettings() {
        timeout = 5000;
        retryCount = 3;
    }
    // code
}
```
---

Before:
```java
boolean isPermittedUser;
// code
if (userAge >= MIN_ALLOWED_AGE) {
    isPermittedUser = true;
} else {
    isPermittedUser = false;
}
```
After: использование тернарного оператора для объявления и инициализации переменной isPermittedUser.
```java
boolean isPermittedUser = userAge >= MIN_ALLOWED_AGE;
// code
```
---

Before:
```java
boolean isPermittedUser = userAge >= MIN_ALLOWED_AGE;
// code
```
After: присвоенно обратное значение при завершении работы с булевой переменной
```java
boolean isPermittedUser = userAge >= MIN_ALLOWED_AGE;
// code
boolean isPermittedUser = !isPermittedUser;
```
---

Before:
```java
int userAge = user.getAge();
```
After: присвоенно недопустимое значение при завершении работы с переменной
```java
int userAge = user.getAge();
// code
userAge = -1;
```
---

Before:
```java
File file = new File(this.getFilePath());
emailNotificationService.sendEmail(NOTIFICATION_EMAIL, file);

```
After: присвоенно недопустимое значение при завершении работы с переменной
```java
File file = new File(this.getFilePath());
emailNotificationService.sendEmail(NOTIFICATION_EMAIL, file); 
file = null;
```
---

Before:
```java
int totlaAmount;
for (int i = 0; i < items.size(); i++) {
  totalAmount += item.get(i).amount(); 
}
```
After: проинициализирован аккумулятор totalAmount перед циклом.
```java
int totalAmount = 0; 
for (int i = 0; i < items.size(); i++) {
    totalAmount += item.get(i).amount();
}
```
---

Before:
```java
int i;
for (i = 0; i < items.size(); i++) {
    // code
}
```
After: переменная счетчик `i` инициализируется непосредственно в заголовке самого цикла и не доступна за пределами цикла 
```java
for (int i = 0; i < items.size(); i++) {
    // code
}
```
---

Before:
```java
int i = 0;
while (i < items.size()) {
    //code
    i++;
}
```
After: использован цикл for, переменная счетчик `i` инициализируется непосредственно в заголовке самого цикла,
и не доступна за пределами цикла
```java
for (int i = 0; i < items.size(); i++) {
    //code
}
```
---

Before:
```java
String[] exeptionArgs = exeption.getArguments();
```
After: использование assert для проверки количества аргументов в переменной
```java
String[] exeptionArgs = exeption.getArguments();
assert exeptionArgs.length != 0 : "Arguments cannot be empty";
```
---

Before:
```java
public void setAddress(Address address) {
  this.address = address;
}
```
After: валидация устанавливаемых данных в поле класса c бросанием исключения
```java
public void setAddress(Address address) {
    Objects.requireNonNull(address, "address can't be null");
    this.address = address;
}
```
---

Before:
```java
public void setAge(int age) {
    this.age = age;
}
```
After: валидация устанавливаемых данных в поле класса c бросанием исключения
```java
public void setAge(int age) {
    if(age < 0) throw new IllegalArgumentException("user age must be positive value"); 
    this.age = age;
}
```
---

Before:
```java
return secondOperand / firstOperand;
```
After: валидация допустимого делителя c бросанием исключения
```java
if (firstOperand != 0) {
    return secondOperand / firstOperand;
} else {
    throw new IllegalArgumentException("firstOperand cannot be 0");
}
```