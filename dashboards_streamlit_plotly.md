# 📊 Guia Completo de Criação de Dashboards Interativos com Python: Plotly & Streamlit

Este documento é um guia consolidado de referência e prática para a construção de painéis analíticos executivos, cobrindo desde a visualização interativa de dados até a arquitetura e publicação de aplicações web em Python.

---

## 📋 Sumário
1. [Arquitetura: Como o Plotly e o Streamlit Trabalham Juntos](#1-arquitetura-como-o-plotly-e-o-streamlit-trabalham-juntos)
2. [Guia de Referência do Plotly Express](#2-guia-de-referência-do-plotly-express)
3. [Parâmetros Obrigatórios e Opcionais do Plotly](#3-parâmetros-obrigatórios-e-opcionais-do-plotly)
4. [Cheat Sheet e Componentes do Streamlit](#4-cheat-sheet-e-componentes-do-streamlit)
5. [Arquitetura e Fluxo de Código no Streamlit](#5-arquitetura-e-fluxo-de-código-no-streamlit)
6. [Passo a Passo Prático: Construindo um Dashboard Completo](#6-passo-a-passo-prático-construindo-um-dashboard-completo)

---

## 1. Arquitetura: Como o Plotly e o Streamlit Trabalham Juntos

O **Plotly** e o **Streamlit** não se substituem; eles desempenham papéis complementares na construção de um dashboard:

* **Plotly (Engine de Data Viz):** Constrói os gráficos interativos (`px.bar`, `px.line`, `px.scatter`), gerando objetos em JavaScript (`Plotly.js`) que permitem ao usuário dar zoom, passar o mouse (*tooltips*), isolar legendas e exportar imagens.
* **Streamlit (Web Framework):** Constrói a **interface do dashboard**. Gerencia o layout em colunas, menus laterais (`st.sidebar`), filtros interativos (`st.multiselect`, `st.date_input`), cartões de KPIs (`st.metric`) e executa o código reativo.

### O Fluxo de Integração:

```

[ Dados Brutos / DB ]
↓
[ Filtros no Streamlit (`st.sidebar`) ] → [ DataFrame Filtrado ]
↓
[ Criação do Gráfico no Plotly (`fig = px.bar(...)`) ]
↓
[ Exibição na Tela do Streamlit (`st.plotly_chart(fig)`) ]

```

---

## 2. Guia de Referência do Plotly Express

| Tipo de Gráfico | Componente / Traço | Eixo(s) | Módulo | Função | Principais Parâmetros | Exemplo de Uso |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Linhas / Tendência** | Traço de Linhas e Marcadores | $X$ (Temporal/Contínuo), $Y$ (Contínuo) | `plotly.express` | `px.line()` | `df`, `x`, `y`, `color`, `markers`, `hover_data`, `title` | `px.line(df, x="data", y="vendas", color="loja", markers=True)` |
| **Barras / Comparação** | Retângulos Interativos | $X$ (Categórico), $Y$ (Numérico) | `plotly.express` | `px.bar()` | `df`, `x`, `y`, `color`, `barmode`, `text_auto`, `title` | `px.bar(df, x="categoria", y="valor", color="regiao", barmode="group")` |
| **Dispersão / Bolhas** | Marcadores Pontuais | $X$ (Contínuo), $Y$ (Contínuo) | `plotly.express` | `px.scatter()` | `df`, `x`, `y`, `color`, `size`, `symbol`, `trendline` | `px.scatter(df, x="renda", y="gasto", size="pop", trendline="ols")` |
| **Histograma / Densidade** | Barras de Distribuição | $X$ (Contínuo), $Y$ (Frequência) | `plotly.express` | `px.histogram()` | `df`, `x`, `color`, `nbins`, `histfunc`, `marginal` | `px.histogram(df, x="idade", nbins=20, marginal="box")` |
| **Boxplot / Outliers** | Caixas e Quartis | $X$ (Categórico), $Y$ (Contínuo) | `plotly.express` | `px.box()` | `df`, `x`, `y`, `color`, `points`, `notched` | `px.box(df, x="depto", y="salario", points="all")` |
| **Violin Plot** | Densidade e Boxplot | $X$ (Categórico), $Y$ (Contínuo) | `plotly.express` | `px.violin()` | `df`, `x`, `y`, `color`, `box`, `points` | `px.violin(df, x="classe", y="idade", box=True, points="all")` |
| **Heatmap / Matriz** | Matriz Térmica | $X$ e $Y$ (Matriz/Pivot) | `plotly.express` | `px.imshow()` | `img/df`, `text_auto`, `color_continuous_scale`, `labels` | `px.imshow(df.corr(), text_auto=".2f", color_continuous_scale="Viridis")` |
| **Pizza / Rosca** | Fatias de Proporção | Proporção / Categoria | `plotly.express` | `px.pie()` | `df`, `values`, `names`, `color`, `hole` | `px.pie(df, values="faturamento", names="canal", hole=0.4)` |
| **Treemap / Hierarquia** | Blocos Proporcionais | Hierárquico | `plotly.express` | `px.treemap()` | `df`, `path`, `values`, `color` | `px.treemap(df, path=["regiao", "estado"], values="vendas")` |
| **Customização Layout** | Tema, Título e Eixos | N/A | `graph_objects` | `fig.update_layout()` | `title`, `template`, `xaxis_title`, `legend_title` | `fig.update_layout(template="plotly_dark", title="Título")` |
| **Customização Traços** | Cor, Linhas e Marcadores | N/A | `graph_objects` | `fig.update_traces()` | `marker_size`, `line_width`, `textposition` | `fig.update_traces(marker_size=10, line_width=2)` |

---

## 3. Parâmetros Obrigatórios e Opcionais do Plotly

### A) Gráfico de Linhas — `px.line()`
* **Obrigatórios:** `data_frame`, `x` (eixo contínuo/temporal), `y` (variável numérica).
* **Opcionais:** `color` (subdivisão por cor), `symbol` (ícone do marcador), `markers` (exibe pontos em cada nó), `hover_data` (colunas extras no tooltip), `title`, `template`.

### B) Gráfico de Barras — `px.bar()`
* **Obrigatórios:** `data_frame`, `x` (categórico), `y` (numérico acumulado/médio).
* **Opcionais:** `color` (subgrupos), `barmode` (`"group"` lado a lado, `"stack"` empilhado), `text_auto` (rótulos de dados automáticos), `orientation` (`"v"` ou `"h"`), `color_discrete_sequence`.

### C) Gráfico de Dispersão — `px.scatter()`
* **Obrigatórios:** `data_frame`, `x` (numérico contínuo), `y` (numérico contínuo).
* **Opcionais:** `color` (cor por categoria/escala contínua), `size` (diâmetro do ponto/bolha), `symbol` (forma do marcador), `trendline` (`"ols"` para linha de regressão).

### D) Histograma — `px.histogram()`
* **Obrigatórios:** `data_frame`, `x` ou `y` (variável numérica contínua).
* **Opcionais:** `nbins` (número de faixas), `histfunc` (`"count"`, `"sum"`, `"avg"`), `marginal` (`"box"`, `"violin"` para gráfico superior), `barmode` (`"overlay"`, `"stack"`).

### E) Boxplot — `px.box()`
* **Obrigatórios:** `data_frame`, `y` (numérico).
* **Opcionais:** `x` (grupos categóricos), `color`, `points` (`"all"` exibe todos os pontos, `"outliers"` apenas pontos discrepantes), `notched` (mínimos e máximos com entalhe).

### F) Heatmap — `px.imshow()`
* **Obrigatórios:** `img` / `data_frame` (matriz 2D/pivot tabular).
* **Opcionais:** `text_auto` (exibe valores nas células, ex: `".2f"`), `color_continuous_scale` (`"Viridis"`, `"Coolwarm"`), `aspect` (`"auto"`, `"equal"`).

### G) Pizza / Rosca — `px.pie()`
* **Obrigatórios:** `data_frame`, `values` (numérico), `names` (categorias).
* **Opcionais:** `hole` (se `hole > 0`, ex `0.4`, transforma em gráfico de **Rosca**), `color_discrete_sequence`.

---

## 4. Cheat Sheet e Componentes do Streamlit

| Categoria | Método / Função | Função / Descrição | Exemplo de Uso |
| :--- | :--- | :--- | :--- |
| **Configuração** | `st.set_page_config()` | Configura título da aba, ícone e layout inicial da página | `st.set_page_config(page_title="App", layout="wide")` |
| **Texto / Títulos** | `st.title()` | Título principal de nível 1 | `st.title("Painel de Vendas")` |
| **Texto / Títulos** | `st.header()` / `st.subheader()` | Subtítulos de nível 2 e 3 | `st.subheader("Desempenho Regional")` |
| **Texto / Títulos** | `st.markdown()` | Texto formatado usando sintaxe Markdown | `st.markdown("**Atenção:** Dados atualizados")` |
| **Texto / Títulos** | `st.caption()` | Texto explicativo pequeno/cinza no rodapé | `st.caption("Fonte: API do IBGE")` |
| **Métricas** | `st.metric()` | Cartão para exibição de números de KPI com variação | `st.metric("Faturamento", "R$ 10k", delta="5%")` |
| **Entradas (Input)** | `st.button()` | Botão de clique (retorna `True` quando acionado) | `if st.button("Calcular"): st.write("Ok")` |
| **Entradas (Input)** | `st.selectbox()` | Menu suspenso para seleção de uma única opção | `st.selectbox("Mês:", ["Jan", "Fev", "Mar"])` |
| **Entradas (Input)** | `st.multiselect()` | Menu para escolha de múltiplas opções em lista | `st.multiselect("Regiões:", ["Norte", "Sul"])` |
| **Entradas (Input)** | `st.slider()` | Seletor deslizante de valores numéricos | `st.slider("Idade:", 0, 100, 25)` |
| **Entradas (Input)** | `st.date_input()` | Seletor interativo de data individual ou intervalo | `st.date_input("Período:", (dt_ini, dt_fim))` |
| **Exibição Dados** | `st.dataframe()` | Tabela interativa com ordenação e busca | `st.dataframe(df, use_container_width=True)` |
| **Gráficos** | `st.plotly_chart()` | Renderiza uma figura interativa da biblioteca Plotly | `st.plotly_chart(fig, use_container_width=True)` |
| **Layout** | `st.sidebar` | Acessa e insere elementos na barra lateral | `st.sidebar.title("Menu Lateral")` |
| **Layout** | `st.columns()` | Divide a tela em colunas paralelas | `col1, col2 = st.columns(2)` |
| **Layout** | `st.tabs()` | Divide o conteúdo da tela em abas navegáveis | `tab1, tab2 = st.tabs(["Aba 1", "Aba 2"])` |
| **Layout** | `st.divider()` | Desenha uma linha horizontal de separação | `st.divider()` |
| **Notificações** | `st.success()` / `st.warning()` | Caixas coloridas de mensagem | `st.warning("Selecione ao menos um filtro.")` |
| **Download** | `st.download_button()` | Botão para baixar arquivos (CSV, TXT, JSON) | `st.download_button("Baixar CSV", data=csv_bytes)` |

---

## 5. Arquitetura e Fluxo de Código no Streamlit

O Streamlit executa seu código de cima para baixo (*Top-to-Bottom*) a cada interação do usuário. A ordem correta das etapas garante que não ocorram erros de escopo ou gráficos desatualizados:


```

┌─────────────────────────────────────────────────────────┐
│ 1. Configuração da Página (`st.set_page_config`)         │
├─────────────────────────────────────────────────────────┤
│ 2. Extração, Limpeza e Caching de Dados (`@st.cache`)   │
├─────────────────────────────────────────────────────────┤
│ 3. Barra Lateral & Filtros Interativos (`st.sidebar`)   │
├─────────────────────────────────────────────────────────┤
│ 4. Filtragem do DataFrame (`df_filtrado`)               │
├─────────────────────────────────────────────────────────┤
│ 5. Cabeçalho Principal e Cartões de KPIs (`st.columns`)  │
├─────────────────────────────────────────────────────────┤
│ 6. Gráficos Interativos (`st.plotly_chart`) & Tabelas   │
└─────────────────────────────────────────────────────────┘

```

---

## 6. Passo a Passo Prático: Construindo um Dashboard Completo

Abaixo está o código em Python consolidado de uma aplicação real pronta para execução.

### Arquivo: `app.py`

```python
import streamlit as st
import pandas as pd
import plotly.express as px
import numpy as np

# =============================================================================
# ETAPA 1: CONFIGURAÇÃO DA PÁGINA (Deve ser o 1º comando Streamlit)
# =============================================================================
st.set_page_config(
    page_title="Dashboard Executivo de Vendas",
    page_icon="📊",
    layout="wide",
    initial_sidebar_state="expanded"
)

# =============================================================================
# ETAPA 2: EXTRAÇÃO, TRATAMENTO E CACHING DE DADOS
# =============================================================================
@st.cache_data(ttl=3600)
def carregar_dados():
    np.random.seed(42)
    datas = pd.date_range(start="2026-01-01", periods=100, freq="D")
    
    dados = []
    for d in datas:
        for _ in range(np.random.randint(5, 12)):
            dados.append({
                "data_venda": d,
                "regiao": np.random.choice(["Sudeste", "Sul", "Nordeste", "Norte"]),
                "categoria": np.random.choice(["Eletrônicos", "Roupas", "Alimentos"]),
                "valor_venda": np.round(np.random.exponential(150) + 20, 2),
                "lucro": np.round(np.random.uniform(10, 80), 2)
            })
            
    df = pd.DataFrame(dados)
    df["data_venda"] = pd.to_datetime(df["data_venda"])
    return df

df_raw = carregar_dados()

# =============================================================================
# ETAPA 3: FILTROS INTERATIVOS (SIDEBAR)
# =============================================================================
st.sidebar.header("🔍 Filtros de Análise")

# Filtro 1: Regiões
lista_regioes = sorted(df_raw["regiao"].unique().tolist())
regioes_selecionadas = st.sidebar.multiselect(
    "Selecione as Regiões:",
    options=lista_regioes,
    default=lista_regioes
)

# Filtro 2: Período de Datas
data_min = df_raw["data_venda"].min().date()
data_max = df_raw["data_venda"].max().date()

intervalo_datas = st.sidebar.date_input(
    "Período de Vendas:",
    value=(data_min, data_max),
    min_value=data_min,
    max_value=data_max
)

# =============================================================================
# ETAPA 4: FILTRAGEM DO DATASET
# =============================================================================
if len(intervalo_datas) == 2:
    data_ini, data_fim = intervalo_datas
    df_filtrado = df_raw[
        (df_raw["regiao"].isin(regioes_selecionadas)) &
        (df_raw["data_venda"].dt.date >= data_ini) &
        (df_raw["data_venda"].dt.date <= data_fim)
    ]
else:
    df_filtrado = df_raw[df_raw["regiao"].isin(regioes_selecionadas)]

# =============================================================================
# ETAPA 5: CABEÇALHO E CARTÕES DE KPIS
# =============================================================================
st.title("📊 Painel Executivo de Desempenho de Vendas")
st.caption("Acompanhamento operacional em tempo real.")
st.divider()

# Validação contra seleções sem dados
if df_filtrado.empty:
    st.warning("⚠️ Nenhum registro encontrado para os filtros selecionados.")
    st.stop()

# Cartões Métrica
col_kpi1, col_kpi2, col_kpi3, col_kpi4 = st.columns(4)

fat_total = df_filtrado["valor_venda"].sum()
lucro_total = df_filtrado["lucro"].sum()
ticket_med = df_filtrado["valor_venda"].mean()
total_pedidos = len(df_filtrado)

col_kpi1.metric("Faturamento Total", f"R$ {fat_total:,.2f}".replace(",", "X").replace(".", ",").replace("X", "."))
col_kpi2.metric("Lucro Líquido", f"R$ {lucro_total:,.2f}".replace(",", "X").replace(".", ",").replace("X", "."))
col_kpi3.metric("Ticket Médio", f"R$ {ticket_med:,.2f}".replace(",", "X").replace(".", ",").replace("X", "."))
col_kpi4.metric("Total de Pedidos", f"{total_pedidos:,}".replace(",", "."))

st.divider()

# =============================================================================
# ETAPA 6: GRÁFICOS INTERATIVOS (PLOTLY) & TABELA
# =============================================================================
col_graf1, col_graf2 = st.columns(2)

with col_graf1:
    st.subheader("📈 Tendência Temporal de Faturamento")
    df_tendencia = df_filtrado.groupby(df_filtrado["data_venda"].dt.date)["valor_venda"].sum().reset_index()
    
    fig_linha = px.line(
        df_tendencia,
        x="data_venda",
        y="valor_venda",
        labels={"data_venda": "Data", "valor_venda": "Faturamento (R$)"},
        template="plotly_white",
        markers=True
    )
    fig_linha.update_traces(line_color="#2b5c8f", line_width=2.5)
    st.plotly_chart(fig_linha, use_container_width=True)

with col_graf2:
    st.subheader("🏆 Comparativo por Região")
    df_regioes = df_filtrado.groupby("regiao")["valor_venda"].sum().reset_index().sort_values(by="valor_venda", ascending=False)
    
    fig_barra = px.bar(
        df_regioes,
        x="regiao",
        y="valor_venda",
        color="valor_venda",
        color_continuous_scale="Viridis",
        labels={"regiao": "Região", "valor_venda": "Faturamento (R$)"},
        template="plotly_white",
        text_auto=".2f"
    )
    st.plotly_chart(fig_barra, use_container_width=True)

# Tabela e Exportação
st.divider()
st.subheader("📄 Registros Detalhados")
st.dataframe(df_filtrado.sort_values(by="data_venda", ascending=False), use_container_width=True, hide_index=True)

st.download_button(
    label="📥 Baixar Relatório Filtrado (CSV)",
    data=df_filtrado.to_csv(index=False).encode("utf-8"),
    file_name="relatorio_vendas.csv",
    mime="text/csv"
)

```

---

### Executando no Terminal:

```bash
# 1. Instalar as bibliotecas
pip install streamlit plotly pandas numpy

# 2. Executar a aplicação
streamlit run app.py

```

