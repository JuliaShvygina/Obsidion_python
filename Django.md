---
aliases: [django, джанго]
---
```py

```

![](https://www.meme-arsenal.com/memes/abe10cfcc26fe025ddb8beb7ab7a9681.jpg)
## Что такое Django?

Django — это высокоуровневый Python веб-фреймворк, который позволяет быстро создавать безопасные и поддерживаемые веб-сайты. Созданный опытными разработчиками, Django берёт на себя большую часть хлопот веб-разработки, поэтому вы можете сосредоточиться на написании своего веб-приложения без необходимости изобретать велосипед. Он бесплатный и с открытым исходным кодом, имеет растущее и активное сообщество, отличную документацию и множество вариантов как бесплатной, так и платной поддержки.

Django помогает писать программное обеспечение, которое будет:

**Полным**

Django следует философии «Всё включено» и предоставляет почти всё, что разработчики могут захотеть сделать «из коробки». Поскольку всё, что вам нужно, является частью единого «продукта», всё это безупречно работает вместе, соответствует последовательным принципам проектирования и имеет обширную и [актуальную документацию](https://docs.djangoproject.com/en/3.0/).

**Разносторонним**

Django может быть (и был) использован для создания практически любого типа веб-сайтов — от систем управления контентом и wiki до социальных сетей и новостных сайтов. Он может работать с любой клиентской средой и может доставлять контент практически в любом формате (включая HTML, RSS-каналы, JSON, XML и т. д.). Сайт, который вы сейчас читаете, создан с помощью Django!

Хотя Django предоставляет решения практически для любой функциональности, которая вам может понадобиться (например, для нескольких популярных баз данных, шаблонизаторов и т. д.), внутренне он также может быть расширен сторонними компонентами, если это необходимо.

**Безопасным**

Django помогает разработчикам избежать многих распространённых ошибок безопасности, предоставляя фреймворк, разработанный чтобы «делать правильные вещи» для автоматической защиты сайта. Например, Django предоставляет безопасный способ управления учётными записями пользователей и паролями, избегая распространённых ошибок, таких как размещение информации о сеансе в файлы cookie, где она уязвима (вместо этого файлы cookie содержат только ключ, а фактические данные хранятся в базе данных) или непосредственное хранение паролей вместо хэша пароля.

_Хэш пароля_ — _это значение фиксированной длины, созданное путём обработки пароля через [криптографическую хэш-функцию](https://ru.wikipedia.org/wiki/%D0%9A%D1%80%D0%B8%D0%BF%D1%82%D0%BE%D0%B3%D1%80%D0%B0%D1%84%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B0%D1%8F_%D1%85%D0%B5%D1%88-%D1%84%D1%83%D0%BD%D0%BA%D1%86%D0%B8%D1%8F). Django может проверить правильность введённого пароля, пропустив его через хэш-функцию и сравнив вывод с сохранённым значением хэша. Благодаря «одностороннему» характеру функции, даже если сохранённое хэш-значение скомпрометировано, злоумышленнику будет сложно определить исходный пароль._

Django, по умолчанию, обеспечивает защиту от многих уязвимостей, включая SQL-инъекцию, межсайтовый скриптинг, подделку межсайтовых запросов и кликджекинг (см. [Website security](https://developer.mozilla.org/ru/docs/Learn/Server-side/First_steps/Website_security) для получения дополнительной информации об этих атаках).

**Масштабируемым**

Django использует компонентную “[shared-nothing](https://en.wikipedia.org/wiki/Shared_nothing_architecture)” архитектуру (каждая её часть  независима от других и, следовательно, может быть заменена или изменена, если это необходимо). Чёткое разделение частей означает, что Django может масштабироваться при увеличении трафика, путём добавления оборудования на любом уровне: серверы кеширования, серверы баз данных или серверы приложений. Одни из самых загруженных сайтов успешно масштабировали Django (например, Instagram и Disqus, если назвать только два из них).

**Удобным в сопровождении**

Код Django написан с использованием принципов и шаблонов проектирования, которые поощряют создание поддерживаемого и повторно используемого кода. В частности, в нём используется принцип «Don't Repeat Yourself» (DRY, «не повторяйся»), поэтому нет ненужного дублирования, что сокращает объём кода. Django также способствует группированию связанных функциональных возможностей в повторно используемые «приложения» и, на более низком уровне, группирует связанный код в модули (в соответствии с шаблоном [Model View Controller (MVC)](https://developer.mozilla.org/en-US/docs/Glossary/MVC)).

**Переносным**

Django написан на Python, который работает на многих платформах. Это означает, что вы не привязаны к какой-либо конкретной серверной платформе и можете запускать приложения на многих версиях Linux, Windows и Mac OS X. Кроме того, Django хорошо поддерживается многими веб-хостингами, которые часто предоставляют определённую инфраструктуру и документацию для размещения сайтов Django.

## Установка
```py
pip install django

django-admin # для проверки установки

>>> Type 'django-admin help <subcommand>' for help on a specific subcommand.

	Available subcommands:
	...

```

## Создание проекта
В терминале PyCharm:
```
django-admin startproject [название приложения]
```

Создадим приложение для Django проекта:
```
python manage.py startapp [имя приложения]
```
![](https://i.imgur.com/PgLPscI.png)

При создании нового приложения его необходимо регистрировать в файле settings.py
![](https://i.imgur.com/0trttOk.png)

Дополнительно создадим нового суперюзера:
```
python manage.py migrate
python manage.py createsuperuser
```

Для проверки можем зайти на локальный сайти перейдем в панель администратора:
```
python manage.py runserver
```
перейдем http://127.0.0.1:5000/admin/, введем логин и пароль.
![](https://i.imgur.com/tjHKw6L.png)
