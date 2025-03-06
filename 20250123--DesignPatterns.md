[TOC]
# 设计模式

- 创建时间: 2025年01月24日 13:36
- Tag: WPS Book
- [实战教程](https://mp.weixin.qq.com/s/9XqcJUdfFgbUkKclfHGz7Q)
- [Link to wps](https://www.kdocs.cn/l/chEwDY3lJvif)
![alt text](assets/20250123--DesignPatterns/image.png)

## UML 类图
### 类图构成
![alt text](assets/20250123--DesignPatterns/image-2.png)
### 类之间的关系
![alt text](assets/20250123--DesignPatterns/企业微信截图_17388203389672.png)
![alt text](assets/20250123--DesignPatterns/image-4.png)

## 设计原则
![alt text](assets/20250123--DesignPatterns/image-3.png)

## 创建型原则
### 单例模式（****）
> 模式要点
> 1. 某个类只能有一个实例
> 2. 它必须自行创建这个实例
> 3. 它必须自行向整个系统提供这个实例

- 延迟加载的单例模式
![alt text](assets/20250123--DesignPatterns/code.png)
- 使用Activator创建`具备私有构造函数类`的单例模板
![alt text](assets/20250123--DesignPatterns/code-1.png)
- **具备延迟加载且支持私有构造函数类的单例模板**
![alt text](assets/20250123--DesignPatterns/code-2.png)
- 进一步优化
```csharp
public abstract class Singleton<T> where T : class
{
    private static class Holder
    {
        static Holder() { }

        internal static readonly Lazy<T> instance = new Lazy<T>(() =>
        {
            //添加了异常处理，以便在实例化失败时抛出详细的异常信息。
            try
            {
                return Activator.CreateInstance(typeof(T), true) as T;
            }
            catch (Exception ex)
            {
                throw new InvalidOperationException($"The {typeof(T)} instance could not be created.", ex);
            }
        });
    }

    public static T Instance
    {
        get
        {
            return Holder.instance.Value;
        }
    }

    protected Singleton()
    {
        //检查 Holder.instance.IsValueCreated，如果实例已经被创建，则抛出异常。这可以防止通过反射创建多个实例。
        if (Holder.instance.IsValueCreated)
        {
            throw new InvalidOperationException("An instance of this singleton class has already been created.");
        }
    }
}
```
### 简单工厂模式（***）
![alt text](assets/20250123--DesignPatterns/image-5.png)
- 定义一个工厂类，它可以根据参数的不同返回不同类的实例；
  - 被创建的实例通常都具有共同的父类。
  - 创建实例的方法是静态方法。
- 客户端传入参数时，可以通过Config配置反射，无需知道具体哪个参数对应哪个具体子类；
- 工厂模式强调，A与B之间的关系只能存在创建/使用，不能兼容；
  - 将对象的创建和使用分离，符合单一职责原则；
  - 客户端可以在工厂模式中以简单方式确定实例化对象，无需关注具体子类的构造函数和业务参数；
- 为了简化简单工厂模式；
  - 可以将抽象产品类与工厂类合并，将静态工厂创建方法转移到抽象产品类中；
- 优缺点
  ![alt text](assets/20250123--DesignPatterns/image-7.png)

### 工厂方法模式（*****）
- 相较于简单工厂模式，将所有产品类的初始化判断放在一个工厂类内部，工厂方法模式是提供一个抽象工厂接口，由不同的具体工厂类来实现不同产品的初始化逻辑；
- 优缺点
![alt text](assets/20250123--DesignPatterns/image-8.png)

### 抽象工厂模式（*****）
- 在工厂方法模式基础上，创建一系列相关或相互依赖的接口，而无需指定具体类，避免一个工厂具体类只生产一种产品；
- 在抽象工厂模式中，增加新的工厂具体类很简单，但是如果增加新的产品结构（修改抽象工厂接口）很麻烦，这种性质称为`开闭原则的倾斜性`；
![alt text](assets/20250123--DesignPatterns/image-9.png)

### 原型模式（***）
- 使用原型实例指定创建对象的种类，并通过拷贝这些原型来创建新的对象；
- 实现Clone的接口，在具体类内部实现；
![alt text](assets/20250123--DesignPatterns/image-10.png)

### 建造者模式（**）
- 常见构造
![alt text](assets/20250123--DesignPatterns/image-11.png)
- 代码实例
![alt text](assets/20250123--DesignPatterns/image-12.png)
- 通过引入钩子方法，可以在Director中不仅指定构造顺序，还可以控制是否执行某些构造方法；
  - 在抽象ActorBuilder中传入可虚方法bool判断，由子类判断是否重载执行该方法；
![alt text](assets/20250123--DesignPatterns/image-13.png)

## 结构型模式
### 适配器模式（****）
- 将一个类的接口转换成客户端希望的另一个接口，使得原本由于接口不兼容而不能一起工作的类可以一起工作；
- 适配器模式主要应用于希望复用一些现存的类，但是接口又与期望的不匹配的情况；

#### 对象适配器
- 类图实例
![alt text](assets/20250123--DesignPatterns/image-14.png)
#### 双向适配器
- Adapter中包含对Target和Adaptee的引用，既可以调用Target的方法也可以调用Adaptee的方法，返回可选；
#### 缺省适配器
- 适配器模式中，适配器类通常需要实现所有适配接口的所有方法；
  - 如果适配的接口很多，适配器类的代码就会很长；
  - 缺省适配器模式通过提供一个默认的实现，简化适配器的编写工作；


### 桥接模式（***）
- 将多个耦合类，在其多个维度进行各自的抽象和实现，最后拼接N个维度的实现；
![alt text](assets/20250123--DesignPatterns/image-15.png)
![alt text](assets/20250123--DesignPatterns/image-16.png)

### 组合模式（****）
- 定义
  - 对于多个对象组合和单个对象的操作具备一致性；
  - 将对象组合成树形结构以表示“部分-整体”的层次结构，使得用户对单个对象和组合对象的使用具有一致性；
![alt text](assets/20250123--DesignPatterns/image-17.png)
- 透明组合模式
  - 在Component中定义了所有子类共有的方法，这样客户端不需要区分是叶子节点还是组合节点；
  - 缺点是叶子节点对于部分公共方法需要处理异常；
- 安全组合模式
  - 在Component中只定义了叶子节点共有的方法，而组合节点特有的方法在Composite中定义；
  - 缺点是客户端需要区分是叶子节点还是组合节点；
- 优缺点
  ![alt text](assets/20250123--DesignPatterns/image-18.png)

### 装饰模式（***）
![alt text](assets/20250123--DesignPatterns/image-19.png)
- 动态地给一个对象添加一些额外的职责，就增加功能来说，装饰模式比生成子类更为灵活；
- 如果客户端需要执行新增的行为，就代表半透明装饰模式；
- 在实现透明模式时，要求具体装饰类的重载原有的Operation方法，并且实现AddBehavior方法；
![alt text](assets/20250123--DesignPatterns/image-20.png)


### 外观模式（*****）
![alt text](assets/20250123--DesignPatterns/image-21.png)
- 在一个系统中可以设置多个外观类，通过抽象的外观类，封装多个子系统的操作；
- 客户端需要知道选择合适的Facade类，并调用其方法；
- 外观类应当避免增加新操作，而是在Facade类中封装原有子系统的方法；
- 优缺点
![alt text](assets/20250123--DesignPatterns/image-22.png)

### 享元模式（*）
- 运用共享技术有效地支持大量细粒度的对象；
  - 享元模式通过减少对象的数量，降低内存消耗；
- 例如提供抽象享元类，其中自己实现了一些共享状态，具体享元类实现一些非共享状态，一般通过工厂方法创建；
![alt text](assets/20250123--DesignPatterns/image-23.png)
![alt text](assets/20250123--DesignPatterns/image-26.png)
#### 单纯享元模式
所有的具体享元类都是在同一个层次上独立的，没有任何共享状态；
![alt text](assets/20250123--DesignPatterns/image-24.png)
#### 复合享元模式
存在一些对象是组合的，一个复合享元对象中包含多个单纯享元对象，每个单纯享元对象都是共享同一个外部状态的；
![alt text](assets/20250123--DesignPatterns/image-25.png)

### 代理模式（****）
- 常用代理模式
  ![alt text](assets/20250123--DesignPatterns/image-27.png)
- 优缺点
![alt text](assets/20250123--DesignPatterns/image-28.png)


## 行为型模式
### 职责链模式（**）
![alt text](assets/20250123--DesignPatterns/image-29.png)
- 纯粹的职责链模式中，每个节点要么处理请求，要么将请求传递给下一个节点；
- 不纯职责链模式中，节点可以部分处理后再传递给下一个节点，也可以决定是否将请求传递给下一个节点；
- 优缺点
![alt text](assets/20250123--DesignPatterns/image-30.png)


### 命令模式（****）
- 核心是提供了命令的封装，在创建命令时，可以将请求者、接收者和具体操作封装为一个对象；
![alt text](assets/20250123--DesignPatterns/image-31.png)
![alt text](assets/20250123--DesignPatterns/image-32.png)

### 解释器模式（*）
### 迭代器模式（*****）
- 迭代器模式允许对象以不同的方式遍历容器，而无需暴露容器的内部结构。
![alt text](assets/20250123--DesignPatterns/image-33.png)
### 中介者模式（**）
- 用一个中介对象来封装一系列的对象交互，中介者使各对象不需要显式地相互引用，从而使其耦合松散，而且可以独立地改变它们之间的交互。
![alt text](assets/20250123--DesignPatterns/image-34.png)
### 备忘录模式（**）
- 在不破坏封装性的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态。这样以后就可将对象恢复到原先保存的状态。
![alt text](assets/20250123--DesignPatterns/image-35.png)
### 观察者模式（*****）
- 定义对象间的一种一对多的依赖关系，使得每当一个对象改变状态，所有依赖于它的对象都会收到通知并自动更新。
![alt text](assets/20250123--DesignPatterns/image-36.png)
### 状态模式（***）
- 允许对象在内部状态改变时改变它的行为，对象看起来似乎修改了它所属的类。
- 将对象在不同状态下的行为封装在不同的类中，并让它们互相转换。
![alt text](assets/20250123--DesignPatterns/image-37.png)


### 策略模式（****）
- 定义一系列算法，并将每一个算法封装起来，使它们可以相互替换，且算法的变化不会影响使用算法的客户。
- 类似之前定制的多种打标规则，最终由外部决定调用；
![alt text](assets/20250123--DesignPatterns/image-38.png)
![alt text](assets/20250123--DesignPatterns/image-39.png)
### 模板方法模式（***）
- 在父类中定义一个算法的骨架，而将一些步骤延迟到子类中实现。使得子类可以不改变算法的结构即可重定义该算法的某些特定步骤。
![alt text](assets/20250123--DesignPatterns/image-40.png)
![alt text](assets/20250123--DesignPatterns/image-41.png)
### 访问者模式（*）
- 表示一个作用于某对象结构中的各元素的操作，它使你可以在不改变各元素的类的前提下定义作用于这些元素的新操作。
![alt text](assets/20250123--DesignPatterns/image-42.png)
![alt text](assets/20250123--DesignPatterns/image-43.png)











