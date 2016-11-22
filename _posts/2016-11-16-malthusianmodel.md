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

**Preferences and Budget Constraints** 

We're going to make a number of simplifying assumptions about demographics here that shouldn't impact the implications of our model. In each period \\(t\\), \\(L_t\\) identical individuals joins the workforce; a new generation of workers. Each individual has a single parent and live for two periods. In their first period, \\(t-1\\), they are supported by their parent, that is, they're a child. In their second period, \\(t\\), they enter adulthood as such will supply their labor, generating an income equal to the output per worker we saw earlier, \\(y_t\\). That income will be then allocated between their own consumption and that of their children. Choices about allocation of limited resources necessitate some way of conceptualizing the benefits arising from each choice, which in Economics is *utility*.

Individuals generate utility from consumption and the number of their children:

$$u^t = (c_t)^{1-\gamma}(n_t)^\gamma; \qquad \gamma \in (0,1)$$

Where \\(c_t\\) is own consumption and \\(n_t\\) is the number of children of the individual. Because resources are limited, there are constraints in how much we can consume AND how much our children can consume. If \\( \rho \\) is the cost of raising a child:

$$\rho n_t + c_t \leq y_t$$

is our budget constraint.

Now that we have our utility function along with our budget constraint, we will need to maximize the first taking into account the second in order to get each household's optimal allocation. However, since we're using a Cobb-Douglas function, we know straight away[^b]that the each household will devote a fraction \\(1-\gamma \\) of their income to consumption and \\( \gamma \\) to child reading:

$$ c_t = (1 - \gamma )y_t$$ 

$$ n_t = \gamma \frac{y_t}{\rho}$$

Finito, we now have a model for the Malthusian model to work with. The next post in this series will deal with the dynamics of our model, namely, how income and population are interrelated. We have already seen that they must indeed be interrelated since as income rises, the number of surviving children must rise as well.

[^a]:If you've not encountered the word exogeneous before, it means that it is determined externally from the model. In this case, the land available to grow wheat is determined by geological processes, and it's largely outside human influence.

[^b]:I'll have a post soon how this can be shown mathematically because it isn't that obvious if you haven't used a Cobb-Douglas function before.


