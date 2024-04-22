[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://github.com/BrunoAraujo84/modelo-expectativa-vida-mundial/blob/main/LICENSE) ![GitHub top language](https://img.shields.io/github/languages/top/BrunoAraujo84/modelo-expectativa-vida-mundial) ![GitHub last commit](https://img.shields.io/github/last-commit/BrunoAraujo84/modelo-expectativa-vida-mundial) ![Contribuições bem-vindas](https://img.shields.io/badge/contribuições-bem_vindas-brightgreen.svg?style=flat)


# Análise de Expectativa de Vida no Brasil dos últimos 50 anos

Este repositório contém um script Python que analisa a evolução da expectativa de vida no Brasil por década, utilizando dados fornecidos pela API do Banco Mundial.

## Dependências

O script utiliza as seguintes bibliotecas:

- `requests`: Para fazer solicitações HTTP à API do Banco Mundial.
- `matplotlib.pyplot`: Para visualizar os dados em forma de gráfico.
- `scipy.stats`: Para realizar cálculos estatísticos como a regressão linear.

## Dados

Os dados são obtidos através da API do Banco Mundial, especificamente a expectativa de vida ao nascer no Brasil desde 1970 até 2024. A URL utilizada para acessar os dados é:

http://api.worldbank.org/v2/country/br/indicator/SP.DYN.LE00.IN?date=1970:2024&format=json


**Observação:** Se desejar obter dados de um país específico ou calcular a média mundial, altere na URL acima a sigla `br` para o código do país desejado ou use `all` para todos os países.


## Processamento dos Dados

O script realiza os seguintes passos para processar os dados:

1. Faz a solicitação HTTP e obtém os dados em formato JSON.
2. Extrai os anos e os valores da expectativa de vida, descartando anos sem dados.
3. Reverte as listas para que os dados estejam em ordem cronológica.
4. Calcula a média da expectativa de vida por década.

## Análise Estatística

Usa regressão linear para projetar a expectativa de vida para as próximas décadas até 2060. O script calcula a inclinação e a interceptação para prever futuros valores da expectativa de vida.

## Visualização

O script gera um gráfico que mostra a evolução da expectativa de vida ao longo das décadas. Os dados históricos são mostrados em linha contínua, e as projeções futuras são representadas em linha pontilhada.

## Uso

Para executar este script, você precisa instalar as dependências listadas e executar o arquivo Python. Certifique-se de que você tem acesso à internet para baixar os dados da API.

1. pip install requests
2. pip install matplotlib
3. pip install scipy

## Licença

Este projeto é licenciado sob a Licença MIT. Veja o arquivo `LICENSE` para mais detalhes.
