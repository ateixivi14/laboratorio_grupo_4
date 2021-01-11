# laboratorio_grupo_4

La realización de este trabajo dio comienzo con la selección de la anomalía que sería eliminada. La anomalía que finalmente fue seleccionada fue Color Cast. Esta anomalía se basa en que la imagen sufre el defecto de encontrarse con una capa de un color constante encima de la misma, haciendo que la imagen se vea del color de la capa.

El segundo paso que se dió fue el de encontrar información y bibliografía interesante que nos ayudará a abordar la anomalía a solucionar. Para ello encontramos un artículo proveniente de Stanford (Su, n.d.) el cual nos sirvió de apoyo para empezar a desarrollar nuestro proyecto. Además, este ofrece imágenes de ejemplo antes y después de solucionar la anomalía, lo que nos servía de ayuda para poder  comparar sus resultados con los nuestros.

Basándonos en el artículo de Stanford (Su, n.d.), comenzamos realizando pruebas con la ecualización del histograma. Observando los resultados que eran arrojados, nos percatamos de que la ecualización de histograma añadía ruido a la imagen.  

Para solucionar este inconveniente implementamos un filtro de mediana para eliminar el ruido generado.  El resultado de este paso extra para eliminar el ruido lo comparamos con la aplicación de la función *fastNlMeansDenoisingColored* que se encuentra dentro del paquete CV2 para de esta manera tener una referencia para saber si nuestro filtro de mediana funcionaba correctamente. Los resultados que teníamos en este momento los podemos observar en la siguiente imagen. Como podemos ver, la imagen está demasiado suavizada y oscurecida. 


<p align="center">
  <img src="/memoria/2.png" width="500">
</p>

<p align="center">
  <img src="/memoria/1.png"  width="300">
 
</p>

 *Imagen 1: Histogramas del canal rojo y resultado hasta este punto tras aplicar la función ecualizacion_histograma y filtro_mediana (ver anexo para observar el código)* 
 
 Para solucionar este oscurecimiento, intentamos aplicar una transformación logarítmica (ver anexo función trasformacion_logaritmica). El resultado obtenido fue el siguiente:
 
 <p align="center">
  <img src="/memoria/3.png"  width="300">
</p>

*Imagen 2: Resultado de aplicar la transformación logarítmica en la imagen tras ser corregida por el filtro mediana y ecualizada.*


Así pues, viendo que el resultado de las funciones que implementamos estropeaba la imagen como podemos ver en la imagen 2, y habiendo comparado con las funciones predeterminadas  como  exposure.equalize_hist que se encuentra dentro del paquete skimage y ver que nuestro resultado no era del todo correcto, decidimos cambiar de estrategia y realizar un estiramiento del histograma en vez de una ecualización. 
Finalmente, implementamos la función *histogram_stretching*, la cual a partir de un porcentaje que se pasa como parámetro, calcula los percentiles y realiza una transformación pixel a pixel mediante las fórmulas:

 <p align="center">
  <img src="/memoria/4.png"  width="200">
</p>

Y posteriormente una saturación en la cual:

 <p align="center">
  <img src="/memoria/5.png"  width="300">
</p>
Con lo cual, obtuvimos los resultados que esperábamos y que podemos ver en el código principal.

**Referencias**

Su, J. (n.d.). Illuminant Estimation: Simplest Color Balance. Color Balancing Algorithms. https://web.stanford.edu/~sujason/ColorBalancing/simplestcb.html
