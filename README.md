# Webpack Starter Kit

<!-- # Webpack starter kit &middot; [![npm](https://img.shields.io/npm/v/npm.svg?style=flat-square)](https://www.npmjs.com/package/npm) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com) [![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](https://github.com/your/your-project/blob/master/LICENSE) -->

## Залежності

На комп'ютері повинна лжена бути встановлена LTS-версія
[Node.js](https://nodejs.org/en/).

### Розробка

Для швидкого старту необхудно склонувати репозиторій.

```bash
git clone https://github.com/go-to-stars/webpack-starter-kit.git
```

Перейменувати папку збірки іменем вашого проекту.

```bash
mv webpack-starter-kit им'я_проекту
```

Потім перейти в папку проекту.

```bash
cd им'я_проекту
```

Знаходячись в папці проекту видалити папку `.git` повязану з репозиторієм збірки
виконав наступну команду.

```bash
npx rimraf .git
```

Встановити всі залежності.

```bash
npm install
```

Та запустити режим розробки.

```bash
npm start
```

У вкладці браузера перейти за адресою
[http://localhost:4040](http://localhost:4040).

<!-- ### Сборка в продакшен

Для того чтобы создать оптимизированные файлы для хостинга, необходимо выполнить
следующую команду. В корне проекта появится папка `build` со всеми
оптимизированными ресурсами.

```shell
npm run build
```

### Deploying/Publishing

Сборка может автоматически деплоить билд на GitHub Pages удаленного (remote)
репозитория. Для этого необходимо в файле `package.json` отредактировать поле
`homepage`, заменив имя пользователя и репозитория на свои.

```json
"homepage": "https://имя_пользователя.github.io/имя_репозитория"
```

После чего в терминале выполнить следующую команду.

```shell
npm run deploy
```

Если нет ошибок в коде и свойство `homepage` указано верно, запустится сборка
проекта в продакшен, после чего содержимое папки `build` будет помещено в ветку
`gh-pages` на удаленном (remote) репозитории. Через какое-то время живую
страницу можно будет посмотреть по адресу указанному в отредактированном
свойстве `homepage`. -->

1. Створюємо теку проекту (наприклад webpack-project) та в ній ініціалізуємо npm:

```bash
npm init -y
```

2. В теці проекту повинен з'явитись файл package.json:

{
"name": "webpack-project",
"version": "1.0.0",
"description": "",
"main": "index.js",
"scripts": {
"test": "echo \"Error: no test specified\" && exit 1"
},
"keywords": [],
"author": "",
"license": "ISC"
}

редагуємо його зараз або потім: додаємо автора, опис, ключові слова тощо.

3. Додамо і сконфігуруємо Babel – транспайлер, котрий переписує код, написаний на стандарті ES6 в код ES5. Не всі браузери підтримують ES6, ось тому і доводиться використовувати транспайлери типу Babel.

Отже, щоб додати Babel до проекту, нам необхідно встановити babel-core компонент, а також пресет @babel-preset-env.

Виконайте команди:

```bash
npm install --save-dev babel-core
# npm install --save-dev babel-preset-env
npm install --save-dev @babel/preset-env
# npm install --save-dev babel-preset-react


```

Погляньте на package.json. Він тепер має виглядати так:

{
"name": "webpack-project",
"version": "1.0.0",
"description": "",
"main": "index.js",
"scripts": {
"test": "echo \"Error: no test specified\" && exit 1"
},
"keywords": [],
"author": "",
"license": "ISC"  
 "devDependencies": {
"babel-core": "^6.26.3",
"@babel/preset-env": "^7.22.5",
}
}

В теці проекту має з'явитись тека node_modules з пакетами, які ми щойно додали до проекту.

4. Створіть файл .babelrc в кореневій теці проекту:

{
 "presets": ["@babel/preset-env"] 
// "presets": ["env", "react"]
}

Babel буде використовувати цей конфігураційний файл для переписання коду з ES6 на ES5, а також для трансформації jsx-файлів в js.

Структура проекту тепер має виглядати так:

[webpack-project]
[node_modules]
.babelrc
package-lock.json
package.json

5. Webpack. Webpack бандлить всі ваші JavaScript файли разом в єдиний файл. Це включає кожен JavaScript файл, що ви написали, а також npm пакети проекту.

Webpack буде працювати з Babel для конвертування вашого коду з ES6 на ES5 поки ви працюєте. Webpack також може мініфікувати .js файл для розгортання на продакшині.

Почнемо з установки:

```bash
npm install --save-dev webpack babel-loader
```

Примітка: babel-loader – це Webpack «loader». Він підтримує запуск Babel з середовища Webpack.

Сконфігуруємо Webpack. Для цього створіть файл webpack.config.js:

const path = require("path");

module.exports = {
context: path.join(**dirname, "src"),
entry: {
app: "./main.js",
},
output: {
path: path.join(**dirname, "dist"),
filename: "bundle.js",
},
module: {
rules: [
{
test: /\.js$/,
exclude: /node_modules/,
use: ["babel-loader"],
},
],
},
resolve: {
modules: [path.join(__dirname, "node_modules")],
},
};

В конфігурації ми вказуємо, що:

вхідний код буде братися з теки src
вихідні модифіковані файли будуть збережені Webpack в теці dist (якщо її немає, то Webpack сам створить її)
Webpack буде шукати .js файли
Вихідний файл буде називатись bundle.js

6.  відредагуємо package.json (додамо рядок "compile": "webpack" в секцію scripts):

{
"name": "webpack-project",
"version": "1.0.0",
"description": "",
"main": "index.js",
"scripts": {
"compile": "webpack",
"test": "echo \"Error: no test specified\" && exit 1"
},
"keywords": [],
"author": "",
"license": "ISC",
"devDependencies": {
"babel-core": "^6.26.0",
"babel-loader": "^7.1.2",
"babel-preset-env": "^1.6.0",  
"webpack": "^3.7.1"
}
}

Для перевірки роботи додамо папку [dist] та файл index.html в ній і папку [src] та файл main.js в ній.

Створимо теку [src], а в ній файл main.js:

// ES6 синтаксис для перевірки
const getDate = () => `сьогодні: ${new Date()}`;
document.getElementById('root').innerHTML = getDate();

Потім створимо теку [dist], а в ній файл index.html:

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Мій webpack-builder</title>
  </head>
  <body>
    <h1>Webpack-builder!</h1>
    <div id="root"></div>     
    <script src="bundle.js"></script>
  </body>
</html>

Ще раз перевірте структуру проекту:

[webpack-project]
[dist]
  index.html
[node_modules]
[src]
  main.js
.babelrc
package-lock.json
package.json
webpack.config.js

<!-- Перевірка
Виконайте команду в консолі:

npm run compile
В консолі має відобразитись лог на зразок цього:

> my-project@1.0.0 compile C:\my-project
> webpack

Hash: ad2bcd3cc54c31589628
Version: webpack 3.7.1
Time: 851ms
    Asset     Size  Chunks             Chunk Names
bundle.js  2.56 kB       0  [emitted]  app
   [0] ./main.js 65 bytes {0} [built]
В теці dist має створитись файл bundle.js:

[my-project]
   [dist]
       bundle.js
       index.html
   [node_modules]
   [src]
       main.js
   .babelrc
   package.json
   webpack.config.js -->

<!-- Відкрийте файл index.html в браузері. Ви маєте побачити щось на зразок:

приклад виконання

Це цікаво: Відкрийте і дослідіть створений bundle.js файл. Знайдіть у ньому трансформований в ES5 код з файлу main.js:

// ES6 синтаксис для перевірки
var getDate = function getDate() {
  return '\u0441\u044C\u043E\u0433\u043E\u0434\u043D\u0456: ' + new Date();
};
document.getElementById('root').innerHTML = getDate(); -->

<!-- Сьогодні ми зробили:

створили проект з нуля
ініціалізували npm
додали підтримку і сконфігурували Babel
додали підтримку і сконфігурували Webpack
створили npm-скрипт компіляції
перевірили скрипт і впевнелись, що код трансформується в синтаксис ES5 -->

<!-- В наступній статті ми:

додамо підтримку стилів SASS
додамо підтримку власних шрифтів
додамо зображення
сконфігуруємо Webpack для запуску в режимі розробника (HMR, mop-source файли, автоматичне відкриття вікна браузера)
сконфігуруємо Webpack для запуску в production режимі (мініфікація bundle.js)
додамо мінімальну підтримку React -->
