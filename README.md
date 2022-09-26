<h1 align="center">Emulador Gocator</h1>



<p id="ejemploGocator">
</p>


## Ejemplo de emulación del Gocator
- Se da doble click sobre el ejecutable

<div align="center">
    <img src="imagenesReadme\ejecutable.png"><img>
    <p align="center"><b>Figura 1.</b> Ejecutable</p>
</div>

Dicho software se puede encontrar en la ubicación 
 
    PAE/PAE Unalmed 2021/Clase 12-Sistemas 3D/laboratorio

- Se elige la referencia que se quiere usar, en este caso se elegirá la 2340 porque es uno de los gocator que tiene el porta instrumentos del proyecto de cotas geometricas

<div align="center">
    <img src="imagenesReadme\2340.png"><img>
    <p align="center"><b>Figura 2.</b> Referencia 2340</p>
</div>

- El emulador ya tiene algunos tools abiertos, por motivos pedagogicos se eliminaran, para <i>"empezar de cero"</i>, como dice la canción

<div align="center">
    <img src="imagenesReadme\borrandoTools.png"><img>
    <p align="center"><b>Figura 3.</b> Borrando tools</p>
</div>

- Se añaden dos herrameintas, para el ejemplo usaremos <i>Profile circle</i> y <i>script</i>

<div align="center">
    <img src="imagenesReadme\addTool.png"><img>
    <p align="center"><b>Figura 4.</b> Añadiendo tools</p>
</div>

Se debe verificar que la ROI(region de interés) encierre la circunferencia a medir

<div align="center">
    <img src="imagenesReadme\regionDeInteres.png"><img>
    <p align="center"><b>Figura 4.</b> Region de interes, rectángulo amarillo</p>
</div>

Algunos parametros a tener en cuenta son el nombre de la herramienta que en este caso es "Profile Circle", sin embargo, lo podemos cambiar libremente; y el otro es el del nombre de los parametros que nos va a entregar la herramienta, los cuales, son seleccinadas por el usuario y que en este caso serán la coordenada horizontal llamada "X" y el radio llamado "Radius". Estos nombres son importantes pues se van a usar dentro del codigo.
Para poder seleccionar los parametros, se debe dar doble click sobre la herramienta. La posibilidad de cambiar los nombres tanto de la herramienta como de los parametros a medir es para evitar confusiones en el codigo cuando se usan varias herramientas con parametros similares.

<div align="center">
    <img src="imagenesReadme\nombresParametros.png"><img>
    <p align="center"><b>Figura 5.</b> Nombre de la herrameinta y de los parametros a medir</p>
</div>

- Se inicializan las variables relacionadas a la herramienta y los parametros a medir

<div align="center">
    <img src="imagenesReadme\inicializaVariables.png"><img>
    <p align="center"><b>Figura 6.</b> Variables relacionadas a la herrameinta y los parametros</p>
</div>

Se agrega un if para verificar que existan dicha herrmaienta y dichos parametros; luego, dentro del mismo se lee el id de que corresponde a X, el cual, nos premite acceder al valor medido mediante el metodo Measurement_Value. Finalmente, se muestra el valor medido, especificando el indice de la salida(Output), especificando el indice de dicha salida que en este caso es 0, pues solo hay un "Output", en caso de haber mas sus indices serán 0,1,2,... en el orden en que se van agregando.


    if (Measurement_NameExists(toolName, measurementName))
    {
    int id_x = Measurement_Id(circulo, coordenada_horizontal);
    Output_SetAt(0, Measurement_Value(id_x), 1);
    }
    else
    {
    Output_SetAt(0, 0, 0);
    }
 
 
<div align="center">
    <img src="imagenesReadme\salidaValue.png"><img>
    <p align="center"><b>Figura 7.</b> Variable visualizada exitosamente</p>
</div>


    if (Measurement_NameExists(toolName, measurementName)) 
    {
    int id_x = Measurement_Id(circulo, coordenada_horizontal);
    Output_SetAt(0, Measurement_Value(id_x), 1);
    }
    else
    {
    Output_SetAt(0, 0, 0);
    }



    if (Measurement_NameExists(circulo, Radius)) 
    {
    int id_r = Measurement_Id(circulo, Radius);
    Output_SetAt(0, Measurement_Value(id_r), 1);
    }
    else
    {
    Output_SetAt(0, 0, 0);
    }


Se repite el proceso para una segunda variable. Se crea la variable a partir del parametro "Radius", se pone un if para verificar la existencia tanto de la herrameinta como del parametro, se detecta el id de este nuevo parametro y se pone en el display el valor medido con el metodo <i>Measurement_Value</i>.

<div align="center">
    <img src="imagenesReadme\salidaValue1.png"><img>
    <p align="center"><b>Figura 7.</b> Segunda variable visualizada exitosamente</p>
</div>

 Es importante a tener en cuenta que no se permite reasignar los valores a las variables. Por ejemplo, si en vez de usar dos "ids", id_x e id_r, se usara id dos veces, el codigo va llevar a errores en la vizualizacion de las variables.

 
    if (Measurement_NameExists(toolName, measurementName))
    {
    int id = Measurement_Id(circulo, coordenada_horizontal);
    Output_SetAt(0, Measurement_Value(id), 1);
    }
    else
    {
    Output_SetAt(0, 0, 0);
    }
 


    if (Measurement_NameExists(circulo, Radius)) 
    {
    int id = Measurement_Id(circulo, Radius);
    Output_SetAt(0, Measurement_Value(id), 1);
    }
    else
    {
    Output_SetAt(0, 0, 0);
    }
 

<div align="center">
    <img src="imagenesReadme\salidaValueMal.png"><img>
    <p align="center"><b>Figura 8.</b> Error en visualización de variables por reasignación de "ids"</p>
</div>
