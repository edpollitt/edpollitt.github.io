---
layout: post
title: 'Festive Brainteasers'
tags: [csharp]
---

*On the first day of Christmas my true love gave to me...*

**A festive message. What’s the output?**

~~~csharp
static void Main()
{
    var sb = new StringBuilder();
    Greetings(sb);
    Console.WriteLine(sb.ToString());
}

static void Greetings(StringBuilder sb)
{
    sb.Append("Merry Christmas");
    sb = null;
    sb = new StringBuilder("Bah Humbug");
}
~~~



*On the second day of Christmas my true love gave to me...*

**A pair of extension methods. Are they equivalent? What’s the difference?**

~~~csharp
public static bool IsGreaterThan(this IComparable first, IComparable second) 
{
    return first.CompareTo(second) > 0;
}
~~~
~~~csharp
public static bool IsGreaterThan<T>(this T first, T second)
	where T : IComparable 
{
    return first.CompareTo(second) > 0;
}
~~~



*On the third day of Christmas my true love gave to me...*

**A unit test. Does it pass?**

~~~csharp
[Test]
void Should_throw_on_non_alphanumeric_characters()
{
    Action encoding = () => Encode("Merry Christmas!!");
    encoding.ShouldThrow<InvalidOperationException>();
}
~~~
~~~csharp
public IEnumerable<char> Encode(string s)
{
    foreach (var c in s)
    {
        if (!Char.IsLetterOrDigit(c))
            throw new InvalidOperationException($"Cannot encode char '{c}'"));
                  
        yield return (char)(c * 17 % 101);
    }
}
~~~



*On the fourth day of Christmas my true love gave to me...*

**Seasonal greetings. What’s the output?**

~~~csharp
var a = "Merry Christmas";
var b = string.Format("{0} {1}", "Merry", "Christmas");

object x = "Merry Christmas";
object y = string.Format("{0} {1}", "Merry", "Christmas");

Console.WriteLine(a == b);
Console.WriteLine(x == y);
Console.WriteLine(a == x);
Console.WriteLine(b == y);
~~~



*On the fifth day of Christmas my true love gave to me...*

**A warped counter. What’s the output?**

~~~csharp
struct Counter
{
    int _counter;
     
    public override string ToString()
    {
        return _counter++.ToString();
    }
}

void Main()
{
    var a = new Counter();
    var b = a;
    var c = (object)b;
    var d = c;
    Console.WriteLine(a);
    Console.WriteLine(b);
    Console.WriteLine(c);
    Console.WriteLine(d);
	Console.WriteLine(a);
}
~~~



*On the sixth day of Christmas my true love gave to me...*

**A broken sum. What’s the output?**

~~~csharp
var floats = new[] { 10.99f, 6.01f, 1.5f };    
var sum = floats.Cast<int>().Sum();
Console.WriteLine(sum);
~~~



*On the seventh day of Christmas my true love gave to me...*

**A type comparison. Can you make the following method return false?**

~~~csharp
bool Foo<T>() where T : new()
{
    var t = new T();
    return t is T;
}
~~~


*On the eighth day of Christmas my true love gave to me...*

**A convoluted inheritance hierarchy. What’s the output?**

~~~csharp
void Main()
{
    Console.WriteLine(new A());
    Console.WriteLine(new B());
    Console.WriteLine(new C());
    Console.WriteLine(new D());
    Console.WriteLine(new E());
}

class A
{
    protected virtual string Name { get { return "A"; } }
    public override string ToString() { return Name; }
}

class B : A
{
    protected new string Name { get { return "B"; } }
}

class C : B
{
    public virtual new string ToString() { return Name; }
}

class D : C
{
    public override string ToString() { return Name; }
}

class E : B
{
    public override string ToString() { return Name; }
}
~~~



*On the ninth day of Christmas my true love gave to me...*

**Actually, that's all I can come up with for now. I'll come back and complete the list if I think of more.**
