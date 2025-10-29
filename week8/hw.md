# 1 
implicit score matching (ISM) loss:
```math
L_{ISM}(\theta) = \mathbb{E}_{x\sim p(x)}\left[\|S(x;\theta)\|^2 +2\nabla_x\cdot S(x;\theta)\right].
```
Expand the scalar and derivative terms
```math
(v^\top S(x;\theta))^2 = v^\top (S(x;\theta) S(x;\theta)^\top) v,
```
and
```math
v^\top \nabla_x (v^\top S(x;\theta))
= \sum_{i,j} v_i v_j \, \partial_{x_i} S_j(x;\theta).
```

Combine into a quadratic form
```math
(v^\top S)^2 + 2\,v^\top \nabla_x (v^\top S)
= v^\top \big( S S^\top + 2\,\nabla_x S \big) v,
```

Thus, the sliced score matching loss can be written as

```math
L_{\mathrm{SSM}} = \mathbb{E}_{x\sim p(x)} \, \mathbb{E}_{v\sim p(v)} 
\left[ (v^\top S(x;\theta))^{2} + 2\,v^\top \nabla_x (v^\top S(x;\theta)) \right].
```

# 2

stochastic differential equation (SDE) describes how a random process evolves over time, similar to an ordinary differential equation but with an added noise term.

```math
dx_t = f(x_t, t)\,dt + g(x_t, t)\,dW_t,
```
where  
\$g(x_t, t)\$: noise strength,  
\$W_t\$: Wiener process .


