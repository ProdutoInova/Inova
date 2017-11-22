## Table of Contents

* [Preface](#preface)
* [1. Programming Specification](#1-programming-specification)
   * [Naming Conventions](#naming-conventions)
   * [Constant Conventions](#constant-conventions)
   * [Formatting Style](#formatting-style)
   * [OOP Rules](#oop-rules)
   * [Collection](#collection)
   * [Concurrency](#concurrency)
   * [Flow Control Statements](#flow-control-statements)
   * [Code Comments](#code-comments)
   * [Other](#other)
* [2. Exception and Logs](#2-exception-and-logs)
   * [Exception](#exception)
   * [Logs](#logs)

## Preface
We are pleased to present **Inova Java Coding Guidelines**, which consolidates the best programming practices over the years from Inova Group's technical teams. A vast number of Java programming teams impose demanding requirements on code quality across projects as we encourage reuse and better understanding of each other's programs. We have seen many programming problems in the past. For example, defective database table structures and index designs may cause software architecture flaws and performance risks. Yet as another example, confusing code structures make it difficult to maintain. Furthermore, vulnerable code without authentication is prone to hackers’ attacks. To address those kinds of problems, we developed this document for Java developers in Inova.

This document is consisted of five parts: ***Programming Specification***, ***Exception and Logs***, ***MySQL Specification***, ***Project Specification*** and ***Security Specification***. Based on the severity of the concerns, each specification is classified into three levels: ***Mandatory***, ***Recommended*** and ***Reference***. Further clarification is expressed in:  
 (1) "**Description**", which explains the content;  
 (2) "**Positive examples**", which describe recommended coding and implementation approaches;   
 (3) "**Counter examples**", which describe precautions and actual error cases.

The main purpose of this document is to help developers improve code quality. As a result, developers can minimize potential and repetitive code errors. In addition, specification is essential to modern software architectures, which enable effective  collaborations. As an analogy, traffic regulations intend to protect public safety in essence rather than to deprive the rights of driving. It is easy to imagine the chaos of traffic without speed limits and traffic lights. Instead of destroying the creativity and elegance of program, the purpose of developing appropriate specification and standards of software is to improve the efficiency of collaboration by limiting excessive personalization.

We will continue to collect feedback from the community to improve Inova Java Coding Guidelines.

## <font color="green">1. Programming Specification</font>
### <font color="green">Naming Conventions</font>
1\. **[Mandatory]** All names should not start or end with an underline or  a dollar sign.   
> <font color="#FF4500">Counter example: </font> \_name / \_\_name / \$Object / name_ / name\$ / Object\$

2\. **[Mandatory]** Using Chinese, Pinyin, or Pinyin-English mixed spelling in naming is strictly prohibited. Accurate English spelling and grammar will make the code readable, understandable, and maintainable.   
> <font color="#019858">Positive example: </font> Inova / taobao / youku / Hangzhou. In these cases, Chinese proper names in Pinyin are acceptable.

3\. **[Mandatory]** Class names should be nouns in UpperCamelCase except domain models: DO, BO, DTO, VO, etc.   
 > <font color="#019858">Positive example: </font>MarcoPolo  /  UserDO  /  HtmlDTO  /  XmlService  /  TcpUdpDeal / TaPromotion  
 > <font color="#FF4500">Counter example: </font>macroPolo  /  UserDo  /  HTMLDto  /  XMLService  /  TCPUDPDeal / TAPromotion  

4\. **[Mandatory]** Method names, parameter names, member variable names, and local variable names should be written in lowerCamelCase.   
> <font color="#019858">Positive example: </font> localValue / getHttpMessage()  /  inputUserId    


5\. **[Mandatory]** Constant variable names should be written in upper characters separated by underscores. These names should be semantically complete and clear.   
> <font color="#019858">Positive example: </font> MAX\_STOCK\_COUNT   
> <font color="#FF4500">Counter example: </font> MAX\_COUNT   

6\. **[Mandatory]** Abstract class names must start with *Abstract* or *Base*. Exception class names must be ended with *Exception*. Test cases shall be started with the class names to be tested and ended with *Test*.

7\. **[Mandatory]** Brackets are a part of an Array type. The definition could be: *<font color="blue">String[]</font> args;*  
> <font color="#FF4500">Counter example: </font>*String args[];*

8\. **[Mandatory]** Do not add 'is' as prefix while defining Boolean variable, since it may cause a serialization exception in some Java Frameworks.  
> <font color="#FF4500">Counter example: </font>*boolean isSuccess;* The method name will be `isSuccess()` and then RPC framework will deduce the variable name as 'success', resulting in a serialization error since it cannot find the correct attribute.

9\. **[Mandatory]** Package should be named in lowercase characters. There should be only one English word after each dot. Package names are always in <font color="blue">singular</font> format while class name can be in plural format if necessary.  
> <font color="#019858">Positive example: </font> `com.inova.open.util` can be used as package name for utils;
`MessageUtils` can be used as class name;


10\. **[Mandatory]** Uncommon abbreviations should be avoided for the sake of legibility.     
 > <font color="#FF4500">Counter example: </font>AbsClass (AbstractClass); condi (Condition)

11\. **[Recommended]**  The pattern name is recommended to be included in the class name if any design pattern is used.  
 > <font color="#019858">Positive example: </font>`public class OrderFactory;  `
`public class LoginProxy;`  `public class ResourceObserver;`  
> <font color="#977C00">Note: </font> Including corresponding pattern names helps readers understand ideas in design patterns quickly.

12\. **[Recommended]** Do not add any modifier, including `public`, to method in interface classes for coding simplicity. Please add valid *Javadoc* comments for methods. Do not define any variables in the interface except for the common constants of the application.  
 > <font color="#019858">Positive example: </font>method definition in the interface: `void f(); `  
constant definition: `String COMPANY = "inova";`    
> <font color="#977C00">Note: </font>In JDK8 it is allowed to define default implementation for interface methods, which is valuable for all implemented classes.

13\. There are mainly two rules for interface and corresponding implementation class naming:  
&emsp;&emsp;1) **[Mandatory]** All *Service* and *DAO* classes must be interface based on SOA principle. Implementation class names should be ended with *Impl*.  
  > <font color="#019858">Positive example: </font>`CacheServiceImpl` to implement `CacheService`.  

&emsp;&emsp;2) **[Recommended]** If the interface name is to indicate the ability of the interface, then its name should be adjective.  
  > <font color="#019858">Positive example: </font>`AbstractTranslator` to implement `Translatable`.

14\. **[For Reference]** An Enumeration class name should end with *Enum*. Its members should be spelled out in upper case words, separated by underlines.  
 > <font color="#977C00">Note: </font>Enumeration is indeed a special constant class and all construction methods are private by default.  
 > <font color="#019858">Positive example: </font>Enumeration name: `DealStatusEnum`; Member name: `SUCCESS  / UNKOWN_REASON`.

15\. **[For Reference]** Naming conventions for different package layers:  
&emsp;&emsp;A) Naming conventions for Service/DAO layer methods  
&emsp;&emsp;&emsp;&emsp;1) Use `get` as name prefix for method to get a single object.  
&emsp;&emsp;&emsp;&emsp;2) Use `list` as name prefix for method to get multiple objects.  
&emsp;&emsp;&emsp;&emsp;3) Use `count` as name prefix for statistical method.  
&emsp;&emsp;&emsp;&emsp;4) Use `insert` or `save` (recommended) as name prefix for method to save data.  
&emsp;&emsp;&emsp;&emsp;5) Use `delete` or `remove` (recommended) as name prefix for method to remove data.  
&emsp;&emsp;&emsp;&emsp;6) Use `update` as name prefix for method to update data.   
&emsp;&emsp;B) Naming conventions for Domain models  
&emsp;&emsp;&emsp;&emsp;1) Data Object: \*DO, where \* is the table name.  
&emsp;&emsp;&emsp;&emsp;2) Data Transfer Object: \*DTO, where \* is domain related name.  
&emsp;&emsp;&emsp;&emsp;3) Value Object: \*VO, where \* is website name in most cases.  
&emsp;&emsp;&emsp;&emsp;4) POJO generally point to DO/DTO/BO/VO but cannot be used in naming as \*POJO.

### <font color="green">Constant Conventions</font>
1\. **[Mandatory]** Magic values, except for predefined, are forbidden in coding.       
> <font color="#FF4500">Counter example: </font> String key = <font color="blue">"Id#taobao_"</font> + tradeId;  

2\. **[Mandatory]** 'L' instead of 'l' should be used for long or Long variable because 'l' is easily to be regarded as number 1 in mistake.  
> <font color="#FF4500">Counter example: </font>`Long a = 2l`, it is hard to tell whether it is number 21 or Long 2.

3\. **[Recommended]** Constants should be placed in different constant classes based on their functions. For example, cache related constants could be put in `CacheConsts` while configuration related constants could be kept in `ConfigConsts`.   
 > <font color="#977C00">Note: </font>It is difficult to find one constant in one big complete constant class.

4\. **[Recommended]** Constants can be shared in the following 5 different layers: *shared in multiple applications; shared inside an application;  shared in a sub-project;  shared in a package; shared in a class;*.  
&emsp;&emsp;1) Shared in multiple applications: keep in  a library, under `constant` directory in client.jar;  
&emsp;&emsp;2) Shared in an application: keep in shared modules within the application, under `constant` directory;  
&emsp;&emsp;<font color="#FF4500">Counter example: </font>Obvious variable names should also be defined as common shared constants in an application. The following definitions caused an exception in the production environment: it returns *false*, but expected to return *true* for `A.YES.equals(B.YES)`.  
&emsp;&emsp;Definition in Class A: `public static final String YES = "yes";`    
&emsp;&emsp;Definition in Class B: `public static final String YES = "y";`    
&emsp;&emsp;3) Shared in a sub-project: placed under `constant` directory in the current project;  
&emsp;&emsp;4) Shared in a package: placed under `constant` directory in current package;  
&emsp;&emsp;5) Shared in a class: defined as 'private static final' inside class;

5\. **[Recommended]** Enumeration class is to be used if variables value lie in a fixed range or if the variable has attributes. The following example shows that extra information (which day it is) can be included in enumeration:  
 > <font color="#019858">Positive example: </font>public Enum{ MONDAY(1), TUESDAY(2), WEDNESDAY(3), THURSDAY(4), FRIDAY(5), SATURDAY(6), SUNDAY(7);}

### <font color="green">Formatting Style</font>
1\. **[Mandatory]** Rules for braces. If there is no content, simply use *{}* in the same line. Otherwise:    
&emsp;&emsp;1) No line break before the opening brace.   
&emsp;&emsp;2) Line break after the opening brace.     
&emsp;&emsp;3) Line break before the closing brace.   
&emsp;&emsp;4) Line break after the closing brace, *only if* the brace terminates a statement or terminates a method body, constructor or named class. There is *no*    line break after the closing brace if it is followed by `else` or a comma.

2\. **[Mandatory]** No space is used between the '(' character and its following character. Same for the ')' character and its preceding character. Refer to the *Positive Example* at the 5th rule.  

3\. **[Mandatory]** There must be one space between keywords, such as if/for/while/switch, and parentheses.

4\. **[Mandatory]** There must be one space at both left and right side of operators, such as '=', '&&', '+', '-', *ternary operator*, etc.

5\. **[Mandatory]** Each time a new block or block-like construct is opened, the indent increases by four spaces. When the block ends, the indent returns to the previous indent level. Tab characters are not used for indentation.   
> <font color="#977C00">Note: </font>If tab characters are not used for indentation, we must set four spaces replacing tab character in IDE software previously. For example, "Use table character" should be unchecked in IDEA, "insert spaces for tabs" should be checked in Eclipse.  
> <font color="#019858">Positive example: </font>     
```java
public static void main(String[] args) {
    // four spaces indent
    String say = "hello";
    // one space before and after the operator
    int flag = 0;
    // one space between 'if' and '(';
    // no space between '(' and 'flag' or between '0' and ')'
    if (flag == 0) {
        System.out.println(say);
    }
    // one space before '{' and line break after '{'
    if (flag == 1) {
        System.out.println("world");
    // line break before '}'but not after '}' if it is followed by 'else'
    } else {  
        System.out.println("ok");
    // line break after '}' if it is the end of the block
    }
}
```

6\. **[Mandatory]** Java code has a column limit of 120 characters. Except import statements, any line that would exceed this limit must be line-wrapped as follows:   
&emsp;&emsp;1) The second line should be intented at 4 spaces with respect to the first one. The third line and following ones should align with the second line.      
&emsp;&emsp;2) Operators should be moved to the next line together with following context.    
&emsp;&emsp;3) Character '.' should be moved to the next line together with the method after it.    
&emsp;&emsp;4) If there are multiple parameters that extend over the maximum length, a line break should be inserted after a comma.   
&emsp;&emsp;5) No line breaks should appear before parentheses.  
> <font color="#019858">Positive example: </font>
```java
StringBuffer sb = new StringBuffer();
// line break if there are more than 120 characters, and 4 spaces indent at
// the second line. make sure character '.' Moved to the next line
// together.  The third and forth line is aligned with the second one.
sb.append("zi").append("xin").
    .append("huang")...
    .append("huang")...
    .append("huang");
```
> <font color="#FF4500">Counter example: </font>
```java
StringBuffer sb = new StringBuffer();
// no line break before '('
sb.append("zi").append("xin")...append
    ("huang");  
// no line break before ',' if there are multiple params
invoke(args1, args2, args3, ...
    , argsX);
```

7\. **[Mandatory]** There must be one space between a comma and the next parameter for methods with multiple parameters.   
> <font color="#019858">Positive example: </font>One space is used after the '<font color="blue">*,*</font>' character in the following method definition.
```java
f("a", "b", "c");
```

8\. **[Mandatory]** The charset encoding of text files should be *UTF-8* and the characters of line breaks should be in *Unix* format, instead of *Windows* format.

9\. **[Recommended]** It is unnecessary to align variables by several spaces.   
> <font color="#019858">Positive example: </font>
```java
int a = 3;
long b = 4L;
float c = 5F;
StringBuffer sb = new StringBuffer();
```
> <font color="#977C00">Note: </font>It is cumbersome to insert several spaces to align the variables above.   

10\. **[Recommended]** It is recommended to separate sections with same logic or semantic with a single blank line.   
> <font color="#977C00">Note: </font>It is unnecessary to use multiple blank lines to do that.

### <font color="green">OOP Rules</font>
1\. **[Mandatory]** A static field or method should be directly referred by its class name instead of its corresponding object name.

2\. **[Mandatory]** An overridden method from an interface or abstract class must be marked with `@Override` annotation.   
 > <font color="#FF4500">Counter example: </font>For `getObject()` and `get0bject()`, the first one has a letter 'O', and the second one has a number '0'. To accurately determine whether the overriding is successful, an `@Override` annotation is necessary. Meanwhile, once the method signature in the abstract class is changed, the implementation class will report a compile-time error immediately.

3\. **[Mandatory]** *varargs* is recommended only if all parameters are of the same type and semantics. Parameters with `Object` type should be avoided.  
 > <font color="#977C00">Note: </font>Arguments with the *varargs* feature must be at the end of the argument list (Programming with the *varargs* feature is not recommended).  
 > <font color="#019858">Positive example: </font>
```java
public User getUsers(String type, Integer... ids);
```

4\. **[Mandatory]** Modifying the <font color="blue">method signature</font> is forbidden to avoid affecting the caller. A `@Deprecated` annotation with explicit descriptions about the new service is necessary when an interface is deprecated.

5\. **[Mandatory]** Using a deprecated class or method is prohibited.  
 > <font color="#977C00">Note: </font>For example, `decode(String source, String encode)` should be used instead of the deprecated method `decode(String encodeStr)`. Once an interface has been deprecated, the interface provider has the obligation to provide a new one. At the same time, client programmers have  the obligation to check out what its new implementation is.

6\. **[Mandatory]** Since `NullPointerException` can possibly be thrown while calling the *equals* method of `Object`, *equals* should be invoked by a constant or an object that is definitely not *null*.  
 > <font color="#019858">Positive example: </font> `"test".equals(object);`   
 > <font color="#FF4500">Counter example: </font> `object.equals("test");`    
 > <font color="#977C00">Note: </font>`java.util.Objects#equals` (a utility class in JDK7) is recommended.

7\. **[Mandatory]** The wrapper classes should be compared by `equals` method rather than by symbol of '==' directly.    
 > <font color="#977C00">Note: </font>Consider this assignment: `Integer var = ?`. When it fits the range from <font color="blue">-128 to 127</font>, we can use `==` directly for a comparison. Because the `Integer` object will be generated by `IntegerCache.cache`, which reuses an existing object. Nevertheless, when it fits the complementary set of the former range, the `Integer` object will be allocated in Heap, which does not reuse an existing object. This is a pitfall. Hence the `equals` method is recommended.

8\. **[Mandatory]** Rules for using primitive data types and wrapper classes:     
&emsp;&emsp;1) Members of a POJO class must be wrapper classes.  
&emsp;&emsp;2) The return value and arguments of a RPC method must be wrapper classes.   
&emsp;&emsp;3) **[Recommended]** Local variables should be primitive data types.  
&emsp;&emsp;<font color="#977C00">Note: </font>In order to remind the consumer of explicit assignments, there are no initial values for members in a POJO class. As a consumer, you should check problems such as `NullPointerException` and warehouse entries for yourself.   
&emsp;&emsp;<font color="#019858">Positive example: </font>As the result of a database query may be *null*, assigning it to a primitive date type will cause a risk of `NullPointerException` because of autoboxing.     
&emsp;&emsp;<font color="#FF4500">Counter example: </font>Consider the output of a  transaction volume's amplitude, like *±x%*. As a primitive data, when it comes to a failure of calling a RPC service, the default return value: *0%* will be assigned, which is not correct. A hyphen like *-* should be assigned instead. Therefore, the *null* value of a wrapper class can represent additional information, such as a failure of calling a RPC service, an abnormal exit, etc.

9\. **[Mandatory]** While defining POJO classes like DO, DTO, VO, etc., do not assign any <font color="blue">default values</font> to the members.   

10\. **[Mandatory]** To avoid a deserialization failure, do not change the *serialVersionUID* when a serialized class needs to be updated, such as adding some new members. If a completely incompatible update is needed, change the value of *serialVersionUID* in case of a confusion when deserialized.  
> <font color="#977C00">Note: </font>The inconsistency of *serialVersionUID* may cause an `InvalidClassException` at runtime.

11\. **[Mandatory]** Business logic in constructor methods is prohibited. All initializations should be implemented in the `init` method.

12\. **[Mandatory]** The `toString` method must be implemented in a POJO class. The `super.toString` method should be called in front of the whole implementation if the current class extends another POJO class.
 > <font color="#977C00">Note: </font>We can call the `toString` method in a POJO directly to print property values in order to check the problem when a method throws an exception in runtime.

13\. **[Recommended]** When accessing an array generated by the split method in String using an index, make sure to check the last separator whether it is null to avoid `IndexOutOfBoundException`.  
> <font color="#977C00">Note: </font>
``` java
String str = "a,b,c,,";
String[] ary = str.split(",");
// The expected result exceeds 3. However it turns out to be 3.
System.out.println(ary.length);  
```

14\. **[Recommended]** Multiple constructor methods or homonymous methods in a class should be put together orderly for better readability.

15\. **[Recommended]** The declarative order of methods within a class is:  
*public or protected methods -> private methods -> getter/setter methods*.          
 > <font color="#977C00">Note: </font> As the most concerned ones for consumers and providers, *public* methods should be put on the first screen. *Protected* methods are only cared for by the subclasses, but they have chances to be vital when it comes to Template Design Pattern. *Private* methods, the black-box approaches, basically are not significant. *Getter/setter* methods of a Service or a DAO should be put at the end of the class implementation because of the low significance.

16\. **[Recommended]** For a *setter* method, the argument name should be the same as the field name. Implementations of business logics in *getter/setter* methods, which will increase difficulties of the troubleshooting, are not recommended.  
 > <font color="#FF4500">Counter example: </font>
 ```java
 public Integer getData() {
     if (true) {
         return data + 100;
     } else {
         return data - 100;
     }
 }
 ```  

17\. **[Recommended]** Use the `append` method in `StringBuilder` inside a loop body when concatenating multiple strings.  
 > <font color="#FF4500">Counter example: </font>  
```java
String str = "start";
for (int i = 0; i < 100; i++) {
    str = str + "hello";
}
```  
> <font color="#977C00">Note: </font>According to the decompiled bytecode file, for each loop, it allocates a `StringBuilder` object, appends a string, and finally returns a `String` object via the `toString` method. This is a tremendous waste of memory.

18\. **[Recommended]** Keyword *final* should be used in the following situations:    
&emsp;&emsp;1) A class which is not allow to be inherited, or a local variable not to be reassigned.  
&emsp;&emsp;2) An argument which is not allow to be modified.   
&emsp;&emsp;3) A method which is not allow to be overridden.

19\. **[Recommended]** Be cautious to copy an object using the `clone` method in `Object`.  
 > <font color="#977C00">Note: </font>The default implementation of `clone` in `Object` is a shadow (not deep) copy, which copies fields as pointers to the same objects in memory.

20\. **[Recommended]** Define the access level of members in class with severe  restrictions:    
&emsp;&emsp;1) Constructor methods must be `private` if an allocation using `new` keyword outside of the class is forbidden.   
&emsp;&emsp;2) Constructor methods are not allowed to be `public` or `default` in a utility class.   
&emsp;&emsp;3) Nonstatic class variables that are accessed from inheritants must be `protected`.  
&emsp;&emsp;4) Nonstatic class variables that no one can access except the class that contains them must be `private`.  
&emsp;&emsp;5) Static variables that no one can access except the class that contains them must be `private`.       
&emsp;&emsp;6) Static variables should be considered in determining whether they are `final`.  
&emsp;&emsp;7) Class methods that no one can access except the class that contains them must be `private`.  
&emsp;&emsp;8) Class methods that are accessed from inheritants must be `protected`.   
 > <font color="#977C00">Note: </font> We should strictly control the access for any classes, methods, arguments and variables. Loose access control will be harmful to the decoupling of modules. Imagine the following situations. For a `private` class member, we can remove it as soon as we want. However, when it comes to a `public` class member, we have to think twice before any updates happen to it.

### <font color="green">Collection</font>
1\. **[Mandatory]** The usage of *hashCode* and *equals* should follow:   
&emsp;&emsp;1) Override *hashCode* if *equals* is overridden.  
&emsp;&emsp;2) These two methods must be overridden for `Set` since they are used to ensure that no duplicate object will be inserted in `Set`.  
&emsp;&emsp;3) These two methods must be overridden if self-defined object is used as the key of `Map`.  
> <font color="#977C00">Note: </font> `String` can be used as the key of `Map` since these two methods have been rewritten.

2\. **[Mandatory]** Do not add elements to collection objects returned by `keySet()`/`values()`/`entrySet()`, otherwise `UnsupportedOperationException` will be thrown.

3\. **[Mandatory]** Do not add nor remove to/from immutable objects returned by methods in `Collections`, e.g. `emptyList()`/`singletonList()`.    
> <font color="#FF4500">Counter example: </font>Adding elements to `Collections.emptyList()` will throw `UnsupportedOperationException`.

4\. **[Mandatory]** Do not cast *subList* in class `ArrayList`, otherwise  `ClassCastException` will be thrown: `java.util.RandomAccessSubList` cannot be cast to `java.util.ArrayList`.  
 > <font color="#977C00">Note: </font>`subList` of `ArrayList` is an inner class, which is a view of `ArrayList`. All operations on the `Sublist` will affect the original list finally.

5\. **[Mandatory]** When using *subList*, be careful to modify the size of original list. It might cause `ConcurrentModificationException` when performing traversing, adding or deleting on the *subList*.   

6\. **[Mandatory]** Use `toArray(T[] array)` to convert list to array. The input array type should be the same with the list whose size is `list.size()`.    
 > <font color="#FF4500">Counter example: </font> Do not use `toArray` method without arguments. Since the return type is `Object[]`, `ClassCastException` will be thrown when casting it to a different array type.  
> <font color="#019858">Positive example: </font>
```java
		List<String> list = new ArrayList<String>(2);
		list.add("guan");
		list.add("bao");		
		String[] array = new String[list.size()];
		array = list.toArray(array);
```  
> <font color="#977C00">Note: </font>When using `toArray` method with arguments, if input array size is not large enough, the method will re-assign the size internally, and then return the address of new array. If the size is larger than needed, the value of `index[list.size()]` will be set to *null* while other values remain the same. Defining an input with the same size of the list is recommended.

7\. **[Mandatory]** Do not use methods which will modify the list after using `Arrays.asList` to convert array to list, otherwise methods like *add/remove/clear* will throw `UnsupportedOperationException`.   
> <font color="#977C00">Note: </font>The result of `asList` is the inner class of `Arrays`, which does not implement methods to modify itself. `Arrays.asList` is only a transferred interface, data inside which is stored as an array.
```java
String[] str = new String[] { "a", "b" };
List<String> list = Arrays.asList(str);
```   
 Case 1: `list.add("c");` will throw a runtime exception.  
 Case 2: `str[0]= "gujin";` `list.get(0)` will be modified.

8\. **[Mandatory]** Method `add` cannot be used for generic wildcard with `<? Extends T>`, method `get` cannot be used with `<? super T>`, which probably goes wrong.   
> <font color="#977C00">Note: </font>About PECS (Producer Extends Consumer Super) principle:  
1) `Extends` is suitable for frequently reading scenarios.   
2) `Super` is suitable for frequently inserting scenarios.

9\. **[Mandatory]** Do not remove or add elements to a collection in a *foreach* loop. Please use `Iterator` to remove an item. `Iterator` object should be synchronized when executing concurrent operations.  
 > <font color="#FF4500">Counter example: </font>
```java
List<String> a = new ArrayList<String>();
a.add("1");
a.add("2");
for (String temp : a) {
    if ("1".equals(temp)){
        a.remove(temp);
    }
}
```
> <font color="#977C00">Note: </font> If you try to replace "1" with "2", you will get an unexpected result.
> <font color="#019858">Positive example: </font>
```java
Iterator<String> it = a.iterator();
while (it.hasNext()) {    
    String temp =  it.next();             
    if (delete condition) {              
        it.remove();       
    }
}    
```  

10\. **[Mandatory]** In JDK 7 and above version, `Comparator` should meet the three requirements listed below, otherwise `Arrays.sort` and `Collections.sort` will throw `IllegalArgumentException`.    
> <font color="#977C00">Note: </font>  
&emsp;&emsp;1) Comparing x,y and y,x should return the opposite result.  
&emsp;&emsp;2) If x>y and y>z, then x>z.  
&emsp;&emsp;3) If x=y, then comparing x with z and comparing y with z should return the same result.    
> <font color="#FF4500">Counter example: </font>The program below cannot handle the case if o1 equals to o2, which might cause an exception in a real case:  
```java
new Comparator<Student>() {
    @Override
    public int compare(Student o1, Student o2) {
        return o1.getId() > o2.getId() ? 1 : -1;
    }
}
```

11\. **[Recommended]** Set a size when initializing a collection if possible.    
> <font color="#977C00">Note: </font>Better to use `ArrayList(int initialCapacity)` to initialize `ArrayList`.

12\. **[Recommended]** Use `entrySet` instead of `keySet` to traverse KV maps.   
> <font color="#977C00">Note: </font>Actually, `keySet` iterates through the map twice, firstly convert to `Iterator` object, then get the value from the `HashMap` by key. `EntrySet` iterates only once and puts keys and values in the entry which is more efficient. Use `Map.foreach` method in JDK8.  
 > <font color="#019858">Positive example: </font>`values()` returns a list including all values, `keySet()` returns a set including all values, `entrySet()` returns a k-v combined object.

13\. **[Recommended]** Carefully check whether a *k/v collection* can store *null* value, refer to the table below:

 | Collection | Key | Value | Super | Note |
  | --- | --- | --- | --- | --- |
 | Hashtable | <font color="#FF4500">Null is not allowed</font>| <font color="#FF4500">Null is not allowed</font>| Dictionary| Thread-safe |
 | ConcurrentHashMap | <font color="#FF4500">Null is not allowed</font>| <font color="#FF4500">Null is not allowed</font>| AbstractMap| Segment lock |
 | TreeMap | <font color="red">Null is not allowed</font>| <font color="blue">Null is allowed</font>| AbstractMap| Thread-unsafe |
 | HashMap | <font color="blue">Null is allowed</font>| <font color="blue">Null is allowed</font>|  AbstractMap| Thread-unsafe |

> <font color="#FF4500">Counter example: </font>Confused by `HashMap`, lots of people think *null* is allowed in `ConcurrentHashMap`. Actually,  `NullPointerException` will be thrown when putting in *null* value.

14\. **[For Reference]** Properly use sort and order of a collection to avoid negative influence of unsorted and unordered one.  
> <font color="#977C00">Note: </font>*Sorted* means that its iteration follows  specific sorting rule. *Ordered* means the order of elements in each traverse is stable. e.g. `ArrayList` is ordered and unsorted, `HashMap` is unordered and unsorted, `TreeSet` is ordered and sorted.

15\. **[For Reference]** Deduplication operations could be performed quickly since set stores unique values only. Avoid using method *contains* of `List` to perform traverse, comparison and de-duplication.  


### <font color="green">Concurrency</font>
1\. **[Mandatory]** Thread-safe should be ensured when initializing singleton instance, as well as all methods in it.
> <font color="#977C00">Note: </font>Resource driven class, utility class and singleton factory class are all included.

2\. **[Mandatory]** A meaningful thread name is helpful to trace the error information, so assign a name when creating threads or thread pools.   
 > <font color="#019858">Positive example: </font>
 ```java
 public class TimerTaskThread extends Thread {
		public TimerTaskThread() {
			super.setName("TimerTaskThread");
		    …
		}
 }
 ```  

3\. **[Mandatory]** Threads should be provided by thread pools. Explicitly creating threads is not allowed.
 > <font color="#977C00">Note: </font>Using thread pool can reduce the time of creating and destroying thread and save system resource. If we do not use thread pools, lots of similar threads will be created which lead to "running out of memory" or over-switching problems.

4\. **[Mandatory]** A thread pool should be created by `ThreadPoolExecutor` rather than `Executors`. These would make the parameters of the thread pool understandable. It would also reduce the risk of running out of system resource.  
 > <font color="#977C00">Note: </font>Below are the problems created by usage of `Executors` for thread pool creation:   
&emsp;&emsp;1) `FixedThreadPool` and `SingleThreadPool`:  
&emsp;&emsp;Maximum request queue size `Integer.MAX_VALUE`. A large number of requests might cause OOM.   
&emsp;&emsp;2) `CachedThreadPool` and `ScheduledThreadPool`:  
&emsp;&emsp;The number of threads which are allowed to be created is `Integer.MAX_VALUE`. Creating too many threads might lead to OOM.

5\. **[Mandatory]** `SimpleDataFormat` is unsafe, do not define it as a *static* variable. If have to, lock or `DateUtils` class must be used.  
 > <font color="#019858">Positive example: </font>Pay attention to thread-safety when using `DateUtils`. It is recommended to use as below:
 ```java
private static final ThreadLocal<DateFormat> df = new ThreadLocal<DateFormat>() {  
    @Override  
    protected DateFormat initialValue() {  
        return new SimpleDateFormat("yyyy-MM-dd");  
    }  
};  
 ```
 > <font color="#977C00">Note: </font>In JDK8, `Instant` can be used to replace `Date`, `Calendar` is replaced by `LocalDateTime`, `Simpledataformatter` is replaced by `DateTimeFormatter`.

6\. **[Mandatory]** `remove()` method must be implemented by `ThreadLocal` variables, especially when using thread pools in which threads are often reused. Otherwise, it may affect subsequent business logic and cause unexpected problems such as memory leak.    
> <font color="#019858">Positive example: </font>
```java
objectThreadLocal.set(someObject);
try {
    ...
} finally {
    objectThreadLocal.remove();
}
```

7\. **[Mandatory]** In highly concurrent scenarios, performance of `Lock` should be considered in synchronous calls. A block lock is better than a method lock. An object lock is better than a class lock.

8\. **[Mandatory]** When adding locks to multiple resources, tables in the database and objects at the same time, locking sequence should be kept consistent to avoid deadlock.    
> <font color="#977C00">Note: </font> If thread 1 does update after adding lock to table A, B, C accordingly, the lock sequence of thread 2 should also be A, B, C, otherwise deadlock might happen.

9\. **[Mandatory]** A lock needs to be used to avoid update failure when modifying one record concurrently. Add lock either in application layer, in cache, or add optimistic lock in the database by using version as update stamp.  
 > <font color="#977C00">Note: </font>If access confliction probability is less than 20%, recommend to use optimistic lock, otherwise use pessimistic lock. Retry number of optimistic lock should be no less than 3.

10\. **[Mandatory]** Run multiple `TimeTask` by using `ScheduledExecutorService` rather than `Timer` because `Timer` will kill all running threads in case of failing to catch exceptions.

11\. **[Recommended]** When using `CountDownLatch` to convert asynchronous operations to synchronous ones, each thread must call `countdown` method before quitting. Make sure to catch any exception during thread running, to let `countdown` method be  executed. If main thread cannot reach `await` method, program will return until timeout.  
> <font color="#977C00">Note: </font>Be careful, exception thrown by sub-thread cannot be caught by main thread.

12\. **[Recommended]** Avoid using `Random` instance by multiple threads. Although it is safe to share this instance, competition on the same seed will damage performance.  
> <font color="#977C00">Note: </font>`Random` instance includes instances of `java.util.Random` and `Math.random()`.  
> <font color="#019858">Positive example: </font>After JDK7, API `ThreadLocalRandom` can be used directly. But before JDK7, instance needs to be created in each thread.

13\. **[Recommended]** In concurrent scenarios, one easy solution to optimize the  lazy initialization problem by using double-checked locking  (referred to The Double-checked locking is broken Declaration), is to declare the object type as `volatile`.    
> <font color="#FF4500">Counter example: </font>
```java
class Foo {
    private Helper helper = null;
    public Helper getHelper() {
        if (helper == null) {
            synchronized(this) {
                if (helper == null)
                helper = new Helper();
            }   
        }
        return helper;
    }
    // other functions and members...
}
```

14\. **[For Reference]** `volatile` is used to solve the problem of invisible memory in multiple threads. *Write-Once-Read-Many* can solve variable synchronization problem. But *Write-Many* cannot settle thread safe problem. For `count++`, use below example:　    
```java
AtomicInteger count = new AtomicInteger();
count.addAndGet(1);
```  
> <font color="#977C00">Note: </font>In JDK8, `LongAdder` is recommended which reduces retry times of optimistic lock and has better performance than `AtomicLong`.

15\. **[For Reference]** Resizing `HashMap` when its capacity is not enough might cause dead link and high CPU usage because of high-concurrency. Avoid this risk in development.  

16\. **[For Reference]** `ThreadLocal` cannot solve update problems of shared object. It is recommended to use a *static* `ThreadLocal` object which is shared by all operations in the same thread.

### <font color="green">Flow Control Statements</font>
1\. **[Mandatory]** In a `switch` block, each case should be finished by *break/return*. If not, a note should be included to describe at which case it will stop. Within every `switch` block, a default statement must be present, even if it is empty.

2\. **[Mandatory]** Braces are used with *if*, *else*, *for*, *do* and *while* statements, even if the body contains only a single statement. Avoid using the following example:
```java
    if (condition) statements;
```

3\. **[Recommended]** Use `else` as less as possible, `if-else` statements could be replaced by:
```java
if (condition) {
    ...
    return obj;  
}  
// other logic codes in else could be moved here
```    
> <font color="#977C00">Note: </font> If statements like `if()...else if()...else...` have to be used to express the logic, **[Mandatory]** nested conditional level should not be more than three.   
> <font color="#019858">Positive example: </font> `if-else` code with over three nested conditional levels can be replaced by *guard statements* or *State Design Pattern*. Example of *guard statement*:

```java
public void today() {
    if (isBusy()) {
        System.out.println("Change time.");
        return;
    }

    if (isFree()) {
        System.out.println("Go to travel.");
        return;
    }

    System.out.println("Stay at home to learn Inova Java Coding Guidelines.");
    return;
}
```

4\. **[Recommended]** Do not use complicated statements in conditional statements (except for frequently used methods like *getXxx/isXxx*). Use *boolean* variables to store results of complicated statements temporarily will increase the code's readability.  
> <font color="#977C00">Note: </font>Logic within many `if` statements are very complicated. Readers need to analyze the final results of the conditional expression to decide what statement is to be executed in certain conditions.    
> <font color="#019858">Positive example: </font>
```java
// please refer to the pseudo-code as follows
boolean existed = (file.open(fileName, "w") != null) && (...) || (...);
if (existed) {
    ...
}  
```  
 > <font color="#FF4500">Counter example: </font>  
```java
if ((file.open(fileName, "w") != null) && (...) || (...)) {
    ...
}
```

5\. **[Recommended]** Performance should be considered when loop statements are used. The following operations are better to be processed outside the loop statement, including object and variable declaration, database connection, `try-catch` statements.

6\. **[Recommended]** Size of input parameters should be checked, especially for batch operations.  

7\. **[For Reference]** Input parameters should be checked in following scenarios:     
&emsp;&emsp;1) Low-frequency implemented methods.  
&emsp;&emsp;2) Overhead of parameter checking could be ignored in long-time execution methods, but if illegal parameters lead to exception, the loss outweighs the gain. Therefore, parameter checking is still recommended in long-time execution methods.  
&emsp;&emsp;3) Methods that needs extremely high stability or availability.    
&emsp;&emsp;4) Open API methods, including RPC/API/HTTP.  
&emsp;&emsp;5) Authority related methods.

8\. **[For Reference]** Cases that input parameters do not require validation:  
&emsp;&emsp;1) Methods very likely to be implemented in loops. A note should be included informing that parameter check should be done externally.   
&emsp;&emsp;2) Methods in bottom layers are very frequently called so generally do not need to be checked. e.g. If *DAO* layer and *Service* layer is deployed in the same server, parameter check in *DAO* layer can be omitted.    
&emsp;&emsp;3) *Private* methods that can only be implemented internally, if all parameters are checked or manageable.

### <font color="green">Code Comments</font>
1\. **[Mandatory]** *Javadoc* should be used for classes, class variables and methods. The format should be '/\*\* comment \*\*/', rather than '// xxx'.   
> <font color="#977C00">Note: </font> In IDE, *Javadoc* can be seen directly when hovering, which is a good way to improve efficiency.

2\. **[Mandatory]** Abstract methods (including methods in interface) should be commented by *Javadoc*. *Javadoc* should include method instruction, description of parameters, return values and possible exceptions.  

3\. **[Mandatory]** Every class should include information of author(s) and date.

4\. **[Mandatory]** Single line comments in a method should be put above the code to be commented, by using `//` and multiple lines by using `/* */`. Alignment for comments should be noticed carefully.

5\. **[Mandatory]** All enumeration type fields should be commented as *Javadoc* style.

6\. **[Recommended]** Local language can be used in comments if English cannot describe the problem properly. Keywords and proper nouns should be kept in English.  
 > <font color="#FF4500">Counter example: </font>To explain "TCP connection overtime" as "Transmission Control Protocol connection overtime" only makes it more difficult to understand.

7\. **[Recommended]** When code logic changes, comments need to be updated at the same time, especially for the changes of parameters, return value, exception and core logic.

8\. **[For Reference]** Notes need to be added when commenting out code.  
> <font color="#977C00">Note: </font> If the code is likely to be recovered later, a reasonable explanation needs to be added. If not, please delete directly because code history will be recorded by *svn* or *git*.

9\. **[For Reference]** Requirements for comments:   
&emsp;&emsp;1) Be able to represent design ideas and code logic accurately.   
&emsp;&emsp;2) Be able to represent business logic and help other programmers understand quickly. A large section of code without any comment is a disaster for readers. Comments are written for both oneself and other people. Design ideas can be quickly recalled even after a long time. Work can be quickly taken over by other people when needed.

10\. **[For Reference]** Proper naming and clear code structure are self-explanatory. Too many comments need to be avoided because it may cause too much work on updating if code logic changes.
 > <font color="#FF4500">Counter example: </font>  
```java
// put elephant into fridge
put(elephant, fridge);  
```  
The name of method and parameters already represent what does the method do, so there is no need to add extra comments.

11\. **[For Reference]** Tags in comments (e.g. TODO, FIXME) need to contain author and time. Tags need to be handled and cleared in time by scanning frequently. Sometimes online breakdown is caused by these unhandled tags.    
&emsp;&emsp;1) TODO: TODO means the logic needs to be done, but not finished yet. Actually,  TODO is a member of *Javadoc*, although it is not realized in *Javadoc* yet, but has already been widely used. TODO can only be used in class, interface and methods, since it is a *Javadoc* tag.   
&emsp;&emsp;2) FIXME: FIXME is used to represent that the code logic is not correct or does not work, should be fixed in time.

### <font color="green">Other</font>
1\. **[Mandatory]** When using regex, precompile needs to be done in order to increase the matching performance.  
> <font color="#977C00">Note: </font> Do not define `Pattern pattern = Pattern.compile(.);` within method body.

2\. **[Mandatory]** When using attributes of POJO in velocity, use attribute names directly. Velocity engine will invoke `getXxx()` of POJO automatically. In terms of *boolean* attributes, velocity engine will invoke `isXxx()` (Do not use *is* as prefix when naming boolean attributes).  
> <font color="#977C00">Note: </font>For wrapper class `Boolean`, velocity engine will invoke `getXxx()` first.

3\. **[Mandatory]** Variables must add exclamatory mark when passing to velocity engine from backend, like \$!{var}.  
 > <font color="#977C00">Note: </font>If attribute is *null* or does not exist, \${var} will be shown directly on web pages.

4\. **[Mandatory]** The return type of `Math.random()` is double, value range is *0<=x<1* (<font color="blue">0</font> is possible). If a random integer is required, do not multiply x by 10 then round the result. The correct way is to use `nextInt` or `nextLong` method which belong to Random Object.

5\. **[Mandatory]** Use `System.currentTimeMillis()` to get the current millisecond. Do not use `new Date().getTime()`.
> <font color="#977C00">Note: </font>In order to get a more accurate time, use `System.nanoTime()`. In JDK8, use `Instant` class to deal with situations like time statistics.

6\. **[Recommended]** It is better not to contain variable declaration, logical symbols or any complicated logic in velocity template files.

7\. **[Recommended]** Size needs to be specified when initializing any data structure if possible, in order to avoid memory issues caused by unlimited growth.

8\. **[Recommended]** Codes or configuration that is noticed to be obsoleted should be resolutely removed from projects.   
> <font color="#977C00">Note: </font>Remove obsoleted codes or configuration in time to avoid code redundancy.  
 > <font color="#019858">Positive example: </font>For codes which are temporarily removed and likely to be reused, use **`///`** to add a reasonable note.
```java
public static void hello() {
    /// Business is stopped temporarily by the owner.
    // Business business = new Business();
    // business.active();
    System.out.println("it's finished");
}
```

## <font color="green">2. Exception and Logs</font>

### <font color="green">Exception</font>
1\. **[Mandatory]** Do not catch *Runtime* exceptions defined in *JDK*, such as `NullPointerException` and `IndexOutOfBoundsException`. Instead, pre-check is recommended whenever possible.  
> <font color="#977C00">Note: </font>Use try-catch only if it is difficult to deal with pre-check, such as `NumberFormatException`.  
> <font color="#019858">Positive example: </font>```if (obj != null) {...}```  
> <font color="#FF4500">Counter example: </font> ```try { obj.method() } catch(NullPointerException e){…}```

2\. **[Mandatory]** Never use exceptions for ordinary control flow. It is ineffective and unreadable.

3\. **[Mandatory]** It is irresponsible to use a try-catch on a big chunk of code. Be clear about the stable and unstable code when using try-catch. The stable code that means no exception will throw. For the unstable code, catch as specific as possible for exception handling.

4\. **[Mandatory]** Do not suppress or ignore exceptions. If you do not want to handle it, then re-throw it. The top layer must handle the exception and translate it into what the user can understand.

5\. **[Mandatory]** Make sure to invoke the rollback if a method throws an Exception.

6\. **[Mandatory]** Closeable resources (stream, connection, etc.) must be handled in *finally* block. Never throw any exception from a *finally* block.  
> <font color="#977C00">Note: </font>Use the *try-with-resources* statement to safely handle closeable resources (Java 7+).

7\. **[Mandatory]** Never use *return* within a *finally* block. A *return* statement in a *finally* block will cause exceptions or result in a discarded return value in the *try-catch* block.

8\. **[Mandatory]** The *Exception* type to be caught needs to be the same class or superclass of the type that has been thrown.

9\. **[Recommended]** The return value of a method can be *null*. It is not mandatory to return an empty collection or object. Specify in *Javadoc* explicitly when the method might return *null*. The caller needs to make a *null* check to prevent `NullPointerException`.   
> <font color="#977C00">Note: </font>It is caller's responsibility to check the return value, as well as to consider the possibility that remote call fails or other runtime exception occurs.

10\. **[Recommended]** One of the most common errors is `NullPointerException`. Pay attention to the following situations:  
&emsp;&emsp;1) If the return type is primitive, return a value of wrapper class may cause `NullPointerException`.  
&emsp;&emsp;&emsp;&emsp;<font color="#FF4500">Counter example: </font>`public int f() { return Integer }` Unboxing a *null* value will throw a `NullPointerException`.   
&emsp;&emsp;2) The return value of a database query might be *null*.    
&emsp;&emsp;3) Elements in collection may be *null*, even though `Collection.isEmpty()` returns *false*.   
&emsp;&emsp;4) Return values from an RPC might be *null*.    
&emsp;&emsp;5) Data stored in sessions might by *null*.  
&emsp;&emsp;6) Method chaining, like `obj.getA().getB().getC()`, is likely to cause `NullPointerException`.  
&emsp;&emsp;&emsp;&emsp;<font color="#019858">Positive example: </font>Use `Optional` to avoid null check and NPE (Java 8+).  

11\. **[Recommended]** Use "throw exception" or "return error code". For HTTP or open API providers, "error code" must be used. It is recommended to throw exceptions inside an application. For cross-application RPC calls, <font color="blue">result</font> is preferred by encapsulating *isSuccess*, *error code* and brief error messages.  
> <font color="#977C00">Note: </font>Benefits to return Result for the RPC methods:  
&emsp;&emsp;1) Using the 'throw exception' method will occur a runtime error if the exception is not caught.  
&emsp;&emsp;2) If stack information it not attached, allocating custom exceptions with simple error message is not helpful to solve the problem. If stack information is attached, data serialization and transmission performance loss are also problems when frequent error occurs.

12\. **[Recommended]** Do not throw `RuntimeException`, `Exception`, or `Throwable` directly. It is recommended to use well defined custom exceptions such as `DAOException`, `ServiceException`, etc.

13\. **[For Reference]** Avoid duplicate code (Do not Repeat Yourself, also known as DRY principle).  
> <font color="#977C00">Note: </font>Copying and pasting code arbitrarily will inevitably lead to duplicated code. If you keep logic in one place, it is easier to change when needed. If necessary, extract common codes to methods, abstract classes or even shared modules.    
> <font color="#019858">Positive example: </font>For a class with a number of public methods that validate parameters in the same way, it is better to extract a method like:
```java
private boolean checkParam (DTO dto) {
    ...
}
```

### <font color="green">Logs</font>
1\. **[Mandatory]** Do not use API in log system (Log4j, Logback) directly. API in log framework SLF4J is recommended to use instead, which uses *Facade* pattern and is conducive to keep log processing consistent.
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
private static final Logger logger = LoggerFactory.getLogger(Abc.class);
```

2\. **[Mandatory]** Log files need to be kept for at least 15 days because some kinds of exceptions happen weekly.

3\. **[Mandatory]** Naming conventions of extended logs of an Application (such as RBI, temporary monitoring, access log, etc.):     
*appName\_logType\_logName.log*   
*logType*: Recommended classifications are *stats*, *desc*, *monitor*, *visit*, etc.    
*logName*: Log description.  
Benefits of this scheme: The file name shows what application the log belongs to, type of the log and what purpose is the log used for. It is also conducive for classification and search.   
> <font color="#019858">Positive example: </font>Name of the log file for monitoring the timezone conversion exception in *mppserver* application: *mppserver_monitor_timeZoneConvert.log*  
> <font color="#977C00">Note: </font>It is recommended to classify logs. Error logs and business logs should be stored separately as far as possible. It is not only easy for developers to view, but also convenient for system monitoring.

4\. **[Mandatory]** Logs at *TRACE / DEBUG / INFO* levels must use either conditional outputs or placeholders.
> <font color="#977C00">Note: </font>`logger.debug ("Processing trade with id: " + id + " symbol: " + symbol);` If the log level is warn, the above log will not be printed. However, it will perform string concatenation operator. `toString()` method of *symbol* will be called, which is a waste of system resources.   
> <font color="#019858">Positive example: </font>
```java
if (logger.isDebugEnabled()) {
    logger.debug("Processing trade with id: " + id + " symbol: " + symbol);
}     
```  
> <font color="#019858">Positive example: </font>
```java
logger.debug("Processing trade with id: {} and symbol : {} ", id, symbol);
```  

5\. **[Mandatory]** Ensure that additivity attribute of a Log4j logger is set to *false*, in order to avoid redundancy and save disk space.  
> <font color="#019858">Positive example: </font>
`<logger name="com.taobao.ecrm.member.config" additivity="false" \>`


6\. **[Mandatory]** The exception information should contain two types of information: the context information and the exception stack. If you do not want to handle the exception, re-throw it.  
 > <font color="#019858">Positive example: </font>
```java
logger.error(various parameters or objects toString + "_" + e.getMessage(), e);
```

7\. **[Recommended]** Carefully record logs. Use *Info* level selectively and do not use *Debug* level in production environment. If *Warn* is used to record business behavior, please pay attention to the size of logs. Make sure the server disk is not over-filled, and remember to delete these logs in time.  
> <font color="#977C00">Note: </font> Outputting a large number of invalid logs will have a certain impact on system performance, and is not conducive to rapid positioning problems. Please think about the log: do you really have these logs? What can you do to see this log? Is it easy to troubleshoot problems?

8\. **[Recommended]** Level *Warn* should be used to record invalid parameters, which is used to track data when problem occurs. Level *Error* only records the system logic error, abnormal and other important error messages.
