# jQuery - bad practices

Využívejte fluent interface (přístup do DOMu je náročný)

```js
$('div ul li').show();
$('div ul li').addClass('.active');

// vs.
$('div ul li').show().addClass('.active')

// or
var $elements = $('div ul li');
$elements.show();
$elements.addClass('.active')
```

Nechápete, jak jQuery funguje

```js
$("a").each(function(){
   $(this).css("color", "red");
});

// vs.

$("a").css("color", "red");
```

Využívejte event bubling

```js
$('li').each(function () {
	$(this).click(function () {
		// do some stuff with list item
	})
})

// vs.

$('ul').on('click', 'li', function () {
	// do some stuff with list item - works event for future list items
});
```

Nepoužívejte .data() pokud chcete pracovat s data-atributy - používejte .attr('data-') [Příklad](http://jsfiddle.net/ondrejcech/u44hfmck/)

```js
<span data-field="old-value"></span>

var $span = $('span');

$span.data('field', 'new-value');

console.log($span.data('field')); // new-value
console.log($span.attr('data-field')); // old-value (WTF?!)
console.log($span[0].getAttribute('data-field')); // old-value (WTF?!)

```