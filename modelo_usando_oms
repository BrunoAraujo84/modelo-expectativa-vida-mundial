# Importando Biblioteca para o modelo
import requests
import matplotlib.pyplot as plt
from scipy.stats import linregress

# URL da API para dados de expectativa de vida do Brasil
url = "http://api.worldbank.org/v2/country/br/indicator/SP.DYN.LE00.IN?date=1970:2024&format=json"

# Fazer a solicitação e obter os dados
response = requests.get(url)
data = response.json()

# Processar os dados
years = []
life_expectancy = []

if data and len(data) > 1:
    for record in data[1]:
        if record['value'] is not None:
            years.append(int(record['date']))
            life_expectancy.append(record['value'])

# Inverter listas para que os anos estejam em ordem crescente
years.reverse()
life_expectancy.reverse()

# Agrupar por década
decade_years = ['1970s']
decade_life_expectancy = []
partial_decade_values = []

# Calcular média parcial para 1974-1979
for year, value in zip(years, life_expectancy):
    if 1974 <= year <= 1979:
        partial_decade_values.append(value)
if partial_decade_values:
    decade_life_expectancy.append(sum(partial_decade_values) / len(partial_decade_values))

# Calcular média a cada 10 anos de 1980 até 2024
for i in range(1980, 2024, 10):
    decade_indexes = [index for index, year in enumerate(years) if i <= year < i + 10]
    if decade_indexes:
        average_life_expectancy = sum(life_expectancy[j] for j in decade_indexes) / len(decade_indexes)
        decade_years.append(str(i) + 's')
        decade_life_expectancy.append(average_life_expectancy)

# Prepara os dados para a regressão linear, incluindo o último ponto dos dados históricos
last_known_year = max(years)
last_known_life_expectancy = life_expectancy[years.index(last_known_year)]
years_complete = [year for year in years if year % 10 == 0] + [last_known_year]
life_expectancy_complete = [life_expectancy[i] for i, year in enumerate(years) if year % 10 == 0] + [last_known_life_expectancy]

# Faz a regressão linear
slope, intercept, r_value, p_value, std_err = linregress(years_complete, life_expectancy_complete)

# Função para calcular a expectativa de vida projetada com base na tendência
def predict_life_expectancy(year):
    return slope * year + intercept

# Gera valores projetados para as décadas futuras, começando do último ponto conhecido
future_decades = list(range(last_known_year + 9, 2060, 10))
predicted_life_expectancy = [predict_life_expectancy(year) for year in future_decades]

# Adiciona os valores projetados aos dados existentes para plotar
decade_years.extend([str(year) + 's' for year in future_decades])
decade_life_expectancy.extend(predicted_life_expectancy)

# Criar o gráfico
plt.figure(figsize=(15, 8))
plt.plot(decade_years[:-4], decade_life_expectancy[:-4], marker='o', label='Dados Históricos')
plt.plot([decade_years[-5]] + decade_years[-4:], [decade_life_expectancy[-5]] + decade_life_expectancy[-4:], marker='o', linestyle='--', color='red', label='Projeção')
plt.title('Evolução Média da Expectativa de Vida ao Longo do Tempo por Década')
plt.xlabel('Década')
plt.ylabel('Expectativa de Vida Média')
plt.legend()
plt.grid(True)
plt.ylim(0, 100)

# Adicionar rótulos aos pontos
for i, txt in enumerate(decade_life_expectancy):
    plt.annotate(f"{txt:.1f}",
                 (decade_years[i], decade_life_expectancy[i]),
                 textcoords="offset points",
                 xytext=(0,10),
                 ha='center')

# Visualizar o gráfico
plt.show()
