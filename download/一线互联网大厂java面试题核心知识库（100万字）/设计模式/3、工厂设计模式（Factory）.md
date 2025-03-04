# 3、工厂设计模式（Factory）

#### **3.1 什么是工厂设计模式？**
****

工厂设计模式，顾名思义，就是用来生产对象的，在java 中，万物皆对象，这些对象都需要创建，如果创建的时候直接new 该对象，就会对该对象耦合严重，假如我们要更换对象，所有new 对象的地方都需要修改一遍，这显然违背了软件设计的开闭原则，如果我们使用工厂来生产对象，我们就只和工厂打交道就可以了，彻底和对象解耦，如果要更换对象，直接在工厂里更换该对象即可，达到了与对象解耦的目的；所以说，工厂模式最大的优点就是：解耦

#### **3.2**** ****简单工厂（****Simple**** ****Factory****）**
****

**定义：**

一个工厂方法，依据传入的参数，生成对应的产品对象； **角色：**

1、抽象产品

2、具体产品

3、具体工厂

4、产品使用者**使用说明：**

先将产品类抽象出来，比如，苹果和梨都属于水果，抽象出来一个水果类Fruit，苹果和梨就是具体的产品类，然后创建一个水果工厂，分别用来创建苹果和梨。代码如 下：

水果接口



public interface Fruit {

    void whatIm();

}

具体类:苹果



public class Apple implements Fruit {

    @Override

    public void whatIm() {

        //苹果

    }

}

具体类:梨



public class Pear implements Fruit {

    @Override

    public void whatIm() {

        //梨

    }

}

具体工厂:水果工厂



public class FruitFactory {

    public Fruit createFruit(String type) {

        if (type.equals("apple")) {//生产苹果

            return new Apple();

        } else if (type.equals("pear")) {//生产梨

            return new Pear();

        }

        return null;

    }

}

产品使用



 FruitFactory mFactory = new FruitFactory();

 Apple apple = (Apple) mFactory.createFruit("apple");//获得苹果

 Pear pear = (Pear) mFactory.createFruit("pear");//获得梨



#### **3.1**** ****工厂方法（****Factory**** ****Method****）**
****

就这样，一个非常简单的工厂设计模式就完成了，但是有没有发现什么问题呢?



对，那就是如果我想吃香蕉，想吃橘子呢，我万一什么都想吃呢??所以，以上的这种方式，每当我想添加一种水果，就必然要修改工厂类，这显然违反了开闭原则，亦不可取;所以简单工厂只适合于产品对象较少，且产品固定的需求，对于产品变化无常的需求来说显然不合适;所以我们来看下一种方式;



工厂方法设计模式

定义：将工厂提取成一个接口或抽象类，具体生产什么产品由子类决定;



角色：



抽象产品类



具体产品类



抽象工厂类



具体工厂类



使用说明：和上例中一样，产品类抽象出来，这次我们把工厂类也抽象出来，生产什么样的产品由子类来决定;



代码如下：



水果接口 苹果类和梨类 代码和上例一样



工厂接口



public interface FruitFactory {

    Fruit createFruit();//生产水果

}

苹果工厂



public class AppleFactory implements FruitFactory {

    @Override

    public Fruit createFruit() {

        return new Apple();

    }

}

梨工厂



public class PearFactory implements FruitFactory {

    @Override

    public Fruit createFruit() {

        return new Pear();

    }

}

使用



AppleFactory appleFactory = new AppleFactory();

PearFactory pearFactory = new PearFactory();

Apple apple = (Apple) appleFactory.createFruit();//获得苹果

Pear pear = (Pear) pearFactory.createFruit();//获得梨

以上这种方式，虽然解耦了，也遵循了开闭原则，但是问题根本还是没有解决啊，换汤没换药，如果我需要的产品很多的话，需要创建非常多的工厂，所以这种方式的缺点也很明显;



抽象工厂设计模式

定义：为创建一组相关或者是相互依赖的对象提供的一个接口，而不需要指定它们的具体类。



角色：和工厂方法一样



抽象工厂和工厂方法的模式基本一样，区别在于，工厂方法是生产一个具体的产品，而抽象工厂可以用来生产一组相同，有相对关系的产品;重点在于一组，一批，一系列;举个例子，假如生产小米手机，小米手机有很多系列，小米note、红米note等;假如小米note生产需要的配件有825的处理器，6英寸屏幕，而红米只需要650的处理器和5寸的屏幕就可以了;用抽象工厂来实现：



cpu接口和实现类



public interface Cpu {

    void run();

    class Cpu650 implements Cpu {

        @Override

        public void run() {

            //625 也厉害

        }

    }

    class Cpu825 implements Cpu {

        @Override

        public void run() {

            //825 处理更强劲

        }

    }

}

屏幕接口和实现类



public interface Screen {

    void size();

    class Screen5 implements Screen {

        @Override

        public void size() {

            //5寸

        }

    }

    class Screen6 implements Screen {

        @Override

        public void size() {

            //6寸

        }

    }

}

工厂接口



public interface PhoneFactory {

    Cpu getCpu();//使用的cpu

    Screen getScreen();//使用的屏幕

}

具体工厂实现类：小米手机工厂



public class XiaoMiFactory implements PhoneFactory {

    @Override

    public Cpu getCpu() {

        return new Cpu.Cpu825();//高性能处理器

    }

    @Override

    public Screen getScreen() {

        return new Screen.Screen6();//6寸大屏

    }

}

具体工厂实现类：红米手机工厂



public class HongMiFactory implements PhoneFactory {

    @Override

    public Cpu getCpu() {

        return new Cpu.Cpu650();//高效处理器

    }

    @Override

    public Screen getScreen() {

        return new Screen.Screen5();//小屏手机

    }

}

以上例子可以看出，抽象工厂可以解决一系列的产品生产的需求，对于大批量，多系列的产品，用抽象工厂可以更好的管理和扩展;



三种工厂方式总结：

1.对于简单工厂和工厂方法来说，两者的使用方式实际上是一样的，如果对于产品的分类和名称是确定的，数量是相对固定的，推荐使用简单工厂模式;



2.抽象工厂用来解决相对复杂的问题，适用于一系列、大批量的对象生产;



> 更新: 2024-05-01 16:54:40  
> 原文: <https://www.yuque.com/zhichangzhishiku/edrbqg/np9foega6pfvpedo>