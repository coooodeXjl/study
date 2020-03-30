# 1.环境配置

使用 idea IDE 进行单元测试，首先需要安装 JUnit 插件

## 1.1.安装JUnit插件步骤

File-->settings-->Plguins-->Browse repositories-->输入 JUnit-->选择 JUnit Generator V2.0 安装

<div align="center"> <img src="../xjl-notes/docs/pics/junit/0.png" width="1000px"/> </div><br>

## 1.2. 使用JUnit插件

在需要进行单元测试的类中，使用快捷键 Alt+Insert，选择 JUnit test，选择 JUnit4

# 2.单元测试

测试文件代码 demo

@BeforeClass ： 修饰的方法在所有方法加载前执行，因为是静态方法在类加载后就会执行，在内存中只有一份实例，适合用来加载配置文件

@AfterClass ： 修饰的方法在所有方法执行完毕之后执行，通常用来进行资源清理，例如关闭数据库连接

@Before 和 @After ：在每个测试方法执行前后都会执行一次

@Test ： 修饰测试方法

```
    ...
    @BeforeClass
    public static void setUpBeforeClass() throws Exception {

    }

    @AfterClass
    public static void setUpAfterClass() throws Exception {

    }

    @Before
    public void before() throws Exception {

    }

    @After
    public void after() throws Exception {

    }

    @Test
    public void testXxx() throws Exception { 
        //TODO: Test goes here...
        assertEquals(a,b);//a 是预期值，b 是测试方法实际返回值
    } 
    ...
```

# 3.注意事项

1.测试方法上面必须使用@Test注解进行修饰。

2.测试方法必须使用public void 进行修饰，不能带有任何参数。

3.新建一个源代码目录用来存放测试代码。

4.测试类的包应该与被测试类的包保持一致。

> 目前只使用的这些功能，待续

# 参考资料

<a href="https://www.cnblogs.com/huaxingtianxia/p/5563111.html" target="_blank">JUnit单元测试--IntelliJ IDEA</a>







