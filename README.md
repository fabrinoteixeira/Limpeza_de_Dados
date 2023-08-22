# Limpeza_de_Dados
Introdução 

Este relatório detalha o projeto de limpeza de dados realizado para analisar os dados de vacinação da COVID-19 no Brasil. O objetivo deste projeto é preparar os dados para análise posterior, identificar padrões e tendências, e fornecer insights úteis para tomadas de decisão.
Etapas do Projeto 
1. Carregamento dos Dados 

Os dados foram carregados a partir do arquivo CSV fornecido, contendo informações sobre a vacinação da COVID-19 no Brasil. 

Pitão 

import pandas as pd

file_path = '/content/drive/MyDrive/Curso de Python/Projeto 1_ Limpeza de Dados Dados de Vacinação da COVID-19 no Brasil/dados_vacinacao.csv'
df = pd.read_csv(file_path)

2. Análise Exploratória 

Realizamos uma análise exploratória inicial para entender a estrutura dos dados e identificar 

Pitão 

# Exibir informações básicas do DataFrame
print(df.info())

# Exibir as primeiras linhas do DataFrame
print(df.head())

3. Tratamento de Dados Ausentes 

Identificamos valores ausentes em várias colunas e utilizamos diferentes abordagens para tratá-los.

Pitão 

# Imputação de valores ausentes com média
colunas_numericas = df.select_dtypes(include=['float64', 'int64']).columns
df[colunas_numericas] = df[colunas_numericas].fillna(df[colunas_numericas].mean())

# Remoção de linhas com valores ausentes em colunas específicas
colunas_para_remover_linhas = ['vacina_fabricante_nome', 'vacina_grupoAtendimento_nome']
df = df.dropna(subset=colunas_para_remover_linhas)

4. Limpeza de Nomes de Colunas 

Removemos prefixos indesejados dos nomes de colunas. 

Pitão 

# Renomear colunas removendo o prefixo '_source.'
df = df.rename(columns=lambda x: x.replace('_source.', ''))

5. Codificação de Variáveis Categóricas 

Variáveis categóricas foram codificadas usando o método de codificação one-hot. 

Pitão 

# Codificar variáveis categóricas usando one-hot encoding
colunas_codificar = ['vacina_fabricante_nome', 'paciente_endereco_nmMunicipio']
df_encoded = pd.get_dummies(df, columns=colunas_codificar, drop_first=True)

6. Análise Estatística Descritiva 

Calculamos estatísticas descritivas para entender a distribuição das variáveis numéricas. 

Pitão 

# Exibir informações estatísticas descritivas do DataFrame
descricao = df.describe(include='all')
print(descricao)

7. Visualizações de Dados 

Criamos gráficos de barras e um heatmap para visualizar padrões e tendências. 

Pitão 

import seaborn as sns
import matplotlib.pyplot as plt

# Gráfico de barras para distribuição das vacinas por fabricante
fabricante_counts = df['vacina_fabricante_nome'].value_counts()
plt.figure(figsize=(10, 6))
fabricante_counts.plot(kind='bar', title='Distribuição das Vacinas por Fabricante')
plt.xticks(rotation=45)
plt.xlabel('Fabricante')
plt.ylabel('Quantidade')
plt.tight_layout()
plt.show()

# Heatmap para visualizar correlações entre idade dos pacientes e doses aplicadas
plt.figure(figsize=(8, 6))
correlation_matrix = df.corr()
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', center=0)
plt.title("Correlações entre Idade dos Pacientes e Doses Aplicadas")
plt.show()

Resultados 
Tratamento de Dados Ausentes 

Identificamos e tratamos valores ausentes em diferentes colunas. A imputação de valores médios para colunas numéricas e a remoção de linhas com valores ausentes em colunas específicas ajudaram a preservar a integridade dos dados.
Codificação de Variáveis Categóricas 

A codificação one-hot das variáveis categóricas nos permitiu incorporar informações adicionais nos dados. Isso foi especialmente útil para anál 
Padrões e Tendências Identificados 

Através da análise estatística descritiva e das visualizações de dados, identificamos padrões relevantes na distribuição de vacinas por fabricante, grupo etário e doses aplicadas. O heatmap destacou correlações entre a idade dos pacientes e as doses aplicadas das vacinas, proporcionando insights sobre o comportamento dos pacientes em relação à vacinação.
Desafios e Soluções 

Durante o projeto, enfrentamos desafios como valores ausentes, codificação de variáveis categóricas e seleção de abordagens apropriadas para análise. Esses desafios foram superados por meio de pesquisa, consultas à documentação e discussões em fóruns de análise de dados.
