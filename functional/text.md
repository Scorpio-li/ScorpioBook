
## 1.高亮文本和取消高亮

```js
/*
参数：
  text：选中的文本标签内容
  words：需要高亮的词
  tag：自定义高亮的样式
*/
function highlight(text, words, tag) {

  // Default tag if no tag is provided
  tag = tag || 'span';

  var i, len = words.length, re;
  for (i = 0; i < len; i++) {
    // Global regex to highlight all matches
    re = new RegExp(words[i], 'g');
    if (re.test(text)) {
      text = text.replace(re, '<'+ tag +' class="highlight">$&</'+ tag +'>');
    }
  }

  return text;
}

function unhighlight(text, tag) {
  // Default tag if no tag is provided
  tag = tag || 'span';
  var re = new RegExp('(<'+ tag +'.+?>|<\/'+ tag +'>)', 'g');
  return text.replace(re, '');
}

// 使用方法：
// $('p').html( highlight(
//     $('p').html(), // the text
//     ['foo', 'bar', 'baz', 'hello world'], // list of words or phrases to highlight
//     'strong' // custom tag
// ));

```



## 2.文字动效：需要结合一个CSS3 transition样式来达到更好的效果。

```js
$.fn.animateText = function(delay, klass) {
  
  var text = this.text();
  var letters = text.split('');
  
  return this.each(function(){
    var $this = $(this);
    $this.html(text.replace(/./g, '<span class="letter">$&</span>'));
    $this.find('span.letter').each(function(i, el){
      setTimeout(function(){ $(el).addClass(klass); }, delay * i);
    });
  });
  
};


//$('p').animateText(150, 'foo');
```

## 3. 逐个显示隐藏元素

```js
$.fn.fadeAll = function (ops) {
  var o = $.extend({
    delay: 500, // delay between elements
    speed: 500, // animation speed
    ease: 'swing' // other require easing plugin
  }, ops);
  var $el = this;
  console.log($el,$el.length);
  for (var i=0, d=0, l=$el.length; i<l; i++, d+=o.delay) {
    $el.eq(i).delay(d).fadeIn(o.speed, o.ease);
  }
  return $el;
}

//$('li').fadeAll({ delay: 300, speed: 300 });
```

## 4. 全局计数:记录用户在当前页面上点击某一个按钮的次数

```js
$('button')
    .data('counter', 0) // begin counter at zero
    .click(function() {
        var counter = $(this).data('counter'); // get
        console.log(counter);
        $(this).data('counter', counter + 1); // set
        // do something else...
    });

//创建动态菜单或下拉列表
function makeMenu(items, tags) {
 
  tags = tags || ['ul', 'li']; // default tags
  var parent = tags[0];
  var child = tags[1];
 
  var item, value = '';
  for (var i = 0, l = items.length; i < l; i++) {
    item = items[i];
    // Separate item and value if value is present
    if (/:/.test(item)) {
      item = items[i].split(':')[0];
      value = items[i].split(':')[1];
    }
    // Wrap the item in tag
    items[i] = '<'+ child +' '+
      (value && 'value="'+value+'"') +'>'+ // add value if present
        item +'</'+ child +'>';
  }
 
  return '<'+ parent +'>'+ items.join('') +'</'+ parent +'>';
}

// Dropdown select month
var str = makeMenu(
  ['January:JAN', 'February:FEB', 'March:MAR'], // item:value
  ['select', 'option']
);
$('body').append(str);
 
// List of groceries
var str2 = makeMenu(
  ['Carrots', 'Lettuce', 'Tomatos', 'Milk'],
  ['ol', 'li']
);
$('body').append(str2);
```

