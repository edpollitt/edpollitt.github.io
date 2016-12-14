---
layout: post
title:   Festive Brainteasers
tags: [C#] [Brainteasers]
---

*On the first day of Christmas my true love gave to me...*
A festive message. What’s the output?

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
