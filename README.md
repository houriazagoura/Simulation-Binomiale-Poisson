### I- Cadre théorique : 

L'**objectif** de ce projet est de montrer, par des simulations et des visualisations, comment la loi binomiale $B(n,p)$ peut être approximée par la loi de Poisson $\lambda = n\*p$ lorsque $n$ est grand et $p$ petit. Pour ce faire, on va s'appuyer sur des bases théoriques à savoir: 

La **loi binomiale** ($$X \sim \text{Bin}(n,p)$$) modélise (à travers $X$) le nombre de succès dans une série de `n` expériences de Bernoulli indépendantes, chacune ayant une probabilité `p` de succès.  

Simuler une loi binomiale revient à tirer `n` fois une variable de Bernoulli(p) et compter le nombre de succès obtenus.  

- Espérance : $$\mathbb{E}[X] = n \cdot p$$  
- Variance : $$\mathrm{Var}(X) = n \cdot p \cdot (1-p)$$  

La fonction de masse (PMF) est donnée par :  

$$
\Pr(X=k) = \binom{n}{k} \, p^k \, (1-p)^{n-k}, \quad k = 0,1,\dots,n
$$


La **loi de Poisson** ($$Y \sim \text{Pois}(\lambda)$$) modélise (à travers $Y$) le nombre d’occurrences d’un événement rare pendant un intervalle de temps ou d’espace donné, lorsque ces événements se produisent indépendamment les uns des autres avec une fréquence moyenne $\lambda$.  

Simuler une loi de Poisson revient à générer directement un nombre d’occurrences à partir du paramètre $\lambda$, qui représente à la fois **l’espérance** et la **variance** de la distribution.  

- Espérance : $$\mathbb{E}[Y] = \lambda$$  
- Variance : $$\mathrm{Var}(Y) = \lambda$$  

La fonction de masse (PMF) est donnée par :  

$$
\Pr(Y=k) = \frac{\lambda^k e^{-\lambda}}{k!}, \quad k = 0,1,2,\dots
$$

Lorsque $n \to \infty$ et $p \to 0$ de telle sorte que $n \cdot p = \lambda$ reste constant, alors :  
$$\text{Bin}(n,p)\longrightarrow\text{Pois}(\lambda)$$

### II- Cas pratique et interprétation des résultats : 

Après avoir présenté les bases théoriques (loi binomiale, loi de Poisson, loi des grands nombres, TCL), nous passons maintenant à la pratique :  
- simuler des tirages aléatoires avec NumPy,  
- comparer les distributions obtenues aux lois théoriques correspondantes,  
- visualiser les résultats par des graphiques,  
- et mesurer quantitativement la qualité des approximations.  
L’objectif est de montrer, par des expériences numériques simples, comment la théorie se vérifie dans des cas concrets de modélisation du risque de crédit.

On commence par simuler la loi binomiale. Et les résultats se présentent comme suit :


Nous simulons `n = 1000` prêts, chacun ayant une probabilité de défaut `p = 2%`.  
L’expérience est répétée `n_sim = 10 000` fois pour estimer la distribution du nombre de défauts.  

- Espérance théorique : **20.0** défauts  
- Moyenne observée : **20.1** défauts  
- Variance théorique : **19.6**  
- Variance observée : **20.0** (écart-type ≈ 4.5)  

Interprétation : en moyenne, environ 20 prêts font défaut, avec une dispersion de ±4 à 5 prêts.  
La simulation correspond très bien aux valeurs théoriques prévues par la loi binomiale.

<img width="576" height="456" alt="image" src="https://github.com/user-attachments/assets/6df14a55-6f3b-45bc-8c1f-7eb013eb30f0" />

L’histogramme (intitulé nombre de défaut sur n prêts) montre la distribution empirique du nombre de défauts simulés. La ligne verticale pointillée correspond à l’espérance théorique (20).  
On observe que les résultats sont bien centrés autour de cette valeur, avec une dispersion cohérente avec la variance attendue (~20).Cela confirme que la simulation respecte bien les propriétés de la loi binomiale.

Après, nous comparons une loi binomiale $B(n=10000, p=0.002)$ avec la loi de Poisson correspondante de paramètre $\lambda = n \cdot p = 20$. 
<img width="576" height="455" alt="image" src="https://github.com/user-attachments/assets/c9b6a573-7e30-4cbf-b2d9-be774dbe8938" />

`Distance chi-deux (plus petit = mieux): 0.001491`

L’histogramme bleu représente la distribution simulée de la loi binomiale, tandis que la courbe bleue correspond à la loi de Poisson théorique.  

On observe une superposition quasi parfaite des deux distributions. La faible valeur de la distance chi-deux (≈ 0.0015) confirme quantitativement que l’approximation de la binomiale par la Poisson est excellente lorsque `n` est grand et `p` est petit.

Maintenant, on simule la perte moyenne par prêt dans un portefeuille de taille croissante, 
pour différentes probabilités de défaut `p`.

<img width="584" height="456" alt="image" src="https://github.com/user-attachments/assets/2c225ee4-7308-44fd-a709-b6d8ef9cd23c" />

Chaque courbe représente l’évolution de la perte moyenne empirique par prêt, au fur et à mesure que le nombre de prêts augmente.  Les lignes pointillées indiquent les valeurs théoriques attendues ($p \cdot EAD \cdot LGD$). On observe que plus le nombre de prêts croît, plus la perte moyenne converge vers sa valeur théorique, confirmant la loi des grands nombres.

On simule les pertes totales pour un portefeuille de `n` prêts, puis on les **normalise** :  
$$ Z = \frac{L - \mu}{\sigma} $$  
où $L$ est la perte totale, $\mu$ la moyenne empirique et $\sigma$ l’écart-type empirique.  
<img width="567" height="455" alt="image" src="https://github.com/user-attachments/assets/95ceceb0-d150-4789-abf9-b9a25ef49e22" />

L’histogramme bleu représente les Z-scores obtenus à partir des pertes simulées, et la courbe orange est la densité de la loi normale standard $N(0,1)$.  
On constate déjà une tendance : même avec `n = 100`, la forme de la distribution normalisée s’approche d’une courbe en cloche. Quand `n` augmente, la convergence vers $N(0,1)$ devient encore plus nette, confirmant le TCL.

On augmente maintenant la taille du portefeuille à `n = 1000`.  

<img width="576" height="455" alt="image" src="https://github.com/user-attachments/assets/401769f3-691b-4a1b-8005-401b18e8f940" />

Cette fois, la distribution des Z-scores (histogramme bleu) se superpose presque parfaitement à la densité de la loi normale standard $N(0,1)$ (courbe orange).  

On augmente encore la taille du portefeuille à `n = 10000`.  
<img width="567" height="455" alt="image" src="https://github.com/user-attachments/assets/dce8bf2e-1a8b-4772-af97-13b7454b67fa" />
Avec `n = 10000`, l’alignement entre l’histogramme des pertes normalisées et la courbe de densité normale standard est quasi parfait. Cette expérience confirme le Théorème Central Limite : lorsque la taille du portefeuille augmente, la loi des pertes normalisées converge vers $N(0,1)$.

### III- Conclusion 

Ce projet met en évidence une idée simple mais puissante : derrière des formules abstraites comme la loi binomiale, la loi de Poisson, la loi des grands nombres ou le TCL, il y a une réalité concrète et intuitive.  
En simulant, on voit que la théorie n’est pas un cadre lointain réservé aux mathématiciens : elle décrit avec précision des phénomènes aléatoires du quotidien de la finance et du risque de crédit.  
En d’autres termes, la simulation n’a pas servi ici à “illustrer” la théorie, mais à la rendre tangible et vivante, à montrer comment un concept probabiliste devient un outil opérationnel de compréhension et de décision.





