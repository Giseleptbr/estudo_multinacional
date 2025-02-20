# Projeto de Engenharia de Dados com Arquitetura Medallion

## Sobre o Projeto
Este projeto tem como objetivo implementar um **pipeline de engenharia de dados** utilizando a **Arquitetura Medallion** no **Databricks**, desde a ingestão dos dados até a construção da camada **Gold**, onde os dados estão preparados para análise.

A base de dados utilizada contém informações sobre **vendas, clientes, vendedores, produtos, categorias, cidades e países**. O processamento dos dados foi estruturado em três camadas distintas (**Bronze, Silver e Gold**), garantindo **qualidade, governança e eficiência** no armazenamento e consulta dos dados.

---

##  Arquitetura Medallion
A **Arquitetura Medallion** é uma abordagem utilizada para organizar os dados dentro de um **Data Lake** em três camadas principais:

### Camada Bronze (Raw Data)
- Contém os **dados brutos**, sem transformação, exatamente como foram extraídos das fontes originais.
- **Formato:** Delta Parquet
- **Objetivo:** Armazenamento de dados históricos para rastreabilidade e reprocessamento.

### Camada Silver (Curated Data)
- Dados processados e **padronizados**, com **correção de tipos, junção de tabelas e tratamento de inconsistências**.
- **Principais transformações aplicadas**:
  - Unificação do nome completo de clientes e vendedores.
  - Remoção da coluna **NumeroTransacao** da Tabela Fato Vendas.
  - Cálculo correto do **PrecoTotal**, aplicando **desconto sobre a quantidade vendida**.
  - Particionamento dos dados de vendas por **ANO e MÊS**.
- **Objetivo:** Criar um conjunto de dados confiável e otimizado para análises e integrações.

### Camada Gold (Analytics Ready Data)
- Dados prontos para **análises avançadas e relatórios**.
- **Principais melhorias aplicadas**:
  - **Aplicação de SK (Surrogate Keys)** para as tabelas dimensões.
  - **Implementação de Slowly Changing Dimension (SCD Type 2)** para capturar mudanças históricas nas dimensões.
  - **Carga incremental na Tabela Fato**, garantindo eficiência no processamento.
  - **Particionamento dos dados** por **ANO e MÊS** para otimizar consultas.
- **Objetivo:** Disponibilizar dados estruturados e performáticos para Business Intelligence e Data Science.

---

## Consultas e Análises
Após a construção das camadas, foram desenvolvidas diversas análises, incluindo:

✅ **Total de vendas por categoria e país**  
✅ **Variação mensal de vendas (MoM)**  
✅ **Top 10 produtos mais vendidos**  
✅ **Distribuição de vendas e participação por categoria**  
✅ **Cálculo correto de descontos e ticket médio por categoria**  

Essas análises foram realizadas com **PySpark** e otimizadas para execução no **Databricks**.

---

## Tecnologias Utilizadas
- **Databricks** para processamento e armazenamento dos dados.  
- **Delta Lake** para versionamento e controle de schema.  
- **PySpark** para transformação e manipulação de dados.  

