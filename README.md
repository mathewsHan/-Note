# -  享元模式&代理模式
享元模式
简介

享元模式主要用于减少创建对象的数量，以减少内存占用和提高性能。这种类型的设计模式属于结构型模式，它提供了减少对象数量从而改善应用所需的对象结构的方式。

用通俗的话来说就是进行共用。生活中也有一些例子，比如之前很火的共享单车，更早之前的图书馆，编程中经常用的String类，数据库连接池等等。当然，享元模式主要的目的是复用，如果该对象没有的话，就会进行创建。

享元模式的角色主要分为三大类，抽象享元类、具体享元类以及享元工厂类。

抽象享元类：所有具体享元类的超类或者接口，通过这个接口，可以接受并作用于外部专题。
具体享元类：实现抽象享元类接口的功能并增加存储空间。
享元工厂类：用来创建并管理抽象享元类对象，它主要用来确保合理地共享。每当接受到一个请求是，便会提供一个已经创建的抽象享元类对象或者新建一个。 享元模式的核心在于享元工厂类，享元工厂类的作用在于提供一个用于存储享元对象的享元池，用户需要对象时，首先从享元池中获取，如果享元池中不存在 ，则创建一个新的享元对象返回给用户，并在享元池中保存该新增对象。
其它的就不再多说，这里依旧使用一个简单的示例来加以说明。
在我们以前读书的时候，经常会用到笔，其中铅笔又是最早接触的，我们最开始使用铅笔可能不是写字，而是进行画画。这里我们可以把笔当作一个抽象享元类，铅笔当作一个具体享元类，然后再创建一个享元工厂类，用于创建和管理，最后再由调用者决定用铅笔进行干嘛。

首先，我们创建一个接口。

interface Pen {
   void write();
}
然后再创建一个享元工厂类，指定需要内部需要做的事情。

class Penil implements Pen {
   private String name;
   private String something; 
   private  int i;
   
   public Penil(String name) {
       this.name = name;
       i++;
       System.out.println(name+" 第:"+i+"次创建");
   }
   
   public String getName() {
       return name;
   }
   
   public void setName(String name) {
       this.name = name;
   }
   
   public String getSomething() {
       return something;
   }
   
   public void setSomething(String something) {
       this.something = something;
   }
   
   @Override
   public void write() {
       System.out.println(name+" 用于铅笔  "+something);
   }
}
继而再创建一个工厂类，用于创建和管理。

class PenFactory {
   private static final Map<String, Penil> map = new HashMap<String, Penil>();

   public static Penil get(String name) {
       Penil penil = map.get(name);
       if (penil == null) {
           penil = new Penil(name);
           map.put(name, penil);
       }
       return penil;
   }
}
最后再来进行调用测试。

public class FlyweightTest {
    public static void main(String[] args) {
        String names[] = { "张三", "李四", "王五", "虚无境" };
        for (int i = 0; i < 8; i++) {
            Penil penil = PenFactory.get(names[i>3?i-4:i]);
            penil.setSomething("画了一条鱼");
            penil.write();
        }
    }
}
输出结果:

            张三 第:1次创建
            张三 用于铅笔  画了一条鱼
            李四 第:1次创建
            李四 用于铅笔  画了一条鱼
            王五 第:1次创建
            王五 用于铅笔  画了一条鱼
            虚无境 第:1次创建
            虚无境 用于铅笔  画了一条鱼
            张三 用于铅笔  画了一条鱼
            李四 用于铅笔  画了一条鱼
            王五 用于铅笔  画了一条鱼
            虚无境 用于铅笔  画了一条鱼
上述示例中，每个对象都使用了两次，但是每个对象都只是创建了一次而已，而享元模式核心的目的其实就是复用，只要我们理解了这一点，想必掌握该模式也就不在话下了。

享元模式优点：

极大的减少对象的创建，从而降低了系统的内存，提升了效率。

享元模式缺点：

提高了系统的复杂度，因为需要将状态进行分离成内部和外部，并且也使外部状态固有化，使得随着内部状态的变化而变化，会造成系统的混乱。

使用场景：

系统有大量相似对象。

注意事项：

需要注意划分外部状态和内部状态，否则可能会引起线程安全问题。 这些类必须有一个工厂对象加以控制。

与单例模式比较

虽然它们在某些方面很像，但是实际上却是不同的东西，单例模式的目的是限制创建多个对象，避免冲突，比如使用数据库连接池。而享元模式享元模式的目的是共享，避免多次创建耗费资源，比如使用String类。

代理模式
简介

代理模式于结构型模式，主要是通过一个类代表另一个类的功能。通常，我们创建具有现有对象的对象，以便向外界提供功能接口。

代理模式，如其名，也就是代理作用。 我们生活中也有不少示例，比如典型的代购，土豪专用的支票，Windows 里面的快捷方式，以及spring中的aop 等等。

代理模式主要由这三个角色组成，抽象角色、代理角色和真实角色。

抽象角色：通过接口或抽象类声明真实角色实现的业务方法。
代理角色：实现抽象角色，是真实角色的代理，通过真实角色的业务逻辑方法来实现抽象方法，并可以附加自己的操作。
真实角色：实现抽象角色，定义真实角色所要实现的业务逻辑，供代理角色调用。
代理模式又分为静态代理、动态代理。

静态代理是由程序员创建或工具生成代理类的源码，再编译代理类。所谓静态也就是在程序运行前就已经存在代理类的字节码文件，代理类和委托类的关系在运行前就确定了。
动态代理是在实现阶段不用关心代理类，而在运行阶段才指定哪一个对象。
这里我们依旧用一个简单的示例来进行说明。
张三和李四是室友，某天，张三在寝室内玩游戏正带劲，感觉肚子饿了，本想下楼去吃饭的，但是想起李四可能快要回来，于是打电话给李四，让李四帮自己带份盒饭。这里的李四就扮演着代理者的作用。

静态代理
首先我们用静态代理来实现该功能。

这里实现相对而言较为简单，依旧是定义一个接口，然后定义一个真实的角色，实现该接口的功能，继而定义一个代理者，也实现该接口，但是添加该真实角色的对象进行相应的业务逻辑处理。
那么该静态代理代码实现如下:

interface Shopping {
    void buyFood();
}

class ExecutePerson implements Shopping {
    private String name;
    public ExecutePerson(String name) {
        this.name = name;
    }

    @Override
    public void buyFood() {
        System.out.println(name + " 买东西");
    }
}

class ProxyPerson implements Shopping {
    private ExecutePerson ep;
    public ProxyPerson(ExecutePerson ep) {
        this.ep = ep;
    }
    @Override
    public void buyFood() {
        ep.buyFood();
    }
}


public class ProxyTest {
    public static void main(String[] args) {    
        String name = "李四";
        Shopping shopping = new ProxyPerson(new ExecutePerson(name));
        shopping.buyFood();
    }
}
输入结果:

 李四 买东西
在使用静态代理实现该功能之后，我们发现实现起来很简单，通过一个代理类就可以在不影响目标对象的前提进行扩展使用。但是我们也发现一个问题，如果我们不确定需要代理某个真实类的时候会比较麻烦，而且在类过多的时候，目标对象与代理对象都要维护，会使系统复杂度提升，维护起来也更加麻烦。
不过这时我们就可以使用动态代理来进行解决。

动态代理
所谓动态代理可以不必强行指定某个真实的角色，只需要在运行时决定就可以了。这里我们可以使用JDK中java.lang.reflect来进行开发。

JDK对动态代理提供了以下支持:

java.lang.reflect.Proxy 动态生成代理类和对象
java.lang.reflect.InvocationHandler
可以通过invoke方法实现对真实角色的代理访问;
每次通过Proxy生成代理类对象时都要指定对象的处理器对象.
那么废话不在多说，开始进行代码改造，之前的接口和真实者不需要更改，我们只需要更改代理者就可以了。
更改之后的代码如下:

class ProxyPerson2 implements InvocationHandler {
 private Shopping shopping;
 private final String methodName = "buyFood";
 public ProxyPerson2(Shopping shopping) {
     this.shopping = shopping;
 }

 @Override
 public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
     Object result = null;
     if (methodName.equals(method.getName())) {
         result = method.invoke(shopping, args);
     }
     return result;
 }
}
测试代码，注意这里调用和之前不同！
这里通过Proxy类中的newProxyInstance方法会动态生成一个代理类，然后进行调用。其中这三个参数的说明如下:

ClassLoader: 生成一个类, 这个类也需要加载到方法区中, 因此需要指定ClassLoader来加载该类
Class[] interfaces: 要实现的接口
InvocationHandler: 调用处理器
public class ProxyTest {
    public static void main(String[] args) {    
        Shopping shopping2 = (Shopping)Proxy.newProxyInstance(ClassLoader.getSystemClassLoader(), new Class[]{Shopping.class}, new ProxyPerson2(new ExecutePerson(name)));
        shopping2.buyFood();
    }
}
代理模式优点：

1、职责清晰。 2、高扩展性。 3、智能化。

代理模式缺点：

1、由于在客户端和真实主题之间增加了代理对象，因此有些类型的代理模式可能会造成请求的处理速度变慢。
2、实现代理模式需要额外的工作，有些代理模式的实现非常复杂。

注意事项：

和适配器模式的区别：适配器模式主要改变所考虑对象的接口，而代理模式不能改变所代理类的接口。
和装饰器模式的区别：装饰器模式为了增强功能，而代理模式是为了加以控制。
