# 🚗 Análise e Previsão de Tráfego Rodoviário (Modelo SARIMA)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![Statsmodels](https://img.shields.io/badge/Statsmodels-Time_Series-success)
![Pandas](https://img.shields.io/badge/Pandas-Data_Analysis-yellow)

Este repositório contém o projeto final da disciplina de **Séries Temporais** do **Instituto Germinare**, focado na análise preditiva do volume de tráfego de veículos na rodovia Metro Interstate (I-94, sentido oeste).

O objetivo central é aplicar algoritmos estatísticos clássicos e avançados para prever congestionamentos e auxiliar no planejamento logístico da malha viária, confrontando modelos heurísticos básicos com modelagem sazonal complexa (SARIMA).

---

## 👥 Autores
- **Gabriel Martins Oliveira**
- **Leticia Nascimento da Silva**
- **Theo Correia Martins**
- **Vitor De Mello Maciel**

## 📊 Sobre a Base de Dados
Utilizamos o **Metro Interstate Traffic Volume Dataset** (origem: *UCI Machine Learning Repository*).
A base original contém medições horárias de tráfego, porém, para os propósitos deste estudo temporal contínuo, a série foi agrupada (resample) pela **média diária**. 

- **Características:** Oscilação densa com forte componente de sazonalidade semanal (dias úteis vs. finais de semana).
- **Período:** 2012 a 2018 (aproximadamente 2.000 amostras contínuas após agregação).

## 🛠️ Metodologia e Pipeline Técnica
Todo o processamento está consolidado no arquivo `pipeline.ipynb`. A esteira de engenharia e modelagem contempla:

1. **Tratamento de Dados:** Remoção de nulos, indexação temporal (datetime) e preenchimento (interpolação linear) para manter continuidade matemática.
2. **Decomposição e Estatística:**
   - Decomposição **STL** com identificação autônoma da força sazonal (onde $m=7$ dominou).
   - Testes de Estacionariedade: **Dickey-Fuller Aumentado (ADF)** e **KPSS**.
   - Análise de autocorrelações lineares e defasadas via **ACF** e **PACF**.
3. **Modelagem de Referência (Base Models):** Implementação manual de:
   - *Simple Moving Average (SMA)*
   - *Exponential Moving Average (EMA)*
   - *Seasonal Naive*
4. **Modelagem Avançada (SARIMA):**
   - Busca em grade (*Grid Search*) iterando ordens de $p, d, q$ e os componentes sazonais $P, D, Q$ para $m=7$.
   - Otimização pautada no **BIC (Bayesian Information Criterion)**.
5. **Validação:**
   - Teste de Ljung-Box nos resíduos.
   - Comparativo com métrica **MAE (Mean Absolute Error)**.
   - Simulação de ambiente produtivo utilizando técnica de **Rolling Forecast**.

## 📑 Relatório Gerencial
As entregas teóricas, as avaliações de negócio, as conclusões de rentabilidade (Rolling Forecast vs Static Forecast) e os principais gráficos do projeto estão consolidados no arquivo **`Relatorio_Final_Metro_Traffic.docx`**, redigido nos padrões ABNT.

---

### 🚀 Como Executar
O ambiente de desenvolvimento exige as bibliotecas `pandas`, `numpy`, `matplotlib` e `statsmodels`.

1. Clone este repositório.
2. Certifique-se de que a base `Metro_Interstate_Traffic_Volume.csv` esteja dentro do diretório `/naoEstacionaria`.
3. Abra o notebook `pipeline.ipynb` em seu ambiente local (Jupyter, VS Code, Google Colab).
4. No menu superior, clique em **Run All Cells** (pode levar alguns minutos na célula do *Grid Search*, aproveite para tomar um café ☕).
