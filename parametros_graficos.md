# 🛠️ Parâmetros Obrigatórios e Opcionais por Tipo de Gráfico

Guia de referência detalhado para os parâmetros das funções do **Seaborn** e **Matplotlib**, especificando a obrigatoriedade e o tipo de valor esperado para cada argumento.

---

## 📋 Sumário
1. [Gráfico de Linhas (`sns.lineplot`)](#1-gráfico-de-linhas--snslineplot)
2. [Gráfico de Barras (`sns.barplot`)](#2-gráfico-de-barras-comparação--snsbarplot)
3. [Gráfico de Contagem / Frequência (`sns.countplot`)](#3-gráfico-de-contagem--frequência--snscountplot)
4. [Gráfico de Dispersão (`sns.scatterplot`)](#4-gráfico-de-dispersão--snsscatterplot)
5. [Histograma (`sns.histplot`)](#5-histograma--snshistplot)
6. [Boxplot (`sns.boxplot`)](#6-boxplot--snsboxplot)
7. [Heatmap / Mapa de Calor (`sns.heatmap`)](#7-heatmap-mapa-de-calor--snsheatmap)
8. [Gráfico de Pizza / Rosca (`plt.pie`)](#8-gráfico-de-pizza--rosca--pltpie-matplotlib)

---

### 1. Gráfico de Linhas — `sns.lineplot()`

* **Parâmetros Obrigatórios:**
  * `data`: *[pd.DataFrame]* O conjunto de dados estruturado em formato tabular.
  * `x`: *[str | array-like]* Nome da coluna com os valores do eixo $X$ (geralmente datas, períodos ou sequência ordenada).
  * `y`: *[str | array-like]* Nome da coluna com a variável numérica contínua para o eixo $Y$.

* **Parâmetros Opcionais Principais:**
  * `hue`: *[str]* Nome da coluna categórica ou numérica para agrupar e colorir linhas distintas.
  * `style`: *[str]* Nome da coluna para diferenciar as linhas por estilo do traço (ex.: contínuo, tracejado, pontilhado).
  * `marker`: *[str | bool]* Estilo do marcador visual nos pontos de amostragem (ex.: `"o"`, `"s"`, `"^"` ou `True`).
  * `linewidth`: *[float]* Espessura da linha desenhada em pontos (ex.: `2.5`).
  * `color`: *[str]* Cor individual da linha em hexadecimal (ex.: `"#2b5c8f"`) ou nome padrão (ex.: `"navy"`).
  * `ax`: *[matplotlib.axes.Axes]* O eixo específico da figura onde o gráfico será renderizado.

---

### 2. Gráfico de Barras (Comparação) — `sns.barplot()`

* **Parâmetros Obrigatórios:**
  * `data`: *[pd.DataFrame]* O DataFrame contendo os dados.
  * `x`: *[str]* Nome da coluna categórica para o eixo $X$ (ou numérica para barras horizontais).
  * `y`: *[str]* Nome da coluna numérica para calcular a média/agregação no eixo $Y$.

* **Parâmetros Opcionais Principais:**
  * `hue`: *[str]* Nome da coluna categórica para agrupar e dividir as barras em subgrupos lado a lado.
  * `palette`: *[str | list]* Nome da paleta de cores do Seaborn (ex.: `"Set2"`, `"Pastel1"`) ou lista de códigos hex.
  * `errorbar`: *[str | None]* Tipo de barra de erro exibida no topo das barras (ex.: `"ci"` para intervalo de confiança, `"sd"` para desvio padrão ou `None` para remover).
  * `estimator`: *[str | callable]* Função estatística de agregação (padrão é `"mean"`, mas aceita `"sum"`, `"median"`, etc.).
  * `orient`: *[str]* Orientação visual das barras: `"v"` (vertical) ou `"h"` (horizontal).
  * `ax`: *[matplotlib.axes.Axes]* O eixo da figura para renderização.

---

### 3. Gráfico de Contagem / Frequência — `sns.countplot()`

* **Parâmetros Obrigatórios:**
  * `data`: *[pd.DataFrame]* O DataFrame contendo os dados.
  * `x` **OU** `y`: *[str]* Nome da coluna categórica cuja frequência/contagem de linhas será calculada. (Passe apenas $X$ para barras verticais ou apenas $Y$ para barras horizontais).

* **Parâmetros Opcionais Principais:**
  * `hue`: *[str]* Coluna categórica secundária para subdividir a contagem.
  * `palette`: *[str | list]* Nome da paleta de cores aplicada às categorias.
  * `order`: *[list]* Lista de strings declarando a ordem exata das categorias no eixo (ex.: `["Baixo", "Médio", "Alto"]`).
  * `stat`: *[str]* Unidade estatística exibida nas barras: `"count"` (absoluto), `"percent"` (porcentagem total) ou `"proportion"`.
  * `ax`: *[matplotlib.axes.Axes]* O eixo para inserção do gráfico.

---

### 4. Gráfico de Dispersão — `sns.scatterplot()`

* **Parâmetros Obrigatórios:**
  * `data`: *[pd.DataFrame]* O DataFrame fonte.
  * `x`: *[str]* Nome da coluna com a variável numérica contínua no eixo $X$.
  * `y`: *[str]* Nome da coluna com a variável numérica contínua no eixo $Y$.

* **Parâmetros Opcionais Principais:**
  * `hue`: *[str]* Coluna para colorir os pontos de acordo com grupos ou categorias.
  * `style`: *[str]* Coluna para alterar o formato dos marcadores (ex.: círculos, quadrados, triângulos) por grupo.
  * `size`: *[str]* Coluna numérica para ajustar o diâmetro proporcional de cada ponto.
  * `s`: *[float]* Tamanho fixo em pontos para todos os marcadores (ex.: `70`).
  * `alpha`: *[float]* Nível de transparência de `0.0` (invisível) a `1.0` (opaco), útil contra sobreposição (*overplotting*).
  * `palette`: *[str | list]* Paleta de cores mapeada para o parâmetro `hue`.
  * `ax`: *[matplotlib.axes.Axes]* O eixo de destino.

---

### 5. Histograma — `sns.histplot()`

* **Parâmetros Obrigatórios:**
  * `data`: *[pd.DataFrame]* O conjunto de dados.
  * `x`: *[str]* Nome da coluna numérica contínua cuja distribuição de frequência será analisada.

* **Parâmetros Opcionais Principais:**
  * `bins`: *[int | list]* Número total de intervalos/barras (ex.: `15`) ou lista definindo os limites exatos de cada classe.
  * `kde`: *[bool]* Se `True`, sobrepõe a curva suave de Estimativa de Densidade de Kernel sobre o histograma.
  * `color`: *[str]* Cor principal do preenchimento das barras.
  * `stat`: *[str]* Métrica do eixo Y: `"count"` (frequência), `"density"` (densidade), `"probability"` ou `"percent"`.
  * `hue`: *[str]* Coluna para sobrepor distribuições de diferentes categorias.
  * `element`: *[str]* Estilo de desenho do histograma: `"bars"`, `"step"` ou `"poly"`.
  * `ax`: *[matplotlib.axes.Axes]* O eixo para renderização.

---

### 6. Boxplot — `sns.boxplot()`

* **Parâmetros Obrigatórios:**
  * `data`: *[pd.DataFrame]* O DataFrame fonte.
  * `y`: *[str]* Nome da coluna numérica contínua para o cálculo dos quartis, mediana e *outliers* (eixo $Y$).

* **Parâmetros Opcionais Principais:**
  * `x`: *[str]* Nome da coluna categórica no eixo $X$ para criar múltiplos boxplots comparativos lado a lado.
  * `hue`: *[str]* Coluna categórica secundária para subdividir e colorir as caixas dentro de cada categoria de $X$.
  * `palette`: *[str | list]* Paleta de cores para preenchimento dos boxplots.
  * `orient`: *[str]* Orientação visual das caixas: `"v"` (vertical) ou `"h"` (horizontal).
  * `width`: *[float]* Largura relativa das caixas (ex.: `0.5`).
  * `ax`: *[matplotlib.axes.Axes]* O eixo de destino.

---

### 7. Heatmap (Mapa de Calor) — `sns.heatmap()`

* **Parâmetros Obrigatórios:**
  * `data`: *[2D array-like | pd.DataFrame Pivot]* Uma matriz bidimensional de números (ex.: saída de `df.corr()` ou `df.pivot()`). Não aceita DataFrames brutos em formato longo.

* **Parâmetros Opcionais Principais:**
  * `annot`: *[bool]* Se `True`, escreve o valor numérico dentro de cada célula.
  * `fmt`: *[str]* Formatação da string numérica quando `annot=True` (ex.: `".2f"` para 2 casas decimais, `"d"` para inteiros).
  * `cmap`: *[str]* Mapa de cores/gradiente térmico (ex.: `"coolwarm"`, `"viridis"`, `"YlGnBu"`).
  * `linewidths`: *[float]* Espessura das linhas brancas de separação entre as células (ex.: `0.5`).
  * `cbar`: *[bool]* Se `True` (padrão), exibe a barra lateral de escala de cores (*colorbar*).
  * `vmin` / `vmax`: *[float]* Valores mínimo e máximo para ancorar a escala de cor (ex.: `vmin=-1`, `vmax=1`).
  * `ax`: *[matplotlib.axes.Axes]* O eixo de destino.

---

### 8. Gráfico de Pizza / Rosca — `plt.pie()` *(Matplotlib)*

* **Parâmetros Obrigatórios:**
  * `x`: *[list | array-like]* Sequência de valores numéricos contendo as proporções ou tamanhos de cada fatia (ex.: `[45, 30, 25]`).

* **Parâmetros Opcionais Principais:**
  * `labels`: *[list[str]]* Lista de nomes associados a cada uma das fatias (ex.: `["Site", "Loja", "App"]`).
  * `autopct`: *[str | callable]* String de formatação para exibir a porcentagem nas fatias (ex.: `"%1.1f%%"` renderiza `45.0%`).
  * `colors`: *[list[str]]* Lista de cores individuais aplicadas ordenadamente às fatias.
  * `startangle`: *[float]* Ângulo inicial de rotação (em graus) onde a primeira fatia começa a ser desenhada (ex.: `90` ou `140`).
  * `explode`: *[tuple | list]* Sequência de offsets para destacar/afastar fatias do centro (ex.: `(0, 0.1, 0)` afasta ligeiramente a 2ª fatia).
  * `wedgeprops`: *[dict]* Dicionário de propriedades visuais das fatias. O uso de `wedgeprops={"width": 0.4}` remove o centro da figura, transformando o gráfico de pizza em um **Gráfico de Rosca**.