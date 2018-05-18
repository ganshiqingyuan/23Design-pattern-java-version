先从最简单的开始，单例模式
顾名思义，只有一个实例，通常是某个类或对象
java类中的static属性是指某个变量或函数只初始化一次，多次生成实例也只是第一次初始化的对象，所以可以用static来标志单例对象
代码
public class Singleton{
	private static Singleton singleton = new Singleton();
	private Singleton(){
			System.out.println(“生成了一个单例");
		}
	public static Singleton getInstance(){
			return singleton;
			}
}

javascript 版本


var getSingle = function (fn) {
        var result;
        return function () {
            return result || ( result = fn.apply(this, arguments) );
        }
    };
    
    
function Singleton(name){
var cc=new Object;
cc.name=name;
return cc

}

var dd=getSingle(Singleton);
var c=dd(123);
var d=dd(456);
console.log(c)
console.log(d)
//{name: 123}
//{name: 123}

	