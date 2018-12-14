# 随笔

1. 如果一个移动的游戏对象不具有刚体组件，那么游戏对象的碰撞器就不会随游戏对象移动，而具有刚体组件的游戏对象在移动时，它本身以及它的所有子对象的碰撞器将逐帧更新

2. 在C#中，一个属性访问它就会运行其中的get{}语句

3. 冻结了刚体组件的旋转，但如果isKinematic设置为true，仍然可以手动设置刚体的旋转角度(isKinematic=true表示刚体会被物理系统跟踪，但由于Rigibody.velocity的关系，它不会自动移动）如果启用了isKinematic，则力，碰撞或关节将不再影响刚体，但是可以影响到其他的非运动刚体。

4. Unity中的父类和子类:子类继承父类后 如果需要父类的Update方法则要把自己的Update()方法删掉，否则会执行自己的Update()函数，private 修饰的父类Update()方法子类依然可以调用

5. InvokeRepeating()是Unity内置的一个函数，用于对同一函数进行重复调用。函数第一个参数是一个字符串，表示要调用的函数名称，第二个参数设置首次调用该函数的时间间隔，最后一个参数是之后调用该函数的时间间隔。

6. 球状碰撞器的直径将取变换组件中三个维度的最大值

7. 当一个维度的长度远大于其他维度时，也可以使用胶囊状碰撞器。网格碰撞器可以与物体轮廓相吻合，但运行速度比其他碰撞器要慢很多。在高性能计算机上这可能不是什么问题，但在IOS或Android等移动平台上，网格碰撞器的速度通常会很慢。

8. 当在Unity中导入一个dll文件时报错时，在项目面板中点击dll文件可以看到报错信息，可能是支持的.NET版本不同。在Unity中的File->Build Settings->Player Settings->Other Settings中的Configuration下的Scripting Runtime Version中修改成.NET 4.x 即可。当然也可以在VS中修改类库的.NET版本，在右键选择属性 -> 应用程序，将目标框架改为 .NET Framework 3.5或以下，然后重新生成dll导入。

   ![Unity中修改](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img1.png)

   ![VS中修改](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img2.png)

9. 在Unity中使用Protobuf实现数据转换：

   首先从Github上下载protobuf源码

   [选择csharp的版本]https://github.com/protocolbuffers/protobuf/releases

   解压之后进入工程目录下的csharp/src/下，用VS打开Google.Protobuf.sln，右键Google.Protobuf生成，之后会在Google.Protobuf\bin\Debug\net45目录下生成dll文件(也可能不是net45，取决于项目支持的.NET版本)

   接下来准备编译器，编译器是用来将.proto文件编译成相应语音脚本的工具， 编译器可以直接从GitHub上下载

   [Github上下载proto-3.6.1-win32.zip]https://github.com/protocolbuffers/protobuf/releases

   下载解压后会在bin目录下有protoc.exe

   实现protobuf数据转换：

   1. 编写一个.proto文件(syntax是你下载的proto语法版本,有proto2和proto3，package是包名，在Unity中引用的时候就是该名称，message相当于一个类，1，2，3不代表值，代表参数标签，repeated可以理解为数组)

      ![person.proto](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img3.png)

   2. 在cmd窗口下将刚才的.proto文件编译成.CS文件

      ![命令台截图](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img4.png)

      ![执行命令之后](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img5.png)

      --proto_path 指定要编译的.proto文件路径 （相对路径）
      --csharp_out 输出cs文件路径（相对路径）

      [更多proto语法，命令]: https://developers.google.com/protocol-buffers/docs/proto3

   3. 将上面生成的Google.Protobuf.dll 和 Person.cs文件导入到Unity中并测试

      ![Unity测试脚本](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img6.png)

      ![运行结果](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img7.png)

   [为什么要使用Protobuf见腾讯游戏学院]: https://gameinstitute.qq.com/course/detail/10091

10. 当在vs中创建Web项目时弹出：无法创建虚拟目录，无法读取配置文件，需要在IIS中手动创建此虚拟目录才能打开此项目。的窗口时，是因为此电脑下的IISExpress快捷方式无效，去Documents下删除无效的IISExpress快捷方式即可解决。

11. C#在变量之间有一个基本区分，把类型级别声明的变量看作字段，而把在方法中声明的变量看作局部变量。在类中声明的变量(字段)会被方法中声明的同名局部变量隐藏，所以取得值是局部变量的。

12. 常量是类似 ```const int a =100; ```常量必须在声明时初始化，常量的值必须在编译时用于计算，常量总是静态的(不必包含修饰符```static```，实际上也不允许)

13. 在C#中，“函数成员”不仅包含方法，也包含类或结构的一些非数据成员，如索引器、运算符、构造函数和析构函数等，甚至还有属性(属性与字段的区别:属性是有get,set方法的)，字段、常量和事件才是数据成员

14. 可变参数(params关键字)与可选参数的区别：

    可变参数：

    1. 使用 params关键字可以指定一个方法参数,该方法参数的数目可变。
    2. 可以发送参数声明中所指定类型的逗号分隔的参数列表或指定类型的参数数组。 还可以不发送参数。 如果未发送任何参数，则 params列表的长度为零。
    3. 在方法声明中的 params关键字之后不允许任何其他参数，并且在方法声明中只允许一个 params关键字。

    可选参数：

      1.参数是可选的，但必须为可选参数提供默认值，而且必须是方法定义的最后一个参数。

15. C#重载方法的参数有一些小限制：两个方法不能仅在返回类型上有区别，两个方法不能仅根据参数是声明为```ref```还是```out```来区分

16. as运算符用于执行**引用类型**的显示类型转换，如果要转换的类型与指定的类型兼容，转换就会成功进行，如果不兼容，as运算符就会返回null值

17. 如果对复杂类型(和非基本类型)使用sizeof运算符，就需要把代码放在unsafe块中

    ```unsafe{Console.WriteLine(sizeof(Customer))}```

18. ```typeof```运算符返回一个表示特定类型的```System.Type```对象，如```typeof(string)```返回表示```System.String```类型的Type对象。在使用反射技术动态查找对象的相关信息时很有用。

19. 可空类型如```int? a = null```，但是在比较可空类型时，只要有一个操作数为null，比较结果就是false。**即不能因为一个条件是false，就认为该条件的对立面为true**，例如：

    ```c#
    int? x = null;
    int? y = a + 4;// y = null
    
    int? a = null;
    int? b = -5;
    if(a >= b)
        Console.WriteLine("a >= b");
    else
        Console.WriteLine("a < b");
    ```

20. 空合并运算符```(??)```，可以在处理可空类型和引用类型时表示null可能的值。**这个运算符要放在两个操作数之间，第一个操作数必须是一个可空类型或引用类型；第二个操作数必须与第一个操作数的类型相同，或者可以隐含地转换为第一个操作数的类型。**

    计算规则为：如果第一个操作数不是null，整个表达式就等于第一个操作数的值。如果第一个操作数是null，整个表达式就等于第二个操作数的值。

    ```C#
    int? a = null;
    int b;
    
    b = a ?? 10;//b has the value 10
    a = 3;
    b = a ?? 10;//b has the value 3
    ```

21. 可空类型隐示地转换为其他可空类型，应遵循非可空类型的转换规则，即```int?```隐式地转换为```long?```、```float?```、```double?```、和```decimal?```。

    非可空类型隐式地转换为可空类型也遵循非可空类型的转换规则，即```int?```隐式地转换为```long?```、```float?```、```double?```、和```decimal?```。

    可空类型不能隐式地转换为非可空类型，必须进行显式转换。

22. 拆箱时要确保得到的值变量有足够的空间存储拆箱的值中的所有字节。

23. C#不允许重载“=”，但如果重载“+”运算符，编译器就会自动使用“+”运算符的重载来执行“+=”运算符的操作

24. C#要求成对重载比较运算符，且比较运算符必须返回布尔类型的值。

25. 用户定义的类型强制转换：类似于重载运算符，也必须同时声明```public```和```static```。例：

    ```C#
    //这里的implicit关键字用于声明隐式用户定义的类型转换运算符。如果保证转换不会导致数据丢失，则使用它来启用用户定义类型与其他类型之间的隐式转换。
    //也可以指定explicit关键字，它声明了必须使用强制转换调用的用户定义的类型转换运算符。
    //运算符的返回类型定义了类型强制转换操作的目标类型(float既是目标类型，也是返回类型)
    //如果数据类型转换声明为隐式(implicit)，编译器就可以隐式或显式地使用这个转换，如果数据类型转换声明为显式(explicit)，编译器就只能显式的使用它。
    public static implicit operator float (Currency value){
        
    }
    ```

26. 类之间的类型强制转换：

    1. 如果某个类派生自另一个类，就不能定义这两个类之间的类型强制转换(这些类型的类型转换已经存在)
    2. 类型强制转换必须在源数据类型或目标数据类型的内部定义
    3. 一旦在一个类的内部定义了类型强制转换，就不能在另一个类中定义相同的类型强制转换。

27. 装箱和拆箱数据类型强制转换：不能从结构或基元值类型中派生。所以基本结构和派生结构之间的强制转换总是基元类型或结构与```System.Object```之间的转换(理论上可以在结构和```System.ValueType```之间进行强制转换，但一般很少这么做)

    ```C#
    object derivedObject = new Currency(40,0);
    object baseObject = new object();
    Currency derivedCopy1 = (Currency)derivedObject;// OK
    Currency derivedCopy2 = (Currency)baseObject;	//Exception thrown
    //第一种可以成功，第二种会失败，因为baseObject没有引用已装箱的Currency对象
    ```

28. .NET MVC下使用```$.ajax({})```访问```Controller```不能通过```Return RedirectToAction(ActionName,ControllerName)```来跳转**视图(View)**，它所返回的将是对应```Action```返回```View```的```text(在浏览器F12下可以打印返回的信息，发现是一个Html页面的源码)```，不能真正的跳转到对应的界面，但是可以通过返回对应```View```或者```Controller```的```Url```在```ajax```的```success```方法中使用```window.locaion.href```来进行跳转。而form表单的Action以及Razor中的```@Html.BeginForm```是可以在Controller实现跳转```View```的。

29. 跳转页面一般不传递集合或一个对象而是一个ID或者简单的数据，因为传递集合时如果数据库中的数据修改了，这个集合传的数据就是错误的，还可能网络带宽的问题，要节省带宽。所以一般传递一个ID之后再在对应的视图再查询一遍这个对象。

30. C#中的Interface中接口声明默认是public的，所以不能对接口中的抽象方法或属性使用public关键字，同时接口中不能声明**字段**但是可以声明**属性**，接口成员不能有 new、static、abstract、override、virtual 修饰符。有一点要注意，当一个接口实现一个接口，这2个接口中有相同的方法时，可用 new 关键字隐藏父接口中的方法。**接口中只能包含方法、属性、事件和索引的组合**。

31. 索引器是一种语法上的遍历，最常见以类型实现，其主要目的是封装内部集合或数组。例如：假设有一个TempRecord表示Farenheit温度的类，在24小时内以10个不同的时间记录。该类包含一个用于存储温度值temps的类型数组float[]。通过在此类中实现索引器，客户端可以访问TempRecord实例中的温度```float temp = tr[4]```而不是```float temp = tr.temps[4]```。索引器表示法不仅简化了客户端应用程序的语法; 它还使该类及其目的更直观，供其他开发人员理解。**要在类或结构上声明索引器，要使用this关键字：```public int this[index]{   //get and set 访问器}```

32. C#中的委托和事件，事件可以理解为类似声明一个进行了封装的委托类型的变量，但在类的内部，不管你用public修饰event还是用protected修饰event，它总是private，在声明委托的时候不能使用static关键字，而声明委托和声明类型类似，可以在后面创建委托变量的时候像类型一样使用。下面代码块第二行和第十行。

    ```C#
     	//委托类型
        public delegate void TestDelegate();
        delegate void CustomizeEvent(NotImpEventArgsClass e);
    	//加泛型则不会在使用系统的EvnetHandler<TEventArgs>
        public delegate void EventHandler();
    
        class Program
        {
            //委托变量
            public static TestDelegate testDelegate;
            //自定义事件
            public static event TestDelegate TestEvent;
            public static event CustomizeEvent ce;
            public static event EventHandler ee;
            //符合.NET FrameWork编码规范的事件，这里的EventArgs可以是任意其它类型
            //这里的泛型类型作用就是存储事件要处理的数据类
            //系统的EventHandler<TEventArgs>定义为： 
            //public delegate void EventHandler<TEventArgs>(object sender, TEventArgs e);
            //也可以不使用系统的EventHandler<TEventArgs>，可以自己写一个EventHandler<T>，但是在当前类中就会使用自己写的EventHandler<T>，如果没有写成EventHandler<T>而是EventHandler则不会影响。
            private static EventHandler<EventArgs> newEvent;
            //写成属性类似的方式就不能使用NewEvent(sender,e)这种，只能使用它对应的字段newEvent
            public static event EventHandler<EventArgs> NewEvent
            {
                add { newEvent += value; }
                remove { newEvent -= value; }
            }
            public static event EventHandler<EventArgs> Another;
    
            static void Main(string[] args)
            {
                testDelegate += Function;
                testDelegate();
    
                TestEvent += Function1;
                TestEvent();
    
                NewEvent += Function2;
                Another += Function2;
    
                //.NET FrameWork自带的泛型委托EventHandler<TEventArgs>要求传递两个参数
                //第一个参数为object类型,第二个参数为泛型TEventArgs
                newEvent(newEvent, new TestEventArgs());
                Another(Another.GetType(), new EventArgs());
    
                ce += Function3;
                ce(new NotImpEventArgsClass());
    
                ee += Function1;
                
                Console.ReadLine();
            }
    
            public static void Function()
            {
                Console.WriteLine("Function 自定义委托");
            }
    
            public static void Function1()
            {
                Console.WriteLine("Function1 使用自定义事件");
            }
    
            public static void Function2(object sender,EventArgs e)
            {
                Console.WriteLine("Function2 使用.NET规范的事件");
            }
    
            public static void Function3(NotImpEventArgsClass customize)
            {
                Console.WriteLine("Function3 使用自定义事件");
            }
        }
    
        class NotImpEventArgsClass
        {
    
        }
    
        class TestEventArgs : EventArgs
        {
    
        }
    ```

33. 在Linux上装好```redis```之后要去```redis.conf```中修改```daemonize``` 为```yes```(在vim编辑器中敲/进入查询模式，敲n查找下一个，N查找上一个)，```redis server```就可以后台启动了，启动```redis```服务可以在```redis-server```可执行文件目录下(一般在```src```目录下)输入```./redis-server ../redis.conf```(要使用配置文件启动)，启动之后就可以使用```./redis-cli```进入了，使用```./redis-cli SHUTDOWN```关闭```redis-server```

    ![运行结果](https://raw.githubusercontent.com/qiqiqidalao/qiqiqidalao.github.io/master/images/img8.png)

34. 不是所有查询都可以用LINQ查询语法完成，也不是所有的扩展方法都映射到LINQ查询子句上。高级查询要使用扩展方法。不能使用LINQ查询的一个例子是Where()方法的重载，在Where方法的重载中，可以传递第二个参数——索引。该索引是被执行查询的集合的索引。可以在表达式中使用这个索引，执行基于索引的计算

    ```C#
    List<Person> people = new List<Person> {
    	new Person { Name = "张三", Age = 29 },
    	new Person { Name = "李四", Age = 39 },
    	new Person { Name = "王五", Age = 22 },
    	new Person { Name = "王二", Age = 29 }
    };
    //两种写法的效果一样
    var useLinq = from p in people
    	where p.Age < 30
    	select p.Name;
    var useExtendMethod = people.Where(p => p.Age < 30).Select(p => p.Name);
    //Where的重载方法，筛选年龄小于30且索引为偶数的人，索引index是people集合中的索引，不是筛选后的索引
    var res = people.Where((p, index) => p.Age < 30 && index % 2 == 0).Select(p => p.Name);
    ```

