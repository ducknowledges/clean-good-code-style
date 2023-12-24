# Variable binding time

## Example 1
Cвязывание переменной во время компиляции кода:
```java
public final class AppLocale {

  public static final Locale LOCALE_EN = Locale.ENGLISH;
  public static final Locale LOCALE_RU = new Locale("ru");

  private AppLocale() {}
}
```
Связывание переменных в выделенном утилитном классе помогает: 
- ограничить область хранения и инциализации этих переменных, 
- улучшить структуру кода выделив переменные в клас который отвечает за локли приложения,
- улучшает читаемость и переиспользование в коде
- легко поменять значение в одном месте, вместо поиска всех мест гед могут применяться локали
- удобно переисвользовать в тестах.

## Example 2
Cвязывание переменной во время компиляции кода:
```java
class ApiIntegrationTest {
  private static final String VALID_TOKEN = JwtSupportUtils.getValidJWT();
}
```
Связывание переменных в тестовом классе помогает:
- генерировать токен при загрузке класса, один раз и переиспользовать во всех тестовых методах класса;
- не менять код при смене логики генерации токена дает, что дает гибкость, 
при применении не статичных значений в токене в котором нет статичных значений(например время истечения токена);
- улучшает читабельность, позволяет не использовать хардкорный токен.


## Example 3
Cвязывание переменной во время выполнения программы
```java
public class ControllerExceptionHandler {
    private final LocalizedMessageProvider messageProvider;
    private final LocaleHolder localeHolder;

    public ControllerExceptionHandler(LocalizedMessageProvider messageProvider) {
        this.messageProvider = messageProvider;
    }
    
    public ApiError handleException(Exception exception) {
        String message = messageProvider.getLocalizedMessage(
            ExceptionErrorCode.UNEXPECTED_ERROR, localeHolder.getLoacale());
        return new ApiError(UNEXPECTED_ERROR, message);
    }
}
```
Связывание переменных в обработчике исключений помогает:
- гибко управлять локализацией сообщений и следовать принципу единственной ответственности(SOLID);
- менять текст сообщения об ошибки динамически во время отправки запроса;
- легко менять реализацию провайдера локализованных сообщений;
- упрощает тестирование, тк можно использовать мок-объект провайдера.