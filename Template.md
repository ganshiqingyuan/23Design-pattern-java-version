##Template模板模式
     

父类中定义处理流程，子类中实现具体处理，说白了就是父类定义方法执行顺序，子类实现具体怎么执行

    

java实现
####抽象父类

    public abstract class AbstractDisplay { // 抽象类AbstractDisplay
    public abstract void open();        // 交给子类去实现的抽象方法(1) open
    public abstract void print();       // 交给子类去实现的抽象方法(2) print
    public abstract void close();       // 交给子类去实现的抽象方法(3) close
    public final void display() {       // 本抽象类中实现的display方法
        open();                         // 首先打开…
        for (int i = 0; i < 5; i++) {   // 循环调用5次print
            print();                    
        }
        close();                        // …最后关闭。这就是display方法所实现的功能
    }
    }

###实现类1

    public class CharDisplay extends AbstractDisplay {  // CharDisplay是AbstractDisplay的子类 
    private char ch;                                // 需要显示的字符
    public CharDisplay(char ch) {                   // 构造函数中接收的字符被
        this.ch = ch;                               // 保存在字段中
    }
    public void open() {                            // 在父类中是抽象方法，此处重写该方法  
        System.out.print("<<");                     // 显示开始字符"<<"
    }
    public void print() {                           // 同样地重写print方法。该方法会在display中被重复调用
        System.out.print(ch);                       // 显示保存在字段ch中的字符
    }
    public void close() {                           // 同样地重写close方法
        System.out.println(">>");                   // 显示结束字符">>"
    }
    }


####实现类2

    public class StringDisplay extends AbstractDisplay {    // StringDisplay也是AbstractDisplay的子类 
    private String string;                              // 需要显示的字符串
    private int width;                                  // 以字节为单位计算出的字符串长度
    public StringDisplay(String string) {               // 构造函数中接收的字符串被
        this.string = string;                           // 保存在字段中
        this.width = string.getBytes().length;          // 同时将字符串的字节长度也保存在字段中，以供后面使用 
    }
    public void open() {                                // 重写的open方法
        printLine();                                    // 调用该类的printLine方法画线
    }
    public void print() {                               // print方法
        System.out.println("|" + string + "|");         // 给保存在字段中的字符串前后分别加上"|"并显示出来 
    }
    public void close() {                               // close方法
        printLine();                                    // 与open方法一样，调用printLine方法画线
    }
    private void printLine() {                          // 被open和close方法调用。由于可见性是private，因此只能在本类中被调用 
        System.out.print("+");                          // 显示表示方框的角的"+"
        for (int i = 0; i < width; i++) {               // 显示width个"-"
            System.out.print("-");                      // 组成方框的边框
        }
        System.out.println("+");                        // /显示表示方框的角的"+"
    }
    }






####入口代码
    public class Main {
    public static void main(String[] args) {
        AbstractDisplay d1 = new CharDisplay('H');                  // 生成一个持有'H'的CharDisplay类的实例 
        AbstractDisplay d2 = new StringDisplay("Hello, world.");    // 生成一个持有"Hello, world."的StringDisplay类的实例 
        AbstractDisplay d3 = new StringDisplay("你好，世界。");     // 生成一个持有"你好，世界。"的StringDisplay类的实例 
        d1.display();                                               // 由于d1、d2和d3都是AbstractDisplay类的子类
        d2.display();                                               // 可以调用继承的display方法
        d3.display();                                               // 实际的程序行为取决于CharDisplay类和StringDisplay类的具体实现 
    }
    }


    
