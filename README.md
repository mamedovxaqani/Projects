# Project MODUSversus

1. [Структура проекта](#Структура-проекта)
2. [EJS](#ejs)

Команды
1. [GIT](#git)
2. [NPM](#npm)

## Структура проекта 

Каталог:
```
├─ public/
|  ├─ index.html
|  └─ css/
|     └─ style.css
|      
└─ src/
   ├─ index.ejs
   ├─ variables.scss
   ├─ style.scss
   └─ components/
      ├─ <название компонента 1>/
      |  ├─ <название компонента 1>.ejs
      |  └─ <название компонента 1>.scss
      |
      ├─ <название компонента 2>/
      |  ├─ <название компонента 2>.ejs
      |  └─ <название компонента 2>.scss
      ...
```
1. В каталоге ```public/``` храняться скомпилированные файлы **.html** и **.css**. Мы их вручную не редактируем.
2. В каталоге ```src/``` хранятся файлы **.ejs** и **.scss**, в которых мы верстаем. После сохранения любого файла из текущего каталога запускается компилятор, который собирает все файлы и переводит их в понятный html и css в папке ```public/``` 
3. Файл **index.ejs** - это стартовый шаблон страницы, в который надо подключать все компоненты!
4. В каталоге ```components/``` храняться подкаталоги с компонентами. _Название папки, самого шаблона ejs и стилей scss для этого компонента, должны быть одинаковым._
5. После того, как создали файл стилей для своего компонента, импортируйте его в конец файла ```src/style.scss```. 
> ```@import 'components/<название компонента>/<название компонента>'```, можно без уточнения расширения .scss.


## EJS
EJS - шаблонизатор, который позволяет писать js код прямо в html и выполнять его сразу с DOM элементами во время рендеринга страницы. Еще позволяет выносить отдельные компоненты в другие файлы и подключать их на разных страницах. 

**Пример:**

ejs:
```javascript
<%
const emails = ['123@gmail.com','456@gmail.com','789@gmail.com','101@gmail.com'];
%>
<ul>
    <% for (var i = 0; i < emails.length; i++) {%>
        <li>{%= emails[i] %}</li>
    <% } %>
</ul>
```
рендерится в такой html:
```html
<ul>
    <li>123@gmail.com</li>
    <li>456@gmail.com</li>
    <li>789@gmail.com</li>
    <li>101@gmail.com</li>
</ul>
```
_______________________________________

1. Возможность писать js в html есть только в файлах с расширением .ejs
2. Код вставляется в тег ```<% ... %>``` и т.д., об это дальше.

Синтаксис:
- ```<% ... %>```  Тег, позволяет испольнять js код, ничего не выводит.
- ```<%=``` Используется, если нужно вывести какие-то значения и переменные на страницу.
- ```<%-``` Используется, если нужно вывести в документе шаблон .ejs из другого файла.

> Закрывающий тег ```%>``` везде одинаковый.

Для вставки на страницу какого-то компонента из папки ```components/``` нужно воспользоваться функцией ```include(PATH_TO_EJS);```, в аргументе написать путь к файлу .ejs без указания расширения .ejs.

Например, вставка компонента **header**, который находится в папке ```components/header/```:
```javascript

<body>

<%- include('components/header/header'); %>
<main> ... </main>
<footer> ... </footer>

</body>

```
Теперь, если поменять что-то внутри компонента **header**, он изменится на всех страницах на которых подключен функцией ```include()```.

> Для удобства, в файле **index.ejs** создана функция ```_COMP(COMPONENT_NAME)``` в которую можно написать название подключаемого компонента, она сама вернет нужный путь в функцию ```include()```. (COMP - сокращение от COMPONENT)
>
> Например компонент **header** можно подключить так ```<%- include(_DIR('header')); %>```

> P.S. Можете установить редкатор VS Code расширение, чтобы в .ejs файла подсвечивался синтаксис. По дефолту не подсвечивается)
> Одно из таких расширений – EJS language support –– https://github.com/Digitalbrainstem/ejs-grammar

## GIT
Команды git, которые пригодятся.
1. ```git status``` - выводит состояние файлов в текущий момент.
2. ```git add <название файла, каталога>``` - добавляет новые изменения файлов в реестр.
3. ```git add .``` - добавляет все файлы каталога в реестр.
4. ```git commit -m "<название коммита>"``` - создает коммит, сохраняя все изменения из реестра.
5. ```git push origin <название ветки>``` - отправляет последние коммиты в нужную ветку текущего проекта на GitHub.
6. ```git pull origin <название ветки>``` - скачивает последние изменения из ветки проекта на GitHub
7. ```git branch``` - показывает какие есть ветки и на какой сейчас находитесь.
8. ```git checkout <название ветки>``` - переходит на другую ветку.
9. ```git checkout -b <название ветки>``` - флаг ```-b``` копирует текущую ветку в новую и переходит на неё.
10. ```git merge <название ветки>``` - сливает ветку ```<название ветки>``` с той, на которой в момент выполнения команды вы находитесь.
11. ```git branch -d <название ветки>``` - удаляет ветку. Перед выполнением этой команды нужно находится на другой ветке.
12. ```git log``` - выводит историю коммитов (по убыванию). Чтобы выйти из просмотра логов, нажмите клавишу **q**.
13. ```git log --pretty=oneline``` - более длинная запись предыдущей команды, но выводит каждый коммит в одну строку.

## NPM
Команды npm, которые пригодятся.
1. ```npm install``` - устанавливает все зависимости в папку ```node_modules```, которые прописаны в package.json
2. ```npm install <название модуля>``` - устанавливает конкретный модуль по его названию. Берет он их с сайта [npmjs.com](https://www.npmjs.com). На страницах модулей можно увидеть информацию про них и почитать документацию.
3. ```npm run <название команды>``` - запускает одну из команд, прописанные в файле package.json, в объекте "scripts".

> В данном проекте нам понадобится команда ```npm run dev```. Она запускает слежение за каталогом ```components/``` и запускает компиляторы ejs и scss в момент сохранения какого-то файла.

Чтобы завершить выполнение какой-нибудь команды (если она сама не завершилась), нужно в командной строке нажать ```Ctrl+C```
