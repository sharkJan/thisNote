一、this指向在函数定义的时候是确定不了的，只有在函数执行时才能确定this到底指向谁，实际上this最终指向的是最后调用它的对象。

1.demo1
``
function a(){
    var user="shark Jan";
    console.log(this.user);
    console.log(this);
    }
    a();
``    
##window是js中的全局对象，在以上例子中，函数a是被window调用的，所以this指向了window.
由于window没有user这个变量，所以this.user打印的结果是undefined；
但是犹豫this指向了window，所以this的打印结构是window.

2.demo2
``
var o={
  user:"shark Jan",
fn:function(){
  console.log(this.user);     //shark Jan
}
}
o.fn();
``
这个例子中，由于fn函数是被o对象调用的，所以fn中的this指向了o对象。所以打印结果是"shark Jan";

3.
demo3
``
var o={
   user:"shark Jan",
   fn:function(){      
   console.log(this.user);      //undefined
   }
}
window.o.fn();
``
##看了上面的例子，按照上面的理论，我们很容易会想到打印undefined;因为window作为全局对象调用了fn，this应该指向window,但是window中并没有user这个属性，所以会返回undefined.
但是这里并非如此，打印结果是"shark Jan"
为了搞清楚这个问题我们再看一个实例
demo4
  ``
var  o={
  a:10,
  b: {
    a: 12,
    fn: function () {
      console.log(this.a);     //12
    }
  }
  };
  o.b.fn();
``  
  这个例子中fn同样是o调用的，但是this并没有指向o,它打印的结果是12.
  这是为什么呢？
##a.如果一个函数中有this，但是它没有被上一级对象调用，那么this指向的就是window（这里暂时不探讨严格版js）。
##b.如果一个函数中有this，同时又被上一级对象调用，那么this指向的是上一级对象。
##如果一个函数中有this，同时又包括多个对象，那么尽管函数是被最外层对象调用，this仍然会指向上一层调用它的对象。
这里插一点，对象不能隔代调用。比如
demo5
``
var  o={
  a:10,
  b: {
    a: 12,
    c:{
      a:13,
      fn: function () {
        console.log(this.a);   //13
      }
    }
  }
  };

  o.b.c.fn();    //13
  o.c.fn();       //报错
``  
  在这里由于o与c之间间隔一个对象b，所以无法打印this指向。
  
  

4.还有一种情况比较特殊，例如
demo6
``
var o={
    a:10,
    b:{
    a:12,
        fn:function(){
            console.log(this.a);      //undefined
            console.log(this);         //window
        }
      }
    }
    var j=o.b.fn;
    j();
    j();
``
    看了上面的实例，你想出的结果可能是12，12，因为这里this应该指向的是上一级对象b呀。
    但是事实并非如此，你还没有理解一句话，this永远指向的是最后调用它的对象，也就是在函数执行时，是谁调用的？
    这里var j=o.b.fn，实际上只是定义了j变量，并没有执行j，所以this指向无法判断，但是后面的j(),执行了j变量，也就调用了fn(),但是这里执行j()的其实是window,所以this实际上指向了window.
    window中并没有a属性,所以this.a指向了undefined,this指向window.
    
    二、构造函数中的this指向
  demo
  ``
    function Fn(){
        this.user="shark Jan"
     }
     var a= new Fn();
      console.log(a.user);   //shark Jan
``
      上面实例中a可以点出Fn里的user,是因为new关键字可以改变this指向。
      这里的new创造了一个构造函数，构造函数的作用就是初始化对象，又使用变量a创建了一个Fn的实例，就相当于复制了一份Fn到对象里，这里的this就指向里新创建出来的a.
      
    三、当this碰到return时，
    ``
    demo1
    function fn(){
    this.user="shark Jan";
    return function(){};
  }
  var a= new fn;
  console.log(a.user);   //undefined
  
  demo2
 function fn(){
    this.user="shark Jan";
    return {};
  }
  var a= new fn;
  console.log(a.user);      //undefined
   
 demo3
    function fn(){
    this.user="shark Jan";
    return 1;
  }
  var a= new fn;
  console.log(a.user);    //"shark Jan"
``

##通过以上实例可以发现，当返回值是一个对象时，this指向的就是那个返回值的对象，但是当返回值不是一个对象时，那么this仍然指向函数的实例。   

##补充说明：
1.在事件中，this指向触发事件的对象，但是比较特殊的是，在IE中attachEvent中的this总是指向全局对象window。

2.严格版javascript中，默认的this不再指向window，而是指向undefined.

3.new操作符的作用
demo
``
function fn(){
  this.num=1;
  }
  var a= new fn();
  console.log(a.num);   //1
``  
  这里this为什么会指向a，因为new关键字会创建一个空对象，然后回自动调用一个apply方法，将this指向这个空对象a，这样的话，函数内部的this就会被这个空对象a代替。
  
  
  
  
    
    
    
    
      
        
        
        
        
   



