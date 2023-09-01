# C# 常用语法实现

## 1.交换两个变量值

### 使用临时变量实现

```c#
    static void Main(string[] args)
    {
        int x = 1;
        int y = 2;
        Console.WriteLine("x={0},y={1}",x, y);
        int temp = x;
        x = y;
        y = temp;
        Console.WriteLine("x={0},y={1}", x, y);
        Console.ReadKey();
    }
```

### 使用加减法实现

试想， 1+2=3，我们得到了两数相加的结果3。3-2=1，把1赋值给y，y就等于1; 3-1=2，把2赋值给x，这就完成了交换。

```c#
    static void Main(string[] args)
    {
        int x = 1;
        int y = 2;
        Console.WriteLine("x={0},y={1}",x, y);
        x = x + y; //x = 3
        y = x - y; //y = 1
        x = x - y; //x = 2 
        Console.WriteLine("x={0},y={1}", x, y);
        Console.ReadKey();
    }
```

### 使用ref和泛型方法实现

```c#
        static void Main(string[] args)
        {
            string x = "hello";
            string y = "world";
            Console.WriteLine("x={0},y={1}",x, y);
            Swap<string>(ref x, ref y);
            Console.WriteLine("x={0},y={1}", x, y);
            Console.ReadKey();
        }
        static void Swap(ref int x, ref int y)
        {
            int temp = x;
            x = y;
            y = x;
        }
        static void Swap(ref string x, ref string y)
        {
            string temp = x;
            x = y;
            y = x;
        }
        static void Swap<T>(ref T x, ref T y)
        {
            T temp = x;
            x = y;
            y = temp;
        }
```

### 使用按位异或运算符实现

对于二进制数字来说，当两个数相异的时候就为1， 即0和1异或的结果是1， 0和0，以及1和1异或的结果是0。关于异或等位运算符的介绍在这里：https://www.jb51.net/article/260847.htm

举例，把十进制的3和4转换成16位二进制分别是：

x = 0000000000000011；//对应十进制数字3
y = 0000000000000100; //对应十进制数字4

把x和y异或的结果赋值给x：x = x ^ y;
x = 0000000000000111;

把y和现在的x异或，结果赋值给y：y = y ^ x
y = 0000000000000011;

把现在的x和现在的y异或，结果赋值给x：x = x ^ y
x = 0000000000000100;

按照上面的算法，可以写成如下：

```c#
    static void Main(string[] args)
    {
        int x = 1;
        int y = 2;
        Console.WriteLine("x={0},y={1}",x, y);
        x = x ^ y;
        y = y ^ x;
        x = x ^ y;
        Console.WriteLine("x={0},y={1}", x, y);
        Console.ReadKey();
    }
```