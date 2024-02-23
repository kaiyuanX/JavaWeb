- [随机数](#随机数)
- [常用 API](#常用-api)
  - [import PackageName](#import-packagename)
  - [String](#string)
      - [构造](#构造)
      - [方法](#方法)
      - [注意事项](#注意事项)
  - [StringBuilder](#stringbuilder)
  - [ArrayList](#arraylist)
      - [方法](#方法-1)
  - [Object](#object)
      - [toString](#tostring)
      - [equals](#equals)
  - [Objects](#objects)
  - [Math](#math)
  - [BigDecimal](#bigdecimal)
  - [System](#system)
  - [包装类](#包装类)
      - [创建](#创建)
      - [类型转换](#类型转换)
      - [进制转换](#进制转换)
  - [Arrays](#arrays)
      - [基本使用](#基本使用)
      - [操作对象数组](#操作对象数组)
  - [正则表达式](#正则表达式)
      - [信息爬取](#信息爬取)
  - [时间](#时间)
      - [Date](#date)
      - [SimpleDateFormat](#simpledateformat)
      - [Calendar](#calendar)
      - [为什么 JDK8 要新增日期类](#为什么-jdk8-要新增日期类)
      - [LocalDateTime](#localdatetime)
      - [Instant](#instant)
      - [ZoneId, ZonedDateTime](#zoneid-zoneddatetime)
      - [DateTimeFormatter](#datetimeformatter)
      - [Period, Duration, ChronoUnit](#period-duration-chronounit)
- [容器](#容器)
  - [Collection](#collection)
      - [常用方法](#常用方法)
      - [遍历](#遍历)
  - [List](#list)
      - [List 集合的常用方法](#list-集合的常用方法)
      - [List 集合的遍历方式](#list-集合的遍历方式)
      - [LinkedList](#linkedlist)
  - [Set](#set)
  - [HashSet](#hashset)
      - [HashSet 集合底层原理](#hashset-集合底层原理)
      - [HashSet 去重原理](#hashset-去重原理)
      - [LinkedHashSet](#linkedhashset)
  - [TreeSet](#treeset)
  - [Collections](#collections)
  - [Map](#map)
      - [概述](#概述)
      - [常用方法](#常用方法-1)
      - [遍历](#遍历-1)

# 随机数

在 JDK 中提供了一个类叫做 `Random`

```java
// 使用方法跟 Scanner 一样

// 1、导包
import java.util.Random;

public class RandomDemo1 {
    public static void main(String[] args) {

        // 2、创建一个 Random 对象
        Random r = new Random();

        // 3、调用 Random 的方法 nextInt()
        int data = r.nextInt(10); // 得到 [0,9] 的随机数
        System.out.println(data);
    }
}
```

# 常用 API

[API](./assets/JDk_API)

Application Program Interface

## import PackageName

一个包中可以放多个类文件

调包的条件

- 同一个包下的 `class`，互相可以直接调用
- 当前程序要调用其他包下的 `class`，则必须导包
- 调用 `Java.lang` 包下的 `class`，不需要我们导包的

`import PackageName.*;`
`import PackageName.ClassaName;`

## String

不可变的字符序列

在 `java.lang` 包中

#### 构造

```java
// 1、直接双引号得到字符串对象
String name = "666";

// 2、new String() 创建字符串对象，并调用构造器初始化字符串 
new String();
new String(String s);
new String(char[] s);
new String(byte[] s);
```

#### 方法

```java
// 1、获取字符串的长度
s.length();

// 2、提取字符串中某个索引位置处的字符
char c = s.charAt(1);

// 3、把字符串转换成字符数组
char[] chars = s.toCharArray();

// 4、判断字符串内容，内容一样就返回 true
s1 == s2;  // 这个只能比较地址
s1.equals(s2); 

// 5、忽略大小写比较字符串内容
s1.equalsIgnoreCase(s2);

// 6、截取字符串内容 (包前不包后的)
s1 = s2.substring(beginIndex, endIndex)
s1 = s2.substring(beginIndex);

// 8、把字符串中的某个内容替换成新内容
s2 = s1.replace(oldCharSequence, newCharSequence);

// 9、判断字符串中是否包含某个关键字
s.contains(CharSequence)

// 10、把字符串按照某个指定内容分割成多个字符串，放到一个字符串数组中返回给我们
split(String regex, int limit)
- regex : 定界正则表达式
- limit : 控制模式应用的次数
```

#### 注意事项


1. String 类的对象是不可变的对象
   - `s = "fuck"` 实际上是新创建了一个 `String` 再把这个它赋给 `s`
   - 只是 `s` 指向的地址变了，`s` 指向的原地址的内容没变

2. 两种构造的区别
   - 通过 `new` 方式创建字符串对象，每 `new` 一次都会产生一个新的对象放在堆内存中
   - 以 `" "` 方式写出的字符串对象，会在堆内存中的字符串常量池中存储，且相同内容的字符串只存储一份

```java
s1="abc",s2="abc";
s1 == s2 // true
```

## StringBuilder

线程不安全的可变的字符序列，高效地做字符串拼接


在 `java.lang` 中

```java
StringBuilder sb = new StringBuilder()

sb.append(sth);

// 转换
sb.toString();
StringBuilder sb = new StringBuilder(String s)
```

> StringBuffer 线程安全的可变的字符序列


## ArrayList

ArrayList 是大小可变的数组

`java.util`

#### 方法

想要使用 ArrayList 存储数据，并对数据进行操作：

- 创建 ArrayList 容器对象
  - 空参数构造方法 `ArrayList<String> a = new ArrayList()`

- 第二步：调用 ArrayList 类的常用方法对容器中的数据进行操作。常用方法如下：

```java
// 1、创建一个 ArrayList 的集合对象
// ArrayList<String> list = new ArrayList<String>();
// 从 jdk_7 开始支持下面的构造
ArrayList<String> list = new ArrayList<>();

list.add("xxx");

// 2、往集合中的某个索引位置处添加一个数据
list.add(n, "xxx");

// 3、根据索引获取集合中某个索引位置处的值
list.get(n);

// 4、获取集合的大小
list.size();

// 5、根据索引删除集合中的某个元素值，返回被删除的元素值
list.remove(n);

// 6、删除某个元素值，删除成功会返回 true
list.remove("Java");

// 7、修改某个索引位置处的数据，修改后会返回原来的值给我们
list.set(n, "xxx");
```

## Object

Object 类是 Java 中所有类的祖宗类

#### toString

```java
public String toString()

默认返回字符串的格式是：“包名.类名@哈希值16进制”

支持 @Override
```

#### equals

```java
public boolean equals(Object obj)

判断此对象与参数对象是否 "相等"

主要还是 @Override 后才有意义（idea 用 generate 生成）
```

```java
if(obj instanceof xx){}
```

## Objects

Objects 是一个工具类，提供了一些方法可以对任意对象进行操作


```java
public static boolean equals(Object a, Object b) // 依然依赖于 Override
public static boolean isNull(Object a)      // a == NULL
public static boolean nonNull(Object a)    // a!=NULL
```

## Math

1. `public static int abs(int a)`：取绝对值 (double 也行)
2. `public static double ceil(double a)`: 向上取整
3. `public static double floor(double a)`: 向下取整
4. `public static long round(double a)`：四舍五入
5. `public static int max/min(int a, int b)`：取最大/小值
6. `public static double pow(double a, double b)`：取次方
7. `public static double random()`： 取随机数 $[0.0 , 1.0)$


## BigDecimal

为了解决计算精度损失的问题，Java 给我们提供了 BigDecimal 类


- 把浮点型数据封装成 `BigDecimal` 对象，再来参与运算
  - `public BigDecimal(double val)` 不推荐使用这个
  - `public BigDecimal(String val)` 
  - `public static BigDecimal valueOf(double val)` 

- `public BigDecimal add(BigDecimal augend)` 加法
- `public BigDecimal subtract(BigDecimal augend)` 减法
- `public BigDecimal multiply(BigDecimal augend)` 乘法
- `public BigDecimal divide(BigDecimal b)` 除法
- `public BigDecimal divide(BigDecimal b, Scale, RoundingMode)` 除法
- `public double doubleValue()` 把 `BigDecimal` 对象又转换成 `double` 类型的数据

## System

这是系统类，提供了一些获取获取系统数据的方法

`public static void exit(int status)`

- 终止当前运行的 Java 虚拟机
- 该参数用作状态代码; 按照惯例，非零状态代码表示异常终止

`public static long currentTimeMillis()`

- 获取当前系统的时间
- 返回的是 long 类型的时间 ms
  - 从 `1970-1-1 0:0:0` 开始走到此刻的总的 ms

`public static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length)`

- 数组拷贝

## 包装类

把 8 种基本数据类型变成对象

| 基本数据类型 | 包装类    |
| ------------ | --------- |
| byte         | Byte      |
| short        | Short     |
| int          | Integer   |
| long         | Long      |
| char         | Character |
| float        | Float     |
| double       | Double    |
| boolean      | Boolean   |

主要学习两点：

- 创建包装类的对象方式、自动装箱和拆箱的特性；
- 利用包装类提供的方法对字符串和基本类型数据进行相互转换

#### 创建

我们先来学习，创建包装类对象的方法，以及包装类的一个特性叫自动装箱和自动拆箱

```java
Integer b = Integer.valueOf(10);

// 自动装箱的写法
Integer c = 10;
// 自动拆箱
int d = c;
```

```java
// 装箱和拆箱在使用集合时就有体现
ArrayList<Integer> list = new ArrayList<>();
// 添加的元素是基本类型，实际上会自动装箱为 Integer 类型
list.add(100);
// 获取元素时，会将 Integer 类型自动拆箱为 int 类型
int e = list.get(0);
```

#### 类型转换

在开发中，经常使用包装类对字符串和基本类型数据进行相互转换

- 把 “字符串” 转换为 “基本类型”：`包装类.parseXxx(字符串)`

```java
public static int parseInt(String s)

把 String 转换为 int
```

- 将 “基本类型” 转换为 “字符串”：`包装类.valueOf(数据)`

```java
public static String valueOf(int a)

把 int 转换为 String
```

- 测试

```java
// 把 String 转换为 int
String ageStr = "29";
int age1 = Integer.parseInt(ageStr);

String scoreStr = 3.14;
double score = Double.prarseDouble(scoreStr);

// 把基本类型数据转换为 String
Integer a = 23;
String s1 = Integer.toString(a);
String s2 = a.toString();
String s3 = a + "";
String s4 = String.valueOf(a);
```

#### 进制转换

`public static String toBinaryString(int i)` 2
`public static String toOctalString(int i)` 8
`public static String toHexString(int i)` 16

## Arrays

#### 基本使用

Arrays 是操作 “数组” 的工具类

```java
public static String toString(arr); // 遍历数组

public static boolean equals(arrA, arrB);

public static int binarySearch(arr, int key);

public static void sort(arr);
```

#### 操作对象数组

如果数组中存储的元素类型是自定义的对象，如何排序呢？

首先我们要准备一个 Student 类，代码如下：

```java
public class Student implements Comparable<Student>{
    private String name;
    private double height;
    private int age;
	
    public Student(String name, double height, int age) {
        this.name = name;
        this.height = height;
        this.age = age;
    }

	@Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", height=" + height +
                ", age=" + age +
                '}';
    }
}

```

然后再写一个测试类，代码如下，运行代码会报错的

```java
public class ArraysTest2 {
    public static void main(String[] args) {
        
        // 往数组中存储 4 个学生对象
        Student[] students = new Student[4];
        students[0] = new Student("蜘蛛精", 169.5, 23);
        students[1] = new Student("紫霞", 163.8, 26);
        students[2] = new Student("紫霞", 163.8, 26);
        students[3] = new Student("至尊宝", 167.5, 24);

        // 排序，会报错
		Arrays.sort(students);
		System.out.println(Arrays.toString(students));
    }
}
```

报错原因 Arrays 就不知道按照什么规则进行排序

为了让 Arrays 知道按照什么规则排序，我们有如下的两种办法：

1. 让 Student 类实现 Comparable 接口，同时重写 compareTo 方法

```java
public class Student implements Comparable<Student>{
    private String name;
    private double height;
    private int age;
    
    //...get、set、空参数构造方法、有参数构造方法...自己补全

    // 指定比较规则
    // this  o
    @Override
    public int compareTo(Student o) {
        // 约定1：认为左边对象 大于 右边对象 请您返回正整数
        // 约定2：认为左边对象 小于 右边对象 请您返回负整数
        // 约定3：认为左边对象 等于 右边对象 请您一定返回0
		/* if(this.age > o.age){
            return 1;
        }else if(this.age < o.age){
            return -1;
        }
        return 0;*/

        //上面的if语句，也可以简化为下面的一行代码
        return this.age - o.age; // 按照年龄升序排列
        // return o.age - this.age; // 按照年龄降序排列
    }
    
    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", height=" + height +
                ", age=" + age +
                '}';
    }
}
```

2. 调用 `Arrays.sort(arr, Comparator);`，除了传递数组之外，传递一个 Comparator 比较器对象
   - Arrays 的 sort 方法底层会根据 Comparator 比较器对象的 compare 方法的返回值来判断大小

```java
public class ArraysTest2 {
    public static void main(String[] args) {
        // 目标：掌握如何对数组中的对象进行排序。
        Student[] students = new Student[4];
        students[0] = new Student("蜘蛛精", 169.5, 23);
        students[1] = new Student("紫霞", 163.8, 26);
        students[2] = new Student("紫霞", 163.8, 26);
        students[3] = new Student("至尊宝", 167.5, 24);

		// 2、public static <T> void sort(T[] arr, Comparator<? super T> c)
        // 参数一：需要排序的数组
        // 参数二：Comparator比较器对象（用来制定对象的比较规则）
        Arrays.sort(students, new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                // 制定比较规则了：左边对象 o1   右边对象 o2
                // 约定1：认为左边对象 大于 右边对象 请您返回正整数
                // 约定2：认为左边对象 小于 右边对象 请您返回负整数
                // 约定3：认为左边对象 等于 右边对象 请您一定返回0
//                if(o1.getHeight() > o2.getHeight()){
//                    return 1;
//                }else if(o1.getHeight() < o2.getHeight()){
//                    return -1;
//                }
//                return 0; // 升序
                 return Double.compare(o1.getHeight(), o2.getHeight()); // 升序
                // return Double.compare(o2.getHeight(), o1.getHeight()); // 降序
            }
        });
        System.out.println(Arrays.toString(students));
    }
}
```

## 正则表达式

`boolean matches(String regex)` 这个方法时属于类 String

![1667469259345](assets/1667469259345.png)

一些应用

- `public String replaceAll(String regex, String newStr)`
- `public String[] split(String regex)`

#### 信息爬取

```java
// 1. 爬取规则
String regex = "xxx";

// 2. 把 regex 封装成一个 Pattern 对象
Pattern pattern = Pattern.compile(regex);

// 3. 通过 Pattern 的对象获取匹配器
Matcher matcher = pattern.matcher(data);

// 4.  循环遍历匹配
while (matcher.find())
{
    matcher.group();
}
```

## 时间


#### Date

Date 对象记录的时间是用毫秒值来表示的

Java 语言规定，`1970年1月1日0时0分0秒` 认为是时间的起点，此时记作 0，那么 1000 就表示 `1970年1月1日0时0分1秒`

“构造方法”

```java
public Date() // 返回当前时间
```

#### SimpleDateFormat

SimpleDateFormat 类: Date 与 String 之间的映射

```java
public final String format(Date date);   // Date 格式化为 String
public final Date parse(String source);  // 将 String 解析为 Date
```

```java
// 更多见 API 相关文档

字母	   表示含义
yyyy	年
MM		月
dd		日
HH		时
mm		分
ss		秒
SSS		毫秒
```

```java
public class Test2SimpleDateFormat {
    public static void main(String[] args) throws ParseException {
        // 1.
        // 准备一些 Date
        Date time = new Date();

        // 创建 SimpleDateFormat 对象指定格式
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd- HH:mm:ss EEE a");

        // 格式化
        String result = sdf.format(time);

        // 2.
        // 准备一些 String
        String dateStr = "2022-12-12 12:12:11";

        // 指定格式
        SimpleDateFormat sdf2 = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");

        // 解析
        Date result = sdf2.parse(dateStr);
    }
}
```

#### Calendar

```java
public class Test4Calendar {
    public static void main(String[] args) {

        // 1. 得到 Calendar 对象
        Calendar now = Calendar.getInstance();

        // 2. 获取 Calendar 中的某个信息
        //    诸如 Calendar.YEAR 是 Calendar 中的静态常量
        //    更多见手册
        int year = now.get(Calendar.YEAR);
        int days = now.get(Calendar.DAY_OF_YEAR);

        // 3. 拿到 Calendar 中的 Date 对象
        Date d = now.getTime();

        // 4. 拿到时间毫秒值
        long time = now.getTimeInMillis();

        // 5. 重置 Calendar 中的某个信息
        now.set(Calendar.MONTH, 9);         // 修改月份成为 10 月份
        now.set(2026, 11, 22);              // 改为 2026.11.22

        // 6. 修改
        now.add(Calendar.DAY_OF_YEAR, 100);
        now.add(Calendar.DAY_OF_YEAR, -10);

        // 7. Calendar 与 Date
        Date x = new Date();
        now.setTime(x);
    }
}
```

#### 为什么 JDK8 要新增日期类

传统的时间类（Date、SimpleDateFormat、Calendar）存在如下问题：
1. 设计不合理，使用不方便，很多都被淘汰了
2. 都是可变对象，修改后会丢失最开始的时间信息
3. 线程不安全
4. 不能精确到纳秒，只能精确到毫秒

#### LocalDateTime

表示日期时间，下面的 3 类用法雷同

- LocalDate
  - 日期

- LocalTime
  - 时间

- LocalDateTime
  - 日期和时间

```java
public class Test3_LocalDateTime {
    public static void main(String[] args) {
        // 0、获取本地日期和时间
        LocalDateTime ldt = LocalDateTime.now(); // 年 月 日 时 分 秒 纳秒
                                                // LocalDateTime.of(...)

        // 1、可以获取日期和时间的信息
        int year = ldt.getYear(); // 年
        int month = ldt.getMonthValue(); // 月
        int day = ldt.getDayOfMonth(); // 日
        int dayOfYear = ldt.getDayOfYear();  // 一年中的第几天
        int dayOfWeek = ldt.getDayOfWeek().getValue();  // 获取是周几
        int hour = ldt.getHour(); //时
        int minute = ldt.getMinute(); //分
        int second = ldt.getSecond(); //秒
        int nano = ldt.getNano(); //纳秒

        // 2、修改时间信息：
        // withYear withMonth withDayOfMonth withDayOfYear withHour
        // withMinute withSecond withNano
        LocalDateTime ldt2 = ldt.withYear(2029);
        LocalDateTime ldt3 = ldt.withMinute(59);

        // 3、加多少:
        // plusYears  plusMonths plusDays plusWeeks plusHours plusMinutes plusSeconds plusNanos
        LocalDateTime ldt4 = ldt.plusYears(2);
        LocalDateTime ldt5 = ldt.plusMinutes(3);

        // 4、减多少：
        // minusDays minusYears minusMonths minusWeeks minusHours minusMinutes minusSeconds minusNanos
        LocalDateTime ldt6 = ldt.minusYears(2);
        LocalDateTime ldt7 = ldt.minusMinutes(3);

        // 5、获取指定日期和时间的 LocalDateTime 对象：
        //    public static LocalDateTime of(
        //                                int year, Month month, int dayOfMonth, int hour,
        //                                int minute, int second, int nanoOfSecond)
        LocalDateTime ldt8 = LocalDateTime.of(2029, 12, 12, 12, 12, 12, 1222);

        // 6、 判断 2 个对象，是否相等，在前还是在后： equals、isBefore、isAfter
        System.out.println(ldt1.equals(ldt2));
        System.out.println(ldt1.isAfter(ldt2));
        System.out.println(ldt1.isBefore(ldt2));

        // 7、把 LocalDateTime 转换成 LocalDate 和 LocalTime
        // public LocalDate toLocalDate()
        // public LocalTime toLocalTime()
        // public static LocalDateTime of(LocalDate date, LocalTime time)
        LocalDate ld = ldt.toLocalDate();
        LocalTime lt = ldt.toLocalTime();
        LocalDateTime ldt_ = LocalDateTime.of(ld, lt);

    }
}
```

#### Instant

Instant 对象可以拿到时间戳，替代 Date

- 该时间由两部分组成：从 `1970-01-01 00:00:00` 开始走到此刻的总秒数
- 精确到纳秒

作用：可以用来记录代码的执行时间，或用于记录用户操作某个事件的时间点

```java
public class Test5_Instant {
    public static void main(String[] args) {
       // 1、创建 Instant 的对象，获取此刻时间信息
        Instant now = Instant.now();

        // 2、获取总秒数
        long second = now.getEpochSecond(); // 单位：秒

        // 3、纳秒数
        int nano = now.getNano();

        // ... 

        // Instant 对象的作用：做代码的性能分析，或者记录用户的操作时间点
        // start
        Instant start = Instant.now();
        // 代码执行
        Instant end = Instant.now();
        // end
    }
}
```

#### ZoneId, ZonedDateTime

- ZoneId 代表时区
- ZonedDateTime 带有时区的时间

```java
// ZoneId
static Set<String> getAvailavleZoneIds();   // 所有支持时区
static ZoneId systemDefault();  // 获取系统默认时区
static ZoneId of(String xx);    // 指定一个时区
```

```java
// 为 Instant 设置时区，返回 ZonedDateTime 对象 (带有时区的时间)

ZonedDateTime z = Instant.now().atZone(ZoneId.systemDefault());
```

#### DateTimeFormatter

代替了原来的 SimpleDateFormat 类，线程安全

```java
public class Test6_DateTimeFormatter {
    public static void main(String[] args) {
        // 1、创建一个日期时间格式化器对象出来
        DateTimeFormatter formatter = 
                            DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");

        // 2、对时间进行格式化
        LocalDateTime now = LocalDateTime.now();
        String rs = formatter.format(now); // 正向格式化

        // 3、格式化时间，其实还有一种方案
        String rs2 = now.format(formatter); // 反向格式化

        // 4、解析时间：解析时间一般使用 LocalDateTime 提供的解析方法来解析
        String dateStr = "2029-12-12 12:12:11";
        LocalDateTime ldt = LocalDateTime.parse(dateStr, formatter);
    }
}
```

#### Period, Duration, ChronoUnit

计算两个时间点的时间间隔

- Period 用来计算日期间隔（年、月、日）
  - `LocalDate`
- Duration 用来计算时间间隔（时、分、秒、纳秒）
  - `LocalTime、LocalDateTime、Instant`
- ChronoUnit

```java
// Period

LocalDate start = LocalDate.of(2029, 8, 10);
LocalDate end = LocalDate.of(2029, 12, 15);

// 1、创建 Period 对象，封装两个日期对象
Period period = Period.between(start, end);

// 2、通过 period 对象获取两个日期对象相差的信息
period.getYears();
period.getMonths();
period.getDays();
```

```java
// Duration

LocalDateTime start = LocalDateTime.of(2025, 11, 11, 11, 10, 10);
LocalDateTime end = LocalDateTime.of(2025, 11, 11, 11, 11, 11);

// 1、创建 Duration 对象
Duration duration = Duration.between(start, end);

// 2、获取信息
duration.toDays();      // 间隔多少天
duration.toHours();     // 间隔多少小时
duration.toMinutes();   // 间隔多少分
duration.toSeconds();   // 间隔多少秒
duration.toMillis();    // 间隔多少毫秒
duration.toNanos();     // 间隔多少纳秒
```

# 容器

Collection: 一对一

Map: 一对二

## Collection

![1666165150752](assets/1666165150752.png)

#### 常用方法

```java
Collection<String> c = new ArrayList<>();

// public boolean add(E e): 添加元素到集合
c.add("java1");

// pubilc boolean remove(E e): 删除某个元素，如果有多个重复元素只能删除第一个
c.remove("java1");

// public int size(): 获取集合的大小
c.size();

// public boolean contains(Object obj): 判断集合中是否包含某个元素
c.contains("java1"); //true

// public void clear(): 清空集合的元素
c.clear(); 

// public boolean isEmpty(): 判断集合为空返回 true 反之返回 false

// public Object[] toArray(): 把集合转换为数组
Object[] array = c.toArray();

// 如果想把集合转换为指定类型的数组，可以使用下面的代码
String[] array1 = c.toArray(new String[c.size()]);
System.out.println(Arrays.toString(array1)); //[java1,java2, java2, java3]

// 还可以把一个集合中的元素，添加到另一个集合中
c1.addAll(c2); // 把 c2 集合中的全部元素，添加到 c1 集合中去
```

#### 遍历

1. 迭代器

```java
// 原型

Iterator<E> iterator();

boolean hasNext();
E next();
```

```java
Collection<String> c = new ArrayList<>();

// 1. 先获取迭代器对象
Iterator<String> it = c.iterator();

// 2. 
while(it.hasNext()){
    String s = it.next();
}
```

2. 简化的写法，叫做增强 for 循环

```java

for(String s: c){
    System.out.println(s); 
}
```

3. forEach

```java
// forEach 方法的参数是一个 Consumer 函数式接口

default void forEach(Consumer<? super T> action)
```

```java
Collection<String> c = new ArrayList<>();

// 
c.forEach(new Consumer<String>{
    @Override
    public void accept(String s){
        System.out.println(s);
    }
});

// 也可以使用 lambda 表达式
c.forEach(s->System.out.println(s));
```

## List

#### List 集合的常用方法

List集合是索引的，所以多了一些有索引操作的方法

```java
void add(int index, E element);
E remove(int index);
E get(int index);
E set(int index, E element); // 修改 index 位置
```

#### List 集合的遍历方式

- for 循环（因为 List 有索引）
- `listIterator`

```java
Iterator<String> it = list.listIterator();
while(it.hasNext())
{
    if(it.next()...)
    {
        // 在用 Iterator 遍历 List 的时候，使用 Iterator 的方法删除元素
        // 避免 ConcurrentModificationException
        it.remove();
        // list.remove(); xxxx
    }
}
```

#### LinkedList

LinkedList 集合是基于双向链表实现了，所以相对于 ArrayList 新增了一些可以针对头尾进行操作的方法，如下图示所示：

```java
public void addFirst(E e);
public void addLast(E e);
public E getFirst();
public E getLast();
public E removeFirst();
public E removeLast();
```

可以用它来设计 `stack` `queue`

- 入队列可以调用 `addLast`，出队列调用 `removeFirst()`
- 压栈 `push` 等价于 `addFirst()`，弹栈 `pop` 等价于 `removeFirst()`


## Set

```java
Set<Integer> set = new HashSet<>();	        // 无序、无索引、不重复
Set<Integer> set = new LinkedHashSet<>();   // 有序、无索引、不重复
Set<Integer> set = new TreeSet<>();         // 有序、无索引、不重复
```

## HashSet

#### HashSet 集合底层原理

HashSet 集合底层是基于哈希表实现

- JDK8以后：哈希表 = 数组 + 链表 + 红黑树

![1666170451762](assets/1666170451762.png)

我们发现往 HashSet 中存储元素时，底层调用了元素的两个方法：

- `hashCode()` 方法获取元素的 hashCode
- `equals()` 方法，用来比较新添加的元素和集合中已有的元素是否相同 

  - 两个函数返回都相同才认为元素重复
  - hashCode 相同，equals 不同，则以链表的形式连接在数组的同一个索引为位置（如上图所示）

在 JDK8 开始后，为了提高性能，当链表的长度超过 8 时，数组长度超过 64，就会把链表转换为红黑树，如下图所示：

![1666171011761](assets/1666171011761-1667311900100.png)



#### HashSet 去重原理

要想保证在 HashSet 集合中没有重复元素，我们需要重写 E 的 hashCode 和 equals 方法

```java
public class Student{
    // 成员变量
    // 构造方法
    //...get、set、toString()...
    
    // 按快捷键生成 hashCode() 和 equals()
    // alt+insert 选择 hashCode and equals
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;

        Student student = (Student) o;

        if (age != student.age) return false;
        if (Double.compare(student.height, height) != 0) return false;
        return name != null ? name.equals(student.name) : student.name == null;
    }

    @Override
    public int hashCode() {
        int result;
        long temp;
        result = name != null ? name.hashCode() : 0;
        result = 31 * result + age;
        temp = Double.doubleToLongBits(height);
        result = 31 * result + (int) (temp ^ (temp >>> 32));
        return result;
    }
}
```

#### LinkedHashSet

LinkedHashSet 额外新增了一个双向链表来维护元素的存取顺序

存取是有序的

![1666171776819](assets/1666171776819-1667311894748.png)

每次添加元素，就和上一个元素用双向链表连接一下

第一个添加的元素是双向链表的头节点，最后一个添加的元素是双向链表的尾节点




## TreeSet

底层是一个红黑树

TreeSet 特点是可以对元素进行排序，但是必须指定元素的排序规则

```java
// Integer

Set<Integer> set1= new TreeSet<>();
set1.add(8);
set1.add(6);
set1.add(4);
set1.add(3);
set1.add(7);
set1.add(1);
set1.add(5);
set1.add(2);
System.out.println(set1); //[1,2,3,4,5,6,7,8]
```

```java
// 自定义类型的元素，需要指定排序规则

// Student
Set<Student> students = new TreeSet<>();

Student s1 = new Student("至尊宝",20, 169.6);
Student s2 = new Student("紫霞",23, 169.8);
Student s3 = new Student("蜘蛛精",23, 169.6);
Student s4 = new Student("牛魔王",48, 169.6);

students.add(s1);
students.add(s2);
students.add(s3);
students.add(s4);
System.out.println(students); // 报错，没有指定排序规则
```

指定排序规则

1. 让 E 的所属 class `implements Comparable` 接口，重写 `compareTo` 方法
2. 在创建 TreeSet 集合时传递 Compartor 对象指定排序规则

例子

```java
// 1. 
// 在往 TreeSet 集合中添加元素时，add 方法底层会调用 compareTo 方法
// 结果是正数、负数、零，决定元素放在后面、前面还是不存

// 让 Student 类，实现 Comparable 接口
public class Student implements Comparable<Student>{
    // 成员变量
    // 构造方法
    //...get、set、toString()...
    
    // 重写 compareTo 方法
    @Override
    public int compareTo(Student o) {
        //this：是将要添加进去的 Student 对象
        //o: 比较的对象
        return this.age-o.age;
    }
}
```

```java
// 2. 
// 创建 TreeSet 集合时，传递 Compartor 对象指定排序规则
// 优先级大于方法 1.

Set<Student> students = new TreeSet<>(new Comparator<Student>{
    @Override
    public int compare(Student o1, Student o2){
        // ... 你的规则
        return result; 
    }
});
```

## Collections

```java
List<String> names = new ArrayList<>();

// 1. public static <T> boolean addAll(Collection<? super T> c, T... e)
Collections.addAll(names, "1", "2", "3", "4");

// 2. public static void shuffle(List<?> list)：对集合打乱顺序
Collections.shuffle(names);

// 3. public static <T> void short(List<T list): 对 List 集合排序
List<Integer> list = new ArrayList<>();
list.add(3);
list.add(5);
list.add(2);
Collections.sort(list);

// 4. public static <T> int banarySearch(List<T> list, T key);

// 5. public static <T> void max/min(Collection<T> coll);

// 6. public static <T> void swap(List<?> list, int i, int j);
```

涉及到比较，需要指定比较规则

- 让元素实现 Comparable 接口，重写 compareTo 方法

    ```java
    public class Student implements Comparable<Student>{
        @Override
        public int compareTo(Student o){
            ...
            return result;
        }
    }
    ```

- 使用调用 sort 方法时，传递比较器

    ```java
    Collections.sort(students, new Comparator<Student>(){
        @Override
        public int compare(Student o1, Student o2){
            return o1.getAge()-o2.getAge();
        }
    });	
    ```

## Map

3 个实现类

- `TreeMap`
- `HashMap`
- `LinkedHashMap`

#### 概述

Map 集合中的每一个元素是以 `key=value` 的形式存在的

在 Java 中有一个类叫 Entry，Entry 的对象用来表示 “键值对”

键不能重复，值可以重复，每一个键只能找到自己对应的值

![1667308506610](assets/1667308506610.png)

#### 常用方法

```java
public V put(K key, V value);  // 添加元素
public V get(Object key);      // key 获取 value
public V remove(Object key);   // key 删除 
public int size();
pubilc void clear();
pubilc boolean isEmpty();
pubilc boolean containsKey(Object key);
pubilc boolean containsValue(Object value);
```

#### 遍历

==一==

1. `public Set<K> keySet();` 获取所有 key 的集合
2. `public V get(Object key);` 遍历 key 找 value

```java
Map<String, Double> map = new HashMap<>();

// 1、all key
Set<String> keys = map.keySet();

// 2、遍历 keys
for (String key : keys) {
    map.get(key);
}
```

==二==

1. `Set<Map.Entry<K, V>> entrySet();` 获取所有 Entry
2. `getKey(); getValue();`

```java
Map<String, Double> map = new HashMap<>();

// 1. 
Set<Map.Entry<String, Double>> entries = map.entrySet();

for (Map.Entry<String, Double> entry : entries) {
    entry.getKey();
    entry.getValue();
}
```

==三==

`dafault void forEach(BiConsumer<? super K, ? super V> action)`

```java
Map<String, Double> map = new HashMap<>();

// 遍历 map 集合，传递匿名内部类
map.forEach(new BiConsumer<String, Double>() {
    @Override
    public void accept(String k, Double v) {
        System.out.println(k + "---->" + v);
    }
});

// 遍历 map 集合，传递 Lambda 表达式
map.forEach(( k,  v) -> {
    System.out.println(k + "---->" + v);
});
```
