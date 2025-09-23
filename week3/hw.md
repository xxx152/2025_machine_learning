
## Lemma 3.1
Let \$k \in \mathbb{N}_0\$ and \$s \in 2\mathbb{N}-1\$. Then, for every \$\varepsilon > 0\$, there exists a shallow tanh neural network
```math
\Psi_{s,\varepsilon} : [-M, M] \to \mathbb{R}^{\tfrac{s+1}{2}}
```
of width $\tfrac{s+1}{2}$ such that, for all odd integers \$p \leq s$,
```math
y^p \cong \Psi_{s,\varepsilon}
```
with approximation error at most $\varepsilon\$ .


## Idea of proof
First, recall the finite difference operator
```math
\triangle f(x)= f(x+1)-f(x) 
```
and its \$p\$-th iteration
```math
\triangle^{p}f(0)=\sum_{i=0}^{p}​ (−1)^{p−i}\left( \begin{array}{c} p \\ i \end{array} \right) f(i).
```
This identity can be proved by induction.  
Now, for monomials $f(x)=x^k$, with \$k\in\mathbb{N}\$, one obtains
```math
\triangle^{p}f(0)=\left\{ \begin{array}{rcl}
0 & \mbox{for}
& k < p \\ p! & \mbox{for} & p = k 
\end{array}\right.
```
Second, define
```math
F_{p,h}(x) = \sum_{i=0}^{p}​ (−1)^{p−i}\left( \begin{array}{c} p \\ i \end{array} \right) tanh((p/2-i)hx) 
```
then Taylor's expansion \$tanh(u)\$ at \$u=(p/2-i)hx\$ gives
```math
F_{p,h}(x) = \sum_{i=0}^{p}​ (−1)^{p−i}\left( \begin{array}{c} p \\ i \end{array} \right) \sum_{j=1}^{\infty}c_{j}[(p/2-i)hx]^{j} 
```
for some \$c_j \in \mathbb{R} \$
```math
F_{p,h}(x) = \sum_{j=1}^{\infty}c_{j}(hx)^{j} \sum_{i=0}^{p}​ (−1)^{p−i}\left( \begin{array}{c} p \\ i \end{array} \right) (p/2-i)^{j} 
```
By the finite difference identity, all terms with \$j < p\$ vanish.  
Hence the first nonzero contribution is the $j=p$ term, which is proportional to \$x^p\$.  
```math
F_{p,h}(x) = C_{p}​(hx)^{p}+(higher-order-terms)
```
where \$C_p \neq 0\$ is a constant depending only on \$p\$ and the Taylor coefficient \$c_p\$.  
Dividing both sides by \$C_p h^p\$ yields
```math
x^p \cong F_{p,h}(x)/C_p h^p
```
All higher-order terms (\$j > p\$) contribute to the approximation error, which can be controlled by choosing \$h\$ small enough.
Since these terms are multiplied by higher powers of $h$, the error can be made arbitrarily small by choosing $h$ sufficiently small.


## lemma 3.2
Let \$k \in \mathbb{N}_0\$ and \$s \in 2\mathbb{N}-1\$. Then, for every \$\varepsilon > 0\$, 
there exists a shallow \$\tanh\$ neural network
```math
\Psi_{s,\varepsilon} : [-M, M] \to \mathbb{R}^{s}
```
of width \$\tfrac{3(s+1)}{2}\$ such that, for all odd integers \$p \leq s\$,
```math
y^p \;\cong\; \Psi_{s,\varepsilon}(y),
```
with approximation error bounded by $\varepsilon\$.

## Idea of Proof (Lemma 3.2)

The goal is to show that **both odd and even powers of $y$** can be well-approximated by the network \$\Psi_{s,\varepsilon}\$.  
**1. Odd powers**  
From Lemma 3.1, we know that for all odd integers \$p \leq s\$,
```math
y^p \cong \Psi_{s,\varepsilon}(y)
```
with approximation error at most $\varepsilon$.  
**2. Expressing even powers**  
To approximate even monomials $y^{2n}$, we use the identity
```math
   \frac{1}{y^{2n}} \;=\; 
   \frac{1}{2\alpha(2n+1)} \Big[ (y+\alpha)^{2n+1} - (y-\alpha)^{2n+1} 
   - \sum_{k=0}^{n-1} \binom{2n+1}{2k} \alpha^{2(n-k)+1} y^{2k} \Big],
```
   valid for $\alpha > 0$.  
   This expresses $y^{2n}$ in terms of odd powers $(y\pm \alpha)^{2n+1}$ and lower even powers $y^{2k}$.


This gives a recursive way to build \$y^{2n}\$ step by step from odd powers and smaller even powers.  
**3. Induction step**  
   - Base case: Using the recursion with $n=1$, \$y^2\$ can be expressed directly from odd powers (which are approximated via Lemma 3.1).  
   Hence \$y^2\$ can be approximated to within error $O(\varepsilon)$.  
   - Inductive step: Assume we already have approximations for all even powers up to \$y^{2(n-1)}\$.  
The recursion formula expresses $y^{2n}$ using odd powers (approximated via Lemma 3.1) and these lower even powers (available by induction).  
Substituting the approximations, we obtain an approximation for \$y^{2n}\$ with error still bounded by \$O(\varepsilon)\$.
   as stated in Lemma 3.2.
```math
y^p \;\cong\; \Psi_{s,\varepsilon}(y), \quad \forall p \leq s
```



