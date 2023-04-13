# Sandpiles
The sandpile model is an algorithm which was first made to be able to simulate the way pouring sand in one spot will cause it to collapse every now and then. However, it was not a good model as it did not resemble reality. The model did end up being an example of cellular automata and self-organised criticality. Scale invariance is when changing the parameters of a function from one parameter to another parameter it is directly proportional to results in the function remaining the same except for a multiplicative factor. Mathematically, this can be shown as $f(x) = C f(x')$ where x and x' are two different parameters that are related by $x = \lambda x'$. The family of functions which follows this scale invariance is given by $f(x) = A x^{\gamma}$ where A and $\gamma$ are constants. Given that $x = \lambda x'$, we have $f(x) = f(\lambda x')$. Also, we have $$f(\lambda x') = A (\lambda x')^{\gamma} = A {(\lambda)^{\gamma}} (x')^{\gamma} = {(\lambda)^{\gamma}} A (x')^{\gamma}$$  $$\therefore f(x) = {(\lambda)^{\gamma}} A (x')^{\gamma} = {(\lambda)^{\gamma}} f(x')$$ In the last formula we can clearly see that $C = {(\lambda)^{\gamma}}$. This makes it easy to transform the the distribution when changing the scale, for example, of length from mm to cm where $\lambda = 10$ or cm to mm where $lambda = frac{1}{10}$.   
