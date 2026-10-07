# Apuntes de clase — Red neuronal y juego de pelotas

**Inteligencia Artificial · 6 de octubre de 2026**

## Ejemplo del juego

Un muñeco dentro de un escenario debe esquivar pelotas. Primero una, después dos y luego tres. La idea es usar las mismas variables y cambiar la cantidad de pelotas presentes.

## ¿Cómo detectar una colisión?

- Tomar el centro del muñeco y el de la pelota.
- Considerar el tamaño de ambos, no solo su posición.
- Una opción sencilla: representar a los dos con círculos.
- Hay choque cuando la distancia entre sus centros es menor o igual a la suma de sus radios.

**Ejemplo:** si los radios son 10 y 15, hay contacto cuando los centros están a 25 unidades o menos.

Detectar el choque nos dice si ya se tocaron. Para esquivarlo, también necesitamos saber hacia dónde se mueve la pelota.

## Variables que importan

- Posición del muñeco: coordenadas **x, y**.
- Posición de cada pelota.
- Distancia y lado en el que está la pelota respecto al muñeco.
- Velocidad y dirección de las pelotas.
- Límites del escenario: cuánto espacio queda para moverse.
- Tamaño del muñeco y las pelotas; pueden mantenerse fijos.

**Ojo:** una pelota cercana que se aleja puede ser menos peligrosa que una que viene directamente hacia el muñeco.

## Reducción de la dimensionalidad

Cada característica que recibe la red cuenta como una dimensión. No se refiere a que el juego sea 2D o 3D.

La idea es usar **los datos necesarios para decidir**, sin agregar información repetida.

Por ejemplo, podemos indicar cuánto está la pelota a la derecha, izquierda, arriba o abajo del muñeco. Con esas diferencias también podemos calcular la distancia.

Usar solo la distancia no basta: no nos dice de qué lado viene ni si se está acercando.

## ¿Qué aprende la red?

Busca patrones en los ejemplos con los que se entrena para relacionar una situación con un movimiento.

**Ejemplo:** una pelota se acerca por la derecha y hay espacio arriba. Subir podría servir, siempre que no haya otra pelota en ese camino.

- **Entrada:** información del muñeco, las pelotas y el espacio disponible.
- **Procesamiento:** la red combina esos datos según lo aprendido.
- **Salida:** movimiento que elige hacer.

Con dos o tres pelotas debe considerar todas. No sirve esquivar una y chocar con otra. Se puede reservar desde el inicio un espacio de datos para cada una e indicar cuáles están presentes.

## Función de activación

En el apunte aparece “función de actividad”; probablemente se refiere a **activación**.

Es una función que transforma el resultado de una neurona antes de pasarlo a la siguiente. Forma parte de cómo la red procesa los datos.

**Ejemplo:** ReLU deja los números positivos como están y convierte los negativos en cero.

## ¿Cómo inicia el muñeco?

Una opción es colocarlo en el centro y comenzar quieto. Hay que comprobar que no aparezca encima de una pelota.

Su posición inicial es una cosa y los valores internos de la red son otra. La red necesita entrenamiento para aprender a esquivar.

**Pendiente de aclarar en clase:** a cuál de estos valores se refería el profesor al preguntar cómo debe iniciar.

## ¿Por qué se queda en las esquinas?

Puede aprender a quedarse ahí porque los ejemplos lo favorecen o porque las pelotas llegan menos a esa zona.

Si el objetivo es sobrevivir y la esquina es segura, quedarse ahí puede funcionar. Si queremos que también recorra el escenario, eso debe tomarse en cuenta al entrenarlo.

**Para recordar:** no basta con saber dónde está la pelota; también importa cómo se mueve y hacia dónde puede escapar el muñeco.
