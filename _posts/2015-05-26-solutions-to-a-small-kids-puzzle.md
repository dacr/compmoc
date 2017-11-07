---
layout: post
title: Solutions to a small kids puzzle
---

How to solve the following [kid puzzle](http://www.theguardian.com/science/alexs-adventures-in-numberland/2015/may/20/can-you-do-the-maths-puzzle-for-vietnamese-eight-year-olds-that-has-stumped-parents-and-teachers)
by using only digits from 1 to 9 exactly one time : 

![puzzle]({{ site.baseurl }}/images/2015-05-26-kids-puzzle.png)

With the following code, I found 20 solutions if we take into account operators priority, 119 without.

```scala
  type NUM = BigDecimal
  val NUM = BigDecimal                            //> NUM  : math.BigDecimal.type = scala.math.BigDecimal$@52ed6f9

  def fctA(ds: List[NUM]) = {
    val List(a, b, c, d, e, f, g, h, i) = ds
    a + NUM(13) * b / c + d + NUM(12) * e - f - NUM(11) + g * h / i - NUM(10)
  }                                               //> fctA: (ds: List[Vietation.NUM])scala.math.BigDecimal

  def fctB(ds: List[NUM]) = {
    val List(a, b, c, d, e, f, g, h, i) = ds
    (((((((((((a + NUM(13)) * b) / c) + d) + NUM(12)) * e) - f) - NUM(11)) + g) * h) / i) - NUM(10)
  }                                               //> fctB: (ds: List[Vietation.NUM])scala.math.BigDecimal

  val digits = List(1, 2, 3, 4, 5, 6, 7, 8, 9).map(x => NUM(x))
                                                  //> digits  : List[scala.math.BigDecimal] = List(1, 2, 3, 4, 5, 6, 7, 8, 9)

  def isSolution(fct:List[NUM]=>NUM)(candidate:List[NUM]):Boolean = {
    val r = fct(candidate)
    r == 66 && r.scale == 0
  }                                               //> isSolution: (fct: List[Vietation.NUM] => Vietation.NUM)(candidate: List[Viet
                                                  //| ation.NUM])Boolean
  
  digits
    .permutations
    .filter(isSolution(fctA))
    .size                                         //> res0: Int = 20

  digits
    .permutations
    .filter(isSolution(fctB))
    .size                                         //> res1: Int = 119
```

The solutions are :

```
List(3, 2, 1, 5, 4, 7, 8, 9, 6)
List(3, 2, 1, 5, 4, 7, 9, 8, 6)
List(5, 2, 1, 3, 4, 7, 8, 9, 6)
List(5, 2, 1, 3, 4, 7, 9, 8, 6)
List(5, 3, 1, 7, 2, 6, 8, 9, 4)
List(5, 3, 1, 7, 2, 6, 9, 8, 4)
List(5, 4, 1, 9, 2, 7, 3, 8, 6)
List(5, 4, 1, 9, 2, 7, 8, 3, 6)
List(5, 9, 3, 6, 2, 1, 7, 8, 4)
List(5, 9, 3, 6, 2, 1, 8, 7, 4)
List(6, 3, 1, 9, 2, 5, 7, 8, 4)
List(6, 3, 1, 9, 2, 5, 8, 7, 4)
List(6, 9, 3, 5, 2, 1, 7, 8, 4)
List(6, 9, 3, 5, 2, 1, 8, 7, 4)
List(7, 3, 1, 5, 2, 6, 8, 9, 4)
List(7, 3, 1, 5, 2, 6, 9, 8, 4)
List(9, 3, 1, 6, 2, 5, 7, 8, 4)
List(9, 3, 1, 6, 2, 5, 8, 7, 4)
List(9, 4, 1, 5, 2, 7, 3, 8, 6)
List(9, 4, 1, 5, 2, 7, 8, 3, 6)
```

