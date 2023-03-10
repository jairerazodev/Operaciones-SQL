# Practica Operaciones-SQL
### Operaciones en SQL con un enfoque de optimización y rendimiento

hola esta practica muestra una ruta sugerida para aprender la sintaxis básica de SQL. A continuación, te presento un resumen del proceso en pasos sencillos:

+ Familiarizarse con los conceptos básicos de SQL: antes de empezar a escribir cualquier código, es importante entender algunos conceptos clave de SQL, como tablas, filas, columnas y consultas.

+ Aprender a crear tablas y a insertar datos: una vez que comprendes los conceptos básicos, puedes empezar a crear tus propias tablas y a insertar datos en ellas.

+ Aprender a seleccionar y filtrar datos: una vez que tienes datos en tus tablas, puedes utilizar consultas SQL para seleccionar y filtrar los datos que deseas ver.

+ Aprender a actualizar y eliminar datos: también es importante saber cómo actualizar y eliminar datos de tus tablas, ya sea para corregir errores o para mantener la integridad de tus datos.

+ Aprender a utilizar funciones y cláusulas adicionales: existen muchas funciones y cláusulas adicionales que puedes utilizar en tus consultas SQL para realizar cálculos, agrupar datos y mucho más.

A continuación, te presento un ejemplo de script SQL con comentarios que te ayudarán a entender cada proceso:

#### Creación de tablas
    -- Crea una tabla llamada "clientes" con dos columnas: "nombre" y "ciudad"
    CREATE TABLE clientes (nombre VARCHAR(50), ciudad VARCHAR(50));

    -- Inserta algunos datos en la tabla "clientes"
    INSERT INTO clientes (nombre, ciudad) VALUES
    ('Juan', 'Madrid'),
    ('Ana', 'Barcelona'),
    ('Pablo', 'Sevilla');

    -- Selecciona todos los datos de la tabla "clientes"
    SELECT * FROM clientes;

    -- Selecciona sólo el nombre de los clientes de Barcelona
    SELECT nombre FROM clientes WHERE ciudad = 'Barcelona';

    -- Actualiza la ciudad de Juan a Valencia
    UPDATE clientes SET ciudad = 'Valencia' WHERE nombre = 'Juan';

    -- Elimina a Pablo de la tabla "clientes"
    DELETE FROM clientes WHERE nombre = 'Pablo';

    -- Utiliza una función para contar el número de clientes en la tabla
    SELECT COUNT(*) FROM clientes;

Espero que este ejemplo te ayude a comprender y recordar mejor la sintaxis básica de SQL.

#### JOIN, GROUP BY, TRANSACTION

Además de las operaciones básicas que mencioné en el primer mensaje (crear tablas, insertar datos, seleccionar y filtrar datos, actualizar y eliminar datos), hay muchas otras cosas que puedes aprender a hacer con SQL en bases de datos relacionales. Algunas de estas operaciones incluyen:

+ JOIN: con JOIN puedes combinar datos de varias tablas en una sola consulta. Por ejemplo, si tienes una tabla de clientes y otra tabla de pedidos, puedes utilizar JOIN para obtener una lista de todos los pedidos realizados por cada cliente.

+ GROUP BY y HAVING: con GROUP BY puedes agrupar los resultados de una consulta por una o varias columnas, y luego utilizar la cláusula HAVING para filtrar los resultados en función de las condiciones especificadas.

+ Subconsultas: con subconsultas puedes utilizar el resultado de una consulta como parte de otra consulta. Por ejemplo, puedes utilizar una subconsulta para seleccionar los clientes que hayan realizado más de un pedido.

+ Índices: los índices son estructuras de datos que se utilizan para optimizar el rendimiento de las consultas en las bases de datos. Puedes crear índices en tus tablas para mejorar la velocidad de búsqueda de datos.

+ Transacciones: las transacciones son una serie de operaciones que se deben realizar juntas para garantizar la integridad de los datos. Con SQL, puedes utilizar las sentencias BEGIN TRANSACTION, COMMIT y ROLLBACK para controlar el proceso de transacciones.

Aquí te presento algunos ejemplos de cómo utilizar JOIN, GROUP BY, HAVING, subconsultas, índices y transacciones en SQL:

#### JOIN
    -- Supongamos que tenemos dos tablas: "clientes" y "pedidos"
    -- La tabla "clientes" tiene las columnas "id", "nombre" y "ciudad"
    -- La tabla "pedidos" tiene las columnas "id", "cliente_id" (que hace referencia al ID del cliente en la tabla "clientes"), "producto" y "cantidad"

    -- Utilizamos INNER JOIN para combinar las tablas "clientes" y "pedidos" por la columna "cliente_id"
    -- Esto nos devuelve una lista de todos los pedidos realizados por cada cliente, con el nombre del cliente y la ciudad
    SELECT c.nombre, c.ciudad, p.producto, p.cantidad
    FROM clientes c INNER JOIN pedidos p
    ON c.id = p.cliente_id;
    GROUP BY y HAVING:

#### GROUP BY
    -- Utilizamos GROUP BY para agrupar los resultados de la consulta por la columna "ciudad"
    -- Utilizamos SUM para calcular la cantidad total de cada producto vendido en cada ciudad
    -- Utilizamos HAVING para filtrar sólo las ciudades donde se hayan vendido más de 100 unidades de un producto determinado
    SELECT ciudad, SUM(cantidad) AS 'unidades_vendidas'
    FROM pedidos
    WHERE producto = 'Producto X'
    GROUP BY ciudad
    HAVING SUM(cantidad) > 100;

#### Subconsulta
    -- Utilizamos una subconsulta para seleccionar los clientes que hayan realizado más de un pedido
    -- La subconsulta cuenta el número de pedidos realizados por cada cliente y devuelve sólo aquellos con una cuenta mayor a 1
    SELECT nombre
    FROM clientes
    WHERE (SELECT COUNT(*) FROM pedidos WHERE pedidos.cliente_id = clientes.id) > 1;


#### Índice
    -- Creamos un índice en la tabla "clientes" utilizando la columna "nombre" como clave
    CREATE INDEX nombre_idx ON clientes (nombre);

    -- Utilizamos la cláusula USE INDEX para forzar el uso del índice "nombre_idx" en la consulta
    SELECT * FROM clientes USE INDEX (nombre_idx) WHERE nombre = 'Juan';
    Transacciones:

#### TRANSACTION
    -- Iniciamos una transacción
    BEGIN TRANSACTION;

Te explicaré cómo utilizar TRANSACTION ó transacciones en SQL, ya que vale la pena entrar en detalle.

Una transacción es una serie de operaciones que se deben realizar juntas para garantizar la integridad de los datos. Por ejemplo, si estás realizando una compra en una tienda en línea, es importante que la operación de descontar el dinero de tu cuenta y la de añadir el producto a tu carrito se realicen juntas, para asegurar que ninguna de las dos falla. Si alguna de las operaciones falla, entonces se cancela la transacción y los datos se mantienen sin cambios.

En SQL, puedes utilizar las sentencias BEGIN TRANSACTION, COMMIT y ROLLBACK para controlar el proceso de transacciones. La sentencia BEGIN TRANSACTION inicia una transacción, la sentencia COMMIT confirma todas las operaciones realizadas en la transacción y las guarda en la base de datos, mientras que la sentencia ROLLBACK cancela todas las operaciones realizadas en la transacción y restaura los datos a su estado anterior.

Aquí te presento un ejemplo de cómo utilizar transacciones en SQL:

    -- Iniciamos una transacción
    BEGIN TRANSACTION;

    -- Realizamos algunas operaciones en la base de datos
    UPDATE clientes SET saldo = saldo - 100 WHERE nombre = 'Juan';
    INSERT INTO compras (cliente_id, producto, cantidad, precio) VALUES (1, 'Producto X', 1, 100);

    -- Si todas las operaciones se realizan correctamente, confirmamos la transacción
    COMMIT;

    -- Si alguna de las operaciones falla, cancelamos la transacción y restauramos los datos a su estado anterior
    ROLLBACK;

> En el ejemplo que te di anteriormente, si alguna de las operaciones realizadas en la transacción falla, entonces se cancela la transacción y se restauran los datos a su estado anterior.

> Por ejemplo, supongamos que en el ejemplo anterior la operación de descontar el dinero de la cuenta de Juan falla porque no tiene suficiente saldo. En este caso, se cancelaría la transacción y los datos se mantendrían sin cambios. Es decir, la compra no se realizaría y el saldo de Juan no se descontaría.

> Es importante tener en cuenta que las transacciones son una herramienta muy útil para garantizar la integridad de los datos en las bases de datos, pero también pueden afectar el rendimiento si se utilizan de manera inadecuada. Por lo tanto, es importante utilizarlas de manera adecuada y sólo cuando sean necesarias.

### Caso practico con preact

En general, la manera adecuada de abordar este tipo de problemas de integridad de datos en aplicaciones web depende en gran medida de la arquitectura y las herramientas utilizadas. Sin embargo, aquí te presento un ejemplo de cómo podrías crear un componente de validación de compra utilizando el framework de JavaScript Preact y teniendo en cuenta lo expuesto sobre transacciones en SQL:

    import { h, Component } from 'preact';
    import axios from 'axios';

    class ValidarCompra extends Component {
      validarCompra = () => {
        // Iniciamos una transacción
        axios.post('/api/iniciar-transaccion');

        // Realizamos algunas operaciones en la base de datos
        axios.patch('/api/clientes/1', { saldo: saldo - 100 });
        axios.post('/api/compras', { cliente_id: 1, producto: 'Producto X', cantidad: 1, precio: 100 });

        // Si todas las operaciones se realizan correctamente, confirmamos la transacción
        axios.post('/api/confirmar-transaccion');

        // Si alguna de las operaciones falla, cancelamos la transacción y mostramos un mensaje de error al usuario
        axios.post('/api/cancelar-transaccion').catch(() => {
          alert('La compra no se pudo realizar');
        });
      }

      render() {
        return (
          <button onClick={this.validarCompra}>Validar compra</button>
        );
      }
    }

    export default ValidarCompra;

Este componente hace uso de la librería de cliente HTTP Axios para realizar solicitudes HTTP a una API que se encarga de manejar las transacciones en la base de datos. En este ejemplo, se envían tres solicitudes HTTP a la API: una para iniciar la transacción, otra para confirmarla y otra para cancelarla en caso de fallo.

Es importante tener en cuenta que este es sólo un ejemplo y que la implementación final podría variar según tus necesidades específicas. Por ejemplo, podrías utilizar una librería diferente para realizar solicitudes HTTP o podrías utilizar un enfoque diferente para manejar las transacciones.

#### Buenas Prácticas = mejor rendimiento en consultas y transcciones
Aquí te presento algunas recomendaciones generales que pueden ayudar a mejorar el rendimiento de las transacciones en SQL:

Utiliza índices adecuadamente: Los índices son estructuras de datos que se utilizan para acelerar la búsqueda de registros en las tablas. Utilizar índices adecuadamente puede mejorar significativamente el rendimiento de las consultas y, por lo tanto, también el rendimiento de las transacciones que involucren estas consultas.

Utiliza un motor de base de datos adecuado: Existen diferentes motores de base de datos que tienen características y rendimiento diferentes. Es importante elegir un motor de base de datos que se adapte a las necesidades de tu aplicación y que ofrezca un buen rendimiento en el escenario de uso previsto.

Utiliza una arquitectura adecuada: Dependiendo del tamaño y la complejidad de la base de datos y del uso previsto, puede ser beneficioso utilizar una arquitectura distribuida, como una base de datos en cluster, para mejorar el rendimiento y la escalabilidad.

Utiliza buenas prácticas de diseño de base de datos: Utilizar buenas prácticas de diseño de base de datos, como la normalización de las tablas y el uso adecuado de claves primarias y foráneas, puede mejorar el rendimiento de las consultas.

Utiliza transacciones sólo cuando sean necesarias: Las transacciones son una herramienta muy útil para garantizar la integridad de los datos, pero también pueden afectar el rendimiento si se utilizan de manera inadecuada. Por lo tanto, es importante utilizarlas de manera adecuada y sólo cuando sean necesarias.

Espero que estas recomendaciones te ayuden a mejorar el rendimiento de las transacciones en SQL.

