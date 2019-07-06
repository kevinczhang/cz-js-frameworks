---
description: The standard query operators are the methods that form the LINQ pattern.
---

# Standard Query Operators

Most of these methods operate on sequences, where a sequence is an object whose type implements the [IEnumerable&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ienumerable-1) interface or the [IQueryable&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.linq.iqueryable-1) interface. There are two sets of LINQ standard query operators, one that operates on objects of type [IEnumerable&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ienumerable-1) and the other that operates on objects of type [IQueryable&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.linq.iqueryable-1). 

 The [Enumerable](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable) type defines two such methods: [Cast&lt;TResult&gt;\(IEnumerable\)](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.cast#System_Linq_Enumerable_Cast__1_System_Collections_IEnumerable_) and [OfType&lt;TResult&gt;\(IEnumerable\)](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.oftype#System_Linq_Enumerable_OfType__1_System_Collections_IEnumerable_), let you enable a non-parameterized, or non-generic, collection to be queried in the LINQ pattern.  The [Queryable](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable) class defines two similar methods, [Cast&lt;TResult&gt;\(IQueryable\)](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.cast#System_Linq_Queryable_Cast__1_System_Linq_IQueryable_) and [OfType&lt;TResult&gt;\(IQueryable\)](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.oftype#System_Linq_Queryable_OfType__1_System_Linq_IQueryable_), that operate on objects of type [Queryable](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable).

## Sorting Data <a id="sorting-data-c"></a>

| Method Name | Description | C\# Query Expression Syntax | More Information |
| :--- | :--- | :--- | :--- |
| OrderBy | Sorts values in ascending order. | `orderby` | [Enumerable.OrderBy](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.orderby)  [Queryable.OrderBy](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.orderby) |
| OrderByDescending | Sorts values in descending order. | `orderby … descending` | [Enumerable.OrderByDescending](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.orderbydescending)  [Queryable.OrderByDescending](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.orderbydescending) |
| ThenBy | Performs a secondary sort in ascending order. | `orderby …, …` | [Enumerable.ThenBy](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.thenby)  [Queryable.ThenBy](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.thenby) |
| ThenByDescending | Performs a secondary sort in descending order. | `orderby …, … descending` | [Enumerable.ThenByDescending](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.thenbydescending)  [Queryable.ThenByDescending](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.thenbydescending) |
| Reverse | Reverses the order of the elements in a collection. | Not applicable. | [Enumerable.Reverse](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.reverse)  [Queryable.Reverse](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.reverse) |

## Set Operations <a id="set-operations-c"></a>

| Method Name | Description | C\# Query Expression Syntax | More Information |
| :--- | :--- | :--- | :--- |
| Distinct | Removes duplicate values from a collection. | Not applicable. | [Enumerable.Distinct](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.distinct)  [Queryable.Distinct](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.distinct) |
| Except | Returns the set difference, which means the elements of one collection that do not appear in a second collection. | Not applicable. | [Enumerable.Except](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.except)  [Queryable.Except](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.except) |
| Intersect | Returns the set intersection, which means elements that appear in each of two collections. | Not applicable. | [Enumerable.Intersect](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.intersect)  [Queryable.Intersect](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.intersect) |
| Union | Returns the set union, which means unique elements that appear in either of two collections. | Not applicable. | [Enumerable.Union](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.union)  [Queryable.Union](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.union) |

## Filtering Data <a id="filtering-data-c"></a>

| Method Name | Description | C\# Query Expression Syntax | More Information |
| :--- | :--- | :--- | :--- |
| OfType | Selects values, depending on their ability to be cast to a specified type. | Not applicable. | [Enumerable.OfType](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.oftype)  [Queryable.OfType](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.oftype) |
| Where | Selects values that are based on a predicate function. | `where` | [Enumerable.Where](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.where)  [Queryable.Where](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.where) |

## Quantifier Operations <a id="quantifier-operations-c"></a>

| Method Name | Description | C\# Query Expression Syntax | More Information |
| :--- | :--- | :--- | :--- |
| All | Determines whether all the elements in a sequence satisfy a condition. | Not applicable. | [Enumerable.All](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.all)  [Queryable.All](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.all) |
| Any | Determines whether any elements in a sequence satisfy a condition. | Not applicable. | [Enumerable.Any](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.any)  [Queryable.Any](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.any) |
| Contains | Determines whether a sequence contains a specified element. | Not applicable. | [Enumerable.Contains](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.contains)  [Queryable.Contains](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.contains) |

## Projection Operations <a id="projection-operations-c"></a>

| Method Name | Description | C\# Query Expression Syntax | More Information |
| :--- | :--- | :--- | :--- |
| Select | Projects values that are based on a transform function. | `select` | [Enumerable.Select](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.select)  [Queryable.Select](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.select) |
| SelectMany | Projects sequences of values that are based on a transform function and then flattens them into one sequence. | Use multiple `from` clauses | [Enumerable.SelectMany](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.selectmany)  [Queryable.SelectMany](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.selectmany) |

## Partitioning Data <a id="partitioning-data-c"></a>

| Operator Name | Description | C\# Query Expression Syntax | More Information |
| :--- | :--- | :--- | :--- |


| Skip | Skips elements up to a specified position in a sequence. | Not applicable. | [Enumerable.Skip](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.skip)  [Queryable.Skip](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.skip) |
| :--- | :--- | :--- | :--- |


| SkipWhile | Skips elements based on a predicate function until an element does not satisfy the condition. | Not applicable. | [Enumerable.SkipWhile](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.skipwhile)  [Queryable.SkipWhile](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.skipwhile) |
| :--- | :--- | :--- | :--- |


| Take | Takes elements up to a specified position in a sequence. | Not applicable. | [Enumerable.Take](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.take)  [Queryable.Take](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.take) |
| :--- | :--- | :--- | :--- |


| TakeWhile | Takes elements based on a predicate function until an element does not satisfy the condition. | Not applicable. | [Enumerable.TakeWhile](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.takewhile)  [Queryable.TakeWhile](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.takewhile) |
| :--- | :--- | :--- | :--- |


## Grouping Data <a id="grouping-data-c"></a>

| Method Name | Description | C\# Query Expression Syntax | More Information |
| :--- | :--- | :--- | :--- |
| GroupBy | Groups elements that share a common attribute. Each group is represented by an [IGrouping&lt;TKey,TElement&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.linq.igrouping-2) object. | `group … by`  -or-  `group … by … into …` | [Enumerable.GroupBy](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.groupby)  [Queryable.GroupBy](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.groupby) |
| ToLookup | Inserts elements into a [Lookup&lt;TKey,TElement&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.linq.lookup-2) \(a one-to-many dictionary\) based on a key selector function. | Not applicable. | [Enumerable.ToLookup](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.tolookup) |

## Generation Operations <a id="generation-operations-c"></a>

| Method Name | Description | C\# Query Expression Syntax | More Information |
| :--- | :--- | :--- | :--- |
| DefaultIfEmpty | Replaces an empty collection with a default valued singleton collection. | Not applicable. | [Enumerable.DefaultIfEmpty](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.defaultifempty)  [Queryable.DefaultIfEmpty](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.defaultifempty) |
| Empty | Returns an empty collection. | Not applicable. | [Enumerable.Empty](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.empty) |
| Range | Generates a collection that contains a sequence of numbers. | Not applicable. | [Enumerable.Range](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.range) |
| Repeat | Generates a collection that contains one repeated value. | Not applicable. | [Enumerable.Repeat](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.repeat) |

## Equality Operations <a id="equality-operations-c"></a>

| Method Name | Description | C\# Query Expression Syntax | More Information |
| :--- | :--- | :--- | :--- |
| SequenceEqual | Determines whether two sequences are equal by comparing elements in a pair-wise manner. | Not applicable. | [Enumerable.SequenceEqual](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.sequenceequal)  [Queryable.SequenceEqual](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.sequenceequal) |

## Element Operations <a id="element-operations-c"></a>

| Method Name | Description | C\# Query Expression Syntax | More Information |
| :--- | :--- | :--- | :--- |
| ElementAt | Returns the element at a specified index in a collection. | Not applicable. | [Enumerable.ElementAt](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.elementat)  [Queryable.ElementAt](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.elementat) |
| ElementAtOrDefault | Returns the element at a specified index in a collection or a default value if the index is out of range. | Not applicable. | [Enumerable.ElementAtOrDefault](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.elementatordefault)  [Queryable.ElementAtOrDefault](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.elementatordefault) |
| First | Returns the first element of a collection, or the first element that satisfies a condition. | Not applicable. | [Enumerable.First](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.first)  [Queryable.First](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.first) |
| FirstOrDefault | Returns the first element of a collection, or the first element that satisfies a condition. Returns a default value if no such element exists. | Not applicable. | [Enumerable.FirstOrDefault](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.firstordefault)  [Queryable.FirstOrDefault](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.firstordefault)  [Queryable.FirstOrDefault&lt;TSource&gt;\(IQueryable&lt;TSource&gt;\)](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.firstordefault#System_Linq_Queryable_FirstOrDefault__1_System_Linq_IQueryable___0__) |
| Last | Returns the last element of a collection, or the last element that satisfies a condition. | Not applicable. | [Enumerable.Last](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.last)  [Queryable.Last](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.last) |
| LastOrDefault | Returns the last element of a collection, or the last element that satisfies a condition. Returns a default value if no such element exists. | Not applicable. | [Enumerable.LastOrDefault](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.lastordefault)  [Queryable.LastOrDefault](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.lastordefault) |
| Single | Returns the only element of a collection or the only element that satisfies a condition. Throws an [InvalidOperationException](https://docs.microsoft.com/en-us/dotnet/api/system.invalidoperationexception) if there is no element or more than one element to return. | Not applicable. | [Enumerable.Single](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.single)  [Queryable.Single](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.single) |
| SingleOrDefault | Returns the only element of a collection or the only element that satisfies a condition. Returns a default value if there is no element to return. Throws an [InvalidOperationException](https://docs.microsoft.com/en-us/dotnet/api/system.invalidoperationexception) if there is more than one element to return. | Not applicable. | [Enumerable.SingleOrDefault](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.singleordefault)  [Queryable.SingleOrDefault](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.singleordefault) |

## Converting Data Types <a id="converting-data-types-c"></a>

| Method Name | Description | C\# Query Expression Syntax | More Information |
| :--- | :--- | :--- | :--- |
| AsEnumerable | Returns the input typed as [IEnumerable&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.ienumerable-1). | Not applicable. | [Enumerable.AsEnumerable](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.asenumerable) |
| AsQueryable | Converts a \(generic\) [IEnumerable](https://docs.microsoft.com/en-us/dotnet/api/system.collections.ienumerable) to a \(generic\) [IQueryable](https://docs.microsoft.com/en-us/dotnet/api/system.linq.iqueryable). | Not applicable. | [Queryable.AsQueryable](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.asqueryable) |
| Cast | Casts the elements of a collection to a specified type. | Use an explicitly typed range variable. For example:  `from string str in words` | [Enumerable.Cast](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.cast)  [Queryable.Cast](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.cast) |
| OfType | Filters values, depending on their ability to be cast to a specified type. | Not applicable. | [Enumerable.OfType](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.oftype)  [Queryable.OfType](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.oftype) |
| ToArray | Converts a collection to an array. This method forces query execution. | Not applicable. | [Enumerable.ToArray](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.toarray) |
| ToDictionary | Puts elements into a [Dictionary&lt;TKey,TValue&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.dictionary-2)based on a key selector function. This method forces query execution. | Not applicable. | [Enumerable.ToDictionary](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.todictionary) |
| ToList | Converts a collection to a [List&lt;T&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.collections.generic.list-1). This method forces query execution. | Not applicable. | [Enumerable.ToList](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.tolist) |
| ToLookup | Puts elements into a [Lookup&lt;TKey,TElement&gt;](https://docs.microsoft.com/en-us/dotnet/api/system.linq.lookup-2) \(a one-to-many dictionary\) based on a key selector function. This method forces query execution. | Not applicable. | [Enumerable.ToLookup](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.tolookup) |

## Concatenation Operations <a id="concatenation-operations-c"></a>

| Method Name | Description | C\# Query Expression Syntax | More Information |
| :--- | :--- | :--- | :--- |
| Concat | Concatenates two sequences to form one sequence. | Not applicable. | [Enumerable.Concat](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.concat)  [Queryable.Concat](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.concat) |

## Aggregation Operations <a id="aggregation-operations-c"></a>

| Method Name | Description | C\# Query Expression Syntax | More Information |
| :--- | :--- | :--- | :--- |
| Aggregate | Performs a custom aggregation operation on the values of a collection. | Not applicable. | [Enumerable.Aggregate](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.aggregate)  [Queryable.Aggregate](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.aggregate) |
| Average | Calculates the average value of a collection of values. | Not applicable. | [Enumerable.Average](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.average)  [Queryable.Average](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.average) |
| Count | Counts the elements in a collection, optionally only those elements that satisfy a predicate function. | Not applicable. | [Enumerable.Count](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.count)  [Queryable.Count](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.count) |
| LongCount | Counts the elements in a large collection, optionally only those elements that satisfy a predicate function. | Not applicable. | [Enumerable.LongCount](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.longcount)  [Queryable.LongCount](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.longcount) |
| Max | Determines the maximum value in a collection. | Not applicable. | [Enumerable.Max](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.max)  [Queryable.Max](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.max) |
| Min | Determines the minimum value in a collection. | Not applicable. | [Enumerable.Min](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.min)  [Queryable.Min](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.min) |
| Sum | Calculates the sum of the values in a collection. | Not applicable. | [Enumerable.Sum](https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable.sum)  [Queryable.Sum](https://docs.microsoft.com/en-us/dotnet/api/system.linq.queryable.sum) |

