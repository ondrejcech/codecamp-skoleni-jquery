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

vs.

$("a").css("color", "red");
```