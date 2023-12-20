# Variable lifetime

Before:
```java
String greetings = "Greetings!";

void printToConsole(message) {
    System.out.println(greetings + " " + message);  
}
```
After: Убрана глобальная переменная , её значение передаётся явно через параметр.
```java

void printToConsole(String message) {
    String greetings = "Greetings!";
    System.out.println(greetings + " " + message);
}
```

Before:
```java
public class User {
    public String firstName;
    public String lastName;
    //Constructor
}
```
After: Поля класса сделаны приватным, добавлен сеттер для изменения.
```java
public class User {
    private String firstName;
    private String lastName;
    //Constructor
    //Getters
    //Setters
}
```

Before:
```java
public class Logger {
    private static String logMessage;

    public static void log(String message) {
      logMessage = message;
      // code
  }
}
```
After: Переменная logMessage теперь является локальной для метода, что уменьшает ее область действия.
```java
public class Logger {
    public static void log(String message) {
      String logMessage = message;
      // code
    }
}
```

Before:
```java
String user; 

if (this.isValidOperation()) {
    user = userService.getUser();
    this.save(user); 
}
```
After: переменная user теперь находится локальной, что уменьшает ее область действия.
```java
if (this.isValidOperation()) {
    this.save(userService.getUser());
}
```

Before:
```java
public class Logger {
    private int logLevel;

    public void configureLogger(int level) {
        // code
        this.logLevel = level;
        // code
    }
}
```
After: выделение в отдельный метода установки уровня логгирования setLogLevel.
```java
public class Logger {
    private LogLevel logLevel;

    public void configureLogger(LogLevel level) {
        this.setLogLevel(level);
        // code
    }

    private void setLogLevel(LogLevel level) {
        this.logLevel = level;
    }
}
```

Before:
```java
public class UserValidator {
    private boolean isValid;

    public void validateUser(User user) {
        // code
        isValid = // validation logic
        // code
    }
}
```
After: выделения логики проверки в отдельный метод performValidation
```java
public class UserValidator {
    private boolean isValid;

    public void validateUser(User user) {
        this.performValidation(user);
        // code
    }

    private boolean performValidation(User user) {
        // code
    }
}
```

Before:
```java
public class ShoppingCart {
    private double totalPrice;

    public void addItem(double price) {
        // code
        totalPrice += price;
        // code
    }
}
```
After: логика обновления totalPrice инкапсулирована в отдельный метод,
```java
public class ShoppingCart {
    private double totalPrice;

    public void addItem(double price) {
        updateTotalPrice(price);
        // code
    }

    private void updateTotalPrice(double price) {
        totalPrice += price;
    }
}
```

Before:
```java
public class Cache {
    private Map<String, Object> cache;

    public void addToCache() {
        // code 
        cache.put("key", "value");
        // code
        increaseCacheCount();
    }

    private void increaseCacheCount() {
        // code
    }
}
```
After: логика выделена в  специальный метод addToCache() для добавления в кеш
```java
public class Cache {
    private Map<String, Object> cache;

    public void addToCache() {
        // code
        addToCache("key", "value");
        // code
        displayCacheContents();
    }

    private void addToCache(String key, Object value) {
        cache.put(key, value);
    }

    private void increaseCacheCount() {
        // code
    }
}
```

Before:
```java
String userInput = this.getUserInput(); 
//code
if(userInput.equals("quit")) {
    //code
}
```
After: создании отдельного метода handleInput, который принимает входные данные в качестве аргумента
```java
String userInput = this.getUserInput();
this.handleInput(input);

void handleInput(String userInput) {
    if("quit".equals(userInput)) {
      //code
    }
}
```

Before:
```
List<String> strings = messageDao.getMessageById(id);

int stringCount = 0;
for(String s : strings) {
    if(s.length() > 5) {
        stringCount++;
    }
}
```
After: логика подсчета строк выделяется в отдельный метод
```java
int countStringsLength(List<String> strings) {
    int count = 0;
    for(String s : strings) {
      if(s.length() > 5) {
        count++;
      }
    }
    return count;
}

List<String> strings = messageDao.getMessageById(id);
int stringCount = countStringsLength(strings);
```

Before:
```java
int total = 0;
//code
for(int i = 0; i < amounts.size(); i++) {
    total += amounts.get(i);
}
//code
this.handleSum(sum);
```
After: вынесение логики суммирования в отдельный метод
```java
int calculateTotal(List<Amount> amounts) {
  int total = 0;
  for(int i = 0; i < amounts.size(); i++) {
    total += amounts.get(i);
  }
  return total;
}

this.calculateSum();
this.handleSum(calculateSum())
```

Before:
```java
public class OrderManagementSystem {
 
  // methods for order, billing, shipping servicing
  
}
```
After: большой класс разбит на более мелкие
```java
public class OrderService {
  // order methods
}

public class BillingService {
  // billing methods
}

public class ShippingService {
  // shipping methods
}
```

Before:
```java
FileWriter file = new FileWriter(filePath);
file.write(data); 
file.close();
```
After: минимизированна область видимости с помощью синтаксического сахара Try-with-resources
```java
try(FileWriter file = new FileWriter(filePath)) {
  file.write(data);
}
```

Before:
```java
public class OrderService {
  private Order order;
  //code
  public void validate() {
    if(order.getTotal() > 100) {
      // code
    }
  } 
}
```
After: в коде параметр order передается явно в метод validate, минимизированна область видимости перменной
```java
public class OrderService {

    public void validate(Order order) {
        if(order.getTotal() > 100) {
          // code
        }
    }
}
```

Before:
```
String input = getInput();
// code
if(input.length < 5) {
// code
}
```
After: проверка ввода вынесена в отдельный метод для повторного использования c ограничением скоупа ввода данных
```java
boolean isInputShort(String input) {
    return input.length() < 5;
}

if(isInputShort(getInput())) {
  // code
}
```