# 📊 Telecom X - Parte 2: Prevendo Cancelamento de Clientes

## 🎯 Missão
Antecipar a evasão de clientes da Telecom X por meio de modelos de machine learning. O objetivo é identificar quais clientes possuem maior probabilidade de cancelar os serviços, permitindo ações preventivas e estratégicas por parte da empresa.

---

## 🛠️ Etapas Realizadas

### 1. 📥 Extração de Dados
- Importação do dataset tratado diretamente da API da Telecom X (formato CSV).
- Leitura e visualização inicial da base de dados.

---

### 2. 🧹 Pré-Processamento

#### 🔎 Remoção de Colunas Irrelevantes
- Exclusão de colunas com IDs e atributos altamente correlacionados que não agregam valor ao modelo.

#### 🧠 Análise de Correlação
- Detecção de pares de colunas com correlação ≥ 0.95.
- Remoção de colunas redundantes para evitar multicolinearidade.

#### 🔁 Encoding de Variáveis Categóricas
- Substituição de valores binários (`Yes/No`, `Male/Female`) por `0/1`.
- One-Hot Encoding aplicado em colunas categóricas multiclasse.

#### ⚖️ Balanceamento de Classes
- Identificação de desequilíbrio na variável alvo `Cancelamento`.
- Aplicação de três técnicas de balanceamento:
  - **Oversampling**
  - **Undersampling**
  - **SMOTE** (selecionado como o método final por preservar dados e gerar exemplos sintéticos de qualidade)

#### 📏 Normalização dos Dados
- Aplicação do `StandardScaler` nas variáveis contínuas (`Meses_de_Contrato`, `Valor_Mensal`).
- Padronização feita **após** o balanceamento e separação treino/teste para evitar vazamento de dados.

---

### 3. 🔍 Análise de Correlação e Visualização
- Cálculo da matriz de correlação entre variáveis numéricas e o alvo.
- Criação de gráficos como:
  - **Boxplot**: Tempo de contrato x evasão
  - **Stripplot**: Valor mensal x evasão

🔎 **Insights identificados:**
- Clientes com contratos mais curtos tendem a evadir.
- Pagamentos mensais mais altos correlacionam-se com maior taxa de evasão.

---

## 🧪 Modelagem Preditiva

### Modelos Treinados:
| Modelo                | Normalização Necessária |
|----------------------|--------------------------|
| Regressão Logística  | ✅ Sim                   |
| Random Forest        | ❌ Não                   |
| KNN                  | ✅ Sim                   |
| Árvore de Decisão    | ❌ Não                   |

### 📈 Avaliação dos Modelos

| Modelo                | Acurácia | Precisão | Recall | F1-Score |
|----------------------|----------|----------|--------|----------|
| **Regressão Logística**  | **0.74**   | 0.51     | **0.78** | **0.62**   |
| Random Forest        | 0.79     | **0.64** | 0.47   | 0.54     |
| KNN                  | 0.76     | 0.55     | 0.49   | 0.52     |
| Árvore de Decisão    | 0.73     | 0.49     | 0.51   | 0.50     |

### 🥇 Modelo Selecionado: **Regressão Logística**
- Melhor F1-Score e equilíbrio entre **precisão e recall**.
- Simples, interpretável e eficaz.
- Ideal para ações estratégicas de retenção de clientes.

---

## 🔍 Interpretação dos Resultados

### 💡 Variáveis com Maior Influência (Regressão Logística):
- **Meses_de_Contrato** (quanto menor, maior a chance de evasão)
- **Valor_Mensal** (valores altos estão associados à evasão)
- **Tipo_Contrato** (planos mensais apresentam mais evasão)
- **Serviços extras (Streaming/Backup/Suporte)**: ausência desses serviços aparece com maior taxa de cancelamento.

---

## ✅ Conclusão Estratégica

A **Regressão Logística** se destacou como o modelo mais robusto para prever evasão de clientes da Telecom X. A análise revelou que contratos curtos e valores mensais elevados são fortes indicadores de possível cancelamento. Com esses insights, a empresa pode:

- Oferecer incentivos para alongamento do contrato.
- Avaliar políticas de preços para clientes com maior risco de evasão.
- Investir em pacotes com serviços adicionais para aumentar o engajamento.

---

## 🧠 Tecnologias e Bibliotecas Utilizadas

- **Python**
- **Pandas / NumPy**
- **Matplotlib / Seaborn**
- **Scikit-learn**
- **Imbalanced-learn (SMOTE, RandomOverSampler, etc.)**

---

## 📁 Organização dos Dados

- `dados_tratados.csv`: Base original com pré-processamento inicial.
- `X_train_scaled`, `X_test_scaled`: Bases normalizadas para modelos sensíveis à escala.
- `y_train`, `y_test`: Variável alvo (Cancelamento) separada para treino e teste.

---

## 🔗 Próximos Passos

- Tunar hiperparâmetros com `GridSearchCV` ou `RandomizedSearchCV`.
- Implementar **XGBoost** ou **LightGBM** como modelos avançados.
- Criar dashboards interativos com os insights usando **Power BI** ou **Streamlit**.

---

> Desenvolvido com foco em **comunicação estratégica**, **inteligência de dados** e **decisão orientada por evidência**.
