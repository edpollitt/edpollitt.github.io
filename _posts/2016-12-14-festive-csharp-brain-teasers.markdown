---
layout: post
title:  "Test"
date:   2016-12-14 08:12:45 +0100
categories: stuff test
---

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
