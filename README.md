# Mini-mémoire-Base-vectorielles

Par score/dim
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Famille</th>
      <th>Methode</th>
      <th>Score F1</th>
      <th>Temps Reduction (s)</th>
      <th>Dimension</th>
      <th>Score F1 / Dimension</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Arctic</td>
      <td>PCA (64)</td>
      <td>0.733080</td>
      <td>0.076523</td>
      <td>64</td>
      <td>0.011454</td>
    </tr>
    <tr>
      <th>1</th>
      <td>MiniLM</td>
      <td>PCA (64)</td>
      <td>0.683000</td>
      <td>0.032008</td>
      <td>64</td>
      <td>0.010672</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arctic</td>
      <td>UMAP (64)</td>
      <td>0.659515</td>
      <td>26.212821</td>
      <td>64</td>
      <td>0.010305</td>
    </tr>
    <tr>
      <th>3</th>
      <td>MiniLM</td>
      <td>UMAP (64)</td>
      <td>0.648152</td>
      <td>36.211846</td>
      <td>64</td>
      <td>0.010127</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Arctic</td>
      <td>Matryoshka (64)</td>
      <td>0.637375</td>
      <td>0.000000</td>
      <td>64</td>
      <td>0.009959</td>
    </tr>
    <tr>
      <th>5</th>
      <td>MiniLM</td>
      <td>Matryoshka (64)</td>
      <td>0.553343</td>
      <td>0.000000</td>
      <td>64</td>
      <td>0.008646</td>
    </tr>
    <tr>
      <th>6</th>
      <td>MiniLM</td>
      <td>Pleine Dim (384 et 768)</td>
      <td>0.704850</td>
      <td>0.000000</td>
      <td>384</td>
      <td>0.001836</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Arctic</td>
      <td>Pleine Dim (384 et 768)</td>
      <td>0.748704</td>
      <td>0.000000</td>
      <td>768</td>
      <td>0.000975</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Baseline</td>
      <td>TF-IDF (1000 dim)</td>
      <td>0.584102</td>
      <td>0.000000</td>
      <td>1000</td>
      <td>0.000584</td>
    </tr>
  </tbody>
</table>
</div>


Par Score
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Famille</th>
      <th>Methode</th>
      <th>Score F1</th>
      <th>Temps Reduction (s)</th>
      <th>Dimension</th>
      <th>Score F1 / Dimension</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Arctic</td>
      <td>Pleine Dim (384 et 768)</td>
      <td>0.748704</td>
      <td>0.000000</td>
      <td>768</td>
      <td>0.000975</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Arctic</td>
      <td>PCA (64)</td>
      <td>0.733080</td>
      <td>0.076523</td>
      <td>64</td>
      <td>0.011454</td>
    </tr>
    <tr>
      <th>2</th>
      <td>MiniLM</td>
      <td>Pleine Dim (384 et 768)</td>
      <td>0.704850</td>
      <td>0.000000</td>
      <td>384</td>
      <td>0.001836</td>
    </tr>
    <tr>
      <th>3</th>
      <td>MiniLM</td>
      <td>PCA (64)</td>
      <td>0.683000</td>
      <td>0.032008</td>
      <td>64</td>
      <td>0.010672</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Arctic</td>
      <td>UMAP (64)</td>
      <td>0.659515</td>
      <td>26.212821</td>
      <td>64</td>
      <td>0.010305</td>
    </tr>
    <tr>
      <th>5</th>
      <td>MiniLM</td>
      <td>UMAP (64)</td>
      <td>0.648152</td>
      <td>36.211846</td>
      <td>64</td>
      <td>0.010127</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Arctic</td>
      <td>Matryoshka (64)</td>
      <td>0.637375</td>
      <td>0.000000</td>
      <td>64</td>
      <td>0.009959</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Baseline</td>
      <td>TF-IDF (1000 dim)</td>
      <td>0.584102</td>
      <td>0.000000</td>
      <td>1000</td>
      <td>0.000584</td>
    </tr>
    <tr>
      <th>8</th>
      <td>MiniLM</td>
      <td>Matryoshka (64)</td>
      <td>0.553343</td>
      <td>0.000000</td>
      <td>64</td>
      <td>0.008646</td>
    </tr>
  </tbody>
</table>
</div>