# Correct_comments

Before:
```java
// Pattern for finding a floating point number
Pattern floatingPointNumberMatcher = Pattern.compile("\\d+\\.\\d+");
```
After: Информативный комментарий
```java
// Pattern for matching a floating point number in text: digits followed by a dot and more digits
Pattern floatingPointNumberMatcher = Pattern.compile("\\d+\\.\\d+");
```

Before:
```java
// Validate user id using a UUID pattern
if (userId.matches("[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}")) {
    // code
}
```
After: Информативный комментарий
```java
// Validate user id as a UUID (8-4-4-4-12 hex chars separated by hyphens)
if (userId.matches("[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}")) {
    // code
}
```

Before:
```java
// Validate time using a UNIX timestamp pattern
public static boolean isBeforeOrEqualToCurrentTimeStamp(long unixTimeStamp) {
    Instant validatedInstant = Instant.ofEpochSecond(unixTimeStamp);
    Instant currentInstant = Instant.now();
    return !currentInstant.isBefore(validatedInstant);
}
```
After: Информативный комментарий
```java
// Check if the given UNIX timestamp is not later than the current time
public static boolean isBeforeOrEqualToCurrentTimeStamp(long unixTimeStamp) {
    Instant validatedInstant = Instant.ofEpochSecond(unixTimeStamp);
    Instant currentInstant = Instant.now();
    return !currentInstant.isBefore(validatedInstant);
}
```

Before:
```java
// Validate time using a UNIX timestamp pattern
public static boolean isAfterOrEqualToCurrentTimeStamp(long unixTimeStamp) {
    Instant validatedInstant = Instant.ofEpochSecond(unixTimeStamp);
    Instant currentInstant = Instant.now();
    return !currentInstant.isAfter(validatedInstant);
}
```
After: Информативный комментарий
```java
// Check if the given UNIX timestamp is not earlier than the current time
public static boolean isAfterOrEqualToCurrentTimeStamp(long unixTimeStamp) {
    Instant validatedInstant = Instant.ofEpochSecond(unixTimeStamp);
    Instant currentInstant = Instant.now();
    return !currentInstant.isAfter(validatedInstant);
}
```

Before:
```java
// only private
private void setContext(UserContext context) {
threadLocalScope.set(context);
}
```
After: Информативный комментарий
```java
//Keeping setContext private to control access and encapsulate internal details.
private void setContext(UserContext context) {
threadLocalScope.set(context);
}
```

Before:
```java
//Needs REFACTORING
if(Objects.isNull(orderDetailResponse)) {
    orderDetailResponse = checkoutOrderClient.getOrderDetail(ORDER_ID);
}
```
After: Комментарии TODO
```java
//TODO needs REFACTORING (it will always be null 
// because @Test is executed and a new instance of the class is created)
if(Objects.isNull(orderDetailResponse)) {
    orderDetailResponse = checkoutOrderClient.getOrderDetail(ORDER_ID);
}
```

Before:
```java
//java-faker
implementation "com.github.javafaker:javafaker:${versions.javafaker}"
```
After: Комментарии TODO
```java
//TODO Delete java-faker after Checkout service will be deployed
implementation "com.github.javafaker:javafaker:${versions.javafaker}"
```

Before:
```java
// encrypts data
public byte[] encryptData(byte[] data, boolean isTestEncryption) {
        MerchantEncryptionArtifacts artifacts = encryptionArtifactsService
                .getDefaultArtifacts()
                .orElseThrow();
        return encryptData(data, isTestEncryption, artifacts);
    }
```
After: Информативный комментарий
```java
// Encrypts data using the default encryption artifacts
public byte[] encryptData(byte[] data, boolean isTestEncryption) {
        MerchantEncryptionArtifacts artifacts = encryptionArtifactsService
                .getDefaultArtifacts()
                .orElseThrow();
        return encryptData(data, isTestEncryption, artifacts);
    }
```

Before:
```java
// Gets vat percent
public static int getPercentFor(int vatCode) {
  
  return Arrays.stream(Vat.values())
      .filter(vat -> vat.codes().contains(vatCode)) 
      .findFirst()
      .map(Vat::percent)
      .orElse(Vat.RATE_DEFAULT.percent());

}
```
After: Информативный комментарий
```java
// Gets vat percent for the given vat code
public static int getPercentFor(int vatCode) {
  
  return Arrays.stream(Vat.values())
      .filter(vat -> vat.codes().contains(vatCode)) 
      .findFirst()
      .map(Vat::percent)
      .orElse(Vat.RATE_DEFAULT.percent());

}
```

Before:
```java
// Encrypt
Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
cipher.init(Cipher.ENCRYPT_MODE, key);
byte[] encrypted = cipher.doFinal(input);
```
After: Комментарий прояснение
```java
// Encrypt the input data using the given using AES-256 in CBC mode with PKCS5 padding
Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
cipher.init(Cipher.ENCRYPT_MODE, key);
byte[] encrypted = cipher.doFinal(input);
```

Before:
```java
// Timeout 
private static final int TIMEOUT_MS = 3 * 1000;
```
After: Комментарий усиление
```java
// Timeout of 3 seconds for the external service call
// is a critical requirement for the business logic
private static final int TIMEOUT_MS = 3 * 1000;
```

Before:
```java
// Check if image is too large
if (imageFile.length() > MAX_IMAGE_SIZE_BYTES) {
    throw new FileException("Image too large"); 
}
```
After: Комментарий предупреждения о последствиях
```java
// Check if image is too large
// Uploading large images can overwhelm the backend - restrict to 10MB to avoid crashes
if (imageFile.length() > MAX_IMAGE_SIZE_BYTES) {
    throw new FileException("Image too large"); 
}
```