<h1>Чеклист производительности Front-End для 2017 </h1>
<p>
    Кто из Вас уже использует прогрессивную загрузку (progressive booting)
    в своих проектах? А как на счет <strong>tree-shaking</strong> и <strong>code-splitting</strong> в React и
    Angular? Успели ли Вы настроить под себя сжатие Brotli или Zopfli, сшивания
    OCSP (OCSP stapling) и сжатие HPACK (HPACK compression)? Не стоит так же забывать
    о подсказках ресурсов (resource hints), клиентских подсказках (client hints)
    и сдерживании CSS— и это не говоря уже о IPv6, HTTP/2 и сервис воркерах?
</p>
<p>
    Давайте вспомним дни, когда производительность часто откладывалась на второй план. Вспоминали о ней аж в конце проекта, и в большинстве случаев это сводилось к минификации, конкатенации и оптимизации содержимого, и, возможно, парой дополнительных строк в конфигурационном файле сервера. Оглядываясь на те времена, понимаешь, что ситуация значительно поменялась с тех пор.
    Производительность касается не только технической стороны вопроса: она действительно важна, нужно учитывать, как может отразится на производительности то или иное решение в момент создания дизайна. Производительность нужно постоянно замерять, отслеживать, и улучшать, и вечно-растущая сложность веб-технологий все чаще бросает разработчику вызов, делая невозможным отслеживание метрик, так как метрики будут значительно отличаться в зависимости от устройства, браузера, сетевого протокола, типа сети и задержки в ней (CDN-ы, ISP, кэши, прокси, фаерволы, балансировщики нагрузки и сами сервера играют большую роль в конечной производительности).

</p>
<p>
    Если бы Вам пришлось сделать обзор на все возможные технологии
    о которых придется помнить в случае если поставлена задача улучшить
    производительность Вашего сайта — от самого начала процесса и до
    финального релиза вебсайта — на что бы Вы обратили свое внимание?
    Ниже приведен (надеюсь, беспристрастный и объективный)
    <strong>чеклист производительности front-end’а для 2017 </strong>— обзор
    всех тем с которыми вам возможно придется столкнуться для обеспечения
    максимально быстрого отклика и плавности работы Вашего вебсайта.
    (Вы так же можете просто <a href="http://provide.smashingmagazine.com/performance-checklist/performance-checklist-1.0.pdf?_ga=1.67706521.905683373.1482741288"><strong>загрузить чеклист в PDF (ENG) (0.129 MB)</strong></a> ,
    <a href="#"
       target="_blank"><strong>загрузить чеклист в PDF (RUS) (0.129 MB)</strong></a>
    или <a href="http://provide.smashingmagazine.com/performance-checklist/performance-checklist-1.0.pages?_ga=1.63331879.905683373.1482741288"><strong>скачать чеклист в формате Apple Pages (ENG) (0.236 MB)</strong></a>. Cчастливой оптимизации!)

</p>

<h1>
    Чеклист производительности Front-End’а в 2017
</h1>
<p>
    Текущие микро-оптимизации — это отличная вещь, чтобы удерживать Ваш продукт в строю, но гораздо важнее предопределить какие цели перед Вами стоят и не забывать о них — измеримые цели, которые будут влиять на любые решения, принимаемые на протяжении всего процесса. Существует множество разнообразных моделей, и приведенные ниже – могут варьироваться, но главное — расставить в своем проекте правильные приоритеты.
</p>
<h2>ГОТОВИМСЯ, СТАВИМ ЦЕЛИ </h2>
<h3>
    1. Будь на 20% быстрее ближайшего соперника.
</h3>
<p>
    По результатам психологического исследования, оказалось, что если вы хотите
    что пользователь ощущал что Ваш вебсайт быстрее других, нужно быть как-минимум
    на 20% быстрее.  Не столь важно время полной загрузки и отображения страницы,
    как метрики, например, время начала рендера страницы, <a href="https://developers.google.com/web/tools/lighthouse/audits/first-meaningful-paint" target="_blank">первой
    значительной отрисовки страницы </a> (к примеру, время необходимое
    что бы страница отобразила ее преймущественный контент) и <a href="https://developers.google.com/web/tools/lighthouse/audits/time-to-interactive" target="_blank">время интерактивности</a>
    (то есть, время необходимое странице или, в большинстве
    случаев, SPA что бы предоставить пользователю возможность взаимодействия с ней).
    Измерить время начала рендера (с помощью <a href="http://www.webpagetest.org/" target="_blank">WebPagetest</a>)
    и время отображения первой
    значимой картинки (с помощью <a href="https://github.com/GoogleChrome/lighthouse" target="_blank">Lighthouse</a>) на  Moto G, на устройстве Samsung
    среднего уровня производительности и на добротном среднестатистическом устройстве,
    например Nexus 4, желательно (<i>пометка переводчика – для прогрессивного мира</i>)
    в <a href="https://www.smashingmagazine.com/2016/11/worlds-best-open-device-labs/" target="_blank">открытой лаборатории девайсов</a> (open device lab) — на стандартных скоростях 3G,
    4G и при подключении к точке доступа Wi-Fi.

</p>
<p>
    <img src="img/lighthouse.png" alt="Lighthouse, ПО для ревизии производительности от Google" />
    <br>  <i><strong>Lighthouse</strong>, ПО для ревизии производительности от Google.</i>
</p>
<p>
    Обратите внимание на Вашу аналитику, что бы определить, на чем зацикливаются пользователи.
    Тогда Вы сможете сымитировать 90% пользовательского экспириенса синтетическим
    тестированием. Соберите информацию, составьте таблицу, ужмите ее на 20%
    и таким образом определитесь с Вашими целями
    (например, с <a href="http://bradfrost.com/blog/post/performance-budget-builder/" target="_blank">бюджетом производительности</a>).
    Теперь у Вас есть что-то измеримое, на что нужно ориентироваться в тестировании. Держа в голове мысль о бюджете производительности, и предпринимая попытки написания хоть малейшего скрипта для уменьшения времени интерактивности Вы можете быть уверены, что вы на верном пути.
</p>
<p>
    <img src="img/perf_budget.png" alt="Билдер бюджета производительности от Брэда Фроста." />
    <br>
    <i><a href="http://bradfrost.com/blog/post/performance-budget-builder/" target="_blank">Билдер</a> бюджета производительности от Брэда Фроста.</i>

</p>
<p>
  <strong>
      Поделитесь чеклистом с коллегами.
  </strong>
    Удостоверьтесь что каждый член Вашей команды ознакомлен с данным чеклистом что бы избежать возможного недопонимания в будущем процессе. Каждое принятое решение имеет влияние на производительность, и проект будет только в выигрыше, если не только фронтендеры, но и UX и графические дизайнеры решаться следовать этому плану. Обозначьте решения дизайнера в бюджете производительности и расставьте приоритеты о которых упоминалось выше.


</p>
<h3>
    2. Время отклика 100-миллисекунд, 60 кадров в секунду.
</h3>
<p>
    Модель производительности RAIL ставит перед Вами амбициозные цели: приложите все усилия и предоставьте пользователю отклик в течении 100 миллисекунд после первого входа. Для создания возможности отклика <100 миллисекунд страница должна уступать управление главному потоку не позже чем через каждые <50 миллисекунд. Для точек повышенной нагрузки, как анимация, лучшим решением будет не добавлять ничего больше там, где Вы еще можете, и лишь самый минимум там, где вы уже не можете.
    Более того, каждый кадр анимации должен сменятся менее чем за 16 миллисекунд, тем самым Вы достигнете заветных 60 fps (1 секунда ÷ 60 = 16.6 миллисекунд) — а еще лучше – уложиться в пределы 10 миллисекунд. Вашему браузеру ведь нужно время что бы отрисовать новый кадр на экране, так что постарайтесь что бы исполнение Вашего кода завершилось в течении 16.6 миллисекунд.
    <a href="http://info.meteor.com/blog/optimistic-ui-with-meteor-latency-compensation" TARGET="_blank">Будьте оптимистом </a>и используйте время простоя с умом. Очевидно, что эта цель относится в большей степени к производительности во время выполнения, а не во время загрузки.


</p>
<h3>
    3. Первая значимая картинка через 1.25 секунды, индекс скорости меньше 1000.
</h3>
<p>
    Несмотря на сложность достижения, Вашей абсолютной целью должно быть начало отрисовки страницы уже через 1 секунду и значение
    <a href="https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index" target="_blank">индекса скорости</a> менее 1000 (на высокоскоростном подключении). Максимально-допустимая длительность отрисовки первого значимого изображения – 1250 миллисекунд. Для мобильных устройств
    <a href="https://www.soasta.com/blog/google-mobile-web-performance-study/" target="_blank"> неплохим</a> показателем будет начало отрисовки страницы меньше чем через 3 секунды для 3G подключения. Если Ваши показатели слегка перевалили за это значения – ничего страшного, но старайтесь понизить эти показатели как можно сильнее.
</p>
<h2>
    ОПРЕДЕЛИМСЯ С ОКРУЖЕНИЕМ
</h2>
<h3>
    4. Выберите для себя и сконфигурируйте инструменты сборки.
</h3>
<p>
    Не стоит слишком зацикливаться на том, что считается трендовым инструментом в данный момент. Придерживайтесь в выборе собственных интересов в разработке, не важно будет ли это Grunt, Gulp, Webpack, PostCSS или комбинация инструментов. До тех пор, пока Вам удается получать достичь результатов быстро, и Вы не ощущаете проблем в процессе использования инструментов сборки – у Вас должно быть все хорошо.
</p>
<h3>
    5. Прогрессивное улучшение.
</h3>
<p>
    Смело делайте ставку на <a href="https://www.aaron-gustafson.com/notebook/insert-clickbait-headline-about-progressive-enhancement-here/" target="_blank">прогрессивное улучшение</a> в качестве ведущего принцип архитектуры вашего front-end’а. Сначала спроектируйте и реализуйте базовые возможности, и только потом, дополняйте их сложными фичами для подходящий браузеров, создавая
    <a href="https://resilientwebdesign.com/" target="_blank">отказоустойчивый интерфейс</a>. В том случае если ваш вебсайт работает быстро на медленном устройстве, со слабым браузером и посредственным интернетом, вы точно можете быть уверены, что он будет отлично работать на устройстве побыстрее, с современным браузером и хорошим интернет соединением.
</p>

<h3>
    6. Angular, React, Ember и компания.
</h3>
<p>
    Присмотритесь к Фреймворку, который
    позволяет отрисовать картинку на стороне сервера.
    Не забудьте замерять время загрузки как в режиме отрисовки на сервере,
    так и на клиенте для мобильных устройств, прежде чем приступать
    к работе с Фреймворком. (так как эти изменения в будущем может быть
    невероятно сложно воплотить). Если Вы уже используете JavaScript фреймворк,
    убедитесь, что Ваш выбор является <a href="https://www.youtube.com/watch?v=6I_GwgoGm1w" target="_blank">оптимальным</a> и
    <a href="https://medium.com/@ZombieCodeKill/choosing-a-javascript-framework-535745d0ab90#.2op7rjakk">
    справедливым</a>. Каждый из фреймворков по-своему будет влиять на конечную производительность
    и будет требовать индивидуальной стратегии оптимизации, поэтому
    Вам нужно отчетливо понимать всю подноготную выбранного фреймворка.
    В процессе построения веб-приложения обратите внимание на <a href="https://developers.google.com/web/fundamentals/performance/prpl-pattern/" target="_blank">шаблон PRPL</a> и архитектуру
    <a href="https://developers.google.com/web/updates/2015/11/app-shell" target="_blank">оболочки приложения</a>.
    
</p>
<p>
    <img src="img/PRPL.png" alt="PRPL " />
    <br>  <i>PRPL отвечает за выгрузку критично-важных ресурсов, Рендер изначальных маршрутов, Пре-кэширование остальных маршрутов и “ленивая” загрузка остальных маршрутов по запросу.</i>
</p>
<p>
    <img src="img/shell.png" alt="Оболочка приложения">
    <br>
    <i><a href="https://developers.google.com/web/updates/2015/11/app-shell" target="_blank">Оболочкой приложения</a> называют
        минимальный HTML, CSS, и JavaScript снабжающий интерфейс пользователя.</i>
</p>
<h3>
    7. AMP от ребят из Google или Instant Articles от Facebook?
</h3>
<p>
    В зависимости от Ваших приоритетов и стратегии организации рабочего процесса Вам предстоит выбирать между <a
        href="https://www.ampproject.org/" target="_blank">Google AMP</a> и <a href="https://instantarticles.fb.com/" target="_blank">Instant Articles</a> от Facebook. Конечно, вы можете добиться отличной производительности и без них, но AMP, к примеру, предлагает фреймворк с превосходной производительностью и бесплатным доступом к СDN, а Instant Articles взвинтят показатели производительности на Facebook. Вы, кстати, можете и сами заняться построением
    <a href="https://www.smashingmagazine.com/2016/12/progressive-web-amps/" target="_blank">прогрессивных веб приложений</a>.
</p>
<h3>
    8. Подойдите мудро к вопросу о выборе вашей CDN
</h3>
<p>
    В зависимости от того насколько статична информация на вашем вебсайте,
    Вы можете попробовать использовать вынести часть контента во
    внешний ресурс (<a href="https://www.smashingmagazine.com/2015/11/static-website-generators-jekyll-middleman-roots-hugo-review/" target="_blank">static site generator</a>),
    выгрузив ее на CDN и запрашивая оттуда статическую версию контента
    при необходимости, таким образом вы спасётесь от запросов к базе данных.
    Вы даже можете выбрать для себя статические <a href="https://www.smashingmagazine.com/2015/11/modern-static-website-generators-next-big-thing/" target="_blank">
    хостинг-платформы </a> базирующиеся на CDN, обогащая страницы вашего вебсайта
    интерактивностью, в качестве прогрессивного улучшения
    (<a href="https://jamstack.org/">JAMStack</a>).
    <br>
    Обратите внимание, что вы можете использовать CDNы для разгрузки (распределения) динамического контента тоже. Так что не обязательно ограничиваться в использовании CDN только для статического контента. Обязательно перепроверьте выполняет ли выбранная CDN сжатие и преобразование контента, умную выгрузку HTTP/2, имеется ли возможность сборки статической и динамической части контента для страницы на стороне CDN’а (ближайший по расположению сервер для пользователя), и другие необходимые задачи.

</p>
<h2>
    ОПТИМИЗАЦИЯ СБОРКИ
</h2>
<h3>
    9. Установите для себя четкие приоритеты.
</h3>
<p>
    Было бы мудро, для начала ознакомиться с чем Вам придется работать. Проведите «инвентаризацию» всех своих ресурсов и контента (JavaScript, изображения, шрифты, внешние скрипты, и “увесистые” модули на странице, такие как карусели, сложная инфографика, и мультимедийный контент), и разделите их на группы.
    <br>
    Составьте таблицу. Определите <strong>основные моменты</strong> для устаревших
    браузеров (т. е. полностью доступный основной контент), затем,
    <strong>улучшенный</strong> интерфейс для подходящих браузеров
    (т.е. улучшенный функционал, полный интерфейс взаимодействия) и
    <strong>дополнения</strong>(активы, который не являются абсолютно-необходимыми
    и могут быть подгружены позже (lazy-load),
    такие как веб шрифты, излишние стили, скрипты каруселей, видеоплейеры,
    кнопки социальных сетей, крупные изображения).
    В качестве примера рекомендуется к рассмотрению статья
    "<a href="https://www.smashingmagazine.com/2014/09/improving-smashing-magazine-performance-case-study/" target="_blank">Improving Smashing Magazine’s Performance</a>" , которая описывает этот подход в подробностях.
</p>
<h3>
    10. Используйте технику «Сбора вершков»
</h3>
<p>

</p>




<p>
    <strong>
        Неотредактированное
    </strong>
    Use the (cutting-the-mustard technique) to send the core experience to legacy browsers and an enhanced experience to modern browsers. Be strict in loading your assets: Load the core experience immediately, the enhancements on DomContentLoaded and the extras on the loadevent.
    Note that the technique deduces device capability from browser version, which is no longer something we can do these days. For example, cheap Android phones in developing countries mostly run Chrome and will cut the mustard despite their limited memory and CPU capabilities. Beware that, while we don’t really have an alternative, use of the technique has become more limited recently.

    11. Consider micro-optimization and progressive booting.
    In some apps, you might need some time to initialize the app before you can render the page. Display skeleton screens instead of loading indicators. Look for modules and techniques to speed up the initial rendering time (for example, tree-shaking and code-splitting), because most performance issues come from the initial parsing time to bootstrap the app. Also, use an ahead-of-time compiler to offload some of the client-side rendering to the server and, hence, output usable results quickly. Finally, consider using Optimize.js for faster initial loading by wrapping eagerly invoked functions (it might not be necessary any longer, though).

    Прогрессивная загрузка (Progressive booting) подразумевает использование отрисовки страницы на сервере что бы получить первую значимую картинку максимально быстро, а также подключите минимальный JavaScript, чтобы привести время интерактивности ближе к времени отрисовки первой значимой картинки.
    Client-side rendering or server-side rendering? In both scenarios, our goal should be to set up (progressive booting): Use server-side rendering to get a quick first meaningful paint, but also include some minimal JavaScript to keep the time-to-interactive close to the first meaningful paint. We can then, either on demand or as time allows, boot non-essential parts of the app. Unfortunately, as (Paul Lewis noticed), frameworks typically have no concept of priority that can be surfaced to developers, and hence progressive booting is difficult to implement with most libraries and frameworks. If you have the time and resources, use this strategy to ultimately boost performance.

    12. Are HTTP cache headers set properly?
    Обязательно перепроверьте что expires, cache-control, max-age и другие заголовки кэша HTTP правильно выставлены. В общем, ресурсы должны подлегать кэшированию или на очень короткий срок (если они могут изменяться) или навсегда (если они неизменны) — вы можете просто изменять их версию в URL при необходимости.
    По возможности, используйте Cache-control: immutable, предназначенный для защищенных отпечатком пальца статических ресурсов, во избежание ре-валидации (на момент написания – Декабрь 2016 - поддерживается только в Firefox (supported only in Firefox) по транзакциям https:// ). Вы можете использовать праймер заголовков HTTP кэша Хироку (Heroku’s primer on HTTP caching headers), «Лучшие практики по кешированию» Джейка Арчибальда (“Caching Best Practices”) и Праймер кэширования HTTP от Ильи Григорика (HTTP caching primer) в качестве руководства.

    13. Ограничьте сторонние библиотеки и загружайте JavaScript асинхронно.
    Когда пользователь запрашивает страницу, браузер извлекает HTML и строит DOM, потом собирает CSS и строит CSSOM, и только потом генерирует дерево рендера, в соответствии с DOM и CSSOM. Если какой-либо скрипт должен отработать, по умолчанию, браузер не начинает рендер страницы пока скрипт не закончит работу, что вызывает задержки рендера. Нам, разработчикам, приходится настойчиво указывать браузеру что не стоит ждать окончания выполнения скриптов для начала рендера страницы. Простейшим способом добиться этого являются HTML атрибуты defer и async.
    На практике, хорошо бы нам отдавать предпочтение (prefer ) defer (to) перед  async (как поблажку для пользователей IE9 и старше (cost to users of Internet Explorer), потому что скорее всего иначе Вы сломаете им все скрипты). Также постарайтесь ограничить влияние сторонних скриптов и библиотек, особенно кнопок социальных сетей и врезок <iframe>  (карт, например). Вместо этого вы можете использовать статические кнопки социальных сетей (static social sharing buttons) (например, SSBG) и статические ссылки на интерактивные карты (static links to interactive maps).

    14. Правильно ли оптимизированы изображения?
    Как можно больше используйте адаптивные изображения (responsive images) с атрибутами srcset, sizes и элементом . While you’re at it, you could also make use of the WebP format by serving WebP images with the element and a JPEG fallback (see Andreas Bovens’ code snippet) or by using content negotiation (используя заголовки Accept). Sketch нативно поддерживает WebP, и изображения в формате WebP могут быть экспортированы из Photoshop используя плагин WebP для Photoshop (WebP plugin for Photoshop).  Конечно, возможны и другие варианты. (Other options are available).

        Генератор брейкпоинтов для адаптивных изображений ( Responsive Image Breakpoints Generator) автоматизирует создание изображений и разметки.
        Вы также могли бы использовать клиентские подсказки, (client hints), они как раз сейчас заручаются поддержкой браузеров (gaining browser support). Не успеваете заняться сложной разметкой для адаптивности Ваших изображений? Вам в помощь Генератор брейкпоинтов для адаптивных изображений ( Responsive Image Breakpoints Generator) а также другие сервисы автоматизированной оптимизации изображений, например Cloudinary. Также, в большинстве случаев, использование одних только srcset и sizes принесет значительную выгоду.  Например, ребята из Smashing Magazine, используют -opt для имён изображений — например, brotli-compression-opt.png; Как только изображение содержит в себе постфикс opt, каждый член команды знает, что его уже не нужно оптимизировать.
        15. Выведите оптимизацию изображений на новый уровень.
        Когда Вы работаете над лэндингом, для которого критичным является молниеносная загрузка некоторых изображений убедитесь что Ваши  JPEGи прогрессивны и сжаты с помощью  mozJPEG (который улучшает скорость начала рендера изображения с помощью манипуляций с уровнями сканирования), Pingo для PNG, Lossy GIF для GIF и SVGOMG для SVG. Размойте ненужные части изображения (применяя к ним размытие по Гауссу) что бы уменьшить размер изображения, если даже это не помогает, в конце концов можете попробовать лишать изображение цвета, черно-белое изображение весит гораздо меньше. Для фоновых изображений вполне приемлемым будет экспорт изображений с качеством от 0 до 10%.
        Все еще не довольны результатом? Ну тогда, Вам придется обратиться к технике множественных фоновых изображений (multiple background images technique).

        16. Как обстоят дела с оптимизацией веб шрифтов?
        Chances are high that the web fonts you are serving include glyphs and extra features that aren’t being used. You can ask your type foundry to subset web fonts or subset them yourself if you are using open-source fonts (for example, by including only Latin with some special accent glyphs) to minimize their file sizes. WOFF2 support is great, and you can use WOFF and OTF as fallbacks for browsers that don’t support it. Also, choose one of the strategies from Zach Leatherman’s “Comprehensive Guide to Font-Loading Strategies,” and use a service worker cache to cache fonts persistently. Need a quick win? Pixel Ambacht has a quick tutorial and case study to get your fonts in order.


        Zach Leatherman’s Comprehensive Guide to Font-Loading Strategies provides a dozen of options for better web font delivery.
        If you can’t serve fonts from your server and are relying on third-party hosts, make sure to use Web Font Loader. FOUT is better than FOIT; start rendering text in the fallback right away, and load fonts asynchronously — you could also use loadCSS for that. You might be able to get away with locally installed OS fonts as well.
        17. Молниеносно выгрузите критичные CSS стили.
        To ensure that browsers start rendering your page as quickly as possible, it’s become a common practice to collect all of the CSS required to start rendering the first visible portion of the page (known as “critical CSS” or “above-the-fold CSS”) and add it inline in the <head> of the page, thus reducing roundtrips. Due to the limited size of packages exchanged during the slow start phase, your budget for critical CSS is around 14 KB. If you go beyond that, the browser will need addition roundtrips to fetch more styles. CriticalCSS and Criticalenable you to do just that. You might need to do it for every template you’re using. If possible, consider using the conditional inlining approach used by the Filament Group.
            With HTTP/2, critical CSS could be stored in a separate CSS file and delivered via a server push without bloating the HTML. The catch is that server pushing isn’t supported consistently and has some caching issues (see slide 114 onwards of Hooman Beheshti’s presentation). The effect could, in fact, be negative and bloat the network buffers, preventing genuine frames in the document from being delivered. Server pushing is much more effective on warm connections due to the TCP slow start. So, you might need to create a cache-aware HTTP/2 server push mechanism. Keep in mind, though, that the new cache-digest specification will negate the need to manually build these “cache-aware” servers.

            18. Используйте tree-shaking и code-splitting для уменьшения нагрузки.
            (Tree-shaking) is a way to clean up your build process by only including code that is actually used in production. You can (use Webpack 2 to eliminate unused exports), and UnCSS or Helium to remove unused styles from CSS. Also, you might want to consider learning how to (write efficient CSS selectors) as well as how to (avoid bloat and expensive styles).
            (Code-splitting) is another Webpack feature that splits your code base into “chunks” that are loaded on demand. Once you define split points in your code, Webpack takes care of the dependencies and outputted files. It basically enables you to keep the initial download small and to request code on demand, when requested by the application.
            Note that Rollup shows significantly better results than Browserify exports. While we’re at it, you might want to check out Rollupify, which converts ECMAScript 2015 modules into one big CommonJS module — because small modules can have a (surprisingly high performance cost) depending on your choice of bundler and module system.

            19. Улучшайте производительность рендера.
            Isolate expensive components with CSS containment — for example, to limit the scope of the browser’s styles, of layout and paint work for off-canvas navigation, or of third-party widgets. Make sure that there is no lag when scrolling the page or when an element is animated, and that you’re consistently hitting 60 frames per second. If that’s not possible, then at least making the frames per second consistent is preferable to a mixed range of 60 to 15. Use CSS’ will-change to inform the browser of which elements and properties will change.
            Also, measure runtime rendering performance (for example, in DevTools). To get started, check Paul Lewis’ free Udacity course on browser-rendering optimization. We also have a lil’ article by Sergey Chikuyonok on how to get GPU animation right.

            20. Warm up the connection to speed up delivery.
            Use skeleton screens, and lazy-load all expensive components, such as fonts, JavaScript, carousels, videos and iframes. Use resource hints to save time on dns-prefetch (which performs a DNS lookup in the background), preconnect (which asks the browser to start the connection handshake (DNS, TCP, TLS) in the background), prefetch(which asks the browser to request a resource), prerender (which asks the browser to render the specified page in the background) and preload (which prefetches resources without executing them, among other things). Note that in practice, depending on browser support, you’ll prefer preconnect to dns-prefetch, and you’ll be cautious with using prefetch and prerender — the latter should only be used if you are very confident about where the user will go next (for example, in a purchasing funnel).

            HTTP/2

            21. Будьте готовы к HTTP/2.
            With Google moving towards a more secure web and eventual treatment of all HTTP pages in Chrome as being “not secure,” you’ll need to decide on whether to keep betting on HTTP/1.1 or set up an HTTP/2 environment. HTTP/2 is supported very well; it isn’t going anywhere; and, in most cases, you’re better off with it. The investment will be quite significant, but you’ll need to move to HTTP/2 sooner or later. On top of that, you can get a major performance boost with service workers and server push (at least long term).

            Eventually, Google plans to label all HTTP pages as non-secure, and change the HTTP security indicator to the red triangle that Chrome uses for broken HTTPS. (Image source)
            The downsides are that you’ll have to migrate to HTTPS, and depending on how large your HTTP/1.1 user base is (that is, users on legacy operating systems or with legacy browsers), you’ll have to send different builds, which would require you to adapt a different build process. Beware: Setting up both migration and a new build process might be tricky and time-consuming. For the rest of this article, I’ll assume that you’re either switching to or have already switched to HTTP/2.

            22. Properly deploy HTTP/2.
            Again, serving assets over HTTP/2 requires a major overhaul of how you’ve been serving assets so far. You’ll need to find a fine balance between packaging modules and loading many small modules in parallel.
            On the one hand, you might want to avoid concatenating assets altogether, instead breaking down your entire interface into many small modules, compressing them as a part of the build process, referencing them via the “scout” approach and loading them in parallel. A change in one file won’t require the entire style sheet or JavaScript to be re-downloaded.

            On the other hand, packaging still matters because there are issues with sending many small JavaScript files to the browser. First, compression will suffer. The compression of a large package will benefit from dictionary reuse, whereas small separate packages will not. There’s standard work to address that, but it’s far out for now. Secondly, browsers have not yet been optimized for such workflows. For example, Chrome will trigger inter-process communications (IPCs) linear to the number of resources, so including hundreds of resources will have browser runtime costs.

            Что бы достичь лучших результатов используя HTTP/2, попробуйте подгружать CSS прогрессивно (load CSS progressively), как было предложено Джеком Арчибальдом из Chrome.

            Still, you can try to load CSS progressively. Obviously, by doing so, you are actively penalizing HTTP/1.1 users, so you might need to generate and serve different builds to different browsers as part of your deployment process, which is where things get slightly more complicated. You could get away with HTTP/2 connection coalescing, which allows you to use domain sharding while benefiting from HTTP/2, but achieving this in practice is difficult.
            What to do? If you’re running over HTTP/2, sending around 10 packages seems like a decent compromise (and isn’t too bad for legacy browsers). Experiment and measure to find the right balance for your website.

            23. Удостоверьтесь в пуленепробиваемой защите вашего сервера.
            All browser implementations of HTTP/2 run over TLS, so you will probably want to avoid security warnings or some elements on your page not working. Double-check that your (security headers are set properly), (eliminate known vulnerabilities), and (check your certificate).
            Haven’t migrated to HTTPS yet? Check (The HTTPS-Only Standard) for a thorough guide. Also, make sure that all external plugins and tracking scripts are loaded via HTTPS, that cross-site scripting isn’t possible and that both (HTTP Strict Transport Security headers) and (Content Security Policy headers) are properly set.

            24. Поддерживают ли Ваш сервер и CDNы HTTP/2?
            Разные сервера и CDNы скорее всего будет поддерживать HTTP/2 по-разному. Попробуйте Is TLS Fast Yet? Что-бы уточнить информацию касательно вашего варианта или в сравнении с другими узнать насколько производителен Ваш сервер и поддержку каких фич стоит ожидать в скором времени.

            Ресурс Is TLS Fast Yet? Позволяет Вам проанализировать конфигурации серверов и CDN при переходе на HTTP/2.
            25. Используется ли сжатие Brotli или Zopfli?
            В прошлом году Google представили миру Brotli (introduced Brotli), новый формат данных без потерь, который уже широко поддерживается (widely supported) в Chrome, Firefox и Opera. На практике, Brotli представляется более эффективным (more effective) чем Gzip и Deflate. Сам процесс сжатия может быть затяжным, в зависимости от настроек и чем дольше длится сжатие, тем выше будет уровень самого сжатия. Кстати говоря, декомпрессия происходит быстро. Не будет сюрпризом что браузеры будут поддерживать этот алгоритм только если пользователь посещает вебсайт через HTTPS, ведь алгоритм разработан в Google, но на самом деле, на то есть еще и технические причины. Загвоздка в том, что Brotli не предустановлен на большинстве серверов сегодня, и не так уж просто его настроить без самостоятельной компиляции NGINX или Ubuntu. Однако, вы можете активировать Brotli даже на тех CDN, которые пока что его не поддерживают (enable Brotli even on CDNs that don’t support it) yet (с помощью сервис воркеров).
            В качестве альтернативы, можете рассмотреть алгоритм сжатия Zopfli (Zopfli’s compression algorithm), который кодирует информацию в форматы Deflate, Gzip и Zlib. Любой ресурс сжатый простым Gzip-ом можно выгодно сжимать с Zopfli’s с улучшеным кодированием Deflate, потому что файлы будут на 3-8% меньше чем может предоставить лушчее сжатие от Zlib’s. Загвоздка в тому, что это займет гораздо больше времени (~в 80 раз дольше). Поэтому использование Zopfli будет отличным решением для ресурсов, которые не очень-то меняются, файлы, которые, были созданы, чтобы однажды быть сжатыми и множество раз скачанными.

            26. Активировано ли OCSP сшивание?
            By enabling OCSP stapling on your server, you can speed up your TLS handshakes. The Online Certificate Status Protocol (OCSP) was created as an alternative to the Certificate Revocation List (CRL) protocol. Both protocols are used to check whether an SSL certificate has been revoked. However, the OCSP protocol does not require the browser to spend time downloading and then searching a list for certificate information, hence reducing the time required for a handshake.

            27. Успели ли Вы взять IPv6 на вооружение?
            Because we’re running out of space with IPv4 and major mobile networks are adopting IPv6 rapidly (the US has reached a 50% IPv6 adoption threshold), it’s a good idea to update your DNS to IPv6 to stay bulletproof for the future. Just make sure that dual-stack support is provided across the network — it allows IPv6 and IPv4 to run simultaneously alongside each other. After all, IPv6 is not backwards-compatible. Also, studies show that IPv6 made those websites 10 to 15% faster due to neighbor discovery (NDP) and route optimization.

            28. Пользуетесь ли Вы HPACK сжатием?
            В случае если вы используете HTTP/2, стоит убедиться, что Ваши сервера используют сжатие HPACK (implement HPACK compression) в заголовках HTTP ответов, чтобы уменьшить использование ресурсов. Из-за того, что сервера HTTP/2 относительно молоды, может иметь место неполноценная поддержка спецификаций, с HPACK, например. H2spec это отличный (и очень детализированный) инструмент что бы проверить работоспособность HPACK (HPACK works).

            H2spec
            29. Работают ли сервис воркеры для кэширования и сетевых фолбэков?
            Как ни оптимизируй сетевую передачу данных, она не будет быстрее чем получение данных из локального кэша, хранящегося на устройстве пользователя. Если Ваш вебсайт использует HTTPS, стоит присмотреться к «Прагматичному гиду по сервис воркерам» (“Pragmatist’s Guide to Service Workers”) что бы добавлять в кэш сервис воркеров статические материалы и локально хранить офлайн фолбэки (или целые офлайн страницы) и открывать их из памяти устройства пользователя а не отправляться за ними в. Будет полезным также посмотреть «Книгу рецептов для Офлайна» от Джейка (Offline Cookbook) и бесплатный Udacity курс “Offline Web Applications.” Волнуетесь о поддержке браузерами? Не стоит, она на подходе (getting there), да и сеть в любом случае останется запасным вариантом.


</p>

<h2>
    ТЕСТИРОВАНИЕ И МОНИТОРИНГ
</h2>
<h3>
    30. Отслеживайте предупреждения микс-контента (mixed-content).
</h3>
<p>
    Если Вы не так давно перешли с HTTP на HTTPS,
    не забудьте промониторить предупреждения микс-контента,
    как активного так и пассивного, для этого подойдёт инструмент
    <a href="https://report-uri.io/" target="_blank">Report-URI.io</a>.
    Вы также можете использовать <a href="https://github.com/bramus/mixed-content-scan">
    Mixed Content Scan</a>
    что бы просканировать
    Ваш вебсайт с активированным HTTPS-на содержание микс-контента.
</p>
<h3>
    31. Оптимизирован ли Ваш рабочий процесс с Инструментами разработчика (DevTools)?
</h3>
<p>
    Выберите для себя инструменты отладки и прокликайте каждую кнопку,
    ссылку. Убедитесь, что Вы знаете, как проанализировать и улучшать
    производительность отрисовки страницы, консольный вывод, и,
    как отладить JavaScript или корректировать CSS стили.
    Не так давно Умар Ганза (Umar Hansa)
    подготовил огромную <a href="https://umaar.github.io/devtools-optimise-your-web-development-workflow-2016/#/" target="_blank">презентацию</a> и <a href="https://www.youtube.com/watch?v=N33lYfsAsoU" target="_blank">речь</a>,
    в которых упоминаются дюжины неизведанных советов и техник
    о которых не стоит забывать, когда дело доходит до отладки
    и тестирования в Инструментах разработчика (DevTools).
</p>
<h3>
    32. Какие результаты тестирования в устаревших браузерах? В прокси браузерах?
</h3>
<p>
    Тестирования в Chrome и Firefox, однозначно недостаточно.
    Оцените, как Ваш вебсайт выглядит в прокси-браузере и в устаревших браузерах.
    К примеру, UC Browser и Opera Mini, <a href="http://gs.statcounter.com/#mobile_browser-as-monthly-201511-201611" target="_blank">
    занимают огромный сегмент рынка в Азии</a>
    (до 35% в Азии). <a href="https://www.webworldwide.io/" target="_blank">
    Исследуйте и замерьте</a> среднюю скорость подключения к сети в странах,
    на которых ориентирован Ваш продукты, чтобы в будущем не столкнуться с
    неприятным сюрпризом. Не забудьте провести тестирование с троттлингом и симулируйте дисплей повышенной плотности.
    <a href="https://www.browserstack.com/" target="_blank">BrowserStack</a>  - это отличный инструмент, но тестирование на физических девайсах не менее.
</p>

<h3>
    33. Вы установили непрерывный мониторинг?
</h3>
<p>
    Всегда гораздо выгоднее иметь собственный экземпляр <a href="http://www.webpagetest.org/" target="_blank">
    WebPagetest
</a>'а для быстрых и неограниченных тестирований.
    Установите непрерывный мониторинг за бюджетом производительности с
    автоматическими извещениями. Установите собственные временные оценки
    что бы измерять, сравнивать и мониторить метрики в зависимости от сферы
    деятельности. Присмотритесь к использованию <a href="https://speedcurve.com/" target="_blank">
SpeedCurve</a> чтобы отслеживать изменения в производительности со временем, и/или
    <a href="https://newrelic.com/browser-monitoring" target="_blank">
        New Relic</a> что бы получить выводы, которые
    <i>WebPagetest</i> не предоставляет. Стоит так же обратить внимание на
    <a href="https://speedtracker.org/" target="_blank">SpeedTracker</a>,
    <a href="https://github.com/GoogleChrome/lighthouse" target="_blank">Lighthouse</a> и
    <a href="https://calibreapp.com/" target="_blank">Calibre</a>.
</p>

<h2>
    Моментальный результат!
</h2>
<p>
    Список достаточно обширный, и выполнение оптимизация может отнять у Вас
    порядочно времени. А что если бы у Вас был лишь 1 час что бы добиться значительных улучшений? Какое бы решение приняли Вы? Давайте сузим список до десятки самых просто-достижимых целей. Очевидно, Вам придется замерять результаты до начала и после окончания оптимизации, включая время начала рендера и Индекс скорости на 3G и проводном подключении.
</p>
<ol>
    <li>Вашей целью является начало отрисовки страницы не позже чем через 1 секунду на проводном подключении и 3 секунды используя 3G, и индекс скорости величиной менее 1000. Оптимизируйте время начала отрисовки и время интерактивности.</li>
    <li>Подготовьте критичный CSS для основных шаблонов, и включите их в <code>
        &lthead&gt</code> вашей страницы. (Ваш бюджет - 14 KB).</li>
    <li>Используйте <i>Defer</i> и <i>lazy-load</i> во всех скриптах, где только возможно, как в своих собственных, так и в сторонних — особенно это касается социальных медиа ссылок, видеоплейеров, и увесистого JavaScript.</li>
    <li>Добавьте подсказки ресурсов, чтобы ускорить загрузки с быстрым <code>dns-lookup, preconnect, prefetch, preload и prerender</code>.</li>
    <li>Разделите веб шрифты и загружайте их асинхронно (или просто переключайтесь на системные шрифты, как альтернатива).</li>
    <li>Оптимизируйте изображения, рассмотрите возможность использования WebP для основных страниц (например, лэндингов).</li>
    <li>Удостоверьтесь что сами заголовки кэша HTTP и их безопасность установлены правильно.</li>
    <li>Активируйте сжатие <i>Brotli</i> или <i>Zopfli</i> на сервере. (В случае если это невозможно, не забывайте про сжатие Gzip.)</li>
    <li>Если HTTP/2 доступен, активируйте сжатие HPACK и начните отслеживать предупреждения смешанного контента. Если вы работаете над LTS, также активируйте сшивание OCSP.</li>
    <li>Если представляется возможным, кэшируйте содержимое, например, шрифты, стили, скрипты и изображения, а вообще, чем больше – тем лучше! — в кэши сервис воркеров.</li>
</ol>





<h2>
    Скачайте чеклист для себя(PDF)
</h2>
<p>
    Держа в голове этот чеклист, вы гарантированно будете подготовлены к разработке любого front-end проекта в 2017 году. Не забывайте скачать PDF файл с чеклистом, подготовленным для печати для Ваших нужд:
</p>
<ul>
    <li><a href="http://provide.smashingmagazine.com/performance-checklist/performance-checklist-1.0.pdf" target="_blank">
        Download the checklist PDF </a></li>
    <li><a href="#" target="_blank">
        Скачать чеклист в PDF на русском </a></li>
    <li><a href="http://provide.smashingmagazine.com/performance-checklist/performance-checklist-1.0.pages?_ga=1.131076231.905683373.1482741288" target="_blank">
    download the checklist in Apple Pages </a></li>
</ul>
<h1>
    Ну что ж, поехали!
</h1>
<p>
    Некоторая часть процесса оптимизации может выходить за рамки вашего проекта и/или бюджета, а также быть попросту невыполнимым заданием, работая, скажем, с доисторическим кодом, который Вам достался. Это вполне нормально! Рекомендуется использовать данный чеклист как общие (и, надеюсь, фундаментальные) инструкции, или создать на его основе свой собственный список тем, которые будут применимы для Вашего проекта. Кстати, не забывайте протестировать и замерить результаты Ваших проектов до начала оптимизации, чтобы определить наиболее важные моменты. Удачной всем оптимизации в новом, 2017 году!
</p>





