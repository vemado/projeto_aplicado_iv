# PROJETO APLICADO 4

# Análise de Séries Temporais de Casos de Dengue nas Capitais do Sudeste (2010–2024)

## Visão Geral

Este repositório reúne todo o material da **Entrega 4** do **Projeto Aplicado IV – Ciência de Dados EaD (2025/01)**. O objetivo é analisar a evolução dos casos de dengue em quatro capitais do Sudeste brasileiro (Belo Horizonte, Vitória, Rio de Janeiro e São Paulo) entre 2010 e 2024, identificar padrões sazonais e avaliar modelos de previsão de séries temporais.

---

## Conteúdo

- `notebook_entrega4.ipynb`

  - Carregamento e pré-processamento dos dados
  - Análise Exploratória (EDA)
  - Ajuste de modelos: auto-ARIMA, ARIMA, SARIMAX e XGBoost
  - Cálculo de métricas (MAE, RMSE)
  - Gráficos de séries históricas e previsões
- `base/`

  - CSVs originais baixados via API InfoDengue para cada capital
- `requirements.txt`

  - Dependências Python necessárias
- `README.md`

  - Este arquivo de descrição do projeto

---

## Instalação

1. **Clone o repositório**

   ```bash
   git clone https://github.com/seu-usuario/seu-repositorio-dengue.git
   cd seu-repositorio-dengue
   ```
2. **Crie e ative um ambiente virtual**

   ```bash
   python3 -m venv venv
   source venv/bin/activate   # Linux/macOS
   venv\Scripts\activate    # Windows
   ```
3. **Instale as dependências**

   ```bash
   pip install -r requirements.txt
   ```

---

## Estrutura dos Dados

- **Fonte:** API InfoDengue (Fiocruz/UFRJ)
- **Formato:** arquivos CSV semanais por capital
- **Principais colunas:**
  - `data_iniSE` – Data de início da semana epidemiológica
  - `SE`, `ano` – Número da semana e ano
  - `casos`, `casos_est`, `casos_est_min`, `casos_est_max`
  - `p_inc100k` – Incidência por 100 mil habitantes
  - Climáticas: `tempmin`, `tempmed`, `tempmax`, `umidmin`, `umidmed`, `umidmax`

---

## Fluxo de Trabalho

1. **Pré-processamento**

   - Leitura e concatenação dos CSVs
   - Limpeza de colunas 100% nulas
   - Tratamento de valores faltantes (interpolação, médias móveis)
2. **Análise Exploratória (EDA)**

   - Estatísticas descritivas por cidade
   - Visualização de séries temporais e correlação com variáveis climáticas
3. **Modelagem**

   - **Auto-ARIMA** (pmdarima) para série de Belo Horizonte
   - **ARIMA** clássico (divisão treino/teste)
   - **SARIMAX** para cada capital (sazonalidade semanal)
   - **XGBoost** com features defasadas e validação temporal
4. **Avaliação**

   - Cálculo de **MAE** e **RMSE**
   - Gráficos comparativos (treino × real × previsão)

---

## Como Executar

1. Abra o notebook Jupyter:
   ```bash
   jupyter notebook notebook_entrega4.ipynb
   ```
2. Execute as células na ordem, certificando-se de que o diretório `data/` contenha os CSVs.
3. Visualize gráficos e revise métricas ao final de cada seção.

---

## Resultados Principais

- Forte **sazonalidade anual** em todas as capitais.
- **Subestimação** sistemática dos picos de surto pelos modelos ARIMA/SARIMAX (alto RMSE e MAE).
- **XGBoost** mostrou leve melhoria, mas ainda requer variáveis exógenas (chuva, mobilidade).

---

## Referências

- Box, G. E. P.; Jenkins, G. M.; Reinsel, G. C. *Time Series Analysis: Forecasting and Control* (2015).
- Tibshirani, R. et al. *Forecasting at Scale* (American Statistician, 2018).
- Gubler, D. *Dengue and Dengue Hemorrhagic Fever* (Clinical Microbiology Reviews, 2011).
- Coelho, F. C. et al. *Bayesian Modeling in InfoDengue Platform* (PLoS NTD, 2019).
