# 🔥 Calorie Burn Efficiency — EDA

> Semana 1 do curso de Análise de Dados · UFSCar  
> Carregamento, inspeção, filtros, tratamento de nulos e feature engineering com pandas

---

## 📋 Sobre o Projeto

Notebook com exploração completa de um dataset sintético de eficiência calórica, cobrindo todo o fluxo básico de análise de dados: desde o carregamento do CSV até a criação de novas variáveis e visualizações exploratórias.

O dataset simula métricas de saúde e atividade física de **1.000.000 indivíduos**, onde a eficiência calórica não é tratada como um valor fixo, mas como resultado da combinação de múltiplos hábitos — sono, hidratação, composição corporal e consistência de treino.

---

## 🗂️ Estrutura do Repositório

```
.
├── calorie_efficiency_analysis.ipynb   ← notebook principal
├── calorie_efficiency_dataset.csv      ← dataset original (input)
├── calorie_efficiency_tratado.csv      ← dataset com features novas (gerado ao rodar)
└── README.md
```

---

## ⚙️ Como Executar

### Opção A — Google Colab (recomendado)

1. Acesse [colab.research.google.com](https://colab.research.google.com)
2. Faça upload do notebook `calorie_efficiency_analysis.ipynb`
3. Faça upload do CSV `calorie_efficiency_dataset.csv` pelo painel lateral de arquivos
4. Execute todas as células: `Runtime → Run all`

> O notebook detecta automaticamente se o CSV está no mesmo diretório ou tenta o upload via Colab.

### Opção B — Ambiente local

```bash
# 1. Clone o repositório
git clone https://github.com/SEU_USUARIO/NOME_DO_REPO.git
cd NOME_DO_REPO

# 2. Crie e ative um ambiente virtual
python -m venv .venv
source .venv/bin/activate        # Linux/Mac
.venv\Scripts\activate           # Windows

# 3. Instale as dependências
pip install -r requirements.txt

# 4. Abra o notebook
jupyter notebook calorie_efficiency_analysis.ipynb
```

---

## 📊 Dataset

| Propriedade | Valor |
|---|---|
| Arquivo | `calorie_efficiency_dataset.csv` |
| Linhas | 1.000.000 |
| Colunas originais | 15 |
| Colunas após feature engineering | 24 |
| Memória (bruto) | ~80 MB |
| Nulos originais | Nenhum |

### Colunas originais

| Coluna | Tipo | Descrição |
|---|---|---|
| `age` | int | Idade |
| `steps_per_day` | int | Passos por dia |
| `active_minutes` | int | Minutos ativos por dia |
| `calories_burned` | int | Calorias queimadas |
| `sleep_hours` | float | Horas de sono |
| `hydration_liters` | float | Hidratação diária (L) |
| `bmi` | float | Índice de Massa Corporal |
| `workouts_per_week` | int | Treinos por semana |
| `muscle_mass_ratio` | float | Proporção de massa muscular |
| `body_fat_percentage` | float | Percentual de gordura corporal |
| `heart_rate_resting` | float | FC de repouso (bpm) |
| `heart_rate_avg` | float | FC média (bpm) |
| `continuous_exercise_days` | int | Dias consecutivos de exercício |
| `efficiency_score` | float | Score numérico de eficiência (0–10) |
| `calorie_efficiency` | str | **Coluna alvo**: `Low Efficiency`, `Moderate`, `High Efficiency` |

---

## 🔬 O que o Notebook Faz

### Seção 0 — Configuração
Importações, tema visual e definição das constantes de cores e da coluna alvo.

### Seção 1 — Carregamento
Leitura do CSV com detecção automática de caminho (local ou Colab), exibindo linhas, colunas e uso de memória.

### Seção 2 — Inspeção Inicial
`head()`, `info()`, `describe()` e distribuição da coluna alvo `calorie_efficiency`.

### Seção 3 — Seleção de Colunas
Seleção de coluna única (Series), múltiplas colunas e separação automática entre numéricas e categóricas com `select_dtypes()`.

### Seção 4 — Filtros
| Técnica | Exemplo |
|---|---|
| Igualdade | `df[df[col] == 'High Efficiency']` |
| Composto com `&` | `workouts > 6 & sleep < 6` |
| `isin()` | Excluir Low Efficiency |
| `query()` | Sintaxe SQL-like |
| `between()` | Score entre 4 e 7 |

### Seção 5 — Tratamento de Nulos
O dataset original não possui nulos. Para fins didáticos, nulos são injetados em 3 colunas (~2–3%) simulando falhas de sensor, e então tratados com:
- `sleep_hours` → **mediana** (robusta a outliers)
- `hydration_liters` → **média global**
- `heart_rate_avg` → **média por grupo** (`calorie_efficiency`)

### Seção 6 — Feature Engineering
9 novas colunas derivadas:

| Coluna | Descrição |
|---|---|
| `raw_efficiency` | Eficiência bruta: `calories / (steps + 20 × active_minutes)` |
| `cal_per_step` | Calorias por passo |
| `sono_insuficiente` | Flag: `sleep_hours < 6` |
| `overtraining` | Flag: `workouts_per_week > 6` |
| `perfil_risco` | Flag combinada: overtraining + sono insuficiente |
| `faixa_etaria` | Categorias: 18–25, 26–35, 36–50, 51–65, 65+ |
| `faixa_bmi` | Classificação WHO: Abaixo do peso / Normal / Sobrepeso / Obesidade |
| `consistency_score` | `exercise_days × (sleep_hours / 8)` |
| `zona_fc_avg` | Repouso / Leve / Moderada / Intensa / Máxima |

### Seção 7 — Visualizações

| Gráfico | O que mostra |
|---|---|
| Histograma + pizza | Distribuição do efficiency score e proporção de classes |
| Boxplots (2×2) | Sono, passos, hidratação e dias de exercício por classe |
| Heatmap de correlação | Relação entre variáveis numéricas (amostra 100k) |
| Barras | Score médio de eficiência por faixa etária |
| Scatter | Mapa de risco: overtraining vs sono (amostra 15k) |

### Seção 8 — Exportação
Salva o DataFrame tratado com todas as novas colunas em `calorie_efficiency_tratado.csv`.

---

## 📈 Distribuição da Coluna Alvo

| Classe | Registros | % |
|---|---|---|
| Low Efficiency | ~938.000 | 93,8% |
| Moderate | ~34.900 | 3,5% |
| High Efficiency | ~26.900 | 2,7% |

> Dataset desbalanceado por design — reflete a dificuldade de atingir alta eficiência calórica na prática.

---

## 📚 Referências

- [Kaggle — Calorie Burn Efficiency Dataset](https://www.kaggle.com)
- [Documentação pandas](https://pandas.pydata.org/docs/)
- [Seaborn — Statistical Data Visualization](https://seaborn.pydata.org)
