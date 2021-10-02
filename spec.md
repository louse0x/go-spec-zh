# Go编程语言规范 #

## 基于版本： 2021年7月26日 ##

## 概述 ##

这是一本Go编程语言的参考手册。关于更新信息和其他文档，见[golang.org](https://golang.org/)。

Go是一种以系统编程为设计目的的通用语言。它是强类型和垃圾回收的，并且明确支持并发编程。程序由包构成，其属性允许有效管理依赖关系。

语法紧凑，解析简单，便于集成开发环境等自动化工具分析。 

## 符号 ##

使用扩展巴科斯-瑙尔范式 (EBNF) 指定语法： 

```go
Production  = production_name "=" [ Expression ] "." .
Expression  = Alternative { "|" Alternative } .
Alternative = Term { Term } .
Term        = production_name | token [ "…" token ] | Group | Option | Repetition .
Group       = "(" Expression ")" .
Option      = "[" Expression "]" .
Repetition  = "{" Expression "}" .
```

> 译：
>
> ```go	
> 生成式 = 生成式名 '=' [ 表达式 ] ['.'] .
> 表达式 = 选择项 { '|' 选择项 } .
> 选择项 = 条目 { 条目 } ;
> 条目   = 生成式名 | 标记 [ '…' 标记 ] | 分组 | 可选项 | 重复项 .
> 分组   = '(' 表达式 ')' .
> 可选项 = '[' 表达式 ']' .
> 重复项 = '{' 表达式 '}' .
> ```

生成式是由术语和以下运算符构成的表达式，其优先级不断提高（*译：自上而下*）。

```go
|   alternation
()  grouping
[]  option (0 or 1 times)
{}  repetition (0 to n times)
```

> 译：
>
> ```go
> |   选择
> ()  分组
> []  可选（0 或 1 次）
> {}  重复（0 到 n 次）
> ```

小写生成式名用于标识词法标记。非终结符使用驼峰记法。词汇标记用**双引号""**或**反引号``**括起来。

`a ... b`的形式表示从`a`到`b`的一组字符作为备选。在规范的其他地方也使用**水平省略号...**来非正式地表示各种枚举或没有进一步指定的代码片断。字符`...`（相对于三个字符`...`而言）不是Go语言的标记。

