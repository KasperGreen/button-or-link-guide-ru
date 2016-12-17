<a name="start"></a>

# Кнопка или [ссылка](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия")?

>Я знаю хабр не для жалоб, 
>
>но доколе
>
>использовать ты  будешь
>
>— [ссылки](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия") вместо кнопок `<UserName />`‽


![Девушка на картинке как бы спрашивает — Куда жать?](https://slasher.ru/articles/link-or-button/+poster.png?1 "Девушка на картинке как бы спрашивает — Куда жать?")

_Автор иллюстрации `<Marat Hilmanov>` gray-monkey@yandex.ru_

Если коротко:
=============
Используйте для кнопок — кнопки, а для [ссылок](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия") — [ссылки](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия").

>Для кнопок использовать
[ссылки](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия")
— не комильфо.



<habracut />
![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

Это не исчерпывающее руководство по кнопкам и не пример невероятного дизайна, а лишь попытка показать, что есть разница между ссылками и кнопками.

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

Для кого эта статья?
------------------------

В первую очередь для дизайнера который делает макет сайта, но не дорисовывает детали свойственные вебу. Своеобразная попытка объяснить, что веб-сайт лежит за пределами плоской полиграфии.


Во вторых для верстальщика к которому пришёл макет без состояний, чтобы было куда дизайнера послать.


В третьих чтобы вместо очередной тирады о разнице в кнопках\ссылках и нужности дизайна состояний, просто давать [ссылку](https://habrahabr.ru/post/317728/).

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

Содержание
----------
* [Ссылки](#ssylki)
    * [Введение](#vvedenie)
    * [Антипаттерн](#antipattern)
    * [Состояния](#sostoyaniya)
* [Кнопки](#html5-buttonknopkabutton)
    * [Доступность](#dostupnost)
    * [Поведение внутри тега `<form>`](#povedenie-vnutri-formy)
    * [Состояния](#sostoyaniya-1)
    * [Отображение](#otobrazhenie)
    * [CSS](#css)
        * [Простой](#css)
        * [Сложный](#primer-poslozhnee)
* [Дизайнеру](#dizayneru)
* [Спасибо](#spasibo)
* [Репозиторий на GitHub](#github)

---------------------------

<a name="ssylki"></a>

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

## Ссылки

<a name="vvedenie"></a>

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

### Введение

```html
<a href="javascript:;">Ссылка которая кнопка</a>
```
Когда наводят указатель на [ссылку](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия") которая кнопка то в левом нижнем углу появляется надпись javascript:;:
![javascript:;](https://slasher.ru/articles/link-or-button/javascript.png)
Или адрес с решёткой:
![https//site.name/page.html#](https://slasher.ru/articles/link-or-button/octothorpe.png)

`ПКМ` на такой кнопке и контекстное меню любезно предложит:
![Контекстное меню предлагает открыть ссылку в новой вкладке: сохранить, копировать…  ](https://slasher.ru/articles/link-or-button/mrb.png)

`ctrl` + `ЛКМ` на такой кнопке откроют новую вкладку на которой будет ровно та страница, с которой она была открыта.

Кроме того такая [ссылка](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия") с решёткой в качестве [ссылки](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия"), станет `:visited`, если ещё не стала до этого, и приобретёт соотстветствующее стилевое оформление. Если дизайнер его конечно не зарезал, что в большинстве случаев конечно зря, о чём ниже.

>В JavaScript скриптах для таких кнопок дополнительно используется `e.preventDefault()`, чтобы предотвратить действие кнопки по умолчанию (переход по [ссылке](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия")) "— это костыль.

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

`<a href="//link.url">Ссылка</a>`
---------------------------------
* Если клик приведёт к смене адреса,
* этот адрес можно скопировать,
* отправить по электронной почте,
* на него можно снова зайти,
* это не адрес самой страницы
**— это [ссылка](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия")**.

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

#### У [ссылки](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия") должны быть стили для обычного, `:active`, `:visited`, `:focus` и `:hover` состояний.

<a name="antipattern"></a>

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

### Антипаттерн
```css
a {
    color: black !important;
    text-decoration: none !important;
    cursor: default !important;
}
```
Поздравляю! С такими стилями все ваши [ссылки](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия") визуально превратятся в обычный текст. Найти их на странице станет крайне затруднительно.

![Антипример с неразличимыми ссылками](https://slasher.ru/articles/link-or-button/a_example_anti.png)

>И помните, если вы ставите `!important` и не очень понимаете почему вы без него не можете обойтись, то читайте это слово как **импотент**. Возможно вам нужно немного  изменить селектор для того, чтобы перекрыть тот, который вам мешает.



<a name="sostoyaniya"></a>

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

### Состояния

![текст с различными состояниями ссылки](https://slasher.ru/articles/link-or-button/link_sates_example.png)
-----------------------
`a` — обычное состояние
-----------------------
```css
a {
    color: #0645ad;
    cursor: pointer;
    text-decoration: none;
}
```
В  обычном состоянии `a`  должна быть  синей или подчёркнутой, а лучше и синей и подчёркнутой, чтобы пользователь без наведения мыши понимал, что это — [ссылка](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия"). Пользователь привык к тому, что синие слова на странице это [ссылки](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия"), даже если они не подчёркнуты. Если вам не нравится синий цвет для [ссылок](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия"), меняйте его, но тогда [ссылки](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия") подчёркивайте.



---------------------
`a:hover` — наведение
---------------------
```css
a:hover {
    text-decoration: underline;
}
```
Когда курсор находится над [ссылкой](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия"), она становится `:hover` и в данном примере приобретает подчёркивание. Так пользователь поймёт, что это *точно* [ссылка](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия"), на которую можно кликнуть.

----------------------------
`a:focus` — фокус клавиатуры
----------------------------
```css
a:focus {
    text-decoration: underline;
}
```
Когда на [ссылку](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия") устанавливается указатель, перемещаемый табулятором `TAB ↹`
она становится `:focus`. В 2016 году это может показаться странным, но есть люди которые работают с сайтам посредством клавиатуры. У некоторых вовсе сломана мышь. В любом случае, занулять `:focus` состояние — это преступление против таких людей.

Особые спецэфекты применять не обязательно, достаточно таких как у `:focus`.

CSS чтобы не писать дважды:
```css
a:focus, a:hover {
    text-decoration: underline;
}
```



-----------------
`a:active` — клик
-----------------
```css
a:active {
    color: #faa700;
}
```
Важное состояние `:active` происходит когда пользователь уже кликнул на [ссылку](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия"), но клавишу ещё не отпустил. Помогает пользователю понять, что его клик сработал, и ему не нужно кликать по ней несколько раз, чтобы точно перейти на нужную страницу.



---------------------------------------
`a:visited` — ранее посещённая страница
---------------------------------------
```css
a:visited {
    color: #0b0080;
}
```
>Можно все посмотреть‽

`:visited`, поможет пользователю не забыть какие странички он уже открывал и не открывать их повторно. Так вместе с `:active` и `:hover` мы чуточку разгрузим интернет от случайных загрузок, и сделаем его чуть лучше и быстре.

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

------------------

>В эпоху `HTML4` вместо кнопок использовались ссылки подчёрнутые
>пунктирной линией. Этот паттерн устарел.
>
>Подчёркивание пунктирной линией рекомендуется для тултипов
>при наведении. Например у `<abbr>` такое выделение поможет
>понять, что можно навести указатель и получить расшифровку.

------------------

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)


Пример нестандартного оформления ссылок:

![Пример на котором состояния ссылок оформленны нестандартно](https://slasher.ru/articles/link-or-button/a_example_not_standart_1.png)

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

>_Слова в ссылке должны подчиняться правилам русского языка, капс непозволителен (исключение — аббревиатуры)_










<a name="html5-buttonknopkabutton"></a>

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

## HTML5 `<button>Кнопка</button>`

* Если клик не меняет адрес страницы,
* адрес нельзя скопировать
* и нельзя этим адресом поделиться **— это кнопка**.

>В кнопке позволителен капс, при условии, что вы не используете аббревиатуры. Особенно в неочевидных местах.
Если у вас встречаются аббревиатуры, то верхний регистр в кнопке не желателен, выделяйте их другим способом. Не искушайте пользователей тапать по тому, что не тапается. У пользователей тачскрина нет возможности подсмотреть `:hover` или `:focus` состояние. Ну или есть, но происходит это всё не очень удобно, обычно уже после свершившегося тапа.


<a name='dostupnost'></a>

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

## Доступность

`<button />` может быть  недоступен на архаичных браузерах или устройствах. У кнопок не применятся стили без специальных JavaScript скриптов.
Но вас это не должно беспокоить. На таких устройствах часто и JavaScript не работает. И быть может CSS.
>Вообще если следовать идеологии что всё, что должно обрабатываться JavaScript'ом, должно добавляться JavaScript'ом, такой проблемы вовсе не возникнет.

>Что *JSΩ*, то *JSॐ*   ! Как говорится.


<a name='povedenie-vnutri-formy'></a>

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

### Поведение внутри формы

`<button>` по умолчанию имеет атрибут `type=submit` даже если его не прописать.

Ещё этот атрибут может принимать значения `reset` для сброса заполнения в форме
и `button` чтобы исключить влияние на форму. Правила хорошего тона предполагают,
что везде нужно писать `<button type="button">Кнопка</button>`.

Но на деле можно ограничится полной записью только внутри `<form></form>`,
`type=submit` в остальных местах ни на, что не влияет.

>Это кстати отличный сбособ для стилизации кнопки отправки формы.
>В отличии от `<input type="submit" value="Кнопка" />`, в содержимое
>`button`  можно писать любой HTML код, а не только текст.
>Например
>```html
><button>
>   <img src="/images/icon.svg" title="Красная таблетка" alt="Иконка" />
>   <span style="color: red;">Красный</span> <span style="color: blue;">Синий</span>
></button>
>```
>Это даёт даже больше свободы в стилевом оформлении чем `<input type="image" />`


<a name='sostoyaniya-1'></a>

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

### Состояния

Похожи на состояния у [ссылок](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия") за исключением того, что у кнопок нет состояния `:visited`, зато есть состояние `:disabled`.
Обычно дефолтное оформление браузера выпиливается основательно, иногда с нейтрализацией отображения состояний отличных от обычного.
_Да. Этот гайд для тебя, любитель превратить веб-страницу в бумажный аналог._

Стилей для этих штучек понадобится немного больше, но всё не так страшно. Кроме того ребята из Twitter и отчасти Google уже позаботились о реализации велосипеда.
Тёплый ламповый [Bootstrap](http://getbootstrap.com/css/#buttons) "и новомодный [MaterializeCSS](http://materializecss.com/buttons.html), например.




<a name='otobrazhenie'></a>

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

### Отображение

Так выглядит `<button>Кнопка</button>` в моём Chrome 54:
![отображение состояний кнопки](https://slasher.ru/articles/link-or-button/button_states.png)
На картинке `button`, `button:hover`, `button:focus`, `button:active` соответственно.

Без излишеств. Но учитывая движение Google в направлении *Material Design*, вполне может статься так, что в скором времени их заменят на [подобные аналоги](https://material.google.com/components/buttons.html "сайт презентация концепта Material Design от Google").

![Material Design кнопки серые стандартные](https://material-design.storage.googleapis.com/publish/material_v_9/0Bx4BSt6jniD7WlduMk1kbTRzQWc/components_buttons_main15.png)
![Material Design кнопки синие](https://material-design.storage.googleapis.com/publish/material_v_9/0Bx4BSt6jniD7UTh2dExpSlRVWVU/components_buttons_main16.png)




<a name='css'></a>

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

### CSS
_Для наглядности — мой вариант велосипеда который выглядит странновато, но для примера сойдёт._
![Состояния кнопки в порядке: обычное, наведение, клик, отключена](https://slasher.ru/articles/link-or-button/button_bicycle_states.png)
Обычная, наведение, клик, отключена соответственно.
----------------------------
`button` — обычное состояние
----------------------------
```css
button {
    background: none;
    outline: none;
    border: none;
    text-transform: uppercase;
}
```



----------------------------------------------
`button:hover`, `button:focus` — при наведении
----------------------------------------------
```css
button:hover, button:focus {
    color: hsla(108, 12%, 0%, 1);
    box-shadow: -1px 1px 2px hsla(108, 62%, 42%, 1);
    background-color: hsla(108, 62%, 92%, 1)
}
```



--------------------------------
`button:active` — в момент клика
--------------------------------
```css
button:active {
    color: hsla(108, 42%, 32%, 1);
    box-shadow: -2px 4px 8px hsla(64, 64%, 42%, 1);
    background-color: hsla(64, 64%, 92%, 1);
}
```


----------------------------
`button:disable` — отключена
----------------------------
```css
button:disabled {
    color: hsla(0, 0%, 64%, 1);
    background: none;
    box-shadow: none;
    opacity: 1;
}
```



<a name="primer-poslozhnee"></a>

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

### Пример посложнее

[Посмотреть в живую на JSFiddle](https://jsfiddle.net/j0vpbzsp/1)

![Кнопки которые похожи на настоящие](https://slasher.ru/articles/link-or-button/buttons_example_complicated.png?1)


<spoiler title="Показать CSS">

```css
button {
    margin: .8rem;
    font-size: 1.42rem;
    padding: 1rem;
    background: hsla(180, 90%, 64%, 1);
    color: hsla(180, 90%, 12%, 1);
    text-shadow: 1px 1px 1px hsla(180, 90%, 32%, 1);
    box-shadow: -4px 4px 0 0 hsla(180, 90%, 22%, .87), -3px 4px 3px hsla(180, 42%, 11%, 1), 1px 5px 4px hsla(180, 42%, 11%, 1), -4px 1px 0 0 hsla(180, 90%, 32%, 1), inset 0 0 1px 0 hsla(180, 90%, 90%, 1);
    border: 1px hsla(180, 92%, 56%, 1) solid;
    border-top-color: hsla(180, 92%, 64%, 1);
    border-radius: 5px;
    outline: none;
    position: relative;
    transition: all .22s ease-in;
}
button:hover {
    background: hsla(420, 90%, 42%, 1);
    color: hsla(420, 90%, 12%, 1);
    text-shadow: 1px 1px 1px hsla(420, 90%, 32%, 1);
    border: 1px hsla(420, 92%, 56%, 1) solid;
    border-top-color: hsla(420, 90%, 64%, 1);
    box-shadow: -4px 4px 0 0 hsla(420, 90%, 22%, .87), -3px 4px 3px hsla(420, 42%, 11%, 1), 1px 5px 4px hsla(420, 42%, 11%, 1), -4px 1px 0 0 hsla(420, 90%, 32%, 1), inset 0 0 1px 0 hsla(420, 90%, 90%, 1);
}
button:focus {
      background: hsla(108, 90%, 42%, 1);
      color: hsla(108, 90%, 12%, 1);
      text-shadow: 1px 1px 1px hsla(108, 90%, 32%, 1);
      border: 1px hsla(108, 92%, 56%, 1) solid;
      border-top-color: hsla(108, 90%, 64%, 1);
      box-shadow: -4px 4px 0 0 hsla(108, 90%, 22%, .87), -3px 4px 3px hsla(108, 42%, 11%, 1), 1px 5px 4px hsla(108, 42%, 11%, 1), -4px 1px 0 0 hsla(108, 90%, 32%, 1), inset 0 0 1px 0 hsla(108, 90%, 90%, 1);
  }
button:active {
    background: hsla(420, 90%, 42%, 1);
    color: hsla(420, 90%, 12%, 1);
    text-shadow: 1px 1px 1px hsla(420, 90%, 32%, 1);
    transform: translate(-4px, 4px);
    border: 1px hsla(420, 92%, 22%, 1) solid;
    border-top-color: hsla(420, 92%, 56%, 1);
    box-shadow: 0 0 0 0 hsla(420, 90%, 22%, .87), 0 0 0 hsla(420, 42%, 11%, 1), 0 0 0 hsla(420, 42%, 11%, 1), 0 0 0 0 hsla(420, 90%, 32%, 1), inset 1px 1px 4px 0 hsla(420, 90%, 22%, 1);
}
button:disabled {
    background: hsla(420, 0%, 64%, 1);
    color: hsla(180, 0%, 12%, 1);
    text-shadow: 1px 1px 1px hsla(180, 0%, 32%, 1);
    transform: translate(-4px, 4px);
    border: 1px hsla(420, 0%, 22%, 1) solid;
    border-top-color: hsla(420, 0%, 56%, 1);
    box-shadow: 0 0 0 0 hsla(420, 0%, 22%, .87), 0 0 0 hsla(420, 42%, 11%, 1), 0 0 0 hsla(420, 42%, 11%, 1), 0 0 0 0 hsla(420, 0%, 32%, 1), inset 1px 1px 4px 0 hsla(420, 0%, 22%, 1);

}
```

</spoiler>



<a name="dizayneru"></a>

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

## Дизайнеру

>Ты цээсэсов можешь и не знать, но состояния **отрисовать обязан**!

От дизайнера помимо макета с обычным состоянием [ссылки](https://ru.wikipedia.org/wiki/%D0%93%D0%B8%D0%BF%D0%B5%D1%80%D1%81%D1%81%D1%8B%D0%BB%D0%BA%D0%B0 "Гиперссылка — Википедия") или кнопки, требуется прилагать различные состояния, дабы не устраивать верстальщику батхерт.
Например так:
![текст с различными состояниями ссылки](https://slasher.ru/articles/link-or-button/link_sates_example.png)
![Состояния кнопки в порядке: обычное, наведение, клик, отключена](https://slasher.ru/articles/link-or-button/button_bicycle_states.png)

>Ребята из Google [сделали такой](https://material.google.com/components/buttons.html) макет.


<a name="spasibo"></a>

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

## Спасибо

Спасибо, что дочитали. Всё здесь написаннное не является 100% истиной в последней инстанции.
[Репозиторий ](https://github.com/KasperGreen/button-or-link-guide-ru)

<a name="github"></a>

![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

## GitHub

[Ссылка на репозиторий этой статьи](https://github.com/KasperGreen/button-or-link-guide-ru). Если хотите дополнить или исправить, присылайте пожалуйста `Pull Request`


![Разделитель](https://slasher.ru/articles/link-or-button/devider.png)

-----------------

![Процесс рисования](https://slasher.ru/articles/link-or-button/paint_process.jpg?1)