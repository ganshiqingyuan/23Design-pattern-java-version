#原型模式
###即对大的对象提前做个拷贝，使用时直接复制而不用重新生成
###java中可以用接口的概念，明确方法，子类做出不同实现作为原型，再注册到调用上进行不同的调用，

* Product类   声明了抽象方法使用use 和 创建克隆对象方法 createClone的接口
* Manager类  注册不同的原型，进行原型克隆调用
* MessageBox类 原型类，实现了接口的方法，方法内容为将字符串放入方框中
* UnderLinePen类 原型类，实现了接口的方法，方法内容为给字符串加上下划线

###Product
    public interface Product extends Cloneable{
        public abstract void use (String s);   //
        public abstract Product creatClone();
        }
###Manager
    public class Manager{
        private HashMap showcase = new HashMap();
        public void register (String name,Product proto){
            showcase.put(name,proto);
            }
        public product creat(String protoname){
            Product p =(product)showcase.get(protoname);
            return p.createClone();
            }
        }
###MessageBox
    private char decochar;
    public MessageBox(char decochar){
        this.decochar=decochar
        }
    public void use(String s){
        ...
        }
    public Product creatClone(){
        Product p=null;
        try{
            p=(Product)clone();
        }catch(CloneNotSupportedException e){
            e.printStackTrace();
        }
        return p;
        }
    }
####Underkine
这个类似，只不过是变成加下划线

####入口代码
    public static void main (String[] args){
    Manager manager = new Manager();
    UnderlinePen upen = new UnderlinePen('~');
    MessageBox mbox = new MessageBox('*');
    MessageBox sbox = new MessageBox('/');
    manager.register("strong message",upen);
    manager.register("warning box",mbox);
    manager.register("slash box".sbox);
    
    
    Product p1 =manager.create("strong message")
    p1.use("Hello,world");
    Product p2 =manager.create("warning box");
    p2.use("hello,word");
    Product p3 = manager.create("slash box");
    p3.use("Hello,world.");
    }
    
####javascript
创建多个原型备份，复制对象时使用object.creat方法将proto指向原型对象
