<div align="center">
  <h1>⚡ Calculadora del Teorema de Fortescue y Analizador de Fallas en SEP</h1>
  <p><strong>Herramienta interactiva para el análisis de componentes simétricas y localización de fallas en líneas de transmisión.</strong></p>
</div>

<hr>

<h2>📌 Características Principales</h2>
<ul>
  <li>
    <strong>Análisis de Fasores (Fortescue):</strong>
    <ul>
      <li>Transformación de componentes de fase (<i>I<sub>R</sub>, I<sub>S</sub>, I<sub>T</sub></i>) a componentes simétricas de secuencia (<i>I<sub>0</sub>, I<sub>1</sub>, I<sub>2</sub></i>).</li>
      <li>Representación gráfica polar interactiva de fasores de fase y de secuencia.</li>
    </ul>
  </li>
  <li>
    <strong>Localización y Clasificación de Fallas en Líneas de Transmisión:</strong>
    <ul>
      <li><strong>Clasificación Automática de Fallas:</strong> Identificación precisa del tipo de evento:
        <ul>
          <li>Monofásica a Tierra (<i>R-G, S-G, T-G</i>).</li>
          <li>Bifásica a Tierra (<i>R-S-G, S-T-G, T-R-G</i>).</li>
          <li>Bifásica Aislada (<i>R-S, S-T, T-R</i>).</li>
        </ul>
      </li>
      <li><strong>Estimación de Distancia de Falla:</strong> Cálculo de la impedancia vista (<i>Z<sub>vista</sub></i>) y distancia en kilómetros utilizando el método de reactancia simple y factor de compensación homopolar (<i>k<sub>0</sub></i>).</li>
      <li><strong>Direccionalidad de Protecciones:</strong> Evaluación del sentido de la falla (<b>Adelante / Forward</b> o <b>Atrás / Reverse</b>) mediante el fasor de impedancia de secuencia negativa (<i>Z<sub>2</sub> = V<sub>2</sub> / I<sub>2</sub></i>).</li>
    </ul>
  </li>
</ul>

<hr>

<h2>📐 Fundamento Teórico y Lógica de Decisión</h2>

<h3>1. Transformación de Fortescue</h3>
<p>El sistema de componentes simétricas descompone un sistema trifásico desbalanceado en tres sistemas balanceados:</p>

<p align="center">
  <i>I<sub>0</sub> = ⅓ (I<sub>R</sub> + I<sub>S</sub> + I<sub>T</sub>)</i><br>
  <i>I<sub>1</sub> = ⅓ (I<sub>R</sub> + a · I<sub>S</sub> + a² · I<sub>T</sub>)</i><br>
  <i>I<sub>2</sub> = ⅓ (I<sub>R</sub> + a² · I<sub>S</sub> + a · I<sub>T</sub>)</i>
</p>

<p><i>Donde a = e<sup>j120°</sup> = -0.5 + j(√3 / 2).</i></p>

<h3>2. Criterio de Clasificación de Fallas</h3>
<p>El algoritmo evalúa la presencia de la corriente homopolar (<i>I<sub>0</sub></i>) y la relación entre las magnitudes de las corrientes de fase:</p>

<pre>
                          ┌───────────────────────────┐
                          │    ¿ |I0| > 0 Amp?        │
                          └─────────────┬─────────────┘
                                        │
                       ┌────────────────┴────────────────┐
                       ▼                                 ▼
                     [ SÍ ]                            [ NO ]
            (Existe retorno por tierra)        (Falla sin contacto a tierra)
                       │                                 │
         ┌─────────────┴─────────────┐                   ▼
         ▼                           ▼            Bifásica Aislada (X-Y)
  ¿I_max > 1.3 * I_med?      ¿I_max <= 1.3 * I_med?  Z_vista = (V_X - V_Y) / (I_X - I_Y)
         │                           │
         ▼                           ▼
  Monofásica (X-G)         Bifásica a Tierra (X-Y-G)
Z_vista = V_X / (I_X + 3*I0*k0)  Z_vista = (V_X - V_Y) / (I_X - I_Y)
</pre>

<hr>

<h2>🚀 Requisitos e Instalación</h2>

<h3>Prerrequisitos</h3>
<p>Tener instalado <strong>Python 3.8+</strong>.</p>

<h3>Instalación de dependencias</h3>
<p>Clona este repositorio e instala las librerías necesarias:</p>

<pre><code>git clone https://github.com/TU_USUARIO/NOMBRE_DEL_REPOSITORIO.git
cd NOMBRE_DEL_REPOSITORIO
pip install -r requirements.txt
</code></pre>

<h4>Contenido de <code>requirements.txt</code>:</h4>
<pre><code>streamlit
numpy
matplotlib
</code></pre>

<div align="center">
  <a href="https://TU-APP-DE-STREAMLIT.streamlit.app" target="_blank">
    <img src="https://static.streamlit.io/badges/streamlit_badge_black__white.svg" alt="Abrir en Streamlit">
  </a>
</div>

<hr>

<h2>💻 Ejecución de la Aplicación</h2>
<p>Para iniciar la interfaz web en tu navegador local, ejecuta:</p>

<pre><code>streamlit run app.py
</code></pre>

<hr>

<h2>🛠️ Tecnologías Utilizadas</h2>
<ul>
  <li><strong>Python 3:</strong> Lenguaje base para los cálculos matemáticos y procesamiento fasorial.</li>
  <li><strong>Streamlit:</strong> Framework para el despliegue de la interfaz web interactiva.</li>
  <li><strong>NumPy:</strong> Manejo de números complejos y álgebra lineal fasorial.</li>
  <li><strong>Matplotlib:</strong> Generación de diagramas polares fasoriales.</li>
</ul>

<hr>

<h2>👤 Autor</h2>
<ul>
  <li><strong>Ing. Jorge Raul Altamirano Garcia</strong></li>
  <li><i>Especialidad:</i> Sistemas Eléctricos de Potencia / Protecciones</li>
</ul>
