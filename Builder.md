# 建造模式 Builder

组装具有复杂结构的实例，

使用类，使用不同的材料，使用一些方法创造东西

java实现

实例：一个编写文档的示例

Builder类，规定所有材料的功能

    public abstract class Builder {
    public abstract void makeTitle(String title);
    public abstract void makeString(String str);
    public abstract void makeItems(String[] items);
    public abstract void close();
	}



director类，导演，监工，使用不同的材料来建造，实例中为编写html文本和纯文本


	public class Director {
    private Builder builder;
    public Director(Builder builder) {              // 因为接收的参数是Builder类的子类
        this.builder = builder;                     // 所以可以将其保存在builder字段中
    }
    public void construct() {                       // 编写文档
        builder.makeTitle("Greeting");              // 标题
        builder.makeString("从早上至下午");         // 字符串
        builder.makeItems(new String[]{             // 条目
            "早上好。",
            "下午好。",
        });
        builder.makeString("晚上");                 // 其他字符串
        builder.makeItems(new String[]{             // 其他条目
            "晚上好。",
            "晚安。",
            "再见。",
        });
        builder.close();                            // 完成文档
    }
}


两个实例材料类，如输入html文本和纯文本文本

TextBuilder类，输入纯文本

	public class TextBuilder extends Builder {
    private String buffer = "";                                 // 文档内容保存在该字段中
    public void makeTitle(String title) {                       // 纯文本的标题
        buffer += "==============================\n";               // 装饰线
        buffer += "『" + title + "』\n";                            // 为标题加上『』
        buffer += "\n";                                             // 换行
    }
    public void makeString(String str) {                        // 纯文本的字符串
        buffer += '■' + str + "\n";                                // 为字符串添加■
        buffer += "\n";                                             // 换行
    }
    public void makeItems(String[] items) {                     // 纯文本的条目
        for (int i = 0; i < items.length; i++) {
            buffer += "　・" + items[i] + "\n";                     // 为条目添加・
        }
        buffer += "\n";                                             // 换行
    }
    public void close() {                                       // 完成文档
        buffer += "==============================\n";               // 装饰线
    }
    public String getResult() {                                 // 完成后的文档
        return buffer;
    }
	}

HtmlBuilder类

	import java.io.*;

	public class HTMLBuilder extends Builder {
    private String filename;                                                        // 文件名
    private PrintWriter writer;                                                     // 用于编写文件的PrintWriter
    public void makeTitle(String title) {                                           // HTML文件的标题
        filename = title + ".html";                                                 // 将标题作为文件名
        try {
            writer = new PrintWriter(new FileWriter(filename));                     // 生成 PrintWriter
        } catch (IOException e) {
            e.printStackTrace();
        }
        writer.println("<html><head><title>" + title + "</title></head><body>");    // 输出标题
        writer.println("<h1>" + title + "</h1>");
    }
    public void makeString(String str) {                                            // HTML文件中的字符串
        writer.println("<p>" + str + "</p>");                                       // 用<p>标签输出
    }
    public void makeItems(String[] items) {                                         // HTML文件中的条目
        writer.println("<ul>");                                                     // 用<ul>和<li>输出
        for (int i = 0; i < items.length; i++) {
            writer.println("<li>" + items[i] + "</li>");
        }
        writer.println("</ul>");
    }
    public void close() {                                                           // 完成文档
        writer.println("</body></html>");                                           // 关闭标签
        writer.close();                                                             // 关闭文件
    }
    public String getResult() {                                                     // 编写完成的文档
        return filename;                                                            // 返回文件名
    }
	}





    
入口代码

	public class Main {
    public static void main(String[] args) {
        if (args.length != 1) {
            usage();
            System.exit(0);
        }
        if (args[0].equals("plain")) {
            TextBuilder textbuilder = new TextBuilder();
            Director director = new Director(textbuilder);
            director.construct();
            String result = textbuilder.getResult();
            System.out.println(result);
        } else if (args[0].equals("html")) {
            HTMLBuilder htmlbuilder = new HTMLBuilder();
            Director director = new Director(htmlbuilder);
            director.construct();
            String filename = htmlbuilder.getResult();
            System.out.println(filename + "文件编写完成。");
        } else {
            usage();
            System.exit(0);
        }
    }
    public static void usage() {
        System.out.println("Usage: java Main plain      编写纯文本文档");
        System.out.println("Usage: java Main html       编写HTML文档");
    }
	}

    



    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    














