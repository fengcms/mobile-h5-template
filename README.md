# 移动端自适应不同手机基础模板

## 主要代码

```js
function set_html_fontsize() {
  var h = Math.max(document.documentElement.clientHeight, window.innerHeight || 0);
  var w = Math.max(document.documentElement.clientWidth, window.innerWidth || 0);
  var width = w > h ? h : w;
  width = width > 720 ? 720 : width
  document.getElementsByTagName("html")[0].style.cssText = 'font-size: ' + ~~(width*100000/36)/10000+"px;";
}
window.orientationchange = function(){set_html_fontsize()};
window.onresize = function(){set_html_fontsize()};
set_html_fontsize();
```
以上代码的作用是获取屏幕的宽和高，取小值为基准，如果小值大于720,则以720为基准，设置网页的`html`元素的`font-size`值。默认安卓手机为`100px`。

然后在代码中可以用`rem`为单位，让所有元素的尺寸都基于`html`元素的`font-size`来进行计算。

对于换算`rem`值也颇为头疼，所以增加了一个`sass`函数
```sass
@function rem($px){
  @return $px / 100 + rem;
}
```
这样，我们就可以拿px值来进行使用了。比如，我想设置某元素的某参数为`12px`，则可以写`rem(12)`

为了便于布局，在`index.html`中增加了一个类`body`的`div`元素，其`class`为`.funleo_mobile_frame`，然后，赋予了其如下的`css`

```css
.funleo_mobile_frame {
  max-width: 720px;width: 100%;margin: 0 auto; position: relative;
  background: $cff;min-height: 100%;
  box-shadow: 0 0 0 rem(10) $cff;
}
```
这样可以让网页在PC浏览器上整体居中。
