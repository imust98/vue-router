# Введение

> В примерах используется синтаксис [ES2015](https://github.com/lukehoban/es6features).

Создать одностраничное приложение используя Vue.js и Vue-router очень просто. Используя Vue.js, мы уже компонуем своё приложение из компонентов. Добавляя Vue-router, мы просто сопоставляем компонентам пути, и указываем, где именно их отображать. Вот простой пример:

> Все примеры используют standalone-сборку Vue, которая позволяет использовать парсинг шаблонов. Подробнее о разнице сборок можно почитать [в документации к Vue.js](https://ru.vuejs.org/v2/guide/installation.html#Standalone-%D0%B8%D0%BB%D0%B8-runtime-%D1%81%D0%B1%D0%BE%D1%80%D0%BA%D0%B0).

### HTML

``` html
<script src="https://unpkg.com/vue/dist/vue.js"></script>
<script src="https://unpkg.com/vue-router/dist/vue-router.js"></script>

<div id="app">
  <h1>Hello App!</h1>
  <p>
    <!-- используйте компонент router-link для создания ссылок -->
    <!-- входной параметр `to` определяет путь для перехода -->
    <!-- <router-link> по умолчанию преобразуется в тег `<a>` -->
    <router-link to="/foo">Go to Foo</router-link>
    <router-link to="/bar">Go to Bar</router-link>
  </p>
  <!-- отображение компонента, для которого совпал путь -->
  <router-view></router-view>
</div>
```

### JavaScript

``` js
// 0. При использовании модульной системы (напр. vue-cli),
// импортируйте Vue и VueRouter и затем вызовите Vue.use(VueRouter)

// 1. Определение используемых компонентов
// Они могут быть импортированы из внешних файлов
const Foo = { template: '<div>foo</div>' }
const Bar = { template: '<div>bar</div>' }

// 2. Определение путей
// Каждый путь должен указывать на компонент
// "Компонентом" может быть как созданный через Vue.extend()
// полноценный конструктор, так и просто объект с настройками компонента
// Вложенные пути будут рассмотрены далее.
const routes = [
  { path: '/foo', component: Foo },
  { path: '/bar', component: Bar }
]

// 3. Создаём инстанс роутера с опцией `routes`
// Можно передать и другие опции, но пока не будем усложнять
const router = new VueRouter({
  routes // сокращение от routes: routes
})

// 4. Создаём и монтируем корневой инстанс Vue нашего приложения.
// Удостоверьтесь, что передали инстанс роутера в опции `router`,
// что позволит приложению знать о его наличии
const app = new Vue({
  router
}).$mount('#app')

// Всё, приложение работает! ;)
```

Вживую этот пример доступен [здесь](http://jsfiddle.net/yyx990803/xgrjzsup/).

Обратите внимание, что `<router-link>` автоматически получает класс `.router-link-active` при совпадении пути. Подробнее об этом можно узнать в [справочнике API](../api/router-link.md).