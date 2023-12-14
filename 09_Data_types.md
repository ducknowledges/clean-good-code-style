# Data types

Before:
```
return secondOperand / firstOperand;
```
After: добавил проверку деления на 0
```
if (firstOperand != 0) {
    return secondOperand / firstOperand;
} else {
    // обработка ошибки деления на 0
}
```

Before: 
```
int result = secondOperand + firstOperand;
```
After: явное приведение к типу long c защитой от переполнения по целому числу
```
long result = (long) secondOperand + (long) firstOperand;
```

Before:
```
int result = secondOperand * firstOperand;
```
After: явное приведение к типу long c защитой от переполнения по целому числу
```
long result = (long) secondOperand * (long) firstOperand;
```

Before:
```
if (temperature > (double) discreteTriggerTemperature) {
}
```
After: явное приведение целого числа к типу double, без потери точности
```
if (temperature > (double) discreteTriggerTemperature) {
}
```

Before:
```
int temperatureScalesNum = 1000;
int discreteTemperature = 38;
double scaleFillingPercent = (double) 
```
After: явное приведение целого числа к типу double, используя подходящую операцию деления
```
int temperatureScalesNum = 1000;
int discreteTemperature = 38;
double scaleFillingPercent = ((double) discreteTemperature / (double) temperatureScalesNum) * 100
```

Before:
```
if (CONSTANT_STRING == string) {
}
```
After: Избегайте сравнений на равенство для строковых значений(объектов)
```
if (CONSTANT_STING.equals(str2)) {
}
```

Before:
```
double totalAmount +=  receiptAmount;
```
After: добавил специальный типо данных для повышения точности и  для избежания ошибок округления финансовых операций
```
BigDecimal totalAmount = totalAmount.add(BigDecimal.valueOf(receiptAmount));;
```

Before:
```
if (employeeAge >= MIN_AGE && employeeAge <= MAX_AGE && employeeSalary > MIN_SALARY && employeeSalary < AVG_SALARY) {

}
```
After: используются логические переменные для повышения читабельности
```
boolean isValidAge = employeeAge >= MIN_AGE && employeeAge <= MAX_AGE;
boolean isValidSalary = employeeSalary > MIN_SALARY && employeeSalary < AVG_SALARY;
if (isValidAge && isValidSalary) {
}
```

Before:
```
if (((double) this.size / this.capacity) < 0.5 && this.capacity > 16) {
      this.shrink();
}
```
After: используются логические переменные и константы для повышения читабельности
```
double loadFactor = (double) this.size / this.capacity;
boolean shouldShrink = loadFactor < LOAD_FACTOR && this.capacity > DEFAULT_CAPACITY;

if (shouldShrink) {
    this.shrink();
}
```

Before:
```
if (userStatus.equals("REGISTERED") && (userType.equals("ADMIN") || userType.equals("MODERATOR"))) {
}
```
After: используются логические переменные и константы для повышения читабельности
```
boolean isAdminOrModerator = ADMIN.equals(userType) || MODERATOR.equals(userType);
if (REGISTERED.equals(userStatus) && isAdminOrModerator) {
}
```

Before:
```
retrun HELLO_MESSAGE_EN;
```
After: добавлено использование локализации вместо непосредственной работы со строками
```
retrun messageProvede.getLoclalzizedMessage(HELLO_MESSAGE_CODE, LOCALE_EN);
```

Before:
```
return messageSource.getMessage("hello.message", null, Locale_EN);
```
After: lобавлено использование обертки над MessageSource и констант вместо магических строк
```
retrun messageProvede.getLoclalzizedMessage(HELLO_MESSAGE_CODE, LOCALE_EN);
```