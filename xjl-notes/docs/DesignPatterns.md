# Java 设计模式

## Intent

增强代码的复用与扩展



## contents：
1. <a href="#策略模式">策略模式</a>

2. <a href="#观察者模式">观察者模式</a>
 
3. <a href="#装饰者模式">装饰者模式</a>

4. <a href="#工厂模式">装饰者模式</a>

5. <a href="#单例模式">装饰者模式</a>

## 策略模式

### Design Principles

- 封装变化

- 针对超类型编程即 Java 多态

- 多用接口组合，少用继承覆写

### Intent

- 为某种行为定义一个算法接口，接口中定义抽象方法，然后定义了一系列实现类实现该接口，在这些实现类中具体实现该接口中的抽象方法，使得这些实现类可以互相替换，然后程序运行时调用该接口的这个抽象方法时会自动判断调用哪个实现类中的具体方法（依据该接口指向哪一个实现类实例），自动判断的基础是多态。

- 策略模式可以让算法独立于使用它的客户端。

### Class Diagram

<div align="center"> <img src="../xjl-notes/docs/pics/designPatterns/0.png" width="1000px"/> </div><br>

> 图片引用自 <a href="https://github.com/CyC2018/CS-Notes/blob/master/notes/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F.md#9-%E7%AD%96%E7%95%A5strategy">cyc2018</a>

- Strategy 作为一个行为算法接口，其内定义了该算法的一系列行为抽象方法，这些方法在其下的一系列实现类中具体实现

- Context 是使用该算法接口的客户端类，Strategy 作为 Context 的成员变量，其中的 doSomething() 方法会调用 behavior()，setStrategy(Strategy) 方法可以动态地改变 strategy 对象，也就是说能动态地改变 Context 所使用的算法。

### Implementation

<div align="center"> <img src="../xjl-notes/docs/pics/designPatterns/1.jpg" width="300px"/> </div><br>

animal 包
```
public abstract class Duck {

    FlyBehavior flyBehavior;
    QuackBehavior quackBehavior;

    public Duck() {
    }

    public abstract void display();

    public void  performFly(){
        flyBehavior.fly();
    }

    public void performQuack(){
        quackBehavior.quack();
    }

    public void swim(){
        System.out.println("all duck float");
    }
}
```
```
public class MallardDuck extends Duck {

    public MallardDuck() {
        quackBehavior = new Quack();
        flyBehavior = new FlyWithWings();
    }

    @Override
    public void display() {
        System.out.println("I'm a real Mallard duck!!");
    }
}

```

behavior 包
```
public interface QuackBehavior {
    public void quack();
}
```
behavior/impl 包
```
public class Quack implements QuackBehavior {
    @Override
    public void quack() {
        System.out.println("quack!!");
    }
}
```
```
public class Squeak implements QuackBehavior {
    @Override
    public void quack() {
        System.out.println("Squack");
    }
}
```

测试类
```
public class MiniDuckSimulator {
    public static void main(String[] args) {
        Duck mallard = new MallardDuck();
        mallard.performFly();
        mallard.performQuack();

    }
}
```

省略了 fly 行为接口及其实现类

> 代码引用自 《Head First设计模式》 第一章

## 观察者模式

### Design Principles

交互对象之间松耦合设计 更有弹性 更能应对变化

### Intent

定义一组一对多的对象依赖，被依赖对象状态改变，其依赖对象收到通知。

主题（Subject）是被观察的对象，而其所有依赖者（Observer）称为观察者。

### Class Diagram

<div align="center"> <img src="../xjl-notes/docs/pics/designPatterns/2.png" width="1000px"/> </div><br>

> 图片引用自 <a href="https://github.com/CyC2018/CS-Notes/blob/master/notes/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F.md#9-%E7%AD%96%E7%95%A5strategy">cyc2018</a>

- 主题（Subject）具有注册和移除观察者、并通知所有观察者的功能，主题与观察者之间的依赖关系是：主题中有一个成员变量 list 用来存放 观察者对象。

- 观察者（Observer）的注册功能需要调用主题的注册方法，即在主题类中将观察者对象 add 至 list 中，观察者也可以有撤销注册方法。

### Implementation

<div align="center"> <img src="../xjl-notes/docs/pics/designPatterns/3.png" width="300px"/> </div><br>

obverser 包

```
public interface Observer {
    public void update(float temp, float humidity, float pressure);
}
```

obverser/impl 包
```
public class CurrentConditionsDisplay implements Observer {

    public CurrentConditionsDisplay(Subject weatherData) {
        weatherData.registerObserver(this);
    }

    @Override
    public void update(float temp, float humidity, float pressure) {
        System.out.println("CurrentConditionsDisplay.update: " + temp + " " + humidity + " " + pressure);
    }
}
```
```
public class StatisticsDisplay implements Observer {

    public StatisticsDisplay(Subject weatherData) {
        weatherData.registerObserver(this);
    }

    @Override
    public void update(float temp, float humidity, float pressure) {
        System.out.println("StatisticsDisplay.update: " + temp + " " + humidity + " " + pressure);
    }
}
```

subject 包
```
public interface Subject {
    public void registerObserver(Observer o);
    public void removeObserver(Observer o);
    public void notifyObserver();
}
```

subject/impl 包
```
public class WeatherData implements Subject {
    private List<Observer> observers;
    private float temperature;
    private float humidity;
    private float pressure;

    public WeatherData() {
        observers = new ArrayList<>();
    }

    public void setMeasurements(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        notifyObserver();
    }

    @Override
    public void registerObserver(Observer o) {
        observers.add(o);
    }

    @Override
    public void removeObserver(Observer o) {
        int i = observers.indexOf(o);
        if (i >= 0) {
            observers.remove(i);
        }
    }

    @Override
    public void notifyObserver() {
        for (Observer observer:observers){
            observer.update(temperature, humidity, pressure);
        }
    }
}
```

测试类
```
public class WeatherStation {
    public static void main(String[] args) {
        WeatherData weatherData = new WeatherData();
        CurrentConditionsDisplay currentConditionsDisplay = new CurrentConditionsDisplay(weatherData);
        StatisticsDisplay statisticsDisplay = new StatisticsDisplay(weatherData);

        weatherData.setMeasurements(1,2,3);
        weatherData.setMeasurements(4,5,6);
    }
}
```

## 装饰者模式

### Design Principles

- 类要对扩展开放 对修改关闭

### Intent

- 为对象动态添加功能。

### Class Diagram

<div align="center"> <img src="../xjl-notes/docs/pics/designPatterns/4.png" width="1000px"/> </div><br>

> 图片引用自 <a href="https://github.com/CyC2018/CS-Notes/blob/master/notes/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F.md#9-%E7%AD%96%E7%95%A5strategy">cyc2018</a>

- 装饰者（Decorator）和具体对象组件（ConcreteComponent）都实现超类对象组件（Component）接口，装饰者模式的关键点在于 装饰者 中设置一个超类对象组件作为自身成员变量，这样它可以装饰其它装饰者或者具体组件（被装饰的装饰者或者具体组件存在当前装饰者的成员变量中）

- 通过装饰者递归调用自身成员变量（上一层装饰者或底层的具体对象组件），实现装饰者们与具体对象组件功能的累加，从而实现为对象（具体组件或装饰者）动态添加功能。

### Implementation

<div align="center"> <img src="../xjl-notes/docs/pics/designPatterns/5.png" width="300px"/> </div><br>

component 包
```
public interface Beverage {
    double cost();
}

```

component/impl 包
```
public class DarkRoast implements Beverage {
    @Override
    public double cost() {
        return 1;
    }
}
```
```
public class HouseBlend implements Beverage {
    @Override
    public double cost() {
        return 1;
    }
}
```

component/decorator 包
```
public abstract class CondimentDecorator implements Beverage {
    protected Beverage beverage;
}
```

component/decorator/ext 包
```
public class Milk extends CondimentDecorator {

    public Milk(Beverage beverage) {
        this.beverage = beverage;
    }

    @Override
    public double cost() {
        return 1 + beverage.cost();
    }
}
```
```
public class Mocha extends CondimentDecorator {

    public Mocha(Beverage beverage) {
        this.beverage = beverage;
    }

    @Override
    public double cost() {
        return 1 + beverage.cost();
    }
}
```

测试类
```
public class Client {
    public static void main(String[] args) {
        Beverage beverage = new HouseBlend();
        beverage = new Mocha(beverage);
        beverage = new Milk(beverage);
        System.out.println(beverage.cost());
    }
}

```

## 工厂模式

### Design Principles

### Intent

### Class Diagram

### Implementation

## 单例模式

### Design Principles

### Intent

### Class Diagram

### Implementation









