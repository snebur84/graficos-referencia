# Métodos e Parâmetros do Plotly Python

---

## 1. Plotly Express (`import plotly.express as px`)

> **Convenção:** Quando usados com DataFrames, o primeiro argumento posicional é o `data_frame`. As colunas são passadas como strings.

### `px.line()` | `px.scatter()` | `px.bar()`

| Parâmetro | Tipo | Status | Descrição |
| :--- | :--- | :--- | :--- |
| `data_frame` | DataFrame | Opcional* | DataFrame contendo os dados. |
| `x` | str / array | **Obrigatório** | Coluna/dados para o eixo X. |
| `y` | str / array | **Obrigatório** | Coluna/dados para o eixo Y. |
| `color` | str | Opcional | Agrupa e colore por uma coluna categórica/numérica. |
| `title` | str | Opcional | Título principal do gráfico. |
| `labels` | dict | Opcional | Renomeia os eixos e legendas: `{"col_x": "Novo Nome"}`. |
| `hover_data` | list | Opcional | Colunas extras para exibir no *tooltip* ao passar o mouse. |
| `hover_name` | str | Opcional | Coluna destacada no topo do *tooltip*. |
| `facet_col` / `facet_row` | str | Opcional | Divide o gráfico em subpainéis por colunas/linhas. |
| `trendline` | str | Opcional | *(Apenas Scatter)* Ex: `"ols"` (regressão) ou `"lowess"`. |
| `barmode` | str | Opcional | *(Apenas Bar)* Disposição das barras: `"group"`, `"stack"`, `"relative"`. |
| `text` | str | Opcional | Coluna cujos valores são exibidos sobre os elementos visuais. |

```python
import plotly.express as px

df = px.data.gapminder().query("country == 'Brazil'")

# Exemplo px.line
fig_line = px.line(df, x="year", y="gdpPercap", title="PIB per Capita no Brasil")

# Exemplo px.scatter
fig_scatter = px.scatter(df, x="gdpPercap", y="lifeExp", size="pop", color="year", title="Relação PIB vs Expectativa de Vida")

# Exemplo px.bar
fig_bar = px.bar(df, x="year", y="pop", title="Crescimento Populacional no Brasil")

```

---

### `px.histogram()`

| Parâmetro | Tipo | Status | Descrição |
| --- | --- | --- | --- |
| `data_frame` | DataFrame | Opcional* | DataFrame contendo os dados. |
| `x` (ou `y`) | str / array | **Obrigatório** | Variável para cálculo da distribuição. |
| `nbins` | int | Opcional | Número aproximado de intervalos (*bins*). |
| `color` | str | Opcional | Agrupa a distribuição por categorias. |
| `histfunc` | str | Opcional | Agregação: `"count"`, `"sum"`, `"avg"`, `"min"`, `"max"`. |
| `marginal` | str | Opcional | Gráfico marginal na borda: `"rug"`, `"box"`, `"violin"`. |
| `barnorm` | str | Opcional | Normalização das barras: `"fraction"` ou `"percent"`. |

```python
import plotly.express as px

df = px.data.iris()
fig_hist = px.histogram(df, x="sepal_length", color="species", nbins=20, marginal="box", title="Distribuição do Comprimento da Sépala")

```

---

### `px.pie()`

| Parâmetro | Tipo | Status | Descrição |
| --- | --- | --- | --- |
| `data_frame` | DataFrame | Opcional* | DataFrame contendo os dados. |
| `names` | str | **Obrigatório** | Coluna categórica que define os rótulos das fatias. |
| `values` | str | **Obrigatório** | Coluna numérica que define a proporção das fatias. |
| `color` | str | Opcional | Mapeamento customizado de esquema de cores. |
| `hole` | float | Opcional | Valor de `0` a `1` para transformar em rosca (*donut*). |
| `title` | str | Opcional | Título principal do gráfico. |

```python
import plotly.express as px

df = px.data.gapminder().query("year == 2007")
fig_pie = px.pie(df, names="continent", values="pop", hole=0.4, title="População Mundial por Continente (2007)")

```

---

## 2. Graph Objects (`import plotly.graph_objects as go`)

> **Convenção:** Trabalha diretamente com estruturas de dados nativas (listas, Séries Pandas, arrays NumPy).

### `go.Scatter()` | `go.Bar()`

| Parâmetro | Tipo | Status | Descrição |
| --- | --- | --- | --- |
| `x` | list / array | **Obrigatório** | Dados do eixo X. |
| `y` | list / array | **Obrigatório** | Dados do eixo Y. |
| `mode` | str | Opcional | *(Apenas Scatter)* Visualização: `"lines"`, `"markers"`, `"lines+markers"`. |
| `name` | str | Opcional | Nome da série exibido na legenda. |
| `marker` | dict | Opcional | Estilo dos pontos/barras: `dict(color="red", size=10)`. |
| `line` | dict | Opcional | Estilo da linha: `dict(color="blue", width=2, dash="dash")`. |
| `text` | list | Opcional | Textos para exibição nos pontos ou no *tooltip*. |
| `hovertemplate` | str | Opcional | Padrão HTML/variáveis para formatar o *tooltip*. |

```python
import plotly.graph_objects as go

# Exemplo go.Scatter
fig_go_scatter = go.Figure()
fig_go_scatter.add_trace(go.Scatter(
    x=[1, 2, 3, 4], 
    y=[10, 11, 12, 13], 
    mode="lines+markers", 
    name="Vendas", 
    line=dict(color="firebrick", width=3)
))

# Exemplo go.Bar
fig_go_bar = go.Figure()
fig_go_bar.add_trace(go.Bar(
    x=["Jan", "Fev", "Mar"], 
    y=[20, 14, 23], 
    marker=dict(color="royalblue")
))

```

---

### `go.Heatmap()`

| Parâmetro | Tipo | Status | Descrição |
| --- | --- | --- | --- |
| `z` | matriz 2D | **Obrigatório** | Matriz de valores numéricos que definem as cores. |
| `x` / `y` | list | Opcional | Rótulos das colunas e linhas. |
| `colorscale` | str | Opcional | Paleta de cores (ex: `"Viridis"`, `"RdBu"`, `"Plasma"`). |
| `showscale` | bool | Opcional | Exibe ou oculta a barra lateral de cores (`True`/`False`). |
| `texttemplate` | str | Opcional | Formatação do texto interno da célula (ex: `"%{z:.2f}"`). |

```python
import plotly.graph_objects as go

fig_heatmap = go.Figure(data=go.Heatmap(
    z=[[1, 20, 30], [20, 1, 60], [30, 60, 1]],
    x=['A', 'B', 'C'],
    y=['A', 'B', 'C'],
    colorscale='Viridis'
))

```

---

### Modificadores do Objeto `Figure` (`fig`)

#### `fig.update_layout()`

| Parâmetro | Tipo | Descrição |
| --- | --- | --- |
| `title` | str / dict | Título do gráfico (ou `dict(text="Título", x=0.5)` para centralizar). |
| `xaxis_title` / `yaxis_title` | str | Rótulos dos eixos principais X e Y. |
| `template` | str | Tema visual (`"plotly_dark"`, `"ggplot2"`, `"seaborn"`, `"simple_white"`). |
| `showlegend` | bool | Oculta ou exibe a legenda global (`True`/`False`). |
| `width` / `height` | int | Dimensões do gráfico em pixels. |
| `barmode` | str | Agrupamento de barras global (`"group"`, `"stack"`). |

#### `fig.update_traces()`

| Parâmetro | Tipo | Descrição |
| --- | --- | --- |
| `selector` | dict | Filtra os traços afetados (ex: `dict(type="bar")`). |
| `marker_color` | str | Altera a cor de preenchimento dos traços selecionados. |
| `line_width` | int/float | Altera a espessura da linha dos traços selecionados. |

```python
import plotly.graph_objects as go

fig = go.Figure(data=[go.Bar(x=["A", "B"], y=[10, 20])])

# Atualizando o layout global
fig.update_layout(
    title=dict(text="Gráfico Customizado", x=0.5),
    xaxis_title="Categorias",
    yaxis_title="Valores",
    template="plotly_dark"
)

# Atualizando estilo das barras
fig.update_traces(marker_color="teal")

```

---

## 3. Subplots (`from plotly.subplots import make_subplots`)

### `make_subplots()`

| Parâmetro | Tipo | Status | Descrição |
| --- | --- | --- | --- |
| `rows` | int | **Obrigatório** | Número de linhas da grade. |
| `cols` | int | **Obrigatório** | Número de colunas da grade. |
| `subplot_titles` | list[str] | Opcional | Títulos individuais de cada painel. |
| `shared_xaxes` / `shared_yaxes` | bool / str | Opcional | Compartilha a mesma escala entre os painéis (`True`, `"all"`). |
| `specs` | matriz dict | Opcional | Define tipos de gráficos por célula: `[{"type": "xy"}, {"type": "domain"}]`. |
| `row_heights` / `column_widths` | list[float] | Opcional | Proporções relativas do tamanho de cada linha/coluna. |

```python
import plotly.graph_objects as go
from plotly.subplots import make_subplots

fig_subplots = make_subplots(
    rows=1, cols=2, 
    subplot_titles=("Gráfico de Linha", "Gráfico de Barras")
)

fig_subplots.add_trace(go.Scatter(x=[1, 2, 3], y=[4, 5, 6]), row=1, col=1)
fig_subplots.add_trace(go.Bar(x=["A", "B", "C"], y=[2, 3, 1]), row=1, col=2)

```

---

## 4. Exportação e Exibição

```python
fig.show()                          # Exibe o gráfico interativo
fig.write_html("grafico.html")      # Salva como arquivo HTML interativo
fig.write_image("grafico.png")      # Salva como imagem estática (requer pacote 'kaleido')

```