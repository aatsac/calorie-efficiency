# Calorie Efficiency Analysis

Análise exploratória e tratamento de dados com **Python + Jupyter Notebook**, focada em investigar padrões de **eficiência calórica** e gerar um dataset limpo a partir do original.

Projeto desenvolvido em um **grupo de estudos**, com foco em praticar um workflow de dados reproduzível.

---

## 📌 Objetivo

* carregar o dataset bruto
* inspecionar e limpar os dados
* aplicar padronizações e transformações
* gerar um dataset tratado
* explorar padrões e métricas relevantes

---

## 🧰 Tecnologias

* Python 3
* Jupyter Notebook
* Pandas
* NumPy
* Matplotlib
* `venv`

---

## 📁 Estrutura

```text
calorie_efficiency/
├── calorie_efficiency_analysis.ipynb
├── calorie_efficiency_dataset.csv
├── requirements.txt
├── README.md
└── .gitignore
```

---

## ▶️ Como executar

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Abra o notebook no VS Code e selecione o kernel:

```text
.venv/bin/python
```

---

## 📓 Fluxo do notebook

1. carregamento do dataset
2. inspeção inicial
3. limpeza e tratamento
4. transformações
5. exportação do dataset tratado
6. análise exploratória

---

## 📦 Dataset tratado

O arquivo de saída `calorie_efficiency_tratado.csv` é gerado automaticamente ao final do notebook.

> ⚠️ O CSV tratado **não foi versionado no repositório** porque ultrapassa o limite de tamanho permitido pelo GitHub (100 MB).

Para reproduzir o resultado, basta executar o notebook até a etapa de exportação.

Saída esperada:

```text
calorie_efficiency_tratado.csv
```

---

## 🚀 Próximos passos

* adicionar visualizações mais avançadas
* comparar grupos e categorias
* transformar em pipeline modular Python
* criar dashboard interativo

---

## 👤 Autor

**Adriano Tavares**

Projeto desenvolvido como parte da primeira semana do grupo de estudos de Engenharia de Dados, com foco em **prática de Python, análise de dados e Jupyter**.
