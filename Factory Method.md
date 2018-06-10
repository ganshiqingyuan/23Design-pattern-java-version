# 工厂模式 Factory Method

用模板模式来构建生成实例的工厂，

父类决定实例的生成方式，但不决定生成具体的类，具体处理交给子类完成，，将生成实例的框架和具体负责生成实例的类解耦，

java实现

为了展示解耦，创建两个包，即生成实例框架包和具体实现的类的实现包

Framework包

Product类，规定工厂生成的物品使用方法
    package framework;

	public abstract class Product {
    public abstract void use();
	}
    
Factory类，负责规定创建方法

	package framework;

	public abstract class Factory {
    public final Product create(String owner) {
        Product p = createProduct(owner);
        registerProduct(p);
        return p;
    }
    protected abstract Product createProduct(String
    owner);
    protected abstract void registerProduct(Product 		
    product);
	}
具体实现工厂包，比如生成一个id卡工厂，
idcard包

IDCard类，负责实现id卡产品的具体信息和实现产品的使用方法，即实现Product的use方法

package idcard;
import framework.*;

public class IDCard extends Product {
    private String owner;
    IDCard(String owner) {
        System.out.println("制作" + owner + "的ID卡。");
        this.owner = owner;
    }
    public void use() {
        System.out.println("使用" + owner + "的ID卡。");
    }
    public String getOwner() {
        return owner;
    }
	}
IDCardFactory类，负责card工厂的具体实现，

	package idcard;
	import framework.*;
	import java.util.*;

	public class IDCardFactory extends Factory {
    private List owners = new ArrayList();
    protected Product createProduct(String owner) {
        return new IDCard(owner);
    }
    protected void registerProduct(Product product) {
        owners.add(((IDCard)product).getOwner());
    }
    public List getOwners() {
        return owners;
    }
	}
    
    
入口代码
	import framework.*;
	import idcard.*;

	public class Main {
    public static void main(String[] args) {
        Factory factory = new IDCardFactory();
        Product card1 = factory.create("小明");
        Product card2 = factory.create("小红");
        Product card3 = factory.create("小刚");
        card1.use();
        card2.use();
        card3.use();
    }
	}
    
输出：

	制作小明的id卡。
	之最小红的id卡。
	制作小刚的id卡。
	使用小明的id卡。
	使用小红的id卡。
	使用小刚的id卡。


    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    














