<h2>记录学习Vue之路</h2>

B站尚硅谷在线学习视频链接: 
[尚硅谷Vue2.0+Vue3.0全套教程丨vuejs从入门到精通](
https://www.bilibili.com/video/BV1Zy4y1K7SH/?p=6&spm_id_from=pageDriver&vd_source=0aba82a4002c00e3a072b82df5f53868)

<h4>第一章: 初识 Vue</h4>

```
1.想让vue工作，就必须创建一个vue实例，且要传入一个配置对象;
2.root容器里的代码依然符合html规范，只不过混入了一些特殊的vue语法;
3.root容器里的代码被称为【vue 模板】;
4.Vue实例和容器是一一对应的； 
5.真实开发中只有一个Vue实例，并且会配合着组件一起使用； 
6.{{xxx}}中的xxx要写js表达式，且xxx可以自动读取到 data中的所有属性； 
7.一旦 data 中的数据发生改变，那么页面中用到该数据的地方也会自动更新；

注意区分：js表达式和js代码（语句） 
  1.表达式:一个表达式会产生一个值，可以放在任何一个需要值的地方：
    (1).a
    (2).a+b
    (3).demo (1)
    (4).x===y?'a':'b'
  2.js 代码（语句）
    (1).if(){}
    (2).for(){}
```

<h4>第二章: Vue模板语法有2大类</h4>

```
1.插值语法：
功能:用于解析标签体内容。
写法:{{xxx}}了，xxx 是 js 表达式，且可以直接读取到 data 中的所有属性。 

2.指今语法：
功能:用于解析标签（包括：标签属性、标签体内容、绑定事件.....）
举例:v-bind:href="xxx” 或 简写为 :href="xxx”，xxx 同样要写 js 表达式，且可以直接读取到 data 中的所有属性。

备注:vue 中有很多的指今，且形式都是：v-????，此处我们具体拿 v-bind 举个例子。
```

<h4>第三章: Vue中有2种数据绑定的方式</h4>

```
1.单向绑定(v-bind)：数据只能从 data 流向页面 
2.双向绑定(v-model)：数据不仅能从 data 流向页面，还可以从页面流向 data。

备注： 
1.双向绑定一般都应用在表单类元素上（如：input、select 等）
2.v-model:value可以简写为v-model，因为v-model默认收集的就是value值。
```

<h4>第四章: data与el的2种写法</h4>

```
1.e1有2种写法
  a.new vue时候配置el属性。
  b.先创建vue实例，随后再通过vm.$mount（’#root’)指定e1的值。

2.data有2种写法
  a.对象式
  b.函数式
  如何选择：目前哪种写法都可以，以后学习到组件时，data必须使用函数式，否则会报错。

3.一个重要的原则：
  由vue管理的函数,一定不要写箭头函数，一旦写了箭头函数，this就不再是vue实例了。
```

<h4>第五章: MVVM模型</h4>

```
1. M：模型(Model): data中的数据
2. V: 视图(View) : 模版代码
3. VM：视图模型 (ViewModel)：vue实例
观察发现：
  1.data中所有的属性，最后都出现在了vm身上，
  2.vm身上所有的属性及vue原型上所有属性，在vue模板中都可以直接使用。
```

<h4>第六章: 数据代理</h4>

一、通过举例的方式回顾Object.defineProperty方法

```
let number = 18;
    let person = {
      name: "王五",
      sex: "男",
      // age:"18"
    };

    Object.defineProperty(person, "age", {
      // 基本属性
      // value: "18",
      // enumerable: true, //控制属性是否可以枚举，默认值是false
      // writable: true, //控制属性是否可以被修改，默认值是false
      // configurable: true, //控制属性是否可以被删除，默认值是false

      // 高级属性
      // 当有人读取person的age属性时，get两数(getter)就会被调用，且返回值就是age的值
      get() {
        console.log("有人读取了age属性");
        return number;
      },

      //当有人修改person的age属性时，set两数(setter）就会被调用，且会收到修改的具体值
      set(value) {
        console.log("有人修改了age属性,且值为", value);
        number = value;
      },
    });

    console.log(person);
```

二、何为数据代理:通过一个对象代理对另一个对象中属性的操作(读/写)
```
let obj = { x: 100 };
let obj2 = { y: 200 };
Object.defineProperty(obj2, "x", {
  get() {
    return obj.x;
  },
  set(value) {
    obj.x = value;
  },
});
```

三、vue中数据代理
```
1.Vue中的数据代理：
  通过vm对象来代理data对象中属性的操作（读/写）
2.Vue中数据代理的好处：
  更加方便的操作data中的数据
3.基本原理：
  通过object.defineProperty()把data对象中所有属性添加到vm上。
  为每一个添加到vm上的属性，都指定一个getter/setter。
  在getter/setter内部去操作（读/写）data中对应的属性。  
```
![数据代理图示](https://github.com/KennyHito/StudyVue/blob/main/img/%E6%95%B0%E6%8D%AE%E4%BB%A3%E7%90%86%E5%9B%BE%E7%A4%BA.png)