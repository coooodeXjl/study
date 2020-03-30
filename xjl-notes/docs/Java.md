# Java的三大特性

## （1）多态
    
多态分为编译时多态和运行时多态：
   
- 编译时多态主要指方法的重载
- 运行时多态指程序中定义的对象引用所指向的具体类型在运行期间才确定

运行时多态有三个条件：

- 继承
- 覆盖（重写）
- 向上转型

多态的好处：可以消除类型之间的耦合，增加可扩充性，可以使得Java的对象更灵活的调用方法

项目示例代码：
```
public class ReturnItem extends ASTNode {
	
	private Variable aliased;
	private Expression expression;
	private List<AbstractFunction> stringFunctions = new ArrayList<>();
	...
}
```
```
...
    case "left" :
		temp = fic.oC_Expression(1).getText();
		length = Integer.valueOf(temp);
		Left left = new Left(length);
		returnItem.addAbstractFunction(left);
		break;
	case "ltrim" :
		LTrim lTrim = new LTrim();
		returnItem.addAbstractFunction(lTrim);
		break;
...							
```