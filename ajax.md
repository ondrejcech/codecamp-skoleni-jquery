# jQuery - AJAX
* Základní kámen všech interaktivních JS aplikací
* Asynchronous Javascript And Xml
	* asynchroní znamená, že se nečeká na odpověd ze serveru, ale vykonávání hned pokračuje. Callback funkce se zavolá, až server odpoví
* běžně není možné posílat AJAXové požadavky na jinou doménu nebo protokol (http:// vs https://)
* Spíše než XML se používá JSON nebo je v odpovědi rovnou vyrenderované HTML, které se vloží do stránky
* v JS se o něj stará XMLHttpRequest
* S jeho pomocí můžeme udělat request na backend a updatovat jenom část stránky bez nutnosti jejího celého načtení
* První s ním přišel MS (Jeeeej)

## jQuery metody pro práci s AJAXem

$.ajax() - základní metoda


$.get() - Provede GET požadavek na server
```js
$.ajax('/get-products', {offset: 1}, function (response) {
	// do something with response
});
```

$.post() - Provede POST požadavek na server - http://jsfiddle.net/ondrejcech/mw0kvp7b/
```js
$.ajax('/get-products', {offset: 1}, function (response) {
	// do something with response
});
```

$.getJSON() - Provede GET požadavek a vrátí JSON odpověď ze serveru
```js
$.getJSON('/get-products', {offset: 1}, function (response) {
	// do something with response
});
```

callback metody pro různé výsledky dotazu
```js
$.getJSON('/get-products', {offset: 1}, function (response) {
	// do something with response
}).fail(function () {
	// handle erro response
}).always(function () {
	// called on both success and error
});
```

* [Získání HTTP hlaviček odpovědi](http://jsfiddle.net/ondrejcech/b409znaj/)

JSONP - možnost, jak pomocí SCRIPT tagu volat požadavek z jiné domény