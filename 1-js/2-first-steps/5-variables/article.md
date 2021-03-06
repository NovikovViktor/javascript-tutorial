# Переменные

В зависимости от того, для чего вы делаете скрипт, понадобится работать с информацией.

Если это электронный магазин -- то это товары, корзина. Если чат -- посетители, сообщения и так далее.

Чтобы хранить информацию, используются *переменные*.
[cut]
## Переменная

*Переменная* состоит из имени и выделенной области памяти, которая ему соответствует.

Для *объявления* или, другими словами, *создания переменной* используется ключевое слово `var`:

```js
var message;
```

После объявления, можно записать в переменную данные:

```js
var message;
message = 'Hello'; // сохраним в переменной строку
```

Эти данные будут сохранены в соответствующей области памяти и в дальнейшем доступны при обращении по имени:

```js
//+ run
var message;
message = 'Hello!';

alert( message ); // выведет содержимое переменной
```

Для краткости можно совместить объявление переменной и запись данных:

```js
var message = 'Hello!';
```

Можно даже объявить несколько переменных сразу:

```js
//+ no-beautify
var user = 'John', age = 25, message = 'Hello';
```

### Аналогия из жизни

Проще всего понять переменную, если представить ее как "коробку" для данных, с уникальным именем. 

Например, переменная `message` -- это коробка, в которой хранится значение `"Hello!"`:

<img src="variable.png"> 

В коробку можно положить любое значение, а позже - поменять его. Значение в переменной можно изменять сколько угодно раз:

```js
//+ run
var message;

message = 'Hello!';

message = 'World!'; // заменили значение

alert( message );
```

При изменении значения старое содержимое переменной удаляется.

<img src="variable-change.png">

Можно объявить две переменные и копировать данные из одной в другую:

```js
//+ run
var hello = 'Hello world!';

var message;

*!*
// скопировали значение
message = hello;
*/!*

alert( hello ); // Hello world!
alert( message ); // Hello world!
```

[smart]
Существуют [функциональные](http://ru.wikipedia.org/wiki/%D0%AF%D0%B7%D1%8B%D0%BA_%D1%84%D1%83%D0%BD%D0%BA%D1%86%D0%B8%D0%BE%D0%BD%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D0%B3%D0%BE_%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F) языки программирования, в которых значение переменной менять нельзя. Например, [Scala](http://www.scala-lang.org/) или [Erlang](http://www.erlang.org/).

В таких языках положил один раз значение в коробку -- и оно хранится там вечно, ни удалить ни изменить. А нужно что-то другое сохранить -- изволь создать новую коробку (объявить новую переменную), повторное использование невозможно.

С виду -- не очень удобно, но, как ни странно, и на таких языках вполне можно  успешно программировать. Более того, оказывается, что в ряде областей, например в распараллеливании вычислений, они имеют преимущества. Изучение какого-нибудь функционального языка рекомендуется для расширения кругозора.
[/smart]

## Имена переменных [#variable-naming]

На имя переменной в JavaScript наложены всего два ограничения. 
<ol>
<li>Имя может состоять из: букв, цифр, символов `$` и `_`</li>
<li>Первый символ не должен быть цифрой.</li>
</ol>

Например:

```js
var myName;
var test123;
```

**Что особенно интересно -- доллар `'$'` и знак подчеркивания `'_'` являются такими же обычными символами, как буквы:**

```js
//+ run untrusted
var $ = 1; // объявили переменную с именем '$'
var _ = 2; // переменная с именем '_'

alert( $ + _ ); // 3
```

А такие переменные были бы неправильными:

```js
//+ no-beautify
var 1a; // начало не может быть цифрой

var my-name; // дефис '-' не является разрешенным символом
```

[smart header="Регистр букв имеет значение"]
Переменные `apple` и `AppLE` - две разные переменные. 
[/smart]

[smart header="Русские буквы допустимы, но не рекомендуются"]

В названии переменных можно использовать и русские буквы, например:

```js
//+ run
var имя = "Вася";
alert( имя ); // "Вася"
```

Технически, ошибки здесь нет, но на практике сложилась традиция использовать в именах только английские буквы.
[/smart]

[warn header="Зарезервированные имена"]

Существует список зарезервированных слов, которые нельзя использовать для переменных, так как они используются самим языком, например: `var, class, return, export` и др.

Например, такой пример выдаст синтаксическую ошибку:

```js
//+ run no-beautify
var return = 5; // ошибка
alert(return);
```

[/warn]


## Важность директивы var

В старом стандарте JavaScript разрешалось создавать переменную и без `var`, просто присвоив ей значение:

```js
num = 5; // переменная num будет создана, если ее не было
```

В режиме `"use strict"` так делать уже нельзя.

Следующий код выдаст ошибку:

```js
//+ run
"use strict";

*!*
num = 5; // error: num is not defined
*/!*
```

Обратим внимание, директиву `use strict` нужно ставить до кода, иначе она не сработает:

```js
//+ run
var something;

"use strict"; // слишком поздно

*!*
num = 5; // ошибки не будет, так как строгий режим не активирован
*/!*
```

[warn header="Ошибка в IE8- без `var`"]
Если же вы собираетесь поддерживать IE8-, то у меня для вас ещё одна причина всегда использовать `var`. 

Следущий документ в IE8- ничего не выведет, будет ошибка:

```html
<div id="test"></div>
<script>
*!*
  test = 5; // здесь будет ошибка!
*/!*
  alert( test ); // не сработает
</script>
```

Это потому, что переменная `test` не объявлена через `var` и совпадает с `id` элемента `<div>`. Даже не спрашивайте почему -- это ошибка в браузере IE до версии 9.

Самое "забавное" -- то, что такая ошибка присвоения значений будет только в IE8- и только если на странице присутствует элемент с совпадающим с именем `id`. 

Такие ошибки особенно "весело" исправлять и отлаживать.

Вывод простой -- всегда объявляем переменные через `var`, и сюрпризов не будет. Даже в старых IE.
[/warn]

## Константы

*Константа* -- это переменная, которая никогда не меняется. Как правило, их называют большими буквами, через подчёркивание. Например:

```js
//+ run
var COLOR_RED = "#F00";
var COLOR_GREEN = "#0F0";
var COLOR_BLUE = "#00F";
var COLOR_ORANGE = "#FF7F00";

var color = COLOR_ORANGE;
alert( color ); // #FF7F00
```

Технически, константа является обычной переменной, то есть её *можно* изменить. Но мы *договариваемся* этого не делать.

Зачем нужны константы? Почему бы просто не писать `var color = "#FF7F00"`?

<ol>
<li>Во-первых, константа `COLOR_ORANGE` -- это понятное имя. По присвоению `var color="#FF7F00"` непонятно, что цвет -- оранжевый. Иными словами, константа `COLOR_ORANGE` является "понятным псевдонимом" для значения `#FF7F00`.</li>
<li>Во-вторых, опечатка в строке, особенно такой сложной как `#FF7F00`, может быть не замечена, а в имени константы её допустить куда сложнее.</li>
</ol>

**Константы используют вместо строк и цифр, чтобы сделать программу понятнее и избежать ошибок.**

## Итого

<ul>
<li>В JavaScript можно объявлять переменные для хранения данных. Это делается при помощи `var`.</li>
<li>Технически, можно просто записать значение и без объявления переменной, однако по ряду причин это не рекомендуется.</li>
<li>Вместе с объявлением можно сразу присвоить значение: `var x = 10`.</li>
<li>Переменные, которые названы `БОЛЬШИМИ_БУКВАМИ`, являются константами, то есть никогда не меняются. Как правило, они используются для удобства, чтобы было меньше ошибок.</li>
</ul>



