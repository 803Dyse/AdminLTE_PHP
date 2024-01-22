# AdminLTE PHP
//Apuntes explicando la lógica del programa.

hacemos un 
<th><a href="/usuarios/order=1">nombre de usuario</a></th>
y asi con todos los campos

comprobar que hay un valor entre 1 y 5
si recibimos un valor que no sea correcto, el order será por el campo numero 1

if($order < 1 && $order > 5){
    valor invalido, se filtrará pro defecto en 1.
} else {
    $order = filtros['order'];
}

asumos que si no recibimos un order, ordenamos por la 1 columna.
asumimos que dentro de filtros(){} recibimos order, en esa query del metodo.


creamos una constante de tipo array que almacena cada campo de la tabla de forma ordenada, y entonces como los array se cuentan desde 0, campo 1, que es el primero, seria 0, por lo cual restamos 1 a cada posicion del array, ten esto en cuenta.

En la vista queremos indicar cual columna se esta organizando, para detectar esto y mostrarlo en la vista, tenemos actualmente una constante que detecta y indica esto, pero esa constante es privada, entonces para poder pasar esta informacion de limite de columnas, sin usar el array, crearemos una funcion publica que ya nos dice el limite. 
    En resumen, creamos una funcion para no utilizar la constante "ORDER_ARRAY", ya que es privada, y ponerla publica no es una opción.
    Para esto, recurrimos a crear una funcion que nos indica esto.
    Esta funcion además puede ser estatica, porque solo accede a un atributo.

    La funcion se llamara "getMaxColumnOrder();"

Ahora la problematica es lograr que una vez pulsado y ordenado en ASC, que a la segunda vez ordene en DESC, y vice versa.


La funcion

Esta funcion es necesaria porque necesitamos pasar el sentido para los order, ya que queremos que el filtro funcione como una pila. 1 click, ordena asc, el proximo click, desc, y el proximo asc, y asi por delante.
La funcion que utilizaremos será "getSentido()".
Esta funcion simplemente retornara diciendo:
     si $order es mayor o igual que 0, que diga:
        true = 'asc' (retorna asc)
        false = 'desc'(retorna desc)

Utilizaremos el "<input type="hidden" value=""> para meterlo justo cuando abrimos la etiqueta form para guardar los valores de la variable "$order", por que queremos esto?
Porque ahora si hacemos un filtro en los campos de rellenar, cuando aplicamos estos filtros y utilizamos la ordenacion por click de campos, nos resetea el filtrado.

Para solucionar esto, guardamos el estado actual del order pasando a la url como primer valor. Para lograr esto lo que se hace es utilizar el input hidden dando estos valores.
