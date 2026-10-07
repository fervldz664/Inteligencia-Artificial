# Árboles de decisión y redes neuronales multicapa

Apuntes de Inteligencia Artificial — 7 de octubre de 2026

## Parte I. Conceptos básicos

### Pregunta 1. ¿Qué es un árbol de decisión y cuál es su objetivo principal dentro de un problema de clasificación?

**Respuesta:** Es un modelo que utiliza preguntas o condiciones sobre los datos para llegar a un resultado. En clasificación, su objetivo es asignar un caso a una categoría, como «compra normal» o «posible fraude».

Por ejemplo, puede revisar la asistencia y las calificaciones de un estudiante para clasificarlo como «con riesgo» o «sin riesgo de reprobar». Las condiciones se aprenden a partir de ejemplos.

### Pregunta 2. Explique con sus propias palabras los siguientes elementos de un árbol de decisión: nodo raíz, nodo interno, rama y hoja.

**Respuesta:**

| Elemento | Significado | Ejemplo ilustrativo |
|---|---|---|
| Nodo raíz | Primera condición que se revisa. Es el inicio del árbol. | ¿La asistencia es menor al 80 %? |
| Nodo interno | Otra condición que ayuda a separar los casos. | ¿El promedio es menor a 6? |
| Rama | Camino que se sigue según el resultado de una condición. | Sí o no. |
| Hoja | Resultado final de un recorrido. | Estudiante con riesgo de reprobar. |

Los números del ejemplo son inventados para explicar la estructura; no son reglas escolares universales.

### Pregunta 3. ¿Qué es una red neuronal multicapa y qué función cumplen la capa de entrada, la capa oculta y la capa de salida?

**Respuesta:** Es un modelo formado por neuronas artificiales conectadas y organizadas en capas. Aprende a relacionar datos de entrada con resultados mediante operaciones numéricas.

- **Capa de entrada:** recibe los datos, como asistencia, calificaciones y tareas entregadas.
- **Capa oculta:** combina y transforma la información para aprender relaciones entre las variables. Puede haber una o varias capas ocultas.
- **Capa de salida:** entrega la predicción, por ejemplo, una puntuación de riesgo de reprobar.

No piensa como una persona: realiza cálculos con los valores que aprendió durante el entrenamiento.

### Pregunta 4. ¿Qué representan los pesos y los sesgos dentro de una red neuronal? Explique también por qué sus valores cambian durante el entrenamiento.

**Respuesta:** Los pesos controlan cuánto influye cada entrada en una neurona y en qué sentido. El sesgo es un valor adicional que permite ajustar su respuesta.

Una neurona puede calcular:

`resultado previo = peso1 × entrada1 + peso2 × entrada2 + sesgo`

Después aplica una función de activación para transformar ese resultado.

Durante el entrenamiento se comparan las predicciones con las respuestas esperadas. Los pesos y sesgos se ajustan para reducir el error. La retropropagación calcula cómo contribuyen al error y el optimizador aplica los cambios.

Aquí «sesgo» significa un parámetro numérico; no significa, por sí mismo, discriminación. Además, un peso aislado no siempre indica la importancia total de una variable en toda la red.

### Pregunta 5. ¿Cuál es la principal diferencia entre la forma en que aprende un árbol de decisión y una red neuronal multicapa? Explique qué elementos aprende cada modelo.

**Respuesta:** El árbol aprende cómo dividir los datos mediante condiciones. La red aprende cómo combinar y transformar los datos ajustando valores numéricos.

| Modelo | ¿Qué aprende? |
|---|---|
| Árbol de decisión | Qué variable revisar en cada nodo, dónde dividir sus valores y qué resultado asignar a cada hoja. |
| Red neuronal multicapa | Los pesos y sesgos de sus conexiones y neuronas. |

En ambos casos, aprender significa encontrar relaciones útiles en los ejemplos para responder ante casos nuevos. Normalmente, quien desarrolla el modelo elige límites del árbol y la cantidad de capas y neuronas de la red.

## Parte II. Análisis y aplicación

### Pregunta 6. Detección de compras fraudulentas

**Planteamiento:** Una institución bancaria desea detectar posibles compras fraudulentas. Dispone del monto, la hora, la ciudad, el tipo de establecimiento, el número de compras realizadas durante el día y el historial de compras del cliente.

**Pregunta:** Analice las ventajas y desventajas de utilizar un árbol de decisión y una red neuronal multicapa. ¿Cuál utilizaría y por qué?

**Respuesta:**

| Modelo | Ventajas | Desventajas |
|---|---|---|
| Árbol de decisión | Permite entender por qué una compra fue marcada y facilita revisar las condiciones usadas. | Puede aprender demasiado los ejemplos de entrenamiento y fallar con compras nuevas; si crece mucho, se vuelve difícil de explicar. |
| Red neuronal multicapa | Puede aprender combinaciones complejas de monto, horario y hábitos del cliente. | Requiere preparar los datos y ajustar el entrenamiento; es más difícil explicar una alerta. |

**Mi elección:** Empezaría con un árbol de tamaño controlado para tener una solución fácil de revisar. Probaría también una red si hay suficientes compras etiquetadas como normales o fraudulentas. La elegiría si demuestra una mejora importante al detectar fraude sin producir demasiadas falsas alarmas.

No asumiría que la red es mejor solo por ser más compleja. Si 990 de 1,000 compras son normales, un sistema que diga «normal» en todas tendría 99 % de aciertos, pero no detectaría ningún fraude. Por eso revisaría cuántos fraudes detecta y cuántas compras normales marca por error.

Para entrenar, usaría únicamente el historial disponible antes de cada compra, sin incluir información del futuro.

### Pregunta 7. Estudiantes con riesgo de reprobar

**Planteamiento:** Una escuela conoce la asistencia, las calificaciones, las tareas entregadas, la participación y el número de materias reprobadas anteriormente. Un árbol y una red neuronal obtienen prácticamente la misma precisión.

**Pregunta:** ¿Qué otros factores tomaría en cuenta para elegir uno de los dos modelos? Justifique su respuesta.

**Respuesta:** Revisaría la facilidad para explicar las alertas, el costo de mantenimiento, los datos necesarios, la estabilidad de los resultados y si alguno perjudica más a ciertos grupos de estudiantes. También compararía los tipos de error: dejar pasar a un alumno que necesita apoyo no es lo mismo que dar una alerta innecesaria.

**Elegiría un árbol pequeño**, siempre que esos factores también sean aceptables, porque permite que docentes y estudiantes entiendan qué información llevó a la alerta y facilita planear apoyos.

El resultado serviría para ofrecer ayuda, no para decidir automáticamente una calificación ni asegurar que el estudiante reprobará. Una predicción de riesgo no demuestra la causa del problema.

### Pregunta 8. Atención prioritaria en un hospital

**Planteamiento:** Un hospital utiliza edad, temperatura, presión arterial, frecuencia cardiaca, síntomas y antecedentes médicos para determinar qué pacientes necesitan atención prioritaria. Una red neuronal obtiene mejores resultados que un árbol, pero es más difícil explicar sus respuestas.

**Pregunta:** ¿La mayor precisión es suficiente para elegir la red neuronal? Analice las consecuencias de esta decisión.

**Respuesta:** No. Antes de elegirla, comprobaría qué significa «mejores resultados» y qué errores comete. Un promedio de aciertos alto puede ocultar fallas en pacientes que realmente necesitan atención urgente.

- **Falso negativo:** el sistema no identifica a un paciente que necesita prioridad; podría retrasar su atención.
- **Falso positivo:** asigna prioridad a alguien que no la necesita; podría ocupar recursos y retrasar otros casos.

Revisaría especialmente la detección de casos urgentes, el desempeño en distintos grupos de pacientes y las pruebas con datos representativos del hospital. También se necesita un procedimiento para revisar errores y actuar cuando falten datos.

Elegiría la red solo si su mejora es relevante y está validada para ese uso, con supervisión del personal de salud. La dificultad para explicar sus respuestas puede complicar la revisión de errores. Un árbol comprensible tampoco garantiza decisiones correctas.

### Pregunta 9. Predicción de entregas tardías

**Planteamiento:** Una empresa considera distancia, tráfico, clima, hora, cantidad de pedidos y experiencia del repartidor. Para un pedido, el árbol indica «llegará a tiempo» y la red neuronal indica «probablemente llegará tarde».

**Pregunta:** ¿Cómo determinaría cuál realiza una mejor predicción? ¿Qué información adicional analizaría?

**Respuesta:** Antes de la entrega no se puede asegurar cuál acertará. Después compararía la hora real de llegada con la hora prometida, usando una definición clara de lo que cuenta como retraso.

Para elegir el mejor modelo en general, evaluaría muchos pedidos nuevos para ambos, preferentemente posteriores a los usados para entrenar. Un acierto en un pedido no demuestra superioridad.

Analizaría:

- El tráfico, clima y carga de trabajo disponibles al momento de predecir.
- Las probabilidades de ambos modelos y el límite usado para decir «tarde».
- Cuántos retrasos detectan y cuántas falsas alertas generan.
- Su desempeño en rutas, horarios y condiciones parecidas.
- Si una probabilidad del 70 % corresponde aproximadamente a un 70 % de retrasos entre muchos pedidos similares.
- El costo de no avisar de un retraso y el de avisar cuando no ocurre.

Si aparece nueva información, como un accidente, actualizaría la predicción. No usaría datos conocidos después de la entrega para evaluar una predicción hecha antes.

### Pregunta 10. Decisiones sobre créditos

**Planteamiento:** Una empresa tiene un árbol de decisión que explica claramente los rechazos y una red neuronal multicapa con mejores resultados de predicción, pero más difícil de explicar.

**Preguntas:** ¿Cuál utilizaría? ¿Qué ventajas y riesgos tendría su elección? ¿Consideraría posible utilizar ambos dentro del mismo sistema?

**Respuesta:** Para este ejercicio, empezaría con un árbol de tamaño controlado como modelo principal, siempre que su desempeño sea suficiente y sus errores sean aceptables. La posibilidad de revisar y explicar un rechazo tiene mucho valor para una decisión que afecta a una persona.

**Ventajas:** Facilita revisar cada decisión, detectar condiciones inadecuadas y explicar qué datos influyeron en el rechazo.

**Riesgos:** Puede omitir relaciones complejas, rechazar personas que podrían pagar o aprobar créditos de alto riesgo. Además, puede reproducir desigualdades de los datos; ser comprensible no lo vuelve automáticamente justo.

**Sí usaría ambos si la combinación demuestra utilidad.** Por ejemplo, el árbol produciría una primera evaluación y la red aportaría una segunda estimación. Las discrepancias o los casos dudosos pasarían a revisión humana, con reglas claras sobre quién toma la decisión final.

Compararía esta combinación con cada modelo por separado. No presentaría la explicación del árbol como si fuera la explicación exacta de la red: pueden llegar a una respuesta similar por razones diferentes. Si la ventaja de la red fuera muy grande, reconsideraría la elección después de evaluar sus errores y mecanismos de revisión.

> Idea para recordar: un árbol aprende condiciones; una red aprende pesos y sesgos. Para elegir, también importan los errores, la explicación y las consecuencias de la decisión.
