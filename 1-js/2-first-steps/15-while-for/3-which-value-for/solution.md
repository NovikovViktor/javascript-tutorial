**Ответ: от 0 до 4 в обоих случаях.**

```js
//+ run
for (var i = 0; i < 5; ++i) alert( i );

for (var i = 0; i < 5; i++) alert( i );
```

Такой результат обусловлен алгоритмом работы `for`:
<ol>
<li>Выполнить присвоение `i=0`</li>
<li>Проверить `i<5`</li>
<li>Если верно - выполнить тело цикла `alert(i)`, затем выполнить `i++`</li>
</ol>

Увеличение `i++` выполняется отдельно от проверки условия (2), значение `i` при этом не используется, поэтому нет никакой разницы между `i++` и `++i`.