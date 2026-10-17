# Correlacao_Portfolio
Análise de correlação entre ativos de um portfólio utilizando python.
### Baixando bibliotecas
```python
import pandas as pd
import numpy as np
import yfinance as yf
```
### Determinando os ativos e seus pesos no portfólio
```python
ativos = ['BOVA11.SA', '^GSPC', 'EURBRL=X', 'USDBRL=X', 'GC=F', 'CL=F']
pesos = np.array([0.20, 0.15, 0.15, 0.20, 0.15, 0.15])
```
### Baixando os dados históricos de fechamento dos ativos pré-selecionados
```python
carteira = yf.download(ativos, start = "2025-01-01", end = "2026-01-01")['Close']
carteira
```
### Determinando os retornos diários dos ativos
```python
retornos = carteira.pct_change()
retornos.dropna(inplace = True)
retornos
```
### Determinando os retornos diários da carteira como um todo, levando em consideração os pesos de cada ativo no portfólio
```python
retorno_carteira = (retornos*pesos).sum(axis=1)
retorno_carteira
```
### Construindo o gráfico com seaborn e matplotlib
```python
import seaborn as sns
import matplotlib.pyplot as plt
plt.figure(figsize=(12,6))
sns.heatmap(retornos.corr(), annot = True, cmap = 'coolwarm', fmt='.2f', linewidths = 0.5)
plt.title('Correlação de Retornos Diários entre Ativos')
plt.show()
```
