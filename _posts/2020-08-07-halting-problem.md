---
toc: false
layout: post
description: 
categories: [computer-science]
title: Halting problem
---

Halting problem is introduced by Alan Turing in his [seminal paper](https://academic.oup.com/plms/article-abstract/s2-42/1/230/1491926?redirectedFrom=fulltext), 1936. It states that there cannot be a general algorithm to decide whether an arbitrary pair of computer program and input halts (finishes execution) or not.

Surprisingly, the proof of such a bold statement is ingeniously simple.

Proof by contradiction. 

Suppose that there exists a computer program H that solves halting problem. For a pair of computer program P and input I, H outputs true if P finished with I. Otherwise, it outputs false. How H can do this is not important for the sake of proof. In Python, H would be roughly such:

```python
def H(program, inpt):
    # with some black magic
    if program_halts_on_inpt:
        return True
    else:
        return False
```

Now, having H, let's define another computer program G, which receives a computer program P. G copies P and asks H whether P halts on P. If H decides that P halts on P, G diabolically loops forever. If H decides otherwise, G halts. 

```python
def G(program):
    if H(program, program):
        while True:
            pass
    else:
        return
```

Now, the interesting part. Let's run G with G as input, i.e. call G(G). It calls H(G, G) and there are two possible outcomes.
1. H decides that program G <u>*halts*</u> on input G and returns true. Then, inside G, first brach of `if` becomes active and G loops forever, i.e. does <u>*not halt*</u>.
1. H decides that program G does <u>*not halt*</u> on input G and returns false. Then, inside G, `else` branch becomes active and G <u>*halts*</u>.

This is a contradiction. Hence, H cannot exist. 
