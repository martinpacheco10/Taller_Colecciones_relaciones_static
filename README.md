# Taller_Colecciones_relaciones_static
# Taller Java - Playlist y Parqueadero

## Parte A - Playlist

Los paquetes musica.modelo y musica.app contienen las clases solicitadas. La clase Playlist limita la lista a tres canciones, evita agregar canciones nulas o repetidas, permite buscar títulos sin importar mayúsculas y elimina canciones recorriendo la lista desde el final.

## Parte B - Parqueadero

La clase Puesto tiene un constructor con acceso de paquete, por lo que solamente las clases del paquete parqueadero.modelo pueden crear puestos.

La clase Parqueadero administra sus puestos y cuenta los ingresos de vehículos mediante un atributo static, que permite compartir el contador entre todos los parqueaderos.

## Parte C - Retos y respuestas

### 1. Eliminar con for-each

La versión eliminarArtistaConForEach está incluida para provocar la excepción ConcurrentModificationException.

Esta excepción ocurre porque el ciclo for-each utiliza internamente un iterador y se modifica directamente la estructura del ArrayList mediante remove(), invalidando ese iterador.

La solución correcta es recorrer la lista con un índice desde el final, como se hace en el método eliminarArtista().

### 2. Método cancionMasLarga()

Devuelve la canción que tiene la mayor duración. Si la lista está vacía, devuelve null.

Este método está implementado en la clase Playlist.

### 3. Método getCanciones()

Devuelve una copia de la lista utilizando:

new ArrayList<>(canciones)

Por esta razón, ejecutar clear() sobre la copia no elimina los elementos de la lista original.

### 4. Crear un Puesto desde parqueadero.app

Al intentar crear un objeto Puesto desde parqueadero.app aparece un error de compilación 
Puesto(int) is not public in Puesto; cannot be accessed from outside package

Esto sucede porque el constructor tiene acceso de paquete.

Esta restricción protege la composición, ya que los puestos son creados y administrados directamente por la clase `Parqueadero`.

### 5. Predicción del ArrayList

**Código analizado:**

```java
ArrayList<Cancion> lista = new ArrayList<>();

Cancion x = new Cancion("A", "Uno", 100);

lista.add(x);
lista.add(x);
lista.add(new Cancion("A", "Uno", 100));

System.out.println(lista.size());
System.out.println(lista.get(0) == lista.get(1));
System.out.println(lista.get(0) == lista.get(2));

lista.remove(x);

System.out.println(lista.size());
System.out.println(lista.contains(x));
```

**Salida esperada:**

```text
3
true
false
2
true
```

**Explicación:**

Las dos primeras posiciones guardan referencias al mismo objeto x. El tercer elemento es un objeto diferente, aunque tiene los mismos datos.

Cuando se ejecuta remove(x), se elimina la primera coincidencia del objeto x. Por eso quedan dos elementos y contains(x) sigue devolviendo true.

## Preguntas

### 1. ¿Por qué ArrayList<int> no compila y ArrayList<Integer> sí?

Los genéricos de Java trabajan con tipos de referencia y no con tipos primitivos. Integer es la clase envolvente de int. Java utiliza autoboxing y unboxing cuando es necesario.

### 2. ¿Por qué eliminar a Nevado de Favoritas no lo eliminó de Viaje? ¿Qué relación muestra eso?

Cada playlist tiene su propio ArrayList. Eliminar una canción de Favoritas no significa eliminarla de Viaje. Esto demuestra una relación de agregación, porque una canción puede existir y compartirse entre diferentes playlists.

### 3. ¿Qué diferencia hay entre Playlist-Cancion y Parqueadero-Puesto?

La relación Playlist-Cancion es de agregación, porque las canciones pueden existir independientemente de una playlist y compartirse entre varias.

La relación Parqueadero-Puesto es de composición, porque los puestos son creados y administrados por el parqueadero como partes propias.

### 4. ¿Por qué totalCanciones debe ser static y titulo no?

totalCanciones debe ser static porque cuenta todas las canciones creadas y su valor es compartido por la clase.

En cambio, titulo pertenece a cada canción y puede ser diferente en cada objeto.

### 5. ¿Por qué un método static no puede usar this?
this representa el objeto actual. Un método static pertenece a la clase y puede ejecutarse sin crear un objeto. Por esta razón, no tiene un objeto actual al cual hacer referencia mediante `this`.

## Diagramas y archivos

El proyecto incluye dos diagramas de clases:

- Diagrama de Playlist en formato PNG.
- Diagrama de Parqueadero en formato PNG.

También se incluyen los archivos editables .drawio

Los miembros static están identificados en los diagramas. Se debe utilizar el subrayado correspondiente a la notación UML cuando sea necesario.

ión, composición y métodos static.
