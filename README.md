#CSS

@import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');

body {
    margin: 0;
    padding: 0;
    font-family: 'Montserrat', sans-serif;
    font-size: 18px;
    line-height: 20px;
    background-color: #fff;
    color: #272727;
}

h1, h2, p {
    margin: 0;
}

ul {
    list-style: none;
    margin: 0;
    padding: 0;
}

.header {
    background-image: url("../img/back.jpg");
    background-size: contain;
    background-repeat: no-repeat;
    background-position: left;
    background-color: #CCE59D;
    padding: 25vh 30px;
    margin-bottom: 60px;
    display: flex;
    flex-direction: column;
    align-items: flex-end;
}

.header__text {
    display: flex;
    flex-direction: column;
    gap: 30px;
    width: fit-content;
    text-align: right;
}

main {
    padding: 0 30px 100px;
}

.main__title {
    text-align: center;
    margin-bottom: 100px;
}

.list {
    display: flex;
    justify-content: space-around;
}

#Main.py 

# Importações
from flask import Flask, render_template


app = Flask(__name__)

def result_calculate(size, lights, device):
    """Calcula o consumo estimado com base na área, número de luminárias e aparelhos.

    Args:
        size (int): Tamanho (área) da residência
        lights (int): Quantidade de luminárias
        device (int): Quantidade de aparelhos

    Returns:
        float: Consumo estimado
    """
    # Coeficientes usados no cálculo do consumo de energia
    home_coef = 100
    light_coef = 0.04
    devices_coef = 5
    return size * home_coef + lights * light_coef + device * devices_coef

# A primeira página
@app.route('/')
def index():
    return render_template('index.html')

# A segunda página
@app.route('/<size>')
def lights(size):
    return render_template(
                            'lights.html', 
                            size=size
                           )

# A terceira página
@app.route('/<size>/<lights>')
def electronics(size, lights):
    return render_template(
                            'electronics.html',
                            size = size, 
                            lights = lights                           
                           )

# Cálculo
@app.route('/<size>/<lights>/<device>')
def end(size, lights, device):
    return render_template('end.html', 
                            result=result_calculate(int(size),
                                                    int(lights), 
                                                    int(device)
                                                    )
                        )
app.run(debug=True)

#light.html

<!doctype html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta
    name="viewport"
    content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0"
  >
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <link rel="stylesheet" href="/static/css/style.css">
  <title>Calculadora de eficiência energética para casas inteligentes</title>
</head>
<body>
  <header class="header">
    <div class="header__text">
      <h1>Calcule a eficiência energética da sua casa!</h1>
      <p>Seja proativo e resolva o problema do consumo excessivo de energia!</p>
    </div>
  </header>
  <main>
    {% block content %}
    <h2 class="main__title">Selecione quantas luminárias existem na sua casa:</h2>
    <ul class="list" id="list">
      <li class="list__item">
        <a href="{{ size ~ '/' ~ '3' }}">
          <img class="item__img" src="/static/img/light.svg" alt="light">
          <span>2-4 lâmpadas</span></a>
      </li>
      <!--Assignment #2 -->
      <li class="list__item">
        <a href="{{ size ~ '/' ~ '7' }}"> 
          <img class="item__img" src="/static/img/light.svg" alt="light">
          <span>4-6 lâmpadas</span></a>
      </li>
      <li class="list__item">
        <a href="{{ size ~ '/' ~ '10' }}">
          <img class="item__img" src="/static/img/light.svg" alt="light">
          <span>8+ lâmpadas</span></a>
      </li>
    </ul>
    {% endblock %}
  </main>
  <footer>

  </footer>
</body>
</html>
