---
description: >-
  Query syntax and method syntax are semantically identical, but many people
  find query syntax simpler and easier to read. Some queries must be expressed
  as method calls.
---

# Query Syntax and Method Syntax

```csharp
//Query syntax:
IEnumerable<int> numQuery1 = 
          from num in numbers
          where num % 2 == 0
          orderby num
          select num;

//Method syntax:
IEnumerable<int> numQuery2 = numbers.Where(num => num % 2 == 0).OrderBy(n => n);
```

## Lambda Expressions

 A lambda expression is an [anonymous function](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/anonymous-methods) that you can use to create [delegates](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/delegates/using-delegates) or [expression tree](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/expression-trees/index) types.  To create a lambda expression, you specify input parameters \(if any\) on the left side of the lambda operator [=&gt;](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-operator), and you put the expression or statement block on the other side. 

{% code-tabs %}
{% code-tabs-item title="Delegate" %}
```csharp
delegate int del(int i);  
static void Main(string[] args)  
{  
    del myDelegate = x => x * x;  
    int j = myDelegate(5); //j = 25  
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="Expression Tree" %}
```csharp
using System.Linq.Expressions;  
  
namespace ConsoleApplication1  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            Expression<del> myET = x => x * x;  
        }  
    }  
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

 The Lambda expression evolves from anonymous method by first removing the delegate keyword and parameter type and adding a lambda operator =&gt;.

![Lambda Expression from Anonymous Method](../../.gitbook/assets/image%20%284%29.png)

1. Lambda Expression is a shorter way of representing anonymous method.
2. Lambda Expression syntax: `parameters => body expression`
3. Lambda Expression can have zero parameter.
4. Lambda Expression can have multiple parameters in parenthesis \(\).
5. Lambda Expression can have multiple statements in body expression in curly brackets {}.
6. Lambda Expression can be assigned to Func, Action or Predicate delegate.
7. Lambda Expression can be invoked in a similar way to delegate.



