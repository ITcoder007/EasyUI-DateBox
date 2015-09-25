Easyui datebox单击文本框显示日期选择
============

Easyui默认是点击文本框后面的图标显示日期，为了更进一步优化体验

修改为单击文本框显示日期选择框

![image](https://raw.githubusercontent.com/itmyhome2013/datebox/master/20150527212808829.png)

修改jquery.easyui.min.js(作者用的是**1.3.6**版本,其他版本或有区别)

可 ctrl+f 搜索 "**_outerWidth():0**" 在本行下面添加如下代码：

```js
// datebox单击文本框出现日期选择 start  
if ($(_83f).hasClass("datebox-f")) {  
    _844.click(function() {  
        _845.click();  
    });  
}  
// end 
```

上下文代码如下：

```js
function _83e(_83f,_840){  
var _841=$.data(_83f,"combo");  
var opts=_841.options;  
var _842=_841.combo;  
var _843=_841.panel;  
if(_840){  
opts.width=_840;  
}  
if(isNaN(opts.width)){  
var c=$(_83f).clone();  
c.css("visibility","hidden");  
c.appendTo("body");  
opts.width=c.outerWidth();  
c.remove();  
}  
_842.appendTo("body");  
var _844=_842.find("input.combo-text");  
var _845=_842.find(".combo-arrow");  
var _846=opts.hasDownArrow?_845._outerWidth():0;  
  
// datebox单击文本框出现日期选择 start  
if ($(_83f).hasClass("datebox-f")) {  
    _844.click(function() {  
        _845.click();  
    });  
}  
// end  
  
_842._outerWidth(opts.width)._outerHeight(opts.height);  
_844._outerWidth(_842.width()-_846);  
_844.css({height:_842.height()+"px",lineHeight:_842.height()+"px"});  
_845._outerHeight(_842.height());  
_843.panel("resize",{width:(opts.panelWidth?opts.panelWidth:_842.outerWidth()),height:opts.panelHeight});  
_842.insertAfter(_83f);  
}; 
```

效果演示: <a href="http://itmyhome.com/datebox/" target="_blank">点击</a>