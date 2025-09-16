🧪 Resultados dos Experimentos de Clusterização
🔹 DBSCAN – Ajustes Iniciais

Figura 1: a execução padrão do DBSCAN retorna um modelo mal definido, com silhueta = NaN e apenas um único cluster formado.

Isso acontece porque os parâmetros padrão (eps=0.5, min_samples=5) não são adequados para a distribuição inicial dos dados.

🔹 Ajuste de Parâmetros (eps e min_samples)

Figura 2 e Figura 3: ao variar eps e min_samples, o DBSCAN passou a retornar agrupamentos mais coesos:

Configuração focada em ARI: separa corretamente os dois clusters (ARI = 1.0).

Configuração focada em Silhouette: retorna 3 clusters bem separados, mas com a maior parte dos pontos marcados como ruído.

📌 Observação:

ARI máximo → obtido com eps < 0.50.

Silhouette máximo → obtido com eps < 0.20.

🌲 Forest Covertypes

A distribuição original mostra dois tipos dominantes de árvores (cover types).

Porém, após a clusterização, essa proporção não se manteve:

O DBSCAN descartou grande parte dos dados como ruído.

Seriam necessários ajustes adicionais de eps e min_samples para melhorar o equilíbrio entre clusters definidos e quantidade de ruídos.

🔵 Comparação de Métricas – make_circles
Método	ARI	NMI	Silhouette
DBSCAN (melhor ARI)	1.000	1.000	0.113
KMeans	-0.001	0.000	0.353
Agglomerative	0.009	0.008	0.330

O DBSCAN (com eps=0.20, min_samples=3) conseguiu uma separação perfeita (ARI = 1.0, NMI = 1.0).

O KMeans praticamente falhou (ARI ≈ 0, NMI ≈ 0).

O Agglomerative teve desempenho muito baixo.

📌 No entanto, o Silhouette do DBSCAN foi menor. Isso acontece porque a métrica não usa rótulos verdadeiros — ela avalia apenas separação geométrica. Nesse aspecto, KMeans e Agglomerative conseguem clusters mais “esféricos”, o que eleva seu score.

🖼️ Olivetti Faces

O dataset Olivetti Faces foi o maior desafio:

DBSCAN não conseguiu formar clusters úteis, agrupando praticamente todas as faces em um único cluster ou marcando como ruído.

KMeans trouxe resultados razoáveis, mas misturou bastante entre diferentes identidades.

Agglomerative Clustering obteve o melhor desempenho, mesmo que por uma margem pequena, conseguindo separar algumas faces de forma mais consistente.

✅ Conclusões Gerais

O DBSCAN funciona muito bem em datasets com padrões de densidade claros (ex.: make_circles).

Para dados de alta dimensão e complexidade (como Olivetti Faces), métodos como KMeans e principalmente Agglomerative se mostram mais adequados.

Silhouette deve ser interpretado com cuidado: valores altos não significam correspondência com os rótulos reais, apenas boa separação geométrica entre clusters.
