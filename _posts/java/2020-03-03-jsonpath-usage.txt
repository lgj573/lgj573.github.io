---
layout: post
title: json解析神器 jsonpath的使用
category: java
tags: [json , jsonpath]
description: json解析神器 jsonpath的使用
---

# json解析神器 jsonpath的使用

github地址:[https://github.com/json-path/JsonPath](https://github.com/json-path/JsonPath)

fastjson 1.2.0之后的版本支持JSONPath。这是一个很强大的功能，可以在java框架中当作对象查询语言（OQL）来使用。

官网地址: https://github.com/alibaba/fastjson/wiki/JSONPath

JSONPath - 是xpath在json的应用。

xml最大的优点就有大量的工具可以分析，转换，和选择性的提取文档中的数据。XPath是这些最强大的工具之一。
如果可以使用xpath来解析json，以下的问题可以被解决：

1，数据不使用特殊的脚本，可以在客户端交互的发现并取并获取。
2，客户机请求的JSON数据可以减少到服务器上的相关部分，这样可以最大限度地减少服务器响应的带宽使用率。
如果我们愿意，这个可以解析json数据的工具会变得有意义。随之而来的问题是它如何工作，jsonpath的表达式看起来怎么样。

事实上，json是由c系统编程语言表示自然数据，有特定语言的特定语法来访问json数据。

xpath的表达式：
- /store/book[1]/title

我们可以看作是：
- x.store.book[0].title
或
- x['store']['book'][0]['title']

在Javascript, Python 和 PHP 中一个变量x表示json数据。经过观察，特定的语言里有内置xpath来解析数据。

JSONPath工具的问题

-依赖某种特定的语言
- 需要依赖XPath 1.0
- 减少代码量和内存的消耗
- 在运行时

## JSONPath 表达式

JSONPath 是参照，xpath表达式来解析xml文档的方式，json数据结构通常是匿名的并且不一定需要有根元素。JSONPaht 用一个抽象的名字$来表示最外层对象。

JOSNPath 表达式可以使用.  符号如下：   
$.store.book[0].title

或者使用[] 符号   
$['store']['book'][0]['title']


从输入路径来看。内部或者输出的路径都会转化成-符号。

JSONPath 允许使用通配符 * 表示所以的子元素名和数组索引。还允许使用 '..' 从E4X参照过来的和数组切分语法[start:end:step]是从ECMASCRIPT 4 参照过来的。

表达式在下面的脚本语言中可以使用显示的名称或者索引：  
$.store.book[(@.length-1)].title


使用'@'符号表示当前的对象，?(<判断表达式>) 使用逻辑表达式来过滤。  
$.store.book[?(@.price < 10)].title

 
## 简单的java项目demo:
```
public class JsonPathDemo {
    public static void main(String[] args) {
        String json = FileUtils.readFileByLines("demo.json");
        ReadContext context = JsonPath.parse(json);

        //1 返回所有name
        List<String> names = context.read("$.result.records[*].name");
        //["张三","李四","王五"]
        System.out.println(names);

        //2 返回所有数组的值
        List<Map<String, String>> objs = context.read("$.result.records[*]");
        //[{"name":"张三","pid":"500234199212121212","mobile":"18623456789","applied_at":"3","confirmed_at":"5","confirm_type":"overdue","loan_type":"1","test":"mytest","all":"2"},{"name":"李四","pid":"500234199299999999","mobile":"13098765432","applied_at":"1","confirmed_at":"","confirm_type":"overdue","loan_type":"3","all":"3"},{"name":"王五","pid":"50023415464654659","mobile":"1706454894","applied_at":"-1","confirmed_at":"","confirm_type":"overdue","loan_type":"3"}]
        System.out.println(objs);

        //3 返回第一个的name
        String name0 = context.read("$.result.records[0].name");
        //张三
        System.out.println(name0);

        //4 返回下标为0 和 2 的数组值
        List<String> name0and2 = context.read("$.result.records[0,2].name");
        //["张三","王五"]
        System.out.println(name0and2);

        //5 返回下标为0 到 下标为1的 的数组值  这里[0:2] 表示包含0 但是 不包含2
        List<String> name0to2 = context.read("$.result.records[0:2].name");
        //["张三","李四"]
        System.out.println(name0to2);

        //6 返回数组的最后两个值
        List<String> lastTwoName = context.read("$.result.records[-2:].name");
        //["李四","王五"]
        System.out.println(lastTwoName);

        //7 返回下标为1之后的所有数组值 包含下标为1的
        List<String> nameFromOne = context.read("$.result.records[1:].name");
        //["李四","王五"]
        System.out.println(nameFromOne);

        //8 返回下标为3之前的所有数组值  不包含下标为3的
        List<String> nameEndTwo = context.read("$.result.records[:3].name");
        //["张三","李四","王五"]
        System.out.println(nameEndTwo);

        //9 返回applied_at大于等于2的值
        List<Map<String, String>> records = context.read("$.result.records[?(@.applied_at >= '2')]");
        //[{"name":"张三","pid":"500234199212121212","mobile":"18623456789","applied_at":"3","confirmed_at":"5","confirm_type":"overdue","loan_type":"1","test":"mytest","all":"2"}]
        System.out.println(records);

        //10 返回name等于李四的值
        List<Map<String, String>> records0 = context.read("$.result.records[?(@.name == '李四')]");
        //[{"name":"李四","pid":"500234199299999999","mobile":"13098765432","applied_at":"1","confirmed_at":"","confirm_type":"overdue","loan_type":"3"}]
        System.out.println(records0);

        //11 返回有test属性的数组
        List<Map<String, String>> records1 = context.read("$.result.records[?(@.test)]");
        //[{"name":"张三","pid":"500234199212121212","mobile":"18623456789","applied_at":"3","confirmed_at":"5","confirm_type":"overdue","loan_type":"1","test":"mytest","all":"2"}]
        System.out.println(records1);

        //12 返回有test属性的数组
        List<String> list = context.read("$..all");
        //["1","4","2","3"]
        System.out.println(list);

        //12 以当前json的某个值为条件查询 这里ok为1 取出records数组中applied_at等于1的数组
        List<String> ok = context.read("$.result.records[?(@.applied_at == $['ok'])]");
        //["1","4","2","3"]
        System.out.println(ok);

        //13 正则匹配
        List<String> regexName = context.read("$.result.records[?(@.pid =~ /.*999/i)]");
        //[{"name":"李四","pid":"500234199299999999","mobile":"13098765432","applied_at":"1","confirmed_at":"","confirm_type":"overdue","loan_type":"3","all":"3"}]
        System.out.println(regexName);

        //14 多条件
        List<String> mobile = context.read("$.result.records[?(@.all == '2' || @.name == '李四' )].mobile");
        //["18623456789","13098765432"]
        System.out.println(mobile);

        //14 查询数组长度
        Integer length01 = context.read("$.result.records.length()");
        //3
        System.out.println(length01);

        //15 查询list里面每个对象长度
        List<Integer> length02 = context.read("$.result.records[?(@.all == '2' || @.name == '李四' )].length()");
        //[9,8]
        System.out.println(length02);

        //16 最大值
        Object maxV = context.read("$.max($.result.records[0].loan_type,$.result.records[1].loan_type,$.result.records[2].loan_type)");
        //3.0
        System.out.println(maxV);

        //17 最小值
        Object minV = context.read("$.min($.result.records[0].loan_type,$.result.records[1].loan_type,$.result.records[2].loan_type)");
        //1.0
        System.out.println(minV);

        //18 平均值
        double avgV = context.read("$.avg($.result.records[0].loan_type,$.result.records[1].loan_type,$.result.records[2].loan_type)");
        //2.3333333333333335
        System.out.println(avgV);

        //19 标准差
        double stddevV = context.read("$.stddev($.result.records[0].loan_type,$.result.records[1].loan_type,$.result.records[2].loan_type)");
        //0.9428090415820636
        System.out.println(stddevV);

        //20 读取一个不存在的
        String haha = context.read("$.result.haha");
        //抛出异常
        //Exception in thread "main" com.jayway.jsonpath.PathNotFoundException: No results for path: $['result']['haha']
        //at com.jayway.jsonpath.internal.path.EvaluationContextImpl.getValue(EvaluationContextImpl.java:133)
        //at com.jayway.jsonpath.JsonPath.read(JsonPath.java:187)
        //at com.jayway.jsonpath.internal.JsonContext.read(JsonContext.java:102)
        //at com.jayway.jsonpath.internal.JsonContext.read(JsonContext.java:89)
        //at cn.lijie.jsonpath.JsonPathDemo.main(JsonPathDemo.java:58)
        //at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        //at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        //at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        //at java.lang.reflect.Method.invoke(Method.java:498)
        //at com.intellij.rt.execution.application.AppMain.main(AppMain.java:147)
        System.out.println(haha);
    }
}
```
原文链接：https://blog.csdn.net/qq_20641565/article/details/77162868

pom文件引入:
```
        <dependency>
            <groupId>com.jayway.jsonpath</groupId>
            <artifactId>json-path</artifactId>
            <version>2.3.0</version>
        </dependency>
```
还需要json-smart，commons-lang

其中demo.json是一个测试json:
```
{
  "action": "/interface.service/xxx/queryBlackUserData",
  "all": "1",
  "result": {
    "count": 2,
    "tenant_count": 2,
    "records": [
      {
        "name": "张三",
        "pid": "500234199212121212",
        "mobile": "18623456789",
        "applied_at": "3",
        "confirmed_at": "5",
        "confirm_type": "overdue",
        "loan_type": 1,
        "test": "mytest",
        "all": "2"
      },
      {
        "name": "李四",
        "pid": "500234199299999999",
        "mobile": "13098765432",
        "applied_at": "1",
        "confirmed_at": "",
        "confirm_type": "overdue",
        "loan_type": 3,
        "all": "3"
      },
      {
        "name": "王五",
        "pid": "50023415464654659",
        "mobile": "1706454894",
        "applied_at": "-1",
        "confirmed_at": "",
        "confirm_type": "overdue",
        "loan_type": 3
      }
    ],
    "all": "4"
  },
  "code": 200,
  "subtime": "1480495123550",
  "status": "success",
  "ok": 3
}
```
FileUtils类是用于读取xx.json文件为字符串的json:
```
public class FileUtils {
    /**
     * 以行为单位读取文件，常用于读面向行的格式化文件
     */
    public static String readFileByLines(String fileName) {
        File file = new File(fileName);
        BufferedReader reader = null;
        String str = "";
        try {
            InputStream is = FileUtils.class.getClassLoader().getResourceAsStream(fileName);
            reader = new BufferedReader(new InputStreamReader(is));
            String tempString = null;
            int line = 1;
            // 一次读入一行，直到读入null为文件结束
            while ((tempString = reader.readLine()) != null) {
                // 显示行号
                str += tempString;
            }
            reader.close();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (reader != null) {
                try {
                    reader.close();
                } catch (IOException e1) {
                }
            }
        }
        return str;
    }
}
```
