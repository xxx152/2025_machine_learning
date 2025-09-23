
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
then Taylor's expansion \$tanh(x)\$ at \$x=(p/2-i)\$ gives
```math
F_{p,h}(x) = \sum_{i=0}^{p}​ (−1)^{p−i}\left( \begin{array}{c} p \\ i \end{array} \right) \sum_{j=1}^{\infty}c_{j}((p/2-i)hx)^{j} 
```
for some \$c_j \in \mathbb{R} \$
```math
F_{p,h}(x) = \sum_{j=1}^{\infty}c_{j}(hx)^{j} \sum_{i=0}^{p}​ (−1)^{p−i}\left( \begin{array}{c} p \\ i \end{array} \right) ((p/2-i))^{j} 
```
By the finite difference identity, all terms with \$j < p\$ vanish.
Hence the first nonzero contribution is the $j=p$ term, which is proportional to \$x^p\$.
All higher-order terms (\$j > p\$) contribute to the approximation error, which can be controlled by choosing \$h\$ small enough.




