---
layout: post
title: A model of the Malthusian argument
category: Economics
tags: [Malthusian Dynamics, Economics]
---

Economists love mathematical models, and with good reason: it forces one to be consistent. 

Debates about the mathiness in economics are evergreen, and it is true that many times complex math is used in order to obfuscate, not to make things clearer, yet it does not follow that economists should ditch math and stick to playing with words. What a nightmare that would be.

Since we're interested in exploring Malthus famous argument, let's try and develop a simple model to help us think about what the argument says and what are its predictions. I will be following [this paper by Ashraf and Galor pretty closely](https://www.nber.org/papers/w17037), so don't feel guilty if you'd rather read a real academic paper than my attempt at grasping it. 

Anyway, here we go:

Let's say our economy produces a single homogeneous good using land and labor as inputs. Bread could be that good; our economy only produces bread. The land in which its wheat grows is fixed over time and exogeneous.[^a] On the other hand, labour supply is determined by the decisions made by the households in the preceding period regarding the number of their children.

**Production**

If the amount of bread our economy produces is determined by how much land and labor is employed in its production, how can we determine how much bread we make per those inputs? A classic production function in economics is called the Cobb-Douglas production function:

$$Y_t = (AX)^\alpha L_t^{1-\alpha} \qquad  0 < \alpha < 1$$

Where \\( X \\) is land, \\(L_t\\) is labor, and \\( A \\) is the technological level; \\( \alpha \\) is the output elasticity of land, which measures how much more bread you can make by adding one more unit of land.

This production function has some interesting characteristics that function well in the context of agriculture, namely that the output displays constant returns to scale, that is, an equal increase in *both* inputs used implies an equal increase in output.

$$ Y_t(2X, 2L) = (A2X)^\alpha (2L_t)^{1-\alpha} = 2 (AX)^\alpha L_t^{1-\alpha} = 2Y_t(X,L)$$

The other characteristic that makes the Cobb-Douglas production function useful is that you get diminishing returns to increasing a single input. If you have a piece of land and more and more workers start working on it, then the productivity of each additional worker diminishes because there's only so much work to do in that land. The same if you increase the land for the same number of workers to work on. This can be shown in the following way:

$$ \frac{\partial Y}{\partial X} = \alpha A^\alpha X^{\alpha -1} L_t^{1-\alpha} \rightarrow \frac{\partial^2 Y}{\partial X^2} < 0$$

$$ \frac{\partial Y}{\partial L_t} = (1-\alpha) (AX)^\alpha L_t^{-\alpha}  \rightarrow \frac{\partial^2 Y}{\partial L_t^2} < 0 $$

Usually, in the Cobb-Douglas function, the productivity factor, \\( A \\) isn't to the power of \\( \alpha \\), as in the Solow Model, but since the productivity here is inherently connected to the land being used, it doesn't make much sense to talk about the output elasticity of land while leaving its productivity constant since not all land is equal, and it is the case that the most productive land is the first being used. That's another reason why you get diminishing returns to increased land use. 

You can also get output per worker at time \\( t \\) by dividing \\( Y_t\\) by the number of workers, \\( L_t \\):


$$y_t = \frac{Y_t}{L_t} =\left (\frac{AX}{L_t}\right )^\alpha$$




[^a]:If you've not encountered the word exogeneous before, it means that it is determined externally from the model. In this case, the land available to grow wheat is determined by geological processes, and it's largely outside human influence.



