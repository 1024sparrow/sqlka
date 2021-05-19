# sqlka
Инструмент для генерирования документации по SQL-запросам, генератор с++-класса, представляющего интерфейс к реляционной БД

Необходимо в генерируемом интерфейсном классе сделать что-то вроде процедурок PostgreSQL, только универсально для БД PostgreSQL или SQlite.

Генерируемая документация - md-страница с описанием "процедур", диаграмма таблиц (картинка, сгенерированная из сгенерированного  [plantuml](http://plantuml.com/))

![dd](https://raw.githubusercontent.com/grafov/plantuml2mysql/master/database.png)
```
UML legend:

table = class
#pkey
+index

@startuml
    class user <<(U,olive)>> {
        Users table example.
        ==
        #id
        +login : varchar(16)
        +mail : varchar(64)
        docsRef : int(10) -- referenced docs for a user
        created : int(11)
        sesid : int(11)
    }

    user "1" -- "0..*" docs

    class session <<(U,olive)>> {
        Sessions table example.
        ==
        #id
        +uid : int(10) unsigned
        remoteip : int(10) unsigned
        useragent : varchar(255)
        data : longtext -- serialized session data
        +lastseen : int(11)
    }

    session "0..*" -- "1" user
    
    class docs <<(F,brown)>> {
        Documents storage example.
        ==
        #id : int(10)
        #fid : int(10) -- link to a file
        +aunthorid : int(10)
        +created : int(11)
    }
    
    class files <<(F,brown)>> {
        File storage example.
        ==
        #id
        +docId : int(10)
        title : varchar(255)
        path : varchar(255)
        hash : int(32) unsigned
    }

    files "1" -- "1..*" docs

@enduml
```
