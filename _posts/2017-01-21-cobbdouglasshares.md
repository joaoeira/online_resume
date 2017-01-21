---
layout: post
title: "How to Derive Labor and Capital Share From the Cobb-Douglas Production Function"
category: Thoughts
tags: [Sentences to ponder]
--- 

In the [previous post](http://lettucebecereal.com/economics/2016/11/16/malthusianmodel/) on the Malthusian model series I promised I would write a short note on how to derive the constant shares for both labor and capital from the Cobb-Douglas production function, so here it is:

We start with the usual Cobb-Douglas production function

$$Y=AK^\alpha L^{1-\alpha}$$

We know from our microeconomics that a profit maximizing firm will choose to employ labor so that its marginal product equals real wages, and will hire capital so that its marginal product equals its real rent, i.e:

$$\left\{\begin{matrix}MP_L = \frac{W}{P}\\MP_K = \frac{R}{P}\end{matrix}\right.$$

where \\(W\\) is the nominal wage, \\(R\\) is the nominal rent, and \\(P\\) the price level. 

Furthermore, we can get \\(MP_L\\) and \\(MP_K\\) from Cobb-Douglas through simple derivation:

$$\left\{\begin{matrix}MP_L =  A(1-\alpha)\left ( \frac{K}{L} \right )^\alpha\\ MP_K =   \alpha A\left ( \frac{L}{K} \right )^{1-\alpha}\end{matrix}\right.$$

Equating both we get:

$$\left\{\begin{matrix}\frac{W}{P} =  A(1-\alpha)\left ( \frac{K}{L} \right )^\alpha\\ \frac{R}{P} =   \alpha A \left ( \frac{L}{K} \right )^{1-\alpha}\end{matrix}\right.$$

So if firms hire \\(L\\) workers for \\(\frac{W}{P}\\), and hire capital \\(K\\) for \\(\frac{R}{P}\\), you have that the labor share is just the number of workers times their real wage divided by total income:

$$\text{Labor's share} = \frac{\left ( \frac{W}{P} \right ) × L}{Y}$$

the same logic for capital

$$\text{Capital's share} = \frac{\left( \frac{R}{P}\right ) \times K}{Y}$$

Now all that's left is substituting the previous equations, as well as the Cobb-Douglass function, and by simple algebra we get:

$$\text{Labor's share} = \alpha$$

$$\text{Capital's share}=1-\alpha$$
