# 🏙️ Análise de Demanda de Locação de Imóveis

## 📌 Objetivo

O objetivo desta atividade é realizar uma análise de dados de locação de imóveis urbanos, focando nos apartamentos situados em bairros com **alta demanda de locação**. A finalidade é fornecer ao departamento de marketing um conjunto de dados refinado com informações sobre a rentabilidade dos imóveis, auxiliando na tomada de decisões estratégicas.

---

## 📊 Etapas do Processo

### 1. Carregamento dos Dados
O conjunto de dados `imoveis_ficticios.csv` foi carregado com a biblioteca `pandas`, permitindo a manipulação eficiente das informações tabulares.

```python
import pandas as pd

df = pd.read_csv('imoveis_ficticios.csv')
```

---

### 2. Filtragem dos Apartamentos com Alta Demanda

Selecionamos apenas os imóveis do tipo **Apartamento** e localizados em bairros com **Alta Demanda** de locação.

```python
df_Apartamentos = df[(df['Tipo'] == 'Apartamento') & (df['Alta_Demanda'] == 'Sim')].copy()
```

---

### 3. Cálculo do Valor do Metro Quadrado

Foi criada uma nova coluna `Valor_m2`, com o valor do aluguel mensal dividido pela área do imóvel em m². O valor foi arredondado para inteiro.

```python
df_Apartamentos['Valor_m2'] = df_Apartamentos['Aluguel_Mensal'] / df_Apartamentos['Area_m2']
df_Apartamentos['Valor_m2'] = df_Apartamentos['Valor_m2'].round(0).astype(int)
```

---

### 4. Classificação de Rentabilidade

Calculamos a **média geral do valor/m²** dos apartamentos filtrados, e criamos uma função que classifica cada imóvel com base nesse valor:

- `Acima da Média`
- `Dentro da Média`
- `Abaixo da Média`

```python
media_geral = df_Apartamentos['Valor_m2'].mean()

def alta_demanda(valor_m2):
    if valor_m2 > media_geral:
        return 'Acima da Média'
    elif valor_m2 == media_geral:
        return 'Dentro da Média'
    else:
        return 'Abaixo da Média'

df_Apartamentos['Alta_demanda'] = df_Apartamentos['Valor_m2'].apply(alta_demanda)
```

---

### 5. Exportação para Arquivo CSV

Geramos um novo arquivo `.csv` contendo apenas os imóveis selecionados e suas informações atualizadas.

```python
df_Apartamentos.to_csv('imoveis_apartamentos_analise.csv', index=False)
```

---

### 6. Entrega ao Departamento de Marketing

O arquivo `imoveis_apartamentos_analise.csv` está pronto para ser entregue ao time de marketing, que poderá utilizá-lo para campanhas focadas nos imóveis mais rentáveis e estratégicos.

---

## ✅ Conclusão

O processo desenvolvido permite uma **análise segmentada** dos imóveis com maior potencial de retorno, proporcionando dados valiosos para o marketing e decisões de investimento. A combinação de filtragem, cálculo de rentabilidade e classificação torna o dataset final uma ferramenta poderosa de apoio estratégico.

---
```
