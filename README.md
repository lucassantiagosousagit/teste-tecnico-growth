# Teste Técnico – Análise de Dados: Vendas e Marketing

## 📖 INTRODUÇÃO

Este repositório reúne todas as etapas do teste técnico de **Analista de Dados** aplicado ao cenário de vendas e marketing. Tem como objetivo demonstrar:

- Conexão e extração de dados de um banco SQLite  
- Consultas em SQL e manipulação em Python (pandas)  
- Análises de vendas, marketing e integração entre as duas áreas  
- Visualização com Matplotlib  
- Geração de métricas adicionais (Repeat Purchase Rate, Novos Clientes)  
- Análise exploratória automática com Sweetviz  


## 1. Conexão e Carregamento de Dados
- Conectado ao SQLite
- Carregano as tabelas em DataFrames para facilitar a manipulação dos dados
- Criado os dataframes (`clientes`,`campanhas`,`interacoes`,`produtos` e `vendas`)

## 🔍 DESCRIÇÃO DAS ANÁLISES

## 2. Análise de Vendas

### A.1 - Total de Vendas por Canal (Último Trimestre)
#### OBJETIVO: comparar Outbound vs Inbound no trimestre anterior ao último registro.

#### COMO:

- Filtrado vendas entre as datas de início e fim do trimestre.

- Agrupado por `canal_aquisicao` e somado `valor_total`.

- Plotado em barras laranja, rótulos K/M e data labels em branco sobre fundo preto.

### A.2 - Top 5 Produtos por Volume e Margem Média
#### OBJETIVO: identificar os 5 produtos com maior quantidade vendida e sua margem média.

#### COMO:

- Calculado margem unitária e através da fórmula `margin = (preço_venda_unit - custo_unitario)/(preco_venda_unit` 

- Agrupado por `id_produto`, somado `quantidade` e calculado `mean(margin)`.

- Agrupado por `canal_aquisicao` e somado `valor_total`.

- Selecionado os 5 maiores volumes e plotado em barras laranja.

### A.3 - Ticket Médio por Segmento (B2B vs B2C)

#### OBJETIVO: comparar o valor médio de compra entre clientes B2B e B2C.

#### COMO:

- Merge com clientes`id_cliente`,`segmento`
- Groupby `segmento`, média de `valor_total`.
- Gráfico de barras laranja, labels em branco/negrito.

### A.4 - Sazonalidade de Vendas Mensais

#### OBJETIVO: entender picos e quedas ao longo do ano.

#### COMO:

- Conversão de `data_venda` em período mensal e agrupando soma.
- Mapeamos mês → abreviação em Português (Jan, Fev, …).
- Plot de linha laranja com marcadores pretos e data labels K/M.

## 3. Análise de Marketing
### B.1 - Eficiências das Campanhas

#### OBJETIVO: relacionar taxa de conversão e custo por conversão.

#### COMO:

- Calculado o  `total_interacoes` e conversoes por `id_campanha`.
- Taxa de conversão = `conversoes/total_interacoes`.
- Custo por conversão = `custo/conversoes`.
- Selecionamos Top-5 menores CPA e plotamos barras horizontais laranja, com rótulos lado a lado (R$ e %)

### B.2 - Engajamento por Canal de Marketing

#### OBJETIVO: identificar quais canais geram mais interações.

#### COMO:

- Merge de interacoes com campanhas`id_campanha`,`canal_marketing`.
- Groupby `canal_marketing`, conta de interações.
- Gráfico de barras laranja, X labels horizontais e data labels em branco.

## 4. Análise Integrada ( Vendas x Marketing)
### C.1 - Produto Mais Vendido por Campanha

#### OBJETIVO: para cada campanha, achar o produto com maior receita.

#### COMO:

- Para cada linha em `Campanhas_Marketing`, filtrar Vendas entre `data_inicio` e `data_fim`.
- Merge com Produtos`id_produto`,`nome_produto`, agrupar soma de `valor_total`.
- Selecionar maior e depois ordenar decrescentemente e pegar Top 5.
- Plotar barras horizontais laranja com rótulo R$… – nome do produto.

### C.2 - Cidades com Maior Venda por Campanha

#### OBJETIVO: para cada campanha, identificar a cidade que mais vendeu.

#### COMO:

- Filtrar Vendas no período de cada campanha e merge com Clientes`id_cliente`,`cidade`.
- Agrupar soma de `valor_total` por cidade, selecionar maior.
- Ordenar decrescentemente, pegar Top 5 e plotar barras horizontais laranja com rótulo R$… – cidade.

## . 🚀 MÉTRICAS ADICIONAIS

### 1. Repeat Purchase Rate (RPR)

#### OBJETIVO:  Calcular % de clientes que compraram mais de uma vez.

#### COMO:

- Calcular a quantiade pela fórmula counts = vendas`id_cliente`.value_counts()

- repeaters = (counts > 1).sum(), total = counts.size

- RPR = repeaters / total * 100.

### 2. Novos Clientes por Mês

#### OBJETIVO: Calcular a contagem de clientes cuja primeira compra ocorreu em cada mês.

#### COMO:

- Calcular a primeira compra first_purchase = vendas.groupby`id_cliente`,`data_venda`.min()

- Extrair year_month e mapear mês para abreviação.

- Agrupar e contar por mês.

- Plotar barras laranja com rótulos numéricos.

### 3. Análise Exploratória com Sweetviz

#### OBJETIVO: Entregar um relatório em HTML de fácil acesso para informar as métricas dos dados , bem como suas relações com o valor total das vendas.

#### Como:

- Combinando as tabelas usando o merge entre as tabelas.
- Utilizar as colunas das tabelas para verificar a relação das colunas com o valor total, para identificar métricas automáticas.
- Gerar o relatório em HTML com as visualizações.

## 📊 RELATÓRIOS GERADOS

### 1. Foi disponibilizado os arquivos `Relatório Growth.pptx` e `Relatório Growth.pdf` com os principais valores e gráficos com as métricas e insights.
### 2. Foi disponibilizado o arquivo `Teste Técnico Growth.ipynb` com todo o script para geração dos gráficos.
### 2. Foi disponibilizado o arquivo `eda_geral_vendas.html`
