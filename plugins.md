# jQuery - Pluginy
* základní způsob rozšíření jQuery
* pluginy na úplně všechno (https://plugins.jquery.com/)
* o všech metodách můžete uvažovat jako o pluginech .ajax(), .css()
* plugin vytvoříte přidáním metody do $.fn

```js
(function ($) {
	$.fn.mysupercoolplugin = function () {
	    this.css( "color", "green" );
	    // return this for fluent interface
	    return this;
	}
}(jQuery));

$("a").mysupercoolplugin().addClass("some-new-class");
```
* přidat příklad na each() - zavoláno na kolekci
* vytvořte plugin, který funguje na kolekci (vymyslet)
* vyzkoušet použití fancyboxu