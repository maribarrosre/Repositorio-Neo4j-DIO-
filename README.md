# Repositorio-Neo4j-DIO-
Projeto desenvolvido durante o curso da Digital Innovation One (DIO) explorando a criação, consulta e manipulação de bancos de dados orientados a grafos utilizando o Neo4j e a linguagem Cypher.
# 📊 Desafio Neo4j DIO: Modelagem e Consultas de Grafos com Cypher

Este repositório contém a solução do Desafio de Projeto prático proposto pela **Digital Innovation One (DIO)** em parceria com a **Neo4j**. O objetivo principal é demonstrar a aplicação de bancos de dados orientados a grafos para solucionar problemas de relacionamentos complexos e consultas otimizadas utilizando a linguagem **Cypher**.

---

## 🎯 Contexto do Problema

Em sistemas relacionais tradicionais (SQL), mapear conexões de múltiplas origens ou em várias camadas (ex: conexões de 2º ou 3º grau em redes sociais, cadeias de suprimentos ou sistemas de recomendação) exige junções (*JOINs*) custosas que degradam a performance do banco de dados à medida que o volume cresce.

A escolha do **Neo4j** (banco de dados em grafos) justifica-se pela sua capacidade de tratar relacionamentos como cidadãos de primeira classe. Isso permite navegação direta entre nós (*pointer hopping*) com performance constante, independente da profundidade da consulta.

---

## 📐 Modelo do Grafo

A estrutura do grafo foi projetada com foco em alta performance e clareza analítica:

- **Labels (Rótulos):** Categorizam as entidades principais do domínio (ex: `:Pessoa`, `:Empresa`, `:Produto`).
- **Relacionamentos:** Conectam os nós de forma direcionada e tipada (ex: `(:Pessoa)-[:CONECTADO_COM]->(:Pessoa)` ou `(:Pessoa)-[:COMPROU]->(:Produto)`).
- **Propriedades:** Atributos chave-valor armazenados nos nós e relacionamentos para permitir filtragem (`WHERE`) e agregação rápida.

![Modelo do Grafo](images/modelo_grafo.png)

---

## 🛠️ Boas Práticas e Conceitos Aplicados

Durante o desenvolvimento do projeto, foram seguidas as melhores práticas recomendadas pela Neo4j:

1. **Uso de Labels no `CREATE`:** Todos os nós são criados com labels claros para facilitar a indexação automática e otimizar as cláusulas `MATCH`.
2. **Prevenção de Duplicidades (`MERGE`):** Em cargas de dados repetíveis, utiliza-se a cláusula `MERGE` acompanhada de *constraints* de unicidade, evitando nós/relacionamentos duplicados.
3. **Manipulação Segura de Dados:**
   - **`SET`**: Adição e atualização de propriedades existentes.
   - **`REMOVE`**: Remoção pontual de labels ou propriedades sem afetar a estrutura básica do nó.
   - **`DELETE` vs `DETACH DELETE`**: Exclusão segura de relacionamentos e uso consciente do `DETACH DELETE` para evitar perda acidental de dados em massa.

---

## 📁 Estrutura do Repositório

```text
.
├── data/
│   └── dataset_amostra.csv         # Amostra dos dados brutos para carga
├── images/
│   ├── modelo_grafo.png            # Visualização da estrutura/esquema
│   └── resultado_query_01.png      # Evidência visual do Neo4j Browser/Bloom
├── scripts/
│   ├── 01_constraints.cypher       # Definição de restrições de unicidade e índices
│   ├── 02_load_data.cypher         # Scripts de criação e carga de dados (Cypher / LOAD CSV)
│   └── 03_queries_negocio.cypher   # Consultas analíticas e perguntas de negócio
└── README.md                       # Documentação principal do projeto
