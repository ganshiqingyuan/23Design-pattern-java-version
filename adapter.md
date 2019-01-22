## 适配器模式
     

对已有代码，已有的类进行适配，增加工作效率

   

java实现
### Banner 类，被适配角色


    public class Banner {
    private String string;
    public Banner(String string) {
        this.string = string;
    }
    public void showWithParen() {
        System.out.println("(" + string + ")");
    }
    public void showWithAster() {
        System.out.println("*" + string + "*");
    }
    }



###Print   类，，定义所需方法

    public interface Print {
    public abstract void printWeak();
    public abstract void printStrong();
    }


#### PrintBanner  类，，适配器，

    public class PrintBanner extends Banner implements Print {
    public PrintBanner(String string) {
        super(string);
    }
    public void printWeak() {
        showWithParen();
    }
    public void printStrong() {
        showWithAster();
    }
    }



#### 入口代码

    public class Main {
    public static void main(String[] args) {
        Print p = new PrintBanner("Hello");
        p.printWeak();
        p.printStrong();
    }
    }
    
    
这里同样的功能被保留了下来，


    

