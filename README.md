# WTBot

## Пример настроек Bots Logic ##

```js
{
    keyWords : {...},
    menus : {...},
    staticWords:{...}
}
```

сначала определяем какие модули мы используем, их всего 3-и на выбор:
1. Меню
2. Ключевые слова
3. Статические слова

Активировав модуль меню, вы обязаны создать объект "menus" внутри объекта настроек.
Объект "menus" содержит описание всех меню их пунктов и вызывающихся функций при клике по пункту.

### Menus Object ###

пример объекта menus
``` js
menus : {
    titles:["main","admin"],
    admin : {...},
    main : {...}
}
```

Объект "menus" обязан содержать масив "titles" в которм должны быть перечислены все существующие меню в вашем боте.

пример описания объектов из массива titles
``` js
admin : {
    items:[...]
}
main : {
    items:[...]
}
```
Каждый элемент массива "titles" должен быть описан в объекте "menus" и обязан содержать массив "items"
``` js
items:[
    {
        text: "Сколько время?",
        type: "function",
        funcName: "getTime"
    },
    {
        text: "Какой день?",
        type: "function",
        funcName: "getDay"
    },
    {
        text: "Админ меню",
        type: "redirect",
        menuName: "admin"
    },
]
```
Каждый элмент массива items является объектом соделжащим поля:
1. text - обязательно
2. type - обязательное
3. funcName - зависит от type
4. menuName - зависит от type

+ поле text - текст пункта меню

+ поле type - должно иметь одно из значений (function,redirect)

>если поле type имеет значение function - это означает, вызванный пункт выполнит функцию описанную в поле funcName

>если поле type имеет значение redirect - это означает, вызванный пункт перекинет пользователя на меню menuName

+ поле funcName - содержит название исполняемой функции

+ поле menuName - содержит название меню в которое будет переброшет пользователь

#### полный вид объекта menus ####
```js
menus : {
    titles:["main","admin"],
    main : {
        items:[
            {
                text: "Сколько время?",
                type: "function",
                funcName: "getTime"
            },
            {
                text: "Какой день?",
                type: "function",
                funcName: "getDay"
            },
            {
                text: "Админ меню",
                type: "redirect",
                menuName: "admin"
            }
        ]
    },
    admin : {
        items:[
            {
                text: "Забанить!",
                type: "function",
                funcName: "admin"
            },
            {
                text: "Назад",
                type: "redirect",
                menuName: "main"
            }
        ]
    },
},
```
### keyWords Object ###

Активировав модуль ключевых слов, вы обязаны создать объект "keyWords" внутри объекта настроек.
Объект "keyWords" содержит совокупность слов/частей слов, которые будут являться сигналом боту для вызова описанных функций.

пример объекта keyWords
``` js
keyWords : {
    getTime : {...},
    getDay : {...}
}
```

Объект "keyWords" обязан содержать объекты именами которых будут являться вызываемые функции.

#### полный вид объекта keyWords ####
``` js
keyWords : {
    getTime : {
        words:['врем','час'],
        useOnlyIn : ["main"]
    },
    getDay : {
        words:['понедел', 'вторн', 'сред', 'четвер', 'пятниц', 'суббот','субот', 'воскр']
    }
}
```
каждый объект находящийсяв объекте keyWords обязан содержать поля:
1. words - обязательное
2. useOnlyIn - не обязательное

поле words - это массив содержащий слова/части слов, , которые будут являться сигналом боту для вызова функции определной выше.
>Т.Е. если в массиве words содержится ['врем'], то в сообщение содержание буквы 'в','р','е','м' в любой соей части, в указаном порядке, вызовет функцию схожую с именем объекта где находится массив words.
>> Т.Е. если предложения "Сколько сейчас времени?", "время" и т.д. будут являться сигналом боту для вызова функции.

поле useOnlyIn - это массив названий меню, в которых может быть использование этого списка words.
>Т.Е. если в массиве useOnlyIn содержится ['admin'], то правильно введенная последовательность букв из массива words не приведет к вызову или редиректу в другое меню.

### staticWords Object ###

Активировав модуль статических слов, вы обязаны создать объект "staticWords" внутри объекта настроек.
Объект "staticWords" содержит слова, которые будут являться сигналом боту для вызова описанных функций.

пример объекта staticWords
``` js
staticWords:{
    "!getAdmin" : {},
    "!goMain" : {},
    "/sayHello" : {}
}
```

Объект "staticWords" обязан содержать объекты именами которых будет являтся команда для вызова функции описанной внутри этого объекта.

#### полный вид объекта staticWords ####
``` js
staticWords:{
    "!getAdmin" : {
        funcName : "getAdmin",
        useOnlyIn : ["admin"]
    },
    "!goMain" : {
        funcName : "goMain"
    },
    "!sayHello" : {
        funcName : "sayHello",
        sayHello : ()=>{return "hello"}
    }
}
```





