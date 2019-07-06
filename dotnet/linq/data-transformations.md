---
description: >-
  Language-Integrated Query (LINQ) is not only about retrieving data. It is also
  a powerful tool for transforming data.
---

# Data Transformations

## Joining Multiple Inputs into One Output Sequence

```csharp
var peopleInSeattle = (from student in students
                    where student.City == "Seattle"
                    select student.Last)
                    .Concat(from teacher in teachers
                            where teacher.City == "Seattle"
                            select teacher.Last);
```

## Selecting a Subset of each Source Element

```csharp
var query = from cust in Customer  
            select new {Name = cust.Name, City = cust.City};
```

## Transforming in-Memory Objects into XML

```csharp
var studentsToXML = new XElement("Root",
            from student in students
            let scores = string.Join(",", student.Scores)
            select new XElement("student",
                       new XElement("First", student.First),
                       new XElement("Last", student.Last),
                       new XElement("Scores", scores)
                    ) // end "student"
                ); // end "Root"
```

## Performing Operations on Source Elements

```csharp
class FormatQuery
{
    static void Main()
    {            
        // Data source.
        double[] radii = { 1, 2, 3 };

        // Query.
        IEnumerable<string> query =
            from rad in radii
            select $"Area = {rad * rad * Math.PI:F2}";

        // Query execution. 
        foreach (string s in query)
            Console.WriteLine(s);

        // Keep the console open in debug mode.
        Console.WriteLine("Press any key to exit.");
        Console.ReadKey();
    }
}
/* Output:
    Area = 3.14
    Area = 12.57
    Area = 28.27
*/
```

