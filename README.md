# 🌤️ Weather App

Aplicação web de clima com interface moderna, responsiva e interativa. O projeto permite buscar uma cidade e visualizar informações como temperatura, umidade e velocidade do vento em tempo real.

## Objetivo

Esse projeto foi desenvolvido para praticar:

- manipulação do DOM com JavaScript
- consumo de APIs públicas
- busca de dados por cidade
- construção de interfaces responsivas e visuais
- uso de animações leves para melhorar a experiência do usuário

## Funcionalidades

- busca por qualquer cidade
- exibição da temperatura atual em °C
- informações de umidade e vento
- ícone do clima dinâmico conforme a condição meteorológica
- mensagem de erro para cidades inválidas ou indisponíveis
- visual premium com efeito glassmorphism e animações suaves

## 📁 Estrutura do projeto

```text
projeto03-weatherapp/
├── index.html
├── style.css
├── img/
│   ├── clear.png
│   ├── clouds.png
│   ├── drizzle.png
│   ├── humidity.png
│   ├── mist.png
│   ├── rain.png
│   ├── search.png
│   ├── snow.png
│   └── wind.png
├── README.md
└── .gitignore
```

## 🛠️ Tecnologias utilizadas

- HTML5
- CSS3
- JavaScript
- API pública do Open-Meteo

## 🔌 API utilizada

A aplicação usa a API de geolocalização e clima do Open-Meteo:

- geocodificação por nome da cidade
- previsão atual com temperatura, umidade, vento e código do clima

A integração é feita via `fetch`, convertendo o nome da cidade em coordenadas e buscando os dados climáticos.

## ▶️ Como executar

1. Abra a pasta do projeto em uma IDE ou editor de código.
2. Localize o arquivo `index.html`.
3. Abra o arquivo no navegador.
4. Digite o nome de uma cidade e clique no botão de busca.

Você também pode utilizar a extensão Live Server para abrir em modo mais prático e dinâmico.

## 🧠 Lógica do projeto

A aplicação funciona em etapas:

1. o usuário digita o nome da cidade
2. o código faz uma consulta à API de geocodificação
3. a API retorna latitude e longitude da cidade
4. outra requisição busca o clima atual
5. os dados são exibidos na interface

Exemplo da lógica principal:

```javascript
async function fetchWeather(city) {
  const geoResponse = await fetch(
    `${geocodingUrl}${encodeURIComponent(city)}&count=1&language=pt&format=json`
  );

  const geoData = await geoResponse.json();

  if (!geoData.results || geoData.results.length === 0) {
    throw new Error("Cidade não encontrada.");
  }

  const { latitude, longitude, name, country } = geoData.results[0];
  const weatherResponse = await fetch(
    `${weatherUrl}&latitude=${latitude}&longitude=${longitude}`
  );

  const data = await weatherResponse.json();
  const current = data.current;

  temp.textContent = `${Math.round(current.temperature_2m)}°C`;
  cityName.textContent = `${name}, ${country}`;
  humidity.textContent = `${current.relative_humidity_2m}%`;
  wind.textContent = `${Math.round(current.wind_speed_10m)} km/h`;
}
```

## 🎨 Design

A interface foi pensada para ter um aspecto mais premium, com:

- fundos em degradê
- card central com efeito vidro (glassmorphism)
- cores vibrantes e elegantes
- botões com hover dinâmico
- animações suaves para ícones e elementos
- layout responsivo para dispositivos menores

---

<p align="center">
  Desenvolvido por <a href="https://github.com/LucMNS"><b>LucMNS</b></a>
</p>