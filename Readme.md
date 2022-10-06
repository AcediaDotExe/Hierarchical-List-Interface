# Интерфейс для работы с иерархическим списком

![Няшный котик](https://www.meme-arsenal.com/memes/2c5f68adf4f6902f956352373689c072.jpg)

## Деплой проекта на хостинг

Прежде всего необходимо скачать npm:
[download npm](https://nodejs.org/en/download/)

***

### MongoDB
* [Зарегистрируйтесь в MongoDB](https://www.mongodb.com/), а после создайте новый
кластер:
![](https://www.mongodb.com/docs/atlas/images/create-cluster-cluster-tier.png)
* Введите данные пользователя, который будет иметь доступ к кластеру,
и в "Network Access" разрешите обращаться к базе данных с любого ip:
`0.0.0.0/0`:
![Network Access](https://webimages.mongodb.com/_com_assets/cms/kkh4nwt30hy01y88y-connect-to-mongodb-clusters.png?auto=format%2Ccompress&ch=DPR&fix=max&w=770px)

* Далее необходимо соединить наш кластер с сервером Node.js:
 ![Connect](https://miro.medium.com/max/1400/1*Gbs6b_wuHc01yRlAHZB1UQ.jpeg)
В итоге скопируем: `mongodb+srv://<login>:<password>@<claster-name>.dftutlo.mongodb.net/<your-DB-name>?retryWrites=true&w=majority`. Замените все
<примеры> на ваши данные. Имя базы данных придумайте сами.

* Вставим скопированный текст вместо текущего url в
`backend/app/config/db.config.js`

* Для удобного использования базы данных рекомендую скачать
[MongoDB Compass](https://www.mongodb.com/products/compass)
и аналогично подключить его к кластеру (выбрать при соединении
"Connect using MongoDB Compass" на оф. странице созданного кластера)
* Загружаем свой JSON в базу данных через mongoShell Compass'a:

 * Введем `use <your-DB-name>`, и вставим предварительно скопированный
 JSON-объект в `db.hierarchies.insertOne(<your-JSON>)`. Или же можно добавить
 его через интерфейс MongoDB Compass.

Отлично, на этом с базой данных все, самая сложная часть позади.

***

### Express

* Развертываем наш сервер:
`/cd /d (yourPath..)/backend` на любом хостинге. Я залил его на
[Heroku](https://quiet-cove-12120.herokuapp.com/). В этот url можно добавить:
`../api/hierarchies` - так мы увидим все объекты в нашей базе данных.
=======
* Open in cmd folder "backend":
`/cd /d (yourPath..)/backend`

 * [Документация по загрузке Node.js на Heruko](https://devcenter.heroku.com/articles/getting-started-with-nodejs#deploy-the-app)

***

### Vue

* Перед сборкой приложения нужно изменить url нашего сервера.
Для этого открываем `./frontend/src/http-common.js`.
В нем редактируем `baseURL: "<url-your-hosted-server>/api"`. В моем случае:
`baseURL: "https://quiet-cove-12120.herokuapp.com/api"`

* Открываем в командной строке папку "frontend":
`cd /d (yourPath..)/frontend`

* Устанавливаем все зависимости:
`npm install`

* Делаем сборку приложения:
`npm run build` или `npx vue-cli-service build`.
В результате получаем готовое приложение в папке `./frontend/dist`.
Её мы и загружаем на любой хостинг.
Я же использовал Open Server, и в `./OpenServer/domains` скопировал папку dist.
(если не получилось, раскомментируйте vue.config.js)
