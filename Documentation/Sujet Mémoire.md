* a passer dans gdoc
## TF-IDF

TF-IDF (Term Frequency - Inverse Document Frequency) est un algorithme de traitement 
du texte appartenant à la famille des modèles "Bag of Words". Il permet de mesurer 
l'importance d'un terme dans un document par rapport à un corpus.

### Term Frequency 
La partie TF mesure la fréquence d'apparition d'un terme dans un document donné.
Plus un mot apparaît souvent dans un document, plus son score TF est élevé.
Elle se calcule de la manière suivante :

$$TF(t, d) = \frac{\text{nombre d'occurrences de } t \text{ dans } d}{\text{nombre total de termes dans } d}$$

exemple pour les documents suivants :

1 : Le chat mange du poisson
2 : Le chien creuse dans le jardin
3 : Le chat et le chien mangent leurs croquettes

| Terme      | TF doc 1 | TF doc 2 | TF doc 3 |
|------------|----------|----------|----------|
| Le         | 0,2      | 0,333    | 0,25     |
| chat       | 0,2      | 0        | 0,125    |
| chien      | 0        | 0,166    | 0,125    |
| mange      | 0,2      | 0        | 0        |
| mangent    | 0        | 0        | 0,125    |
| creuse     | 0        | 0,166    | 0        |
| et         | 0        | 0        | 0,125    |
| dans       | 0        | 0,166    | 0        |
| leurs      | 0        | 0        | 0,125    |
| du         | 0,2      | 0        | 0        |
| croquettes | 0        | 0        | 0,125    |
| poisson    | 0,2      | 0        | 0        |
| jardin     | 0        | 0,166    | 0        |

### Inverse Document Frequency

La partie IDF mesure l'importance d'un terme à travers l'ensemble du corpus.
Un terme présent dans tous les documents est peu informatif (ex: "le"), 
tandis qu'un terme rare est plus discriminant. Elle fonctionne de cette manière :

$$IDF(t) = \log\left(\frac{\text{nombre total de documents}}{\text{nombre de documents contenant } t}\right)$$

exemple pour les documents suivants :

1 : Le chat mange du poisson
2 : Le chien creuse dans le jardin
3 : Le chat et le chien mangent leurs croquettes

| Terme      | Docs contenant t | IDF                        |
|------------|------------------|----------------------------|
| le         | 3                | log(3/3) = **0**           |
| chat       | 2                | log(3/2) ≈ **0,176**       |
| chien      | 2                | log(3/2) ≈ **0,176**       |
| mange      | 1                | log(3/1) ≈ **0,477**       |
| mangent    | 1                | log(3/1) ≈ **0,477**       |
| creuse     | 1                | log(3/1) ≈ **0,477**       |
| et         | 1                | log(3/1) ≈ **0,477**       |
| dans       | 1                | log(3/1) ≈ **0,477**       |
| leurs      | 1                | log(3/1) ≈ **0,477**       |
| du         | 1                | log(3/1) ≈ **0,477**       |
| croquettes | 1                | log(3/1) ≈ **0,477**       |
| poisson    | 1                | log(3/1) ≈ **0,477**       |
| jardin     | 1                | log(3/1) ≈ **0,477**       |

### Application de TF-IDF

on applique TF-IDF de la manière suivante :

$$TF\text{-}IDF(t, d) = TF(t, d) \times IDF(t)$$

Plus le score est élevé, plus le terme est caractéristique du document dans le corpus.

| Terme      | TF-IDF doc 1 | TF-IDF doc 2 | TF-IDF doc 3 |
|------------|--------------|--------------|--------------|
| le         | **0**        | **0**        | **0**        |
| chat       | **0,035**    | **0**        | **0,022**    |
| chien      | **0**        | **0,029**    | **0,022**    |
| mange      | **0,095**    | **0**        | **0**        |
| mangent    | **0**        | **0**        | **0,060**    |
| creuse     | **0**        | **0,079**    | **0**        |
| et         | **0**        | **0**        | **0,060**    |
| dans       | **0**        | **0,079**    | **0**        |
| leurs      | **0**        | **0**        | **0,060**    |
| du         | **0,095**    | **0**        | **0**        |
| croquettes | **0**        | **0**        | **0,060**    |
| poisson    | **0,095**    | **0**        | **0**        |
| jardin     | **0**        | **0,079**    | **0**        |

## BERT

BERT (Bidirectional Encoder Representations from Transformers) est un modèle de 
traitement du texte basé sur l'architecture Transformer. Contrairement aux modèles 
"Bag of Words" comme TF-IDF, BERT prend en compte le contexte et l'ordre des mots 
pour produire des représentations vectorielles riches et contextualisées.

### Tokenisation

Avant tout traitement, BERT découpe le texte en tokens via un algorithme WordPiece.
Des tokens spéciaux sont ajoutés automatiquement :

- `[CLS]` : placé en début de séquence, son vecteur final représente la phrase entière
- `[SEP]` : placé en fin de séquence (ou entre deux phrases)

Par exemple, pour les documents suivants :

1 : Le chat mange du poisson
2 : Le chien creuse dans le jardin
3 : Le chat et le chien mangent leurs croquettes

| Document | Tokens                                                        |
|----------|---------------------------------------------------------------|
| doc 1    | [CLS] le chat mange du poisson [SEP]                         |
| doc 2    | [CLS] le chien creuse dans le jardin [SEP]                   |
| doc 3    | [CLS] le chat et le chien mangent leurs croquettes [SEP]     |

### Embeddings contextuels

BERT produit pour chaque token un vecteur de dimension 768 (BERT-base) qui dépend 
du contexte entier de la phrase. Ainsi, un même mot peut avoir des représentations 
différentes selon son usage.

$$E(t, d) = \text{Transformer}(t \mid \text{contexte de } d)$$

Par exemple, le mot "chat" n'aura pas le même vecteur dans le doc 1 et le doc 3, 
car son contexte est différent — contrairement à TF-IDF qui lui attribuerait 
le même score.

| Terme | TF-IDF (contexte ignoré) | BERT (contexte pris en compte) |
|-------|--------------------------|-------------------------------|
| chat  | score unique : 0,035     | vecteur propre à chaque doc   |
| mange | score unique : 0,095     | vecteur propre à chaque doc   |

### Attention bidirectionnelle

Le mécanisme clé de BERT est l'**attention bidirectionnelle** : pour encoder un token,
BERT regarde simultanément les mots à gauche ET à droite. Cela lui permet de 
capturer des dépendances longue distance dans la phrase.

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V$$

Avec :
- $Q$ (Query) : le token courant
- $K$ (Key) et $V$ (Value) : tous les autres tokens de la séquence
- $d_k$ : dimension des vecteurs clés (facteur de normalisation)

### Les dimensions de BERT

BERT existe en plusieurs configurations selon le compromis souhaité entre 
performance et coût de calcul. Chaque configuration est définie par 
trois paramètres clés :

- **L** : nombre de couches Transformer (profondeur du modèle)
- **H** : taille des vecteurs d'embeddings (dimension cachée)
- **A** : nombre de têtes d'attention

$$\text{Paramètres totaux} \approx 12 \times L \times H^2$$

| Modèle          | Couches (L) | Dimension (H) | Têtes d'attention (A) | Paramètres |
|-----------------|-------------|---------------|-----------------------|------------|
| BERT-Tiny       | 2           | 128           | 2                     | ~4M        |
| BERT-Mini       | 4           | 256           | 4                     | ~11M       |
| BERT-Small      | 4           | 512           | 8                     | ~29M       |
| BERT-Medium     | 8           | 512           | 8                     | ~41M       |
| BERT-Base       | 12          | 768           | 12                    | ~110M      |
| BERT-Large      | 24          | 1024          | 16                    | ~340M      |

#### Couches Transformer (L)

Chaque couche affine progressivement la représentation des tokens en 
intégrant davantage de contexte. Les premières couches capturent la 
syntaxe (nature des mots), les couches profondes capturent la sémantique 
(sens des phrases).

| Couches | Ce que BERT capture |
|---------|---------------------|
| 1 - 4   | Morphologie, syntaxe de base |
| 5 - 8   | Relations grammaticales, dépendances |
| 9 - 12  | Sémantique, sens contextuel |

#### Dimension cachée (H)

La dimension H correspond à la taille du vecteur qui représente chaque token 
à la sortie de chaque couche. Plus H est grand, plus la représentation est 
riche, mais plus le modèle est coûteux.

$$E(t) \in \mathbb{R}^H$$

Par exemple pour "chat" dans le doc 1 avec BERT-Base :

$$E(\text{chat}) = [0.23, -0.81, 0.14, \ \dots \ , 0.67] \in \mathbb{R}^{768}$$

#### Têtes d'attention (A)

Chaque tête d'attention apprend à se concentrer sur un type de relation 
différent entre les tokens. Elles opèrent en parallèle sur des sous-espaces 
de dimension $H/A$.

$$d_k = H / A$$

| Modèle    | H    | A  | Dimension par tête ($d_k$) |
|-----------|------|----|---------------------------|
| BERT-Base | 768  | 12 | 64                        |
| BERT-Large| 1024 | 16 | 64                        |

> La dimension par tête reste constante à **64** entre BERT-Base et BERT-Large : 
> c'est le nombre de têtes qui augmente, permettant de capturer plus de types 
> de relations simultanément.

### La malédiction de la dimensionnalité

La malédiction de la dimensionnalité désigne l'ensemble des problèmes qui 
apparaissent lorsque l'on travaille avec des données dans des espaces vectoriels 
de très haute dimension, comme les embeddings produits par BERT.

#### Le problème de la distance

Dans un espace de faible dimension, la distance euclidienne entre deux points 
est intuitive et discriminante. Mais à mesure que la dimension augmente, 
un phénomène contre-intuitif se produit : **toutes les distances tendent 
à se rapprocher**.

$$\lim_{H \to \infty} \frac{d_{max} - d_{min}}{d_{min}} \to 0$$

Concrètement, dans un espace à 768 dimensions (BERT-Base), la différence 
de distance entre le voisin le plus proche et le voisin le plus éloigné 
devient si faible que la notion de "proximité" perd de son sens.

| Dimension | Distance min | Distance max | Écart relatif |
|-----------|-------------|-------------|---------------|
| 2         | 0,12        | 1,94        | Fort          |
| 50        | 3,21        | 4,10        | Modéré        |
| 768       | 27,3        | 27,9        | Quasi nul     |

#### La concentration des volumes

En haute dimension, le volume d'un espace se concentre de manière 
contre-intuitive sur la surface d'une hypersphère plutôt qu'en son centre. 
Cela signifie que la quasi-totalité des points d'un échantillon se retrouve 
loin du centre et loin les uns des autres.

$$V_H(r) = \frac{\pi^{H/2}}{\Gamma(H/2 + 1)} r^H$$

Le volume croît exponentiellement avec la dimension $H$, ce qui implique 
qu'il faut exponentiellement plus de données pour couvrir cet espace de 
manière représentative.

| Dimension | Points nécessaires pour une couverture uniforme |
|-----------|-------------------------------------------------|
| 2         | ~100                                            |
| 10        | ~100 000                                        |
| 100       | ~$10^{20}$                                      |
| 768       | astronomique                                    |

#### Impact sur les résultats

Ces phénomènes ont des conséquences directes sur les tâches de NLP :

**Similarité cosinus dégradée**

La similarité cosinus est la mesure standard pour comparer deux embeddings BERT.
Mais en haute dimension, les vecteurs tendent à devenir quasi-orthogonaux 
entre eux, ce qui compresse les scores vers une plage étroite et rend 
la comparaison moins fiable.

$$\cos(\theta) = \frac{E(t_1) \cdot E(t_2)}{||E(t_1)|| \cdot ||E(t_2)||}$$

| Paire de termes       | Similarité attendue | Similarité observée (768d) |
|-----------------------|--------------------|-----------------------------|
| chat / chien          | Élevée             | 0,82                        |
| chat / poisson        | Modérée            | 0,79                        |
| chat / jardin         | Faible             | 0,76                        |

L'écart entre les scores est faible, ce qui rend le classement par similarité 
moins précis.

**Recherche de voisins (k-NN) moins efficace**

Les algorithmes de recherche par proximité (utilisés en recherche sémantique 
ou en RAG) deviennent moins précis et plus coûteux car la notion de 
"voisin proche" est dégradée.

**Surapprentissage**

Avec peu de données d'entraînement, un modèle travaillant en haute dimension 
risque de mémoriser les exemples plutôt que de généraliser, car l'espace 
est trop vaste pour être bien couvert.

#### Solutions courantes

| Technique                  | Principe                                              |
|----------------------------|-------------------------------------------------------|
| PCA                        | Réduction linéaire de dimension                       |
| UMAP                       | Réduction non-linéaire en préservant la topologie     |
| Matryoshka Representation  | Embeddings entraînés à fonctionner à plusieurs dims   |
| Mean Pooling               | Agrégation des vecteurs pour réduire la variance      |
| Fine-tuning                | Adapter l'espace vectoriel à la tâche cible           |

### Réduction de dimensionnalité

Face à la malédiction de la dimensionnalité, deux techniques sont couramment 
utilisées pour projeter les embeddings dans un espace de dimension réduite 
tout en préservant un maximum d'information.

---

### PCA (Principal Component Analysis)

PCA est une technique de réduction de dimension **linéaire** qui transforme 
les données en un nouvel ensemble d'axes appelés **composantes principales**. 
Ces axes sont construits de manière à maximiser la variance expliquée des données.

#### Fonctionnement

PCA opère en trois étapes :

**1. Centrage des données**

On soustrait la moyenne de chaque dimension pour centrer les données autour 
de l'origine :

$$\tilde{X} = X - \mu_X$$

**2. Décomposition en valeurs singulières (SVD)**

PCA décompose la matrice centrée pour identifier les directions de variance maximale :

$$X = U \Sigma V^T$$

Avec :
- $U$ : vecteurs propres (directions des composantes principales)
- $\Sigma$ : valeurs singulières (quantité de variance expliquée par chaque axe)
- $V^T$ : projection des données sur les nouveaux axes

**3. Projection**

On projette les données sur les $k$ premières composantes principales :

$$X_{réduit} = \tilde{X} \cdot U_k \quad \in \mathbb{R}^{k}$$

#### Variance expliquée

Chaque composante principale explique une part de la variance totale. 
On choisit $k$ de façon à conserver un seuil suffisant (ex: 95%) :

$$\text{Variance expliquée}(k) = \frac{\sum_{i=1}^{k} \sigma_i^2}{\sum_{i=1}^{n} \sigma_i^2}$$

Par exemple, sur les embeddings BERT-Base (768 dimensions) :

| Composantes (k) | Variance expliquée |
|-----------------|--------------------|
| 10              | ~42%               |
| 50              | ~71%               |
| 128             | ~88%               |
| 256             | ~95%               |
| 768             | 100%               |

#### Implémentation avec scikit-learn

```python
from sklearn.decomposition import PCA

# Conserver 95% de la variance
pca = PCA(n_components=0.95)
X_réduit = pca.fit_transform(embeddings)  # embeddings : (n_docs, 768) → (n_docs, k)

print(f"Dimensions réduites : {X_réduit.shape[1]}")  # ex: 256
print(f"Variance conservée : {pca.explained_variance_ratio_.sum():.2%}")
```

#### Limites

PCA est une transformation **linéaire** : elle ne peut capturer que des relations 
linéaires entre les dimensions. Des structures complexes et non-linéaires présentes 
dans les embeddings BERT (clusters sémantiques, relations hiérarchiques) peuvent 
être perdues ou aplaties lors de la projection.

---

### UMAP (Uniform Manifold Approximation and Projection)

UMAP est une technique de réduction de dimension **non-linéaire** qui cherche 
à préserver la structure topologique locale et globale des données. Contrairement 
à PCA, UMAP est capable de capturer des relations complexes entre les points.

#### Fonctionnement

UMAP opère en deux phases :

**1. Construction du graphe de voisinage (espace de départ)**

Pour chaque point, UMAP identifie ses $k$ voisins les plus proches et construit 
un graphe pondéré représentant les relations de proximité dans l'espace 
haute dimension :

$$w_{ij} = \exp\left(\frac{-\max(0, d(x_i, x_j) - \rho_i)}{\sigma_i}\right)$$

Avec :
- $d(x_i, x_j)$ : distance entre les points $i$ et $j$
- $\rho_i$ : distance au voisin le plus proche de $i$
- $\sigma_i$ : facteur de normalisation local

**2. Optimisation dans l'espace réduit**

UMAP projette ensuite les données dans l'espace cible (ex: 2D ou 3D) en 
minimisant la divergence entre le graphe original et le graphe projeté :

$$\mathcal{L} = \sum_{(i,j)} \left[ w_{ij} \log\frac{w_{ij}}{\tilde{w}_{ij}} + (1 - w_{ij}) \log\frac{1 - w_{ij}}{1 - \tilde{w}_{ij}} \right]$$

#### Paramètres clés

| Paramètre        | Rôle                                              | Valeur typique |
|------------------|---------------------------------------------------|----------------|
| `n_components`   | Dimension cible                                   | 2, 3, 128      |
| `n_neighbors`    | Taille du voisinage local (structure locale vs globale) | 15         |
| `min_dist`       | Compacité des clusters dans l'espace réduit       | 0.1            |
| `metric`         | Mesure de distance utilisée                       | `cosine`       |

#### Implémentation

```python
import umap

reducer = umap.UMAP(
    n_components=2,      # projection pour visualisation
    n_neighbors=15,      # voisinage local
    min_dist=0.1,        # compacité des clusters
    metric='cosine'      # adapté aux embeddings
)

X_réduit = reducer.fit_transform(embeddings)  # (n_docs, 768) → (n_docs, 2)
```

#### Limites

UMAP est **non-déterministe** : deux exécutions sur les mêmes données peuvent 
produire des projections différentes. De plus, les distances absolues entre 
clusters dans l'espace réduit ne sont pas directement interprétables — seules 
les relations de voisinage sont fiables.

---

### Comparaison PCA vs UMAP

| Critère               | PCA                        | UMAP                          |
|-----------------------|----------------------------|-------------------------------|
| Type de transformation | Linéaire                  | Non-linéaire                  |
| Structure préservée   | Variance globale           | Topologie locale et globale   |
| Vitesse               | Rapide                     | Plus lent                     |
| Déterminisme          | Oui                        | Non (stochastique)            |
| Interprétabilité      | Forte (variance expliquée) | Faible                        |
| Usage typique         | Réduction avant modèle     | Visualisation, clustering     |
| Adapté aux embeddings | Partiellement              | Oui                           |

## Sources 
Info générales :
https://huggingface.co/spaces/hesamation/primer-llm-embedding?section=what_are_embeddings?

TF-IDF :
https://youtu.be/zLMEnNbdh4Q?si=yMQ6nLAF4OCeukn8

BERT :
- https://www.youtube.com/watch?v=O3xbVmpdJwU

- https://arxiv.org/pdf/1810.04805

- https://arxiv.org/pdf/1908.08962

Curse of Dimensionality :
https://mlwiki.org/index.php/Curse_of_Dimensionality

PCA :
https://medium.com/@libertihub/principal-component-analysis-pca-an-intuitive-guide-for-everyone-5ea5431d7c17
