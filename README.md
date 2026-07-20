<div align="center">
  <h1>⚡ Calculadora del Teorema de Fortescue y Analizador de Fallas en SEP ⚡</h1>
  <p><strong>Herramienta interactiva para el análisis de componentes simétricas y localización de fallas en líneas de transmisión</strong></p>
</div>
<hr>

<h2>Aquí te comparto el link que te llevará al analizador: </h2>
<div align="center">
  <a href="https://jorgeraul9-calcu-fasores-fortescue.streamlit.app/" target="_blank">
    <img src="https://static.streamlit.io/badges/streamlit_badge_black__white.svg" alt="Abrir en Streamlit">
  </a>
</div>

<h2>¿De qué se trata?</h2>
<ul>
  <p>
  Para empezar, realizo este proyecto con fines netamente investigativos y en afán de lograr una automatización a nivel de cálculos eléctricos mediante software open source que faciliten las actividades de desarrollo de matemática con números complejos y cálculo fasorial.
</p>
  
  <p>
  Esta aplicación es una herramienta interactiva diseñada para el análisis fasorial en sistemas eléctricos de potencia (SEP) a través de la transformación de componentes simétricas mediante el Teorema de Fortescue. A partir de las corrientes de fase (<i>I<sub>R</sub>, I<sub>S</sub>, I<sub>T</sub></i>), el sistema realiza la conversión automática a componentes de secuencia (<i>I<sub>0</sub>, I<sub>1</sub>, I<sub>2</sub></i>) y ofrece una representación gráfica polar interactiva para visualizar con claridad el comportamiento de los fasores.
</p>

<p>
  Asimismo, la plataforma integra un módulo especializado en la localización y clasificación automática de fallas en líneas de transmisión, capaz de discernir entre eventos monofásicos a tierra (<i>R-G, S-G, T-G</i>), bifásicos a tierra (<i>R-S-G, S-T-G, T-R-G</i>) y bifásicos aislados (<i>R-S, S-T, T-R</i>). A partir de dicha clasificación, estima la impedancia vista (<i>Z<sub>vista</sub></i>) y la distancia al punto de falla en kilómetros empleando el método de reactancia simple junto al factor de compensación homopolar (<i>k<sub>0</sub></i>). Finalmente, evalúa la direccionalidad de la protección (<b>Adelante / Forward</b> o <b>Atrás / Reverse</b>) mediante la impedancia de secuencia negativa (<i>Z<sub>2</sub> = V<sub>2</sub> / I<sub>2</sub></i>).
</p>

<blockquote style="background-color: #f9f9f9; border-left: 4px solid #ff4b4b; padding: 10px; margin: 10px 0;">
  📌 <strong>Aviso:</strong> Actualmente estás explorando la <strong>versión Demo</strong> de la aplicación, configurada para la validación de cálculos y pruebas conceptuales del algoritmo.
</blockquote>
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

<p><i>Donde a = e<sup>j120°</sup> = -0.5 + j(√3 / 2) = 1<120°.</i></p>

<h3>2. Criterio de Clasificación de Fallas</h3>
<p>El algoritmo evalúa la presencia de la corriente homopolar (<i>I<sub>0</sub></i>) y la relación entre las magnitudes de las corrientes de fase:</p>

<pre> 
                            ┌──────────────────────────────┐
                            │ ¿Existe corriente a tierra?  │
                            │   (|I₀| > 0 A o I_residual)  │
                            └──────────────┬───────────────┘
                                           │
                          ┌────────────────┴────────────────┐
                          ▼                                 ▼
                      [ SÍ ]                              [ NO ]
            (Falla con contacto a tierra)       (Falla limpia entre fases)
                          │                                 │
            ┌─────────────┴─────────────┐                   │
            ▼                           ▼                   ▼
  ¿Una sola fase domina?     ¿Dos fases con corrientes   Falla Bifásica Aislada
(Una corriente es mucho más    elevadas y similares?             (L-L)
    alta que las otras)                 │                   │
            │                           │                   │
            ▼                           ▼                   ▼
     Falla Monofásica            Falla Bifásica          Impedancia medida:
        a Tierra                    a Tierra             Tensión Fase-Fase
         (L-G)                       (L-L-G)             ───────────────────
            │                           │                Corriente Fase-Fase
            ▼                           ▼
    Impedancia medida:          Impedancia medida:
     Tensión Fase-Tierra        Tensión Fase-Fase
   ────────────────────────    ───────────────────
   Corriente con compensación  Corriente Fase-Fase
        por tierra (K₀)
</pre>

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
