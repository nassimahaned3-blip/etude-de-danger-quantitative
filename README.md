# etude-de-danger-quantitative
EDDQ par Nassima Haned : Modélisation séquentielle d'Étude de Danger Quantitative. Combine écoulements compressibles critiques (V5), formulation en nombres entiers mixtes (PLNEM), optimisation Branch &amp; Bound d'efficacité maximale (sans coût) et audit économétrique final par régression Logit.
L'AMDEC est purgée de sa cotation qualitative habituelle (grille de criticité subjective $G \times F \times D$ notée de 1 à 10). Elle sert exclusivement de procédure de screening systématique pour produire trois inventaires bruts :
*   **La liste des scénarios d'accidents majeurs ($k = 1, \dots, n$)** : Échelonnée selon la taille géométrique des brèches (fuite mineure sur joint, rupture de piquage, rupture guillotine), recensant les modes de défaillance et causes physiques (matérielles, procédé, installation, externes).
*   **Le catalogue des moyens de sécurité candidats** : Organisé en postes de décision (Détection, Isolement, Déluge). Chaque poste propose plusieurs paliers techniques tranchables et indivisibles (ex. : redondance $1\text{oo}1$ / $1\text{oo}2$ / $2\text{oo}3$), incluant un palier ``Absent'' à coût nul.
*   **La cartographie de transversalité** : Détermine quelles barrières agissent sur quels scénarios, et par quel mécanisme physique (réduction de fréquence $P$ ou réduction de gravité $G$).
    

## X.3 Étape 2 — Le calcul physique et mathematique 
exact du risque $R_0 = P_0 \times G_0$

Une fois la structure fixée par l'AMDEC, chaque scénario $k$ reçoit ses valeurs numériques initiales $P_0(k)$ et $G_0(k)$, obtenues par des lois physiques et fiabilistes dédiées :
*   **$P_0(k)$** : Combinaison des causes par le théorème d'inclusion-exclusion de Poincaré, chaque cause étant calculée à partir d'une loi adaptée (Weibull pour la corrosion, Gumbel pour les pics de surpression, Poisson pour les agressions externes), corrigée en température par l'équation cinétique d'**Arrhenius**.
*   **$G_0(k)$** : Calcul géométrique de la zone d'impact à partir de la masse de produit libérée. En régime **critique étranglé (\textit{choked flow})**, le relâchement massique est bridé de manière déterministe par la variable de plafond physique propre à chaque type d'activité et masse d'inventaire initiale ($M_{\text{plafond}}$).

Le risque initial du scénario est alors $R_0(k) = P_0(k) \times \big[ G_0(k) \big]$. Cette étape caractérise le danger nu de l'installation, avant toute mesure de protection.


## X.4 Étape 3 — Le Branch & Bound comme sélecteur d'efficacité maximale pure

Le Branch & Bound reçoit en entrée le triplet issu des phases précédentes (scénarios avec risques nus, paliers discrets, facteurs d'atténuation) et résout le problème de couverture par programmation linéaire en nombres entiers mixtes (PLNEM) :
*   Il explore l'arbre des combinaisons de paliers et **tranche de manière absolue (sans intervalle flou)** : il sélectionne le vecteur de décision binaire $Z^*$ ($0$ ou $1$).
*   Pour chaque feuille de l'arbre, il recalcule le risque résiduel exact via un produit géométrique d'atténuation linéarisé par un passage au logarithme népérien ($\ln$), éliminant le biais de bilinéarité.
*   **Principe de précaution absolue** : L'algorithme exclut totalement le budget ou le coût financier. Il sélectionne la configuration matérielle offrant l'atténuation maximale du risque physiquement disponible, sous la contrainte non compensatoire qu'un scénario sur-protégé ne peut jamais masquer la vulnérabilité d'une brèche majeure.

---

## X.5 Étape 4 — La modélisation économétrique comme moteur de validation *a posteriori*

L'introduction de la phase économétrique en terminus du flux méthodologique assure le verrouillage de la rigueur scientifique. Elle n'intervient pas pour orienter le choix opérationnel, mais pour auditer et valider statistiquement la robustesse de la décision binaire $Z^*$.

Le modèle déploie une **régression logistique binaire (Modèle Logit)** estimant la probabilité d'homologation d'un établissement ($Y \in \{0, 1\}$) face à l'historique des données du tissu industriel global :

$$\ln\left( \frac{P(Y = 1)}{1 - P(Y = 1)} \right) = \beta_0 + \beta_1 \cdot \max(\mathbf{R}_{\text{Systémique}}) + \beta_2 \cdot \tilde{\Omega}_{\text{V5}} + \beta_3 \cdot \text{Effort}_{\text{BTS}} + \varepsilon$$

L'analyse des coefficients $\beta$ par le test du Maximum de Vraisemblance et le calcul du pseudo-$R^2$ de McFadden permettent d'apporter la preuve mathématique que la décision de l'Étape 3 est exempte de biais de spécification ou de dérives paramétriques.

---

## X.6 Propriété clé de l'architecture : irréversibilité et traçabilité

Cette séquence est à sens unique : l'AMDEC ne dépend pas des calculs physiques, le calcul physique ignore les barrières, le Branch & Bound ignore le coût financier, et l'économétrie audite le résultat final. Chaque exigence matérielle imposée au guichet unique est ainsi mathématiquement corrélée à une chaîne causale pure, garantissant une intégrité technique totale devant un jury d'examen ou une autorité de régulation internationale.
