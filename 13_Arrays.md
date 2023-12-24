# Arrays

Before
```java
String[] args = exception.getArguments();
StringBuilder exceptionMessage = new StringBuilder();
for (int i = 0; i < args.length; i++) {
    exceptionMessages.append(this.formatExceptionArg(args[i]));
}
```

After: работа с массивом без его прямой индексации
```java
String[] args = exception.getArguments();
StringBuilder exceptionMessage = new StringBuilder();
for (String arg : args) {
    exceptionMessages.append(this.formatExceptionArg(args));
}
```

Before
```java
private void shiftElementsToLeftFrom(int index) {
    for (int i = index + 1; i < this.size; i++) {
        array[i - 1] = array[i];
    }
}
```

After: смещает элементы массива влево c с помощью метода System.arraycopy
```java
System.arraycopy(array, index + 1, array, index, this.size - index - 1);
```

Before
```java
public static int findElement(int[] array, int value) {
  for (int i = 0; i < array.length; i++) {
    if (array[i] == value) {
      return i;
    }
  }
  return -1;
}
```

After: использование имплементаций интерфейса List вместо массива, для посика позиции элемента в массиве
```java
public static int findElement(List<Integer> array, int value) {
  return array.indexOf(value);
}
```

Before
```java
public static boolean containsElement(int[] array, int value) {
  for (int i = 0; i < array.length; i++) {
    if (array[i] == value) {
      return true;
    }
  }
  return false;
}
```

After: использование имплементаций интерфейса List вместо массива, для проверки наличия элемента в массиве
```java
public static boolean containsElement(List<Integer> array, int value) {
  return array.contains(value);
}
```

Before
```java
int[] numbers = this.getInputNumbers();
Set<Integer> sortedSetNumbers = new TreeSet<>();
for (int i = 0; i < numbers.length; i++) {
    sortedSet.add(numbers[i]);
}
```

After: использование имплементации List, Set вместо массива, для сортировки массива
```java
List<Integer> numbers = this.getInputNumbers();
Set<Integer> sortedSetNumbers = new TreeSet<>();
for (int number : sortedNumbers) {
    sortedSet.add(number);
}
```