L'objectif de ce projet est de montrer, par des simulations et des visualisations, comment la loi binomiale $B(n,p)$ peut être approximée par la loi de Poisson $\lambda = n\*p$ lorsque $n$ est grand et $p$ petit. Pour ce faire, on va s'appuyer sur les bases théoriques suivantes: 

$B(n,p)$
 Loi binomiale :
 
- Notation : \(X \sim \mathrm{Bin}(n,p)\)
- Espérance / variance : \(\mathbb{E}[X]=np\), \(\mathrm{Var}(X)=np(1-p)\)
- Fonction de masse (PMF) :
$$
\Pr(X=k)=\binom{n}{k}\, p^{k}\,(1-p)^{\,n-k}, \quad k=0,1,\dots,n.

$$
Loi de Poisson :

- Notation : \(Y \sim \mathrm{Pois}(\lambda)\)
- Espérance / variance : \(\mathbb{E}[Y]=\lambda\), \(\mathrm{Var}(Y)=\lambda\)
- Fonction de masse (PMF) :
$$
\Pr(Y=k)=\frac{\lambda^{k}\,e^{-\lambda}}{k!}, \quad k=0,1,2,\dots
$$
