---
layout: post
title: A simple way to add interleaving to your studies
---

The gist of interleaved practice is that you're better off by switching between topics during your study session than you would be if you were to study one thing, then move on to another.

That is, instead of studying with the following pattern:

1 1 1 1 1 2 2 2 2 2

You study with this one:

1 2 1 2 1 2 1 2 1 2 1 2

Or any sort of combination that makes you jump between topics while you're studying. I will one day write about what the theory and empirical data behind interleaved practice is, what I intend to do today is to share a simple way to implement interleaved practice in your studies.

Imagine you're studying for a test for one of your classes, and you have a list of exercises from several chapters you have to go through.[^a] If you're anything like me and my friends, you will probably do every exercise from the first chapter you have to study, then do the ones from the following chapter, *ad infinitum* until you have no more exercises left to do. That's not that bad a study strategy since most people would be content to just read the book, but it's not making use of the benefits of interleaved practice.

A simple way to introduce interleaved practice in your studies is to create a simple script that chooses one exercise from a list of exercises you have to do. Here is the one I did for my Intermediate Macroeconomics test[^b]:

``` python
from random import randint
exercises = [[1,2,3,4,5,6],[1,2,3,4,5,6,7,8,9,10,11,12,13,14],[1,2,3],[1,2,3,4,5,6],[1,2,3,4,5,6,7,8],[1,2,3,4]]

a = randint(0,len(exercises)-1)
b = randint(0,len(exercises[a])-1)

material = [ "folha de exercicios","exercicios exemplo escolha multipla","exercicios exemplo desenvolvimento","capitulo 11 do livro","capitulo 12 do livro","capitulo 14 do livro"]

print "Do the exercise number", exercises[a][b], "from ->", material[a]
```


The result ends up like this:

```
Do the exercise number 3 from -> capitulo 11 do livro
```

As you can see, it's not that hard a script to write, and it has the added benefit that you can't fool yourself into doing the wrong exercises.

You could modify this so that you would input how many exercises you want to solve during this study session and the script would tell you which ones to do in which order. Another useful modification would be to add another set of exercises from another class and interleaving between classes. If you don't want to repeat exercises you could also write a line to remove the exercise chosen from the list of exercises, but there's no real need to overengineer your script; if it chooses one you've already done you can just run the script again until it gives you one you haven't done. Or you can just do it again, who knows, maybe you'll discover you've forgotten something, or you'll notice a new nuance you hadn't noticed before.

Anyway, this script it's a simple way to of reaping the learning benefits of interleaved practice. It takes just a few minutes to write, which you can do when you're bored or procrastinating, so there's no excuse not to do it.


[^a]: I don't have to remind you that the best way to study is to do practice questions, do I?
[^b]: It works best when topics you're studying for that class are fairly independent of one another (or you've studied enough of every chapter so that you aren't doing exercises of things you've never heard about). 
