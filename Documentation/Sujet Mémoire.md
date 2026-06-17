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