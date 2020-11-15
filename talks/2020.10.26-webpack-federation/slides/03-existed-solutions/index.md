# 3. Существующие решения

-----

## Server-Side Fragment Composition <!-- .element: class="orange" -->

- Также известно как Transclusion, Server Side Includes. <!-- .element: class="fragment" -->
- Очень древняя технология. Когда веб-сервер собирает из разных блоков (сервисов) в единую html страницу.  <!-- .element: class="fragment" -->
- Nginx SSI, Zalando Tailor и пр. <!-- .element: class="fragment" -->
- Отлично поддерживает SSR <!-- .element: class="fragment green" -->
- Слабо применима к современным SPA-приложениям <!-- .element: class="fragment red" -->

-----

## Iframes <!-- .element: class="orange" -->

- Transclusion который работает на клиенте. Позволяет вставлять блоки по URL. Появился как стандарт в HTML 4.01 (1998 год) <!-- .element: class="fragment" -->
- Zoid (ифреймы могут общаться через postMessage) <!-- .element: class="fragment" -->
- Боль с модальными окнами, выпадающими менюшками <!-- .element: class="fragment red" -->
- Проблема с SEO для поисковиков <!-- .element: class="fragment red" -->
- Проблема с перформансом (одни и те же библиотеки загружаются несколько раз) <!-- .element: class="fragment red" -->

-----

## Web Components <!-- .element: class="orange" -->

- Веб-стандарт из 2011-2013 для браузеров. Позволяет определять и регистрировать динамические настраиваемые элементы в инкапсулированной области. <!-- .element: class="fragment" -->
- Самая большая проблема с SSR, т.к web components сильно завязаны на DOM API <!-- .element: class="fragment red" -->
- Поможет инкапсулировать компонент, но не поможет сделать большое SPA приложение <!-- .element: class="fragment red" -->
- По мне, это чутка поумневший iframe не более того. <!-- .element: class="fragment red" -->

-----

## Linked Pages & SPAs <!-- .element: class="orange" -->

- Подход при котором load-балансировщик согласно адреса страницы отдает то или иное SPA-приложение. <!-- .element: class="fragment" -->
- Пример реализации: Next.js Multi Zones <!-- .element: class="fragment" -->
- На одном адресе, только одно приложение <!-- .element: class="fragment red" -->
- При таком подходе переход между приложениями будет "дорогим" для пользователя. <!-- .element: class="fragment red" -->
- Но роутинг внутри SPA-приложения будет дешевым и быстрым. <!-- .element: class="fragment green" -->
- Жизнь и разработка фронтендеров практически никак не усложняются. <!-- .element: class="fragment green" -->

-----

## single-spa <!-- .element: class="orange" -->

- Один из самых популярных фреймворков на данный момент для SPA (since 2016). <!-- .element: class="fragment" -->
- Он ведет себя как тонкий слой оркестровки, который согласно URL запускает тот или иной микрофронтенд, "выключая" предыдущий. <!-- .element: class="fragment" -->
- Погружаемся в systemjs и мапперы, что-то костылим с подгрузкой ассетов css, fonts, images <!-- .element: class="fragment red" -->
- Одни и те же библиотеки загружаются несколько раз, хотя lazy loading по URL облегчает жизнь <!-- .element: class="fragment red" -->
- Клеим что хотим – React, Angular, Vue, Svelte <!-- .element: class="fragment green" -->

-----

## Module Federation <!-- .element: class="orange" -->

- Новая киллер фича в Webpack 5 (since 2020). <!-- .element: class="fragment" -->
- Позволяет точечно подключать модули из другой webpack-сборки, которая расположена на другом хосте. <!-- .element: class="fragment" -->
- Альтернатива systemjs. <!-- .element: class="fragment" -->
- Плюсы и минусы будем разбирать дальше. <!-- .element: class="fragment" -->

Notes:

- Если в systemjs вы вынуждены вручную собирать import maps, то с Module Federation это происходит автоматически под капотом.

-----

## Свой велосипед 🚲 <!-- .element: class="orange" -->

- обычно дорого – R&D, тесты, документация, bus factor <!-- .element: class="fragment red" -->
- нужно опенсорсить, чтоб сократить косты на R&D <!-- .element: class="fragment" -->
- хорошо если на systemjs, еще лучше если на Module Federation <!-- .element: class="fragment" -->
