# Class names

- должны представлять собой существительные и их комбинации
(исключаем Manager, Processor, Data Info)
```
QuzManagerService - QuizRunner
ResponseData      - Response
UserInfo          - User
DataHandler       - UserRegistrationHandler
TaskManager       - Scheduler
```

- одно слово для представления одной абстрактной концепции
```
//methods
receiveSomething - getSomething
processSomething - handleSomething
deleteSomething  - removeSomething
putSomething     - addSomething
updateSomething  - setSomething
searchSomething  - findSoething
createSomething  - buildSomething

//classes
BackupExecutor        - BackupRunner            
EventObserverr        - EventListener            
MessageProcessor      - MessageHandler          
ValidationUtils       - ValidationHelper        
MessageTransformer    - MessageFormatter        
NotificationGenerator - NotificationBuilder     
ResourceSupplier      - ResourceProvider        
OrderVerifier         - OrderValidator          
```

