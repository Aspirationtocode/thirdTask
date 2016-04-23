# 3 задание. Яндекс Мобилизация

Склонируйте код из репозитория: `git clone https://github.com/shri-msk-2016/task3.git`, перейдите в директорию проекта `cd task3`.

Выполните `npm install`, а затем `npm start` и откройте приложение в браузере (<http://localhost:3000>).

Приложение позволяет добавлять и редактировать данные студентов ШРИ (ФИО, ссылку на фотографию и краткую информацию). Для работы в офлайне оно использует ServiceWorker, позволяя при этом, как минимум, просматривать данные студентов.

Однако при реализации были допущены несколько ошибок:

* Без подключения к серверу приложение не работает.
* Не всегда обновляется список студентов после добавления нового.

Найдите и исправьте ошибки. В качестве дополнительного задания вы можете реализовать добавление студентов в офлайне с последующей синхронизацией. При выполнении обратите внимание на способы определения режима «онлайн/офлайн».

Результат пришлите в виде ссылки на https://github.com

#Решение.

## Ошибка №1
Строки: `3 - 7 файла worker.js`
Для исправления ошибки требуется заменить данный код:
```javascript
var urlsToCache = [
  '/',
  '/index.css',
  '/index.js'
];
```
на такой код:
```javascript
var urlsToCache = [
  '/',
  'css/index.css',
  'js/index.js'
];
```
`Комментарий к ошибке:`
_Консоль сообщала об отсутствии доступа к js и css файлам. Для исправления потребовалось прописать новый путь._

## Ошибка №2
Строки: `35 - 37 файла worker.js`
Для исправления ошибки требуется заменить данный код:
```javascript
return event.respondWith(
  getFromCache(event.request).catch(fetchAndPutToCache);
);
```
на такой код:
```javascript
return event.respondWith(
  getFromCache(event.request).catch(fetchAndPutToCache)
);
```
`Комментарий к ошибке:`
_Консоль сообщала об ошибке на 36 строке файла worker.js. Убрав лишнюю `;` удалось устранить ошибку._

## Ошибка №3
Строки: `26 - 37 файла worker.js`
Для исправления ошибки требуется заменить данный код:
```javascript
  if (/^\/api\/v1/.test(requestURL.pathname)) {
      return event.respondWith(
          Promise.race([
              fetchAndPutToCache(event.request),
              getFromCache(event.request)
          ])
      );
  }

  return event.respondWith(
      getFromCache(event.request).catch(fetchAndPutToCache)
  );
```
на такой код:
```javascript
return event.respondWith(fetchAndPutToCache(event.request));
```
`Комментарий к ошибке:`
_Консоль сообщала об ошибке на 36 строке файла worker.js. Убрав лишнюю `;` удалось устранить ошибку._

