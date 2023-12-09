# OOP and interfaces

## Перегрузка конструкторов
```
// before - after
new UserContext(uderId, merchantId) - UserContext.fromDecodedJWT(DecodetJWT decodedJWT)

new Triangle(pointA, pointB, pointC) - Triangle.fromPoints(pointA, pointB, pointC)

new User(firstName, lastName) - User.createWithName(firstName, lastName)
```

## Интерфейсы и реализации
```
                            // реализация 
EncryptionArtifactsProvider // EncryptionArtifactsProviderResource, EncryptionArtifactsProviderVault

                            // реализация       
MessageProvider             // ExceptionMessageProvider, MailMessageProvider, NotificationMessageProvider

                            // реализация 
NotificationListener        // SmsNotificationListener, PushNotificationListener, MailNotificationListener
```