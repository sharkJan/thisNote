һ��thisָ���ں��������ʱ����ȷ�����˵ģ�ֻ���ں���ִ��ʱ����ȷ��this����ָ��˭��ʵ����this����ָ��������������Ķ���

1.demo1
``
function a(){
    var user="shark Jan";
    console.log(this.user);
    console.log(this);
    }
    a();
``    
##window��js�е�ȫ�ֶ��������������У�����a�Ǳ�window���õģ�����thisָ����window.
����windowû��user�������������this.user��ӡ�Ľ����undefined��
������ԥthisָ����window������this�Ĵ�ӡ�ṹ��window.

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
��������У�����fn�����Ǳ�o������õģ�����fn�е�thisָ����o�������Դ�ӡ�����"shark Jan";

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
##������������ӣ�������������ۣ����Ǻ����׻��뵽��ӡundefined;��Ϊwindow��Ϊȫ�ֶ��������fn��thisӦ��ָ��window,����window�в�û��user������ԣ����Ի᷵��undefined.
�������ﲢ����ˣ���ӡ�����"shark Jan"
Ϊ�˸����������������ٿ�һ��ʵ��
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
  ���������fnͬ����o���õģ�����this��û��ָ��o,����ӡ�Ľ����12.
  ����Ϊʲô�أ�
##a.���һ����������this��������û�б���һ��������ã���ôthisָ��ľ���window��������ʱ��̽���ϸ��js����
##b.���һ����������this��ͬʱ�ֱ���һ��������ã���ôthisָ�������һ������
##���һ����������this��ͬʱ�ְ������������ô���ܺ����Ǳ�����������ã�this��Ȼ��ָ����һ��������Ķ���
�����һ�㣬�����ܸ������á�����
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
  o.c.fn();       //����
``  
  ����������o��c֮����һ������b�������޷���ӡthisָ��
  
  

4.����һ������Ƚ����⣬����
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
    ���������ʵ����������Ľ��������12��12����Ϊ����thisӦ��ָ�������һ������bѽ��
    ������ʵ������ˣ��㻹û�����һ�仰��this��Զָ��������������Ķ���Ҳ�����ں���ִ��ʱ����˭���õģ�
    ����var j=o.b.fn��ʵ����ֻ�Ƕ�����j��������û��ִ��j������thisָ���޷��жϣ����Ǻ����j(),ִ����j������Ҳ�͵�����fn(),��������ִ��j()����ʵ��window,����thisʵ����ָ����window.
    window�в�û��a����,����this.aָ����undefined,thisָ��window.
    
    �������캯���е�thisָ��
  demo
  ``
    function Fn(){
        this.user="shark Jan"
     }
     var a= new Fn();
      console.log(a.user);   //shark Jan
``
      ����ʵ����a���Ե��Fn���user,����Ϊnew�ؼ��ֿ��Ըı�thisָ��
      �����new������һ�����캯�������캯�������þ��ǳ�ʼ��������ʹ�ñ���a������һ��Fn��ʵ�������൱�ڸ�����һ��Fn������������this��ָ�����´���������a.
      
    ������this����returnʱ��
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

##ͨ������ʵ�����Է��֣�������ֵ��һ������ʱ��thisָ��ľ����Ǹ�����ֵ�Ķ��󣬵��ǵ�����ֵ����һ������ʱ����ôthis��Ȼָ������ʵ����   

##����˵����
1.���¼��У�thisָ�򴥷��¼��Ķ��󣬵��ǱȽ�������ǣ���IE��attachEvent�е�this����ָ��ȫ�ֶ���window��

2.�ϸ��javascript�У�Ĭ�ϵ�this����ָ��window������ָ��undefined.

3.new������������
demo
``
function fn(){
  this.num=1;
  }
  var a= new fn();
  console.log(a.num);   //1
``  
  ����thisΪʲô��ָ��a����Ϊnew�ؼ��ֻᴴ��һ���ն���Ȼ����Զ�����һ��apply��������thisָ������ն���a�������Ļ��������ڲ���this�ͻᱻ����ն���a���档
  
  
  
  
    
    
    
    
      
        
        
        
        
   



