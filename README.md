[![Open in MATLAB Online](https://www.mathworks.com/images/responsive/global/open-in-matlab-online.svg)](https://matlab.mathworks.com/open/github/v1?repo=PradoIT/MSFP3)

# Práctica 3: Modelado y control del sistema musculoesquelético

## Información del estudiante
David Esau Cerano Fuentes  \[23210696]; L23210696@tijuana.tecn.mx

Modelado de Sistemas Fisiológicos

Ingeniería Biomédica

## Docente
Dr. Paul Antonio Valle Trujillo; paul.valle@tectijuana.edu.mx

Departamento de Ingeniería Eléctrica y Electrónica, Tecnológico Nacional de México/IT Tijuana, Blvd. Alberto Limón Padilla s/n, Tijuana, C.P. 22454, B.C., México.

## Descripción de la asignatura

El modelizado de sistemas fisiológicos es una herramienta importante en Ingeniería Biomédica, permite comprender el funcionamiento del cuerpo humano, así como diseñar y evaluar terapias y dispositivos médicos; se define como el proceso de formular modelos matemáticos o computacionales que representan el comportamiento y la interacción de los sistemas biológicos y fisiológicos. Esta asignatura pretende aportar al perfil del Ingeniero Biomédico la capacidad de realizar investigación científica en el área de Biología de Sistemas con la finalidad de dirigir y participar en equipos de trabajo interdisciplinarios en contextos nacionales e internacionales, así como de proporcionar soluciones informáticas para resolver problemas en el campo de la Ingeniería Biomédica con ética profesional; lo anterior al proporcionar al estudiante bases sólidas para modelizar sistemas y diseñar controladores para la solución de problemas en las áreas de atención médica y del sector industrial médico. La construcción de analogías entre circuitos eléctricos y sistemas fisiológicos para la formulación de modelos matemáticos y el diseño de controladores mediante la experimentación in silico brindan herramientas de gran aplicación en el quehacer profesional del Ingeniero Biomédico.

La asignatura de Modelado de Sistemas Fisiológicos forma parte del plan de estudios de la carrera en Ingeniería Biomédica con la siguiente competencia general del curso: Utiliza las propiedades de los circuitos RLC para describir la dinámica de sistemas fisiológicos, obtener modelos matemáticos y aplicar el control clásico, esto con el objetivo de integrar los principios de la Ingeniería de Control, la Electrónica Analógica y las Ciencias de la Computación con la Anatomía y Fisiología del cuerpo humano para proporcionar descripciones cuantitativas y cualitativas de sistemas fisiológicos complejos con el objetivo de modelizar, analizar, controlar, ilustrar y predecir su dinámica tanto en el corto como en el largo plazo.

## Objetivos

1. Identificar los elementos del modelo mecánico del sistema musculoesquelético y describir su función.
2. Construir el circuito eléctrico equivalente mediante la analogía fuerza–voltaje.
3. Formular las ecuaciones del sistema y obtener la función de transferencia entre la fuerza aplicada y el desplazamiento.
4. Analizar el error en estado estacionario y la estabilidad para un individuo sano (control) y un caso simulado de atrofia muscular.
5. Implementar el modelo matemático y la función de transferencia en MATLAB/Simulink, y el circuito equivalente en Simscape Electrical.
6. Comparar las respuestas al impulso unitario del control y del caso en el intervalo de 0 a 10 segundos.
7. Diseñar y sintonizar un controlador PID para reducir la diferencia entre la respuesta del caso y la del individuo sano.
8. Implementar las funciones de transferencia y el sistema controlado en Python, utilizando Visual Studio Code, y comparar los resultados con MATLAB/Simulink.
9. Relacionar los elementos mecánicos y eléctricos con las estructuras biológicas mediante un diagrama del sistema musculoesquelético.

## Descripción detallada del sistema

El modelo representa de manera simplificada las propiedades viscoelásticas del sistema musculoesquelético mediante un elemento contráctil activo, un amortiguador y dos elementos elásticos. Permite estudiar la relación entre la fuerza desarrollada por el músculo, su desplazamiento y las propiedades mecánicas de los tejidos y tendones.

La fuerza del elemento contráctil se representa mediante $F_0(t)$ y la fuerza transmitida por el sistema mediante $F(t)$. La relación establecida en la práctica es:

$$
F_0(t)=\alpha F(t), \qquad 0<\alpha<1.
$$

El amortiguador $R$ representa el comportamiento viscoso del tejido. Los elementos $C_p$ y $C_s$ representan las compliancias del elemento paralelo y del elemento en serie, respectivamente. El desplazamiento total es $x(t)$, mientras que $x_1(t)$ corresponde al elemento elástico en serie. Por tanto, la deformación del amortiguador es $x(t)-x_1(t)$ y su velocidad relativa es:

$$
\frac{d}{dt}\left[x(t)-x_1(t)\right].
$$

### Analogía electromecánica

Para construir el circuito eléctrico equivalente se utiliza la analogía fuerza–voltaje:

| Sistema mecánico | Sistema eléctrico equivalente |
| --- | --- |
| Fuerza $F(t)$ | Voltaje $V(t)$ |
| Velocidad $\dot{x}(t)$ | Corriente $I(t)$ |
| Desplazamiento $x(t)$ | Carga eléctrica $q(t)$ |
| Amortiguador | Resistencia $R$ |
| Compliancia mecánica | Capacitancia $C$ |
| Masa, cuando está presente | Inductancia $L$ |

Las conexiones mecánicas y eléctricas no conservan necesariamente la misma topología. Los elementos mecánicos en paralelo pueden representarse mediante elementos eléctricos en serie, y los elementos mecánicos en serie mediante elementos eléctricos en paralelo. Deben revisarse los nodos de referencia y la ubicación de los desplazamientos antes de establecer el circuito equivalente.

### Parámetros del control y del caso

Los siguientes valores corresponden al circuito eléctrico equivalente indicado en la práctica:

| Parámetro | Control: individuo sano | Caso: atrofia muscular simulada |
| --- | --- | --- |
| Entrada equivalente a $F(t)$ | 1 V | 1 V |
| $\alpha$ | 0.25 | 0.25 |
| $C_s$ | 10 µF | 10 µF |
| $C_p$ | 100 µF | 100 µF |
| $R$ | 100 Ω | 10 kΩ |

La diferencia entre ambas condiciones se representa mediante el incremento de $R$, que modifica la componente viscosa del modelo. Estos valores son parámetros de simulación eléctrica y no mediciones directas de un paciente.

### Modelo matemático y sistema de control

A partir de las relaciones constitutivas y del equilibrio de fuerzas se deben obtener las ecuaciones del sistema. Considerando condiciones iniciales nulas y el desplazamiento como salida, la función de transferencia se expresa como:

$$
G(s)=\frac{X(s)}{F(s)}.
$$

Se deben obtener las funciones correspondientes al control y al caso, calcular sus polos y analizar el error en estado estacionario. La respuesta del individuo sano se utiliza como referencia para el caso simulado. La señal de error se define como:

$$
e(t)=x_{\mathrm{control}}(t)-x_{\mathrm{caso}}(t).
$$

El sistema de retroalimentación incorpora un controlador PID. Las ganancias $k_P$, $k_I$ y $k_D$ se determinan mediante la herramienta **Tune** del bloque **PID Controller** de Simulink. Posteriormente se comparan las respuestas del control, del caso en lazo abierto y del caso con controlador, considerando amplitud, velocidad de respuesta, amortiguamiento y diferencia respecto a la referencia.

La práctica se realiza exclusivamente mediante experimentación *in silico*, con fines académicos y de simulación; no constituye un tratamiento para la atrofia muscular.

Palabras clave: Sistema musculoesquelético; Analogía fuerza–voltaje; Modelo matemático; Controlador PID; Simulaciones numéricas.

## Imagen del sistema musculoesquelético

![Diagrama biológico del sistema musculoesquelético](image%2820261105-043853%29.png)

*Figura 1. Diagrama biológico del sistema musculoesquelético proporcionado para la práctica.*

| Elemento del modelo | Interpretación biológica |
| --- | --- |
| $F_0(t)$ | Fuerza generada por el elemento contráctil activo del músculo. |
| $C_s$ | Compliancia en serie, asociada principalmente a los tendones. |
| $C_p$ | Compliancia en paralelo, asociada a la elasticidad pasiva del músculo y del tejido conectivo. |
| $R$ | Componente viscosa del tejido y resistencia interna al movimiento. |
| $x(t)$ | Desplazamiento total del modelo. |
| $x_1(t)$ | Desplazamiento del elemento elástico en serie. |

En la imagen también aparece la etiqueta $x_2(t)$; en el instructivo, la deformación relativa del amortiguador se expresa como $x(t)-x_1(t)$.

<!-- Mantener image(20261105-043853).png en la misma carpeta que este README para visualizar la imagen. -->

## Lista de archivos incluidos en el repositorio

La siguiente lista corresponde a los entregables solicitados por el instructivo. Los archivos de simulación y sus resultados deberán incorporarse conforme se complete la práctica.

1. Archivo README.md con la descripción y documentación de la práctica.
2. Análisis del modelo mecánico y desarrollo de la analogía electromecánica.
3. Circuito eléctrico equivalente y desarrollo matemático del sistema.
4. Cuaderno computacional de MATLAB y figuras exportadas en PDF.
5. Modelos de Simulink para las ecuaciones, las funciones de transferencia y el sistema de control [.slx].
6. Modelo del circuito equivalente en Simscape Electrical.
7. Código fuente de Python para las respuestas en lazo abierto y en lazo cerrado [.py].
8. Parámetros y capturas de la sintonización del controlador PID.
9. Figuras de las respuestas del control, del caso y del sistema controlado obtenidas en MATLAB y Python.
10. Capturas de las simulaciones y comparación entre las diferentes implementaciones.
11. Diagrama biológico del sistema musculoesquelético [image(20261105-043853).png].
12. Archivos complementarios utilizados durante la práctica.
13. Archivo CITATION.cff con la información del alumno y del repositorio.

## Referencias

\[1] P. A. Valle, *Syllabus para Modelado de Sistemas Fisiológicos*, Tecnológico Nacional de México / Instituto Tecnológico de Tijuana, Tijuana, B.C., México, 2025. https://biomath.xyz/course/

\[2] *Práctica 5.5: Modelado y control del sistema musculoesquelético*, instructivo proporcionado, pp. 87–94.

\[3] M. C. Khoo, *Physiological Control Systems: Analysis, Simulation, and Estimation*, 2nd ed., IEEE Press, 2018.

\[4] F. C. Hoppensteadt y C. S. Peskin, *Modeling and Simulation in Medicine and the Life Sciences*, Springer.

\[5] J. E. Hall, *Guyton and Hall Textbook of Medical Physiology*, 14th ed., Elsevier, 2021.
