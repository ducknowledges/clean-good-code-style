# Bad comments

Before:
```java
// check processed
public boolean isProcessed() {
  return this.operationId != null;
}
```
After: комментарий сделан очевидным(1. Неочевидные комментарии)
```java
/**
 * Checks if the refund has been processed.
 *
 * @return {@code true} if the refund has been processed;
 */
public boolean isProcessed() {
  return this.operationId != null;
}
```

Before:
```java
// check inventory availability
if(product.getInventory() > 0) {
  // code
}
```
After: комментарий сделан очевидным(1. Неочевидные комментарии)
```java
// Checking if the product is in stock
if(product.getInventory() > 0) {
  // code
}
```

Before:
```java
// Здесь мы вычисляем общую стоимость всех товаров в корзине
public double calculateTotal() {
  // code
}
```
After: улучшение комментария(2. Бормотание)
```java
/**
 * Calculates the total cost of the shopping cart.
 *
 * @return The total cost of items in the shopping cart.
 */
public double calculateTotal() {
  // code
}
```

Before:
```java
// call the task launch method
public void runTasks(List<Task> tasks) {
  // start running tasks
  for(Task task : tasks) {
      task.run();
  }
  // sinish completing the launch of tasks
  this.finishProcessing();
}
```
After: улучшен комментарий, удален шум(2.Бормотание, 4. Комментарии-шум)
```java
/**
 * Executes a list of tasks by invoking their run methods 
 * and completes the task execution process.
 *
 * @param tasks The list of tasks to be executed.
 *              Each task's run method will be called.
 */
public void runTasks(List<Task> tasks) {
  for(Task task : tasks) {
      task.run();
  }
  this.finishTasksRunning();
}
```

Before:
```java
@Data
// This is the Product class
public class Product {
  // This field stores the product name
  private String name;
  // This field stores the price of the product
  private double price;
  // This field stores the quantity of the product in stock
  private int inventory;
}
```
After: комментарии удалены(4. Шум)
```java
@Data
public class Product {
  private String name;
  private double price;
  private int inventory;
}
```

Before:
```java
// This method saves the order to the database
public void saveOrder(Order order) {
  // save the order
}
```
After: комментарии удалены(4. Шум)
```java
public void saveOrder(Order order) {
}
```

Before:
```java
// Method for checking the presence of an element in the list
public boolean checkTaskInList(List<Task> tasks, Task checkedTask) {
  return !list.contains(element);
}
```
After: удалены недостоверные комментарии, улучшен комментарий(3. Недостоверные комментарии)
```java
/**
 * Checks if a specified task is present in the given list of tasks
 *
 * @param tasks         The list of tasks to be checked
 * @param checkedTask   The task to be checked
 * @return              {@code true} if the specified task is not present in the list,
 *                      {@code false} otherwise.
 */
public boolean containTaskInList(List<Task> tasks, Task checkedTask) {
  return !list.contains(element);
}
```

Before:
```java
// ==============================================
// Method for saving settings
// ==============================================
public void saveSettings(Settings settings) {
}
```
After: удалены комментарии(4. Шум, 5. Позиционные маркеры)
```java
public void saveSettings(Settings settings) {
}
```

Before:
```java
// *************************
// Method for calculating discount
// *************************
public double calculateDiscount(double totalPrice) {
}
```
After: удалены комментарии(4. Шум, 5. Позиционные маркеры)
```java
public double calculateDiscount(double totalPrice) {
}
```

Before:
```java
public List<Product> getProductsInStock() {
  List<Product> productsInStock = new ArrayList<>();
  //code
  return productsInStock; 
} // receiving products in stock
```
After: удалены комментарии(6. Комментарии за закрывающей фигурной скобкой)
```java
public List<Product> getProductsInStock() {
  List<Product> productsInStock = new ArrayList<>();
  //code
  return productsInStock; 
}
```

Before:
```java
/**
 * Because sometimes even refunds need a moment of introspection before being processed.
 * If a refund appears to have it all figured out and claims to be processed, 
 * let's throw a ReverseProcessingException and give it a chance to reconsider its life choices.
 */
private void checkRefundNotProcessed(Refund refund) {
  if (refund.isProcessed()) {
    throw new ReverseProcessingException();
  }
}
```
After: комментарий сокращен и сделан лаконичным(7. Избыточные комментарии)
```java
// Check the refund is not already processed to avoid repeatable reverse.
private void checkRefundNotProcessed(Refund refund) {
  if (refund.isProcessed()) {
    throw new ReverseProcessingException();
  }
}
```

Before:
```java
/**
 * The method calculates the cost of the order including delivery.
 * It takes an order object, retrieves a list of products,
 * calculates the total cost of products in the order,
 * adds delivery cost depending on the city and distance,
 * returns the total order amount.
 *This method is used before placing an order.
 */
public double calculateOrderTotal(Order order) {
}
```
After: комментарий сокращен и сделан лаконичным(7. Избыточные комментарии)
```java
/**
 * Calculates the total cost of the order with delivery.
 * @param order customer order
 * @return total order amount
 */
public double calculateOrderTotal(Order order) {
}
```

Before:
```java
/**
* This method calculates a product's rating based on reviews
* It takes a list of reviews, calculates the average rating and returns
* Rating is used to sort products
*/
public double calculateRating(List<Review> reviews) {
  //code
}
```

After: комментарий сокращен(удалена лишняя) и сделан лаконичным(8. Слишком много информации)
```java
/**
 * Calculates the rating of a product based on a list of reviews.
 *
 * @param reviews The list of reviews for the product.
 * @return The calculated rating of the product.
 */
public double calculateRating(List<Review> reviews) {
  //code
}
```

Before:
```java
// Method for sending email
/*
public void sendEmail(String recipient, String subject, String body) {
// Implementation of the mail sending method
// ...
}
*/
```
After: удален закомментированный код(11. Закомментированный код)
```java
public void sendEmail(String recipient, String subject, String body){
}
```

Before:
```java
public double calculateTotal(List<Product> products) {
  double total = 0;
  for(Product product : products) {
    total += product.getPrice(); 
  }
  return total;
  
  // прежний код с учетом скидок
  /*
  double discountedTotal = 0;
  for(Product product: products) {
    double price = product.getPrice();
    if(product.onSale()) {
      price *= 0.9; 
    }
    discountedTotal += price;
  }
  return discountedTotal;
  */
  
}
```
After: удален закомментированный код(11. Закомментированный код)
```java
public double calculateTotal(List<Product> products) {
  double total = 0;
  for(Product product : products) {
    total += product.getPrice(); 
  }
  return total;
}
```