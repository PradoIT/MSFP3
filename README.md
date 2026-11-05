[README (3) (1).md](https://github.com/user-attachments/files/34408381/README.3.1.md)

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

<p align="center">
  <img src="imagenes/sistema_musculoesqueletico.png" alt="Diagrama biológico del sistema musculoesquelético: músculo, tendón, componente viscosa y elasticidad pasiva" width="1000">
</p>

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



## Desarrollo de la práctica

### 1. Identificación del modelo mecánico

El sistema se divide en dos ramas que comparten el desplazamiento total. Una contiene el elemento elástico paralelo $C_p$; la otra contiene el elemento elástico en serie $C_s$ y la combinación del elemento contráctil con el amortiguador. El movimiento de cada parte está limitado por sus conexiones con las demás.

| Símbolo | Significado | Papel dentro del análisis |
| --- | --- | --- |
| $F(t)$ | Fuerza transmitida por el sistema | Entrada utilizada para definir la función de transferencia. |
| $F_0(t)$ | Fuerza contráctil activa | Se relaciona con la entrada mediante el factor $\alpha$. |
| $\alpha$ | Factor de proporcionalidad | Establece la relación entre fuerza activa y fuerza transmitida. |
| $R$ | Amortiguamiento viscoso | Relaciona fuerza viscosa y velocidad relativa. |
| $C_p$ | Compliancia en paralelo | Describe la deformabilidad pasiva de la rama paralela. |
| $C_s$ | Compliancia en serie | Describe la deformabilidad de la rama en serie. |
| $x(t)$ | Desplazamiento total | Variable de salida seleccionada. |
| $x_1(t)$ | Desplazamiento de la compliancia en serie | Variable interna del modelo. |

La compliancia es el inverso de la rigidez: una compliancia mayor implica una deformación mayor para una misma fuerza. Aunque en el dibujo se usan resortes, los símbolos $C_p$ y $C_s$ se interpretan como compliancias, no como constantes de rigidez.

### 2. Construcción de la analogía electromecánica

La conversión comienza por identificar fuerzas, desplazamientos y velocidades. Después se asignan voltajes, cargas y corrientes equivalentes. El elemento activo se representa mediante una fuente cuya relación con la entrada conserva el factor $\alpha$.

Para establecer las conexiones se revisan las restricciones mecánicas. Dos ramas con el mismo desplazamiento también comparten la misma velocidad; en la analogía fuerza–voltaje esa condición se traduce en igualdad de corrientes. Por ello, el circuito no se obtiene copiando visualmente las conexiones del dibujo mecánico.

El circuito de esta práctica utiliza resistencias, capacitores y fuentes. La equivalencia masa–inductancia se incluye como referencia general, pero no debe agregarse una inductancia si el modelo mecánico no contiene una masa.

### 3. Formulación de las ecuaciones

Para cada elemento elástico, la relación entre fuerza y deformación es:

$$
F_C(t)=\frac{\Delta x(t)}{C}.
$$

Las fuerzas elásticas de los elementos paralelo y serie se pueden expresar, con una convención de signos consistente, como:

$$
F_p(t)=\frac{x(t)}{C_p},\qquad F_s(t)=\frac{x_1(t)}{C_s}.
$$

La fuerza viscosa depende de la velocidad relativa de los extremos del amortiguador:

$$
F_R(t)=R\left[\dot{x}(t)-\dot{x}_1(t)\right].
$$

Estas relaciones se combinan con el equilibrio de fuerzas y con $F_0(t)=\alpha F(t)$. Antes de sumar las fuerzas es necesario fijar sus sentidos de referencia en el diagrama. En el circuito equivalente se utilizan las relaciones:

$$
V_R(t)=R I_R(t),\qquad V_C(t)=\frac{q_C(t)}{C},\qquad I_C(t)=\frac{dq_C(t)}{dt}.
$$

La comprobación consiste en verificar que las ecuaciones mecánicas y eléctricas coincidan al sustituir fuerza por voltaje y desplazamiento por carga.

#### 3.1. Desarrollo del circuito por superposición

El cálculo manuscrito separa la contribución de las dos fuentes para obtener la señal $F_s(t)$ asociada al capacitor $C_p$:

$$
F_s(t)=F_{s1}(t)+F_{s2}(t),\qquad F_0(t)=\alpha F(t).
$$

En la analogía eléctrica, $F_s$ corresponde al voltaje del capacitor $C_p$. Se utiliza $i(t)$ para identificar las corrientes del circuito y distinguirlas del desplazamiento $x(t)$.

**Primera contribución: fuente $F(t)$ activa y fuente $F_0(t)$ anulada.**

Al anular la fuente ideal de voltaje $F_0(t)$ se sustituye por un cortocircuito. La ley de corrientes establece:

$$
i(t)=i_s(t)+i_R(t).
$$

Las relaciones de cada rama son:

$$
i(t)=C_p\frac{dF_{s1}(t)}{dt},
$$

$$
i_s(t)=C_s\frac{d[F(t)-F_{s1}(t)]}{dt},\qquad
i_R(t)=\frac{F(t)-F_{s1}(t)}{R}.
$$

Por sustitución:

$$
C_p\frac{dF_{s1}(t)}{dt}
=C_s\frac{d[F(t)-F_{s1}(t)]}{dt}
+\frac{F(t)-F_{s1}(t)}{R}.
$$

**Segunda contribución: fuente $F_0(t)$ activa y fuente $F(t)$ anulada.**

Con la fuente externa sustituida por un cortocircuito, los capacitores quedan en paralelo y su capacitancia equivalente es:

$$
C_{\mathrm{eq}}=C_p+C_s.
$$

Con la polaridad del circuito dibujado, la fuente equivalente es $-F_0(t)$. La ecuación de esta contribución es:

$$
R(C_p+C_s)\frac{dF_{s2}(t)}{dt}+F_{s2}(t)=-F_0(t).
$$

Las contribuciones se calculan tratando primero ambas entradas por separado; después se impone la relación $F_0(t)=\alpha F(t)$.

**Ecuación diferencial total.**

Al sumar ambas contribuciones se obtiene:

$$
R(C_p+C_s)\frac{dF_s(t)}{dt}+F_s(t)
=RC_s\frac{dF(t)}{dt}+(1-\alpha)F(t).
$$

Este desarrollo conserva el resultado final de los cálculos proporcionados y presenta las ecuaciones intermedias con una notación uniforme.

### 4. Obtención de las funciones de transferencia

El procedimiento comprende aplicar la transformada de Laplace con condiciones iniciales nulas, sustituir las relaciones entre las variables internas y despejar el cociente entre salida y entrada. Se obtiene una expresión general en función de $R$, $C_p$, $C_s$ y $\alpha$.

Posteriormente se sustituyen por separado los parámetros de las dos condiciones:

$$
G_{\mathrm{control}}(s)=\frac{X_{\mathrm{control}}(s)}{F(s)},\qquad
G_{\mathrm{caso}}(s)=\frac{X_{\mathrm{caso}}(s)}{F(s)}.
$$

El numerador y el denominador de cada función deben registrarse para utilizarlos en los bloques de Simulink y en la implementación de Python. Las expresiones particulares deben proceder del desarrollo del modelo, no de un ajuste arbitrario de las gráficas.

#### 4.1. Transformada de Laplace de la primera contribución

Con condiciones iniciales nulas:

$$
C_p sF_{s1}(s)=C_s s[F(s)-F_{s1}(s)]
+\frac{F(s)-F_{s1}(s)}{R}.
$$

Agrupando los términos de salida:

$$
\left[(C_p+C_s)s+\frac{1}{R}\right]F_{s1}(s)
=\left(C_s s+\frac{1}{R}\right)F(s).
$$

Multiplicando por $R$ y despejando:

$$
F_{s1}(s)=\frac{RC_s s+1}{R(C_p+C_s)s+1}F(s).
$$

#### 4.2. Transformada de Laplace de la segunda contribución

La ecuación de la segunda contribución se transforma en:

$$
[R(C_p+C_s)s+1]F_{s2}(s)=-F_0(s).
$$

Por tanto:

$$
F_{s2}(s)=-\frac{F_0(s)}{R(C_p+C_s)s+1}
=-\frac{\alpha F(s)}{R(C_p+C_s)s+1}.
$$

#### 4.3. Suma de las contribuciones y función de transferencia

Aplicando superposición:

$$
F_s(s)=F_{s1}(s)+F_{s2}(s)
=\frac{RC_s s+1}{R(C_p+C_s)s+1}F(s)
-\frac{\alpha}{R(C_p+C_s)s+1}F(s).
$$

Se obtiene el resultado final del PDF:

$$
\boxed{\frac{F_s(s)}{F(s)}
=\frac{RC_s s+1-\alpha}{R(C_p+C_s)s+1}}.
$$

#### 4.4. Relación con el desplazamiento de salida

La función anterior tiene como salida $F_s$, no directamente el desplazamiento. Como la carga de $C_p$ representa el desplazamiento y satisface $q_p=C_pF_s$, en las variables equivalentes se cumple:

$$
X(s)=C_pF_s(s).
$$

Así, la función de transferencia definida en esta práctica para el desplazamiento es:

$$
\boxed{G(s)=\frac{X(s)}{F(s)}
=C_p\frac{RC_s s+1-\alpha}{R(C_p+C_s)s+1}}.
$$

Esta conversión permite comparar la misma salida entre el modelo matemático, la función de transferencia y el circuito eléctrico. Los valores eléctricos representan variables equivalentes; no deben interpretarse automáticamente como desplazamientos físicos en metros sin una escala de conversión.

#### 4.5. Sustitución de los parámetros del control y del caso

Usando $C_p=100\times10^{-6}$ F, $C_s=10\times10^{-6}$ F y $\alpha=0.25$:

| Condición | $R$ | $RC_s$ | $R(C_p+C_s)$ |
| --- | --- | --- | --- |
| Control | 100 Ω | 0.001 s | 0.011 s |
| Caso | 10 000 Ω | 0.1 s | 1.1 s |

Para la salida $F_s$:

$$
\frac{F_{s,\mathrm{control}}(s)}{F(s)}
=\frac{0.001s+0.75}{0.011s+1},\qquad
\frac{F_{s,\mathrm{caso}}(s)}{F(s)}
=\frac{0.1s+0.75}{1.1s+1}.
$$

Para la salida de desplazamiento equivalente:

$$
G_{\mathrm{control}}(s)
=\frac{1\times10^{-7}s+7.5\times10^{-5}}{0.011s+1},
$$

$$
G_{\mathrm{caso}}(s)
=\frac{1\times10^{-5}s+7.5\times10^{-5}}{1.1s+1}.
$$

Las sustituciones numéricas y la conversión a desplazamiento complementan el desarrollo manuscrito. No corresponden a resultados de simulación ni a una sintonización del PID.

#### 4.6. Evidencia de los cálculos manuscritos

**Hoja 1. Circuito equivalente y separación por superposición.**

![Circuito equivalente y superposición](imagenes/calculos-1.png)

**Hoja 2. Ecuaciones del circuito y primera contribución.**

![Ecuaciones y transformada de Laplace](imagenes/calculos-2.png)

**Hoja 3. Segunda contribución y función de transferencia final.**

![Suma de contribuciones y función de transferencia](imagenes/calculos-3.png)

### 5. Error en estado estacionario

Se utiliza una entrada adecuada para estudiar el comportamiento final, por ejemplo un escalón. Esta prueba es distinta del análisis al impulso solicitado para comparar la dinámica.

Si se cumplen las condiciones del teorema del valor final:

$$
x(\infty)=\lim_{s\to0}sX(s).
$$

La diferencia final entre control y caso se expresa como:

$$
e_{\mathrm{ss}}=x_{\mathrm{control}}(\infty)-x_{\mathrm{caso}}(\infty).
$$

Se debe comprobar si la modificación de $R$ cambia el valor final, la evolución temporal o ambos. Una diferencia durante el transitorio no significa necesariamente que exista un error permanente.

### 6. Estabilidad del sistema

Los polos se calculan a partir de las raíces del denominador de cada función de transferencia. Para un sistema continuo racional, los polos en el semiplano izquierdo corresponden a modos que decaen; los polos en el semiplano derecho indican inestabilidad. Los polos sobre el eje imaginario requieren un análisis adicional.

La comparación debe incluir la ubicación de los polos y su relación con la rapidez de respuesta. También debe revisarse la estabilidad después de incorporar el controlador, porque la estabilidad de la planta por sí sola no garantiza la estabilidad del lazo cerrado.

### 7. Implementación en MATLAB, Simulink y Simscape Electrical

| Representación | Construcción | Verificación principal |
| --- | --- | --- |
| Ecuaciones del sistema | Integradores, ganancias y sumadores en Simulink | Correspondencia entre cada bloque y la ecuación que representa. |
| Función de transferencia | Bloques Transfer Fcn para control y caso | Coeficientes y orden de los polinomios. |
| Circuito equivalente | Fuentes, resistencia y capacitores en Simscape Electrical | Conexiones, referencia eléctrica y medición de la salida equivalente. |

Las implementaciones deben utilizar los mismos parámetros y condiciones iniciales. La salida también debe representar la misma magnitud: si el desplazamiento corresponde a carga eléctrica, una medición directa de corriente o voltaje no puede compararse como desplazamiento sin la transformación correspondiente.

### 8. Respuesta en lazo abierto

Se aplica un impulso unitario y se estudia la respuesta entre 0 y 10 segundos. En esta etapa no se incluye el controlador. Las dos condiciones reciben la misma entrada para observar el efecto del cambio de resistencia.

En una simulación temporal que aproxime el impulso mediante un pulso rectangular, el producto de amplitud por duración debe ser igual a uno. La duración y el paso temporal deben documentarse para que la comparación sea reproducible.

Se comparan la amplitud, la duración del transitorio y la rapidez con que disminuye la respuesta. Los indicadores habituales de respuesta al escalón no deben trasladarse automáticamente a una respuesta al impulso.

### 9. Construcción del sistema de control

La salida del individuo sano se toma como referencia $r(t)$. Esta referencia se compara con la salida del caso controlado $y(t)$ mediante un sumador con realimentación negativa:

$$
e(t)=r(t)-y(t).
$$

El PID recibe el error y genera la señal aplicada al modelo del caso. Se conserva también una rama con el caso en lazo abierto para comparar las tres respuestas bajo una misma entrada externa.

### 10. Sintonización del controlador PID

La forma ideal del controlador se escribe como:

$$
C(s)=k_P+\frac{k_I}{s}+k_Ds.
$$

| Acción | Función principal | Aspecto que se debe vigilar |
| --- | --- | --- |
| Proporcional | Actúa según el error presente. | Una ganancia excesiva puede deteriorar la respuesta. |
| Integral | Acumula el error en el tiempo. | Puede aumentar el sobreimpulso o el tiempo de recuperación. |
| Derivativa | Responde a la variación del error. | Es sensible a variaciones rápidas y requiere considerar el filtrado. |

Se emplea la herramienta **Tune** y se registran las ganancias obtenidas. Si el bloque utiliza filtro derivativo, también se documenta su parámetro para reproducir el mismo controlador en Python.

| Parámetro | Valor obtenido |
| --- | --- |
| $k_P$ | Pendiente de sintonización. |
| $k_I$ | Pendiente de sintonización. |
| $k_D$ | Pendiente de sintonización. |
| Filtro derivativo, si aplica | Pendiente de registrar. |

### 11. Respuesta en lazo cerrado

Para realimentación unitaria negativa, la transferencia desde la referencia hasta la salida controlada es:

$$
\frac{Y(s)}{R_{\mathrm{ref}}(s)}=
\frac{C(s)G_{\mathrm{caso}}(s)}{1+C(s)G_{\mathrm{caso}}(s)}.
$$

Aquí $R_{\mathrm{ref}}(s)$ representa la transformada de la referencia, no la resistencia. Como la referencia se genera mediante el modelo sano, la transferencia desde la entrada externa hasta la salida controlada incluye además $G_{\mathrm{control}}(s)$.

En una misma gráfica se representan $x_{\mathrm{control}}(t)$, $x_{\mathrm{caso}}(t)$ y $x_{\mathrm{PID}}(t)$. Se evalúa si el controlador reduce la diferencia respecto a la referencia sin introducir una respuesta inestable.

### 12. Cuaderno computacional de MATLAB

El cuaderno debe organizar los parámetros, ejecutar las simulaciones, recuperar las señales del Workspace y generar las figuras. Se recomienda separar la configuración de los modelos de la función encargada de graficar.

Cada figura debe identificar el tiempo en segundos, la variable de salida, sus unidades o su escala equivalente, y las condiciones comparadas. Las figuras se exportan en PDF con nombres que permitan distinguir control, caso y sistema controlado.

### 13. Implementación en Python

Se reproducen las funciones de transferencia del control y del caso, se calcula la respuesta al impulso y se incorpora el controlador con las mismas ganancias utilizadas en Simulink.

La implementación debe conservar el intervalo de simulación, los parámetros, la definición de la salida y la estructura de realimentación. Si existen diferencias de muestreo, las señales deben compararse en tiempos compatibles antes de calcular errores numéricos.

### 14. Verificación cruzada

| Comparación | Coincidencia esperada |
| --- | --- |
| Ecuaciones y función de transferencia en Simulink | Misma dinámica bajo condiciones iniciales nulas. |
| Simulink y Simscape Electrical | Respuestas equivalentes después de convertir correctamente las variables. |
| MATLAB y Python | Respuestas consistentes con los mismos modelos y entradas. |
| PID en Simulink y Python | Misma realimentación, ganancias y tratamiento del término derivativo. |

Las posibles diferencias se revisan considerando unidades, signos, coeficientes, paso temporal, método numérico, aproximación del impulso y filtrado derivativo. La coincidencia visual se complementa con una medida numérica cuando los datos estén disponibles.

### 15. Interpretación del diagrama biológico

El diagrama relaciona el elemento contráctil con la generación de fuerza, el tendón con la elasticidad en serie, el tejido conectivo con la elasticidad pasiva en paralelo y el comportamiento viscoso con la resistencia interna al movimiento.

Es una representación simplificada: cada componente agrupa propiedades de varias estructuras. Por ello, la equivalencia ayuda a interpretar el modelo, pero no describe de manera completa toda la anatomía ni todos los mecanismos de la contracción muscular.

<p align="center">
  <img src="imagenes/diagrama_pdf-000.png" alt="Diagrama biológico del sistema musculoesquelético: fuerza activa muscular, tendones y componentes viscosos y elásticos" width="1000">
</p>

*Figura 2. Diagrama biológico del sistema musculoesquelético incluido en el PDF.*

### 16. Documentación y resguardo

El repositorio debe reunir el desarrollo matemático, los modelos, el código, las figuras, el diagrama y los parámetros del controlador. El README funciona como documento central para explicar el objetivo, el procedimiento y la interpretación de las simulaciones.

El archivo CITATION.cff debe identificar al autor y al repositorio. También deben conservarse las versiones de los archivos utilizadas para generar las figuras finales.

## Resultados y evidencias

Los materiales disponibles contienen el instructivo, los diagramas biológicos y los cálculos manuscritos del modelo matemático y la función de transferencia. No incluyen las simulaciones ni las ganancias del PID; por ello, los resultados experimentales se dejan identificados para completarse con las evidencias reales.

| Evidencia | Información que debe incorporarse | Estado |
| --- | --- | --- |
| Circuito equivalente | Esquema manuscrito, superposición y parámetros. | Incluido; implementación en Simscape pendiente. |
| Desarrollo matemático | Ecuaciones, superposición, transformada de Laplace y funciones de transferencia. | Incluido. |
| Estabilidad | Polos del control, del caso y del lazo cerrado. | Pendiente. |
| Estado estacionario | Entrada empleada, valores finales y error. | Pendiente. |
| Lazo abierto | Gráficas al impulso para control y caso. | Pendiente. |
| Sintonización | Ganancias y captura de Tune. | Pendiente. |
| Lazo cerrado | Comparación del control, caso y caso con PID. | Pendiente. |
| Verificación cruzada | Comparación entre las implementaciones. | Pendiente. |
| Diagrama biológico | Imagen e interpretación de sus componentes. | Incluido. |

## Discusión

La discusión debe explicar el efecto observado al aumentar $R$ de 100 Ω a 10 kΩ, manteniendo constantes los demás parámetros. Se debe distinguir entre cambios en la respuesta transitoria y cambios en el valor final.

También debe analizarse si el PID mejora el seguimiento y qué compromisos aparecen entre rapidez, amplitud y estabilidad. La comparación entre herramientas permite detectar si una diferencia proviene del modelo o de su implementación numérica.

El caso de atrofia muscular es una condición simulada mediante un cambio de parámetro. No equivale a una validación clínica del modelo ni permite generalizar resultados a todos los pacientes con atrofia.

## Conclusiones

El modelo permite relacionar las propiedades contráctiles, elásticas y viscosas del sistema musculoesquelético con elementos eléctricos y ecuaciones dinámicas. La analogía fuerza–voltaje proporciona una base para estudiar distintas representaciones del mismo sistema.

Las conclusiones sobre la diferencia entre control y caso y sobre la eficacia del PID deben establecerse después de obtener y verificar las simulaciones. Con los materiales disponibles se documentan el planteamiento, los parámetros y el procedimiento, sin atribuir resultados numéricos que aún no se han aportado.

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
11. Diagrama biológico del sistema musculoesquelético [imagenes/sistema_musculoesqueletico.png].
12. Archivos complementarios utilizados durante la práctica.
13. Archivo CITATION.cff con la información del alumno y del repositorio.

## Referencias

\[1] P. A. Valle, *Syllabus para Modelado de Sistemas Fisiológicos*, Tecnológico Nacional de México / Instituto Tecnológico de Tijuana, Tijuana, B.C., México, 2025. https://biomath.xyz/course/

\[2] *Práctica 5.5: Modelado y control del sistema musculoesquelético*, instructivo proporcionado, pp. 87–94.

\[3] M. C. Khoo, *Physiological Control Systems: Analysis, Simulation, and Estimation*, 2nd ed., IEEE Press, 2018.

\[4] F. C. Hoppensteadt y C. S. Peskin, *Modeling and Simulation in Medicine and the Life Sciences*, Springer.

\[5] J. E. Hall, *Guyton and Hall Textbook of Medical Physiology*, 14th ed., Elsevier, 2021.
