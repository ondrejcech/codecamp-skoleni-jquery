# jQuery - eventy
* Základní stavební kámen každé JS aplikace
* Uvedeny v Netscape Navigator 2 - první použití pro hover efekt a client side validaci formulářů
* [Seznam eventů](https://developer.mozilla.org/en-US/docs/Web/Events)
* V dnešní době eventy snad na úplně všechno
* Pro pohodlnou práci s touch eventy se hodí třeba [hammer.js](http://hammerjs.github.io/) (nebo [jQueryMobile](https://jquerymobile.com/))

## Registrace eventů

V HTML šabloně **to nechceš**:

```js
<a href="somewhere.html" onclick="alert('I\'ve been clicked!')"></a>
```

Ve scriptu:

```js
$(‘a’).on(‘click’, function () {
	alert('I\'ve been clicked!'');
});
```

Pomoci onevent vlastnosti:

```js
element.onclick = doSomething;
```

Historicky problém s kompatibilitou MS a W3C specifikace (jQuery to řeší za vás)

* Microsoft

```js
element.attachEvent('onclick', doSomething)
```

* W3C

```js
element.addEventListener('click',doSomething,false);
```

## Event order 

Capturing phase (Netscape):

	               | |
	---------------| |-----------------
	| element1     | |                |
	|   -----------| |-----------     |
	|   |element2  \ /          |     |
	|   -------------------------     |
	|        Event CAPTURING          |
	-----------------------------------


Bubling phase (Microsoft):

	               / \
	---------------| |-----------------
	| element1     | |                |
	|   -----------| |-----------     |
	|   |element2  | |          |     |
	|   -------------------------     |
	|        Event BUBBLING           |
	-----------------------------------


W3C model:

	                 | |  / \
	-----------------| |--| |-----------------
	| element1       | |  | |                |
	|   -------------| |--| |-----------     |
	|   |element2    \ /  | |          |     |
	|   --------------------------------     |
	|        W3C event model                 |
	------------------------------------------


```js
element1.addEventListener('click', doSomething2, true /* capturing phase */)
element2.addEventListener('click', doSomething, false /* bubbling phase */)
```

**jQuery používá bubbling phase**

## Event object
```js
$(‘a’).on(‘click’, function (e) {
	// e = Event object
	console.log(e.target);
});```

* e.stopPropagation() - přeruší bublání eventu výš [Příklad](http://jsfiddle.net/ondrejcech/8dj7ns89/)

* e.preventDefault() - zruší defaultní akci (odkazu, formuláře, checkboxu) [Příklad](http://jsfiddle.net/ondrejcech/spgzebxn/)

e.stopImmediatePropagation() - přeruší bublání eventu výš a přeruší vykonávání dalších handlerů [Příklad](http://jsfiddle.net/ondrejcech/1dks7yte/1/)

**! return false v event handleru je anti-pattern !**, protože volá jak e.stopPropagation() tak e.preventDefault() a přeruší vykonávání handleru.

```js
$("div a").click(function (e) {
   // Do something else
   return false;
});

$("div").click(function (e) {
   // won't be called
});
```
