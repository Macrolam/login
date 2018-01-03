# login
# 简介：
这是一个登录模块，采用原生表单的形式提交，当然你也可以把表单默认行为取消，采用异步的ajax提交。采用的都是纯原生的形式，html采用的第五代超文本标记语言即：H5;样式采用CSS3;js部分基本都采用的是ES5,没有使用JQuery，全篇只有一处采用ES6语法（let）：for>事件,解决ES5需要借助闭包才能实现的效果。
# 相关资料说明：
## 表单验证分类：
1、必填性：可以利用原生的表单元素的自身属性，required ;当采用表单原生的提交（非Ajax 异步请求（js方式提交））方式时，可以调起内部的校验，不合法会有弹窗提示："请填写此字段"。这个是HTML5中新增的。
![案例.png](http://upload-images.jianshu.io/upload_images/3233350-a00b7445afb25501.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
点击submit按钮时候，表单内必填字段处会有提示。
2、长度限制：利用原生自带的maxlength="数字"，minlength="数字"
3、规定的类型：写正则过滤，对应错误提示代码。
4、逻辑校验：自己写js代码。（第一个数值要小于后一个数值-时间段的选择等问题上）
## 原生表单的形式：
```
form(action method)>input[*]+input[submit]
每一个都是必要的，最外层必须由form 标签包裹，内部必须由类型是submit的输入框。
```
## 一些定制demo
##### 1.修改必填性不合法时候的提示文字
核心代码：
```
oninvalid="setCustomValidity('请输入您的姓名');" oninput="setCustomValidity('');"
```

完整代码：
```
 <input type="text" id="username" required oninvalid="setCustomValidity('请输入您的姓名');" oninput="setCustomValidity('');" >
```
![demo.png](http://upload-images.jianshu.io/upload_images/3233350-6b41c330f7fd518e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 2.阻止form表单点击提交按钮时自动提交
```
$("input:submit").click(function(e){
     e = e||window.event;
    e.preventDefault();    //阻止默认行为
})

或是：
    form表单.onsubmit = function () {
        return false
    }
```
验证是否生效：
填写好合法的字段，点击提交，浏览器的刷新按钮不动（表单提交时同步行为，肯定会刷新页面），说明ok了，或是给action一个提交的后台地址，这里可以给百度的试试，点击提交，不跳转百度，说明ok。
![刷新按钮.png](http://upload-images.jianshu.io/upload_images/3233350-8f6e6fa8592a3a89.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 3.定制required字段不符时的提示框的样式。
对于这个H5的新功能，貌似只能修改文字。不同浏览器的渲染样式是不一样的（浏览器程序中定制了提示框的API）

）。
##### 4.定制required字段不符时的输入框的样式。
```
html:
<input type="text" name="name" required>
css:
/* 无效 */
input:required:invalid{
    CSS代码
}
/* 有效 */
input:required:valid{
    CSS代码
}
```
##### 5.占位符的样式定制
```
 input::placeholder {
            color: #DDDDDD;
            font-size: 16px;
            letter-spacing: 1px;
        }

        /*placeholder兼容处理*/
 input::-webkit-input-placeholder {
            color: #DDDDDD;
            font-size: 16px;
            letter-spacing: 1px;
        }
 input:-ms-input-placeholder {
            color: #DDDDDD;
            font-size: 16px;
            letter-spacing: 1px;
        }
```

# 其他
submit和button提交表单的区别
input 的type 类型分别为submit和button时候放在form标签里的区别：
1.  <input type="button" />单纯的一个按钮。没有默认行为，不写js脚本的话，按下去什么反应也没有。

2.  <input type="submit" /> 有默认行为，点击会提交 form，除非写了js阻止它。(<form onsubmit="return false;"> )

3.  <button> 标签，这个按钮放在 form 中也会点击自动提交，比前两个的优点是样式好定制些。缺点可能有浏览器兼容问题。


# 参考文章：
1：http://www.the-art-of-web.com/html/html5-form-validation/
