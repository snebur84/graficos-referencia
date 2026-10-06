# 📊 Matplotlib & Seaborn Visualizations Cheat Sheet

Um guia de referência rápida e prático para criação de visualizações de dados em Python usando **Matplotlib** e **Seaborn**.

---

## 🏛️ Guia de Referência por Tipo de Gráfico

A tabela abaixo está organizada hierarquicamente por **Tipo de Gráfico**, **Componente do Gráfico** e **Eixos**, incluindo exemplos diretos de código em Python para fácil consulta:

| Tipo de Gráfico | Componente do Gráfico | Eixo(s) | Biblioteca | Método / Função | Principais Parâmetros | Exemplo de Uso |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Linhas / Tendência** | Dados / Marcas (Linhas e Pontos) | $X$ (Temporal/Contínuo), $Y$ (Contínuo) | **Seaborn** | `sns.lineplot()` | `data`, `x`, `y`, `hue`, `style`, `marker`, `linewidth`, `color`, `ax` | `sns.lineplot(data=df, x="data", y="vendas", marker="o", ax=ax)` |
| **Barras / Comparação** | Dados / Marcas (Retângulos) | $X$ (Categórico), $Y$ (Numérico) | **Seaborn** | `sns.barplot()` | `data`, `x`, `y`, `hue`, `palette`, `errorbar`, `orient`, `ax` | `sns.barplot(data=df, x="categoria", y="valor", palette="Set2", ax=ax)` |
| **Barras de Frequência** | Dados / Contagem de Frequência | $X$ ou $Y$ (Categórico) | **Seaborn** | `sns.countplot()` | `data`, `x`, `y`, `hue`, `palette`, `stat`, `ax` | `sns.countplot(data=df, x="categoria", palette="Blues", ax=ax)` |
| **Dispersão / Correlação** | Dados / Marcas (Pontos) | $X$ (Contínuo), $Y$ (Contínuo) | **Seaborn** | `sns.scatterplot()` | `data`, `x`, `y`, `hue`, `style`, `size`, `s`, `alpha`, `palette`, `ax` | `sns.scatterplot(data=df, x="peso", y="altura", hue="sexo", s=80, ax=ax)` |
| **Regressão / Tendência** | Linha de Regressão / Tendência | $X$ (Contínuo), $Y$ (Contínuo) | **Seaborn** | `sns.regplot()` | `data`, `x`, `y`, `scatter` (bool), `color`, `line_kws`, `ax` | `sns.regplot(data=df, x="renda", y="gasto", scatter=False, color="red", ax=ax)` |
| **Distribuição / Frequência** | Dados / Marcas (Histograma + KDE) | $X$ (Contínuo), $Y$ (Frequência) | **Seaborn** | `sns.histplot()` | `data`, `x`, `bins`, `kde` (bool), `color`, `stat`, `element`, `ax` | `sns.histplot(data=df, x="idade", bins=15, kde=True, ax=ax)` |
| **Densidade Estimada (KDE)** | Dados / Curva de Densidade | $X$ (Contínuo), $Y$ (Densidade) | **Seaborn** | `sns.kdeplot()` | `data`, `x`, `y`, `fill` (bool), `bw_adjust`, `cmap`, `ax` | `sns.kdeplot(data=df, x="salario", fill=True, color="green", ax=ax)` |
| **Distribuição Acumulada** | Dados / Distribuição Acumulada | $X$ (Contínuo), $Y$ (Proporção) | **Seaborn** | `sns.ecdfplot()` | `data`, `x`, `hue`, `stat` (*count/proportion*), `ax` | `sns.ecdfplot(data=df, x="tempo_espera", hue="tipo", ax=ax)` |
| **Boxplot / Outliers** | Dados / Marcas (Caixa, Mediana e Outliers) | $X$ (Categórico), $Y$ (Contínuo) | **Seaborn** | `sns.boxplot()` | `data`, `x`, `y`, `hue`, `palette`, `orient`, `width`, `ax` | `sns.boxplot(data=df, x="depto", y="salario", palette="Pastel1", ax=ax)` |
| **Violin Plot / Densidade** | Dados / Distribuição + Boxplot | $X$ (Categórico), $Y$ (Contínuo) | **Seaborn** | `sns.violinplot()` | `data`, `x`, `y`, `hue`, `split` (bool), `inner`, `palette`, `ax` | `sns.violinplot(data=df, x="classe", y="idade", split=True, ax=ax)` |
| **Dispersão Categórica** | Dados / Pontos de Observações Individuais | $X$ (Categórico), $Y$ (Contínuo) | **Seaborn** | `sns.stripplot()` / `sns.swarmplot()` | `data`, `x`, `y`, `hue`, `jitter`, `dodge`, `size`, `ax` | `sns.stripplot(data=df, x="dia", y="total", jitter=True, alpha=0.6, ax=ax)` |
| **Heatmap / Matriz Térmica** | Dados / Matriz de Cores | $X$ e $Y$ (Categóricos/Matriz) | **Seaborn** | `sns.heatmap()` | `data`, `annot` (bool), `fmt`, `cmap`, `linewidths`, `cbar`, `ax` | `sns.heatmap(df.corr(), annot=True, fmt=".2f", cmap="coolwarm", ax=ax)` |
| **Matriz de Dispersão** | Grade de Subplots de Pares | Múltiplos $X$ e $Y$ (Numéricos) | **Seaborn** | `sns.pairplot()` | `data`, `hue`, `palette`, `kind` (*scatter/reg*), `diag_kind` | `sns.pairplot(df, hue="especie", corner=True)` |
| **Painéis / Facetas** | Interface Nível Figura (*FacetGrid*) | Ambos ($X$ e $Y$) | **Seaborn** | `sns.catplot()` / `sns.relplot()` | `data`, `x`, `y`, `hue`, `kind`, `col`, `row`, `col_wrap`, `height` | `sns.catplot(data=df, x="dia", y="conta", col="tempo", kind="box")` |
| **Anotação de Texto** | Anotação e Texto Customizado | Ambos ($X$ e $Y$) | **Matplotlib** | `ax.annotate()` / `ax.text()` | `text`, `xy`, `xytext`, `arrowprops`, `fontsize` | `ax.annotate("Pico", xy=(5, 100), xytext=(6, 120), arrowprops=dict(arrowstyle="->"))` |
| **Barra de Cores** | Barra de Cores (*Colorbar*) | Eixo Z / Escala de Cor | **Matplotlib** | `plt.colorbar()` | `mappable`, `ax`, `orientation`, `label` | `fig.colorbar(im, ax=ax, orientation="vertical", label="Escala")` |
| **Eixos e Escalas** | Limites da Escala dos Eixos | $X$ ou $Y$ | **Matplotlib** | `ax.set_xlim()` / `ax.set_ylim()` | `left`/`bottom`, `right`/`top`, `auto` | `ax.set_xlim(0, 100); ax.set_ylim(0, 500)` |
| **Marcas dos Eixos** | Marcas de Graduação (*Ticks*) | $X$ ou $Y$ | **Matplotlib** | `ax.set_xticks()` / `ax.set_yticks()` | `ticks`, `labels`, `rotation`, `minor` | `ax.set_xticks([0, 1, 2]); ax.set_xticklabels(["A", "B", "C"], rotation=45)` |
| **Linhas de Referência** | Linhas Horizontal / Vertical | $X$ ou $Y$ | **Matplotlib** | `ax.axhline()` / `ax.axvline()` | `y`/`x`, `color`, `linestyle`, `linewidth`, `label` | `ax.axhline(y=50, color="r", linestyle="--", label="Meta")` |
| **Estrutura Base** | Figura (`Figure`) e Eixo (`Axes`) | Ambos ($X$ e $Y$) | **Matplotlib** | `plt.subplots()` | `figsize`, `nrows`, `ncols`, `sharex`, `sharey` | `fig, ax = plt.subplots(figsize=(10, 6))` |
| **Título Principal** | Título Principal | N/A | **Matplotlib** | `ax.set_title()` | `label`, `fontsize`, `fontweight`, `loc`, `pad` | `ax.set_title("Vendas do Ano", fontsize=14, fontweight="bold")` |
| **Rótulos de Eixo** | Rótulos dos Eixos X e Y | $X$ ou $Y$ | **Matplotlib** | `ax.set_xlabel()` / `ax.set_ylabel()` | `xlabel`/`ylabel`, `fontsize`, `fontweight`, `labelpad` | `ax.set_xlabel("Meses", fontsize=11); ax.set_ylabel("Total ($)", fontsize=11)` |
| **Legendas** | Legenda Explicativa | Ambos ($X$ e $Y$) | **Matplotlib** | `ax.legend()` | `title`, `loc`, `frameon`, `fontsize`, `ncol` | `ax.legend(title="Categorias", loc="upper right", frameon=True)` |
| **Linhas de Grade** | Grade de Fundo | Ambos ($X$ e $Y$) | **Matplotlib** | `ax.grid()` | `visible`, `linestyle`, `linewidth`, `alpha`, `color` | `ax.grid(True, linestyle="--", alpha=0.5)` |
| **Ajuste e Estilo Global** | Layout e Tema Global | N/A | **Matplotlib** / **Seaborn** | `plt.tight_layout()` / `sns.set_theme()` | `style`, `palette`, `font_scale`, `pad` | `sns.set_theme(style="whitegrid"); plt.tight_layout()` |
| **Exportação de Imagem** | Exportação / Arquivo | N/A | **Matplotlib** | `plt.savefig()` | `fname`, `dpi`, `bbox_inches`, `format`, `transparent` | `plt.savefig("grafico.png", dpi=300, bbox_inches="tight")` |

---

## 🛠️ Configuração Inicial do Ambiente

```python
import matplotlib.pyplot as plt
import seaborn as sns

# Configuração de estilo do Seaborn
sns.set_theme(style="whitegrid")

# Datasets padrão de exemplo
df_tips = sns.load_dataset("tips")        # Dados de contas e gorjetas
df_flights = sns.load_dataset("flights")  # Dados temporais de passageiros
```

---

## 📈 Exemplos Práticos por Tipo de Gráfico

### 1. Gráfico de Linhas (Tendências / Séries Temporais)

> **Uso:** Acompanhar mudanças ao longo do tempo ou de uma sequência contínua.

```python
fig, ax = plt.subplots(figsize=(10, 5))

sns.lineplot(
    data=df_flights[df_flights["year"] == 1960],
    x="month",
    y="passengers",
    marker="o",
    color="#2b5c8f",
    linewidth=2,
    ax=ax,
)

ax.set_title("Evolução do Número de Passageiros (1960)", fontsize=14, fontweight="bold")
ax.set_xlabel("Mês", fontsize=11)
ax.set_ylabel("Total de Passageiros", fontsize=11)

plt.tight_layout()
plt.show()
```

### 2. Gráfico de Barras (Comparação Categórica)

> **Uso:** Comparar métricas numéricas entre categorias discretas.

```python
fig, ax = plt.subplots(figsize=(8, 5))

sns.barplot(
    data=df_tips,
    x="day",
    y="total_bill",
    hue="sex",
    palette="Set2",
    errorbar=None,
    ax=ax,
)

ax.set_title("Média do Valor da Conta por Dia e Gênero", fontsize=14, fontweight="bold")
ax.set_xlabel("Dia da Semana", fontsize=11)
ax.set_ylabel("Média da Conta ($)", fontsize=11)
ax.legend(title="Gênero", frameon=True)

plt.tight_layout()
plt.show()
```

### 3. Gráfico de Dispersão / Scatter Plot (Relação e Correlação)

> **Uso:** Analisar a relação ou correlação entre duas variáveis contínuas.

```python
fig, ax = plt.subplots(figsize=(8, 5))

# Pontos de dispersão
sns.scatterplot(
    data=df_tips,
    x="total_bill",
    y="tip",
    hue="time",
    style="time",
    s=70,
    alpha=0.8,
    ax=ax,
)

# Linha de tendência
sns.regplot(
    data=df_tips,
    x="total_bill",
    y="tip",
    scatter=False,
    color="gray",
    ax=ax,
)

ax.set_title("Relação entre Valor da Conta e Gorjeta", fontsize=14, fontweight="bold")
ax.set_xlabel("Valor Total da Conta ($)", fontsize=11)
ax.set_ylabel("Gorjeta ($)", fontsize=11)

plt.tight_layout()
plt.show()
```

### 4. Histograma com KDE (Distribuição e Frequência)

> **Uso:** Entender a distribuição, assimetria e frequência de uma variável numérica.

```python
fig, ax = plt.subplots(figsize=(8, 5))

sns.histplot(
    data=df_tips,
    x="total_bill",
    kde=True,
    bins=15,
    color="#4c72b0",
    ax=ax,
)

ax.set_title("Distribuição dos Valores das Contas", fontsize=14, fontweight="bold")
ax.set_xlabel("Valor da Conta ($)", fontsize=11)
ax.set_ylabel("Frequência", fontsize=11)

plt.tight_layout()
plt.show()
```

### 5. Boxplot (Quartis e Outliers)

> **Uso:** Identificar mediana, variação quartílica e *outliers* de grupos categóricos.

```python
fig, ax = plt.subplots(figsize=(8, 5))

sns.boxplot(
    data=df_tips,
    x="day",
    y="total_bill",
    palette="Pastel1",
    ax=ax,
)

ax.set_title("Dispersão dos Valores das Contas por Dia", fontsize=14, fontweight="bold")
ax.set_xlabel("Dia da Semana", fontsize=11)
ax.set_ylabel("Valor da Conta ($)", fontsize=11)

plt.tight_layout()
plt.show()
```

---

## ⚡ Comandos Rápidos e Utilitários

```python
# Ajustar layout para evitar corte de elementos
plt.tight_layout()

# Salvar gráfico em alta resolução
plt.savefig("grafico.png", dpi=300, bbox_inches="tight")

# Exibir o gráfico na tela
plt.show()

# Limpar figura atual
plt.clf()
plt.close()
```