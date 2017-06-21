# Material Colors Sass Variables

Just include `_material-colors.sass` into your file and you are ready to go.

All colors are available as sass variables. For example, **Red 500** is **`$red-500`** and **Light Green A400** is **`$light-green-A400`**. But I didn't include black and white variables. For those I prefer using just color keywords.

I didn't copied and pasted those colors manually. I used some javascript code in page's console to parse colors and just output them. *I would like to avoid explaining it*.

> **Link to material colors:**

> https://material.io/guidelines/style/color.html#color-color-palette

### Below is the code for that link
*(Sorry, if you see it as a mess... I used that code mostly as an ES6 spread array thing)*
```
var groups = document.querySelectorAll('.color-group');

var colors = [].map.call(groups, (group) => {
  return group.querySelectorAll('.color');
});

colors = colors.map( el => { 
  return [].concat(...el) 
});

var maps = [].concat(...colors.map( arr => {
  let color = undefined;
  let obj = {};
  arr.forEach( el => {
    if (!!el.querySelector('.name'))
		color = el.querySelector('.name').textContent.replace(' ', '-').toLowerCase();
  });
  obj[color] = arr;
  return [obj];
}));

maps.pop();

maps = maps.map( el => {
  let key = Object.keys(el)[0];
  let arr = el[key];
  arr.shift();
  arr = arr.map( li => {
    return [
		'$', 
		key, 
		'-', 
		li.querySelector('.shade').textContent, 
		': ', 
		li.querySelector('.hex').textContent
	].join('');
  });
  return arr;
});

var output = [].concat(...maps).join('\n');

console.log(output);
```
