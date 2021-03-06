# Java类的加载顺序

1. 父类静态代码块（包括静态初始化块，静态属性，但不包括静态方法）
2. 子类静态代码块（包括静态初始化块，静态属性，但不包括静态方法）
3. 父类非静态代码块（ 包括非静态初始化块，非静态属性）
4. 父类构造方法
5. 子类非静态代码块（包括非静态初始化块，非静态属性）
6. 子类构造方法

其中：

* 类中静态块按照声明顺序执行，并且1和2不需要调用new类实例的时候就执行了(意思就是在类加载到方法区的时候执行的)
* 其次，需要理解子类覆盖父类方法的问题，也就是方法重写实现多态问题
* 静态代码块：用static申明，JVM加载类时执行，仅执行一次
* 构造代码块：类中直接用{}定义，每一次创建对象时执行 
* 执行顺序优先级：静态代码块 > main() > 构造代码块 > 构造方法