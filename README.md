# Solar Power Generation Forecasting and Monitoring
# Sistema de Previsão e Monitoramento de Geração de Energia Solar Fotovoltaica

[English](#english) | [Português](#português)

---

<a id="english"></a>

# English

A machine learning-based decision support system for forecasting photovoltaic power generation and identifying periods of low generation in solar power plants.

## Overview

Solar photovoltaic generation is highly dependent on weather conditions. This project explores how machine learning can support solar plant operation by estimating expected power output from environmental variables and identifying periods of generation below expectations.

The system combines two supervised learning tasks:

- **Regression:** estimates expected AC power output based on weather conditions.
- **Classification:** identifies periods of low generation to support operational planning and maintenance decisions.

An interactive prototype was also developed to present predictions and monitoring information through a dashboard.

## Objectives

- Analyze the relationship between environmental conditions and photovoltaic power generation.
- Develop and compare regression models to estimate expected AC power output.
- Develop and compare classification models to identify periods of low generation.
- Investigate feature importance and model performance.
- Build an interactive decision-support prototype for solar plant managers.

## Dataset

The project uses the public [Solar Power Generation Data dataset](https://www.kaggle.com/datasets/anikannal/solar-power-generation-data).

The dataset contains generation and weather sensor records from two photovoltaic power plants in India, collected over 34 days at 15-minute intervals.

Main features:

| Feature | Description |
|---|---|
| `IRRADIATION` | Solar irradiation |
| `MODULE_TEMPERATURE` | Solar module temperature |
| `AMBIENT_TEMPERATURE` | Ambient temperature |
| `AC_POWER` | AC power output (target variable) |
| `PLANT_ID` | Solar plant identifier |
| `HOUR` | Hour of the day |

## Methodology

### 1. Data Preprocessing

The preprocessing pipeline included:

- Datetime conversion and temporal feature extraction.
- Aggregation of inverter-level generation records.
- Merging generation and weather sensor datasets.
- Physical plausibility checks, including the removal of negative power readings.
- Feature selection and preparation for model training.

### 2. Preventing Data Leakage

One of the most important methodological decisions was excluding `DC_POWER` and conversion efficiency from the input features.

Although these variables are strongly correlated with AC power, they are measured by the inverter at the same time as the target variable. Using them would make predictions artificially easy and prevent the model from being used for genuine future forecasting.

The final models rely on environmental variables and plant identification, making the approach suitable for both forecasting and monitoring scenarios.

### 3. Regression Models

The regression task estimates expected AC power output.

Models evaluated:

- Linear Regression
- Random Forest Regressor
- Multi-Layer Perceptron (MLP) Regressor

Evaluation metrics:

- RMSE (Root Mean Squared Error)
- MAE (Mean Absolute Error)
- R² (Coefficient of Determination)

### 4. Classification Models

The classification task identifies periods of low generation during daylight hours.

The target variable, `LOW_GENERATION`, is defined using the 40th percentile of daytime AC power for each plant separately.

Models evaluated:

- Logistic Regression
- Random Forest Classifier
- MLP Classifier

Evaluation metrics:

- Accuracy
- AUC-ROC
- Confusion Matrix
- Precision and Recall

## Results

### Regression Performance

| Model | RMSE (kW) | MAE (kW) | R² |
|---|---:|---:|---:|
| Linear Regression | 3337.25 | 2434.03 | 0.709 |
| Random Forest | **2410.32** | **1332.18** | **0.848** |
| MLP Neural Network | 2412.51 | 1361.62 | 0.848 |

Random Forest achieved the lowest prediction errors, with an R² of 0.848.

### Classification Performance

| Model | Accuracy | AUC-ROC |
|---|---:|---:|
| Logistic Regression | 0.855 | 0.930 |
| Random Forest | **0.928** | **0.975** |
| MLP Neural Network | 0.900 | 0.954 |

Random Forest also achieved the best classification performance, with 92.8% accuracy and an AUC-ROC of 0.975.

### Feature Importance

Solar irradiation was the most influential feature in both tasks.

For regression, its feature importance was 0.794, followed by `PLANT_ID` at 0.122.

For classification, irradiation had an importance of 0.535, followed by module temperature at 0.248.

These results reinforce the importance of environmental conditions in explaining photovoltaic power generation.

## Interactive Decision-Support Prototype

An interactive dashboard was developed using `ipywidgets`.

The prototype supports two operating modes:

**Planning Mode**
- Select a solar plant.
- Adjust environmental conditions.
- Estimate expected AC power output.
- Predict the probability of low generation.

**Monitoring Mode**
- Compare expected and actual power generation.
- Calculate the deviation between predicted and measured values.
- Display an operational recommendation when the deviation exceeds the defined threshold.

## Technologies and Concepts

- Python
- Scikit-learn
- Pandas
- NumPy
- Matplotlib
- Seaborn
- IPython / ipywidgets
- Supervised Machine Learning
- Regression and Classification
- Random Forest
- Neural Networks (MLP)
- Data Preprocessing
- Feature Importance
- Model Evaluation
- Data Leakage Prevention

## Limitations and Future Improvements

The study has some limitations:

- The dataset covers only 34 days, limiting seasonal generalization.
- The low-generation threshold is statistically defined and may not represent each plant's operational requirements.
- Module temperature is not always available in advance, which limits strictly future-oriented forecasting.
- The model may require recalibration when applied to new solar plants.

Potential improvements include:

- Temporal validation using chronological train/test splits.
- Hyperparameter optimization.
- Prediction intervals and uncertainty estimation.
- Integration with weather forecast APIs.
- Evaluation across additional solar plants.

## Authors

**João Pedro Pereira Frutuoso**  
**Thallisson Douglas de Freitas Nunes**

Department of Exact and Natural Sciences  
Federal Rural University of the Semi-Arid Region (UFERSA)  
Mossoró, Rio Grande do Norte, Brazil.

## References

- Anikannal, V. (2020). [Solar Power Generation Data — Kaggle](https://www.kaggle.com/datasets/anikannal/solar-power-generation-data).
- Breiman, L. (2001). Random Forests. *Machine Learning*, 45, 5–32.
- Goodfellow, I., Bengio, Y., & Courville, A. (2016). *Deep Learning*. MIT Press.
- Pedregosa, F. et al. (2011). Scikit-learn: Machine Learning in Python. *Journal of Machine Learning Research*, 12, 2825–2830.

---

<a id="português"></a>

# Português

Sistema de apoio à decisão baseado em Aprendizado de Máquina para estimar a geração de energia solar fotovoltaica e identificar períodos de baixa geração em usinas solares.

## Visão Geral

A geração de energia solar fotovoltaica depende diretamente das condições climáticas. Este projeto investiga como técnicas de Aprendizado de Máquina podem auxiliar na operação de usinas solares, estimando a potência esperada a partir de variáveis ambientais e identificando períodos de geração abaixo do esperado.

O sistema combina duas tarefas de aprendizado supervisionado:

- **Regressão:** estima a potência esperada em corrente alternada (AC) com base nas condições climáticas.
- **Classificação:** identifica períodos de baixa geração para auxiliar no planejamento operacional e nas decisões relacionadas à manutenção.

Também foi desenvolvido um protótipo de interface interativa para apresentar previsões e informações de monitoramento.

## Objetivos

- Analisar a relação entre as condições ambientais e a geração de energia fotovoltaica.
- Desenvolver e comparar modelos de regressão para estimar a potência AC esperada.
- Desenvolver e comparar modelos de classificação para identificar períodos de baixa geração.
- Investigar a importância das variáveis e o desempenho dos modelos.
- Construir um protótipo interativo de apoio à decisão para gestores de usinas solares.

## Conjunto de Dados

O projeto utiliza o conjunto de dados público [Solar Power Generation Data](https://www.kaggle.com/datasets/anikannal/solar-power-generation-data).

O dataset contém registros de geração de energia e sensores climáticos de duas usinas solares fotovoltaicas na Índia, coletados durante 34 dias, em intervalos de 15 minutos.

Principais variáveis:

| Variável | Descrição |
|---|---|
| `IRRADIATION` | Irradiação solar |
| `MODULE_TEMPERATURE` | Temperatura do módulo fotovoltaico |
| `AMBIENT_TEMPERATURE` | Temperatura ambiente |
| `AC_POWER` | Potência gerada em corrente alternada (variável-alvo) |
| `PLANT_ID` | Identificador da usina |
| `HOUR` | Hora do dia |

## Metodologia

### 1. Pré-processamento dos Dados

O pré-processamento incluiu:

- Conversão dos timestamps para o formato datetime e extração de atributos temporais.
- Agregação dos registros de geração por inversor.
- Integração das tabelas de geração e dos sensores climáticos.
- Verificação de plausibilidade física, incluindo a remoção de leituras de potência negativas.
- Seleção e preparação das variáveis para o treinamento dos modelos.

### 2. Prevenção de Vazamento de Dados (Data Leakage)

Uma das principais decisões metodológicas foi excluir `DC_POWER` e a eficiência de conversão das variáveis de entrada.

Embora essas variáveis tenham forte correlação com a potência AC, elas são medidas pelo inversor no mesmo instante da variável-alvo. Sua utilização tornaria a previsão artificialmente simples e impediria o uso do modelo em cenários reais de previsão futura.

Por isso, os modelos finais utilizam variáveis ambientais e a identificação da usina, permitindo sua aplicação tanto na previsão quanto no monitoramento da geração.

### 3. Modelos de Regressão

A tarefa de regressão busca estimar a potência AC esperada.

Modelos avaliados:

- Regressão Linear
- Random Forest Regressor
- Rede Neural MLP (Multi-Layer Perceptron)

Métricas de avaliação:

- RMSE (Raiz do Erro Quadrático Médio)
- MAE (Erro Absoluto Médio)
- R² (Coeficiente de Determinação)

### 4. Modelos de Classificação

A tarefa de classificação busca identificar períodos de baixa geração durante o dia.

A variável-alvo, `LOW_GENERATION`, é definida utilizando o 40º percentil da distribuição de potência AC durante o período diurno, calculado separadamente para cada usina.

Modelos avaliados:

- Regressão Logística
- Random Forest Classifier
- Rede Neural MLP Classifier

Métricas de avaliação:

- Acurácia
- AUC-ROC
- Matriz de confusão
- Precisão e revocação (Precision e Recall)

## Resultados

### Desempenho dos Modelos de Regressão

| Modelo | RMSE (kW) | MAE (kW) | R² |
|---|---:|---:|---:|
| Regressão Linear | 3337,25 | 2434,03 | 0,709 |
| Random Forest | **2410,32** | **1332,18** | **0,848** |
| Rede Neural MLP | 2412,51 | 1361,62 | 0,848 |

O Random Forest apresentou os menores erros de previsão, alcançando R² de 0,848.

### Desempenho dos Modelos de Classificação

| Modelo | Acurácia | AUC-ROC |
|---|---:|---:|
| Regressão Logística | 0,855 | 0,930 |
| Random Forest | **0,928** | **0,975** |
| Rede Neural MLP | 0,900 | 0,954 |

O Random Forest também apresentou o melhor desempenho na classificação, com 92,8% de acurácia e AUC-ROC de 0,975.

### Importância das Variáveis

A irradiação solar foi a variável de maior influência nas duas tarefas.

Na regressão, sua importância foi de 0,794, seguida por `PLANT_ID`, com 0,122.

Na classificação, a irradiação apresentou importância de 0,535, seguida pela temperatura do módulo, com 0,248.

Os resultados reforçam a relevância das condições ambientais na explicação da geração de energia fotovoltaica.

## Protótipo Interativo de Apoio à Decisão

Foi desenvolvido um painel interativo utilizando `ipywidgets`.

O protótipo possui dois modos de operação:

**Modo de Planejamento**
- Seleção da usina solar.
- Ajuste das condições ambientais.
- Estimativa da potência AC esperada.
- Previsão da probabilidade de baixa geração.

**Modo de Monitoramento**
- Comparação entre a geração esperada e a geração real.
- Cálculo do desvio entre os valores previstos e medidos.
- Apresentação de uma recomendação operacional quando o desvio ultrapassa o limite definido.

## Tecnologias e Conceitos Utilizados

- Python
- Scikit-learn
- Pandas
- NumPy
- Matplotlib
- Seaborn
- IPython / ipywidgets
- Aprendizado de Máquina Supervisionado
- Regressão e Classificação
- Random Forest
- Redes Neurais (MLP)
- Pré-processamento de dados
- Importância de atributos
- Avaliação de modelos
- Prevenção de vazamento de dados (Data Leakage)

## Limitações e Trabalhos Futuros

O estudo apresenta algumas limitações:

- O conjunto de dados abrange apenas 34 dias, limitando a análise de variações sazonais.
- O limiar de baixa geração foi definido estatisticamente e pode não representar as necessidades operacionais de cada usina.
- A temperatura do módulo nem sempre está disponível antecipadamente, o que limita previsões estritamente futuras.
- A aplicação em novas usinas pode exigir recalibração dos modelos.

Como melhorias futuras, são propostas:

- Validação temporal utilizando divisões cronológicas entre treino e teste.
- Otimização de hiperparâmetros.
- Estimativa de intervalos de previsão e incerteza.
- Integração com APIs de previsão meteorológica.
- Avaliação em um número maior de usinas solares.

## Autores

**João Pedro Pereira Frutuoso**  
**Thallisson Douglas de Freitas Nunes**

Departamento de Ciências Exatas e Naturais  
Universidade Federal Rural do Semi-Árido (UFERSA)  
Mossoró, Rio Grande do Norte, Brasil.

## Referências

- Anikannal, V. (2020). [Solar Power Generation Data — Kaggle](https://www.kaggle.com/datasets/anikannal/solar-power-generation-data).
- Breiman, L. (2001). Random Forests. *Machine Learning*, 45, 5–32.
- Goodfellow, I., Bengio, Y., & Courville, A. (2016). *Deep Learning*. MIT Press.
- Pedregosa, F. et al. (2011). Scikit-learn: Machine Learning in Python. *Journal of Machine Learning Research*, 12, 2825–2830.

---

*Este projeto foi desenvolvido como trabalho de pesquisa acadêmica na UFERSA.*