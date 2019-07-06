---
description: >-
  Language-Integrated Query (LINQ) is the name for a set of technologies based
  on the integration of query capabilities directly into the C# language.
---

# LINQ

You can write LINQ queries in C\# for SQL Server databases, XML documents, ADO.NET Datasets, and any collection of objects that supports [IEnumerable](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerable) or the generic [IEnumerable&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ienumerable-1) interface. LINQ support is also provided by third parties for many Web services and other database implementations.

For a developer who writes queries, the most visible "language-integrated" part of LINQ is the query expression. Query expressions are written in a declarative _query syntax_. By using query syntax, you can perform filtering, ordering, and grouping operations on data sources with a minimum of code. 

## Query expression overview

1.  A query is not executed until you iterate over the query variable.
2.  As a rule when you write LINQ queries, we recommend that you use **query syntax** whenever possible and **method syntax** whenever necessary.
3.  Some query operations, such as [Count](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.count) or [Max](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.max), have no equivalent query expression clause and must therefore be expressed as a method call. Method syntax can be combined with query syntax in various ways. For more information, see [Query syntax and method syntax in LINQ](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq).
4.  Query expressions can be compiled to expression trees or to delegates, depending on the type that the query is applied to. [IEnumerable&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ienumerable-1) queries are compiled to delegates. [IQueryable](https://docs.microsoft.com/en-us/dotnet/api/system.linq.iqueryable) and [IQueryable&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.linq.iqueryable-1)queries are compiled to expression trees. For more information, see [Expression trees](https://docs.microsoft.com/en-us/dotnet/csharp/expression-trees).

{% hint style="info" %}
 To force immediate execution of any query and cache its results, you can call the [ToList](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.tolist) or [ToArray](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.toarray) methods.
{% endhint %}

## Basic LINQ Query Operations <a id="basic-linq-query-operations-c"></a>

### Filtering:  <a id="filtering"></a>

 The result is produced by using the `where` clause. 

```csharp
var queryLondonCustomers = from cust in customers
                           where cust.City == "London"
                           select cust;
// With And or OR
where cust.City=="London" && cust.Name == "Devon"
where cust.City == "London" || cust.City == "Paris"
```

### Ordering: <a id="ordering"></a>

 The `orderby` clause will cause the elements in the returned sequence to be sorted according to the default comparer for the type being sorted. 

```csharp
var queryLondonCustomers3 = 
    from cust in customers
    where cust.City == "London"
    orderby cust.Name ascending
    select cust;
```

### Grouping: <a id="grouping"></a>

 The `group` clause enables you to group your results based on a key that you specify.

```csharp
// queryCustomersByCity is an IEnumerable<IGrouping<string, Customer>>
  var queryCustomersByCity =
      from cust in customers
      group cust by cust.City;

  // customerGroup is an IGrouping<string, Customer>
  foreach (var customerGroup in queryCustomersByCity)
  {
      Console.WriteLine(customerGroup.Key);
      foreach (Customer customer in customerGroup)
      {
          Console.WriteLine("    {0}", customer.Name);
      }
  }
```

 When you end a query with a `group` clause, your results take the form of a list of lists. Each element in the list is an object that has a `Key` member and a list of elements that are grouped under that key. 

 If you must refer to the results of a group operation, you can use the `into` keyword to create an identifier that can be queried further.

```csharp
// custQuery is an IEnumerable<IGrouping<string, Customer>>
var custQuery =
    from cust in customers
    group cust by cust.City into custGroup
    where custGroup.Count() > 2
    orderby custGroup.Key
    select custGroup;
```

### Joining: <a id="joining"></a>

 Join operations create associations between sequences that are not explicitly modeled in the data sources.  In LINQ the `join` clause always works against object collections instead of database tables directly.

```csharp
var innerJoinQuery =
    from cust in customers
    join dist in distributors on cust.City equals dist.City
    select new { CustomerName = cust.Name, DistributorName = dist.Name };
```

### Selecting \(Projections\): <a id="selecting-projections"></a>

 The `select` clause produces the results of the query and specifies the "shape" or type of each returned element. 

