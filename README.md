# ADBD_Prac2
## Descripción de las Entidades
### Vivero
Vivero: Centro físico de venta de plantas, productos de jardinería y decoración gestionado por la empresa Tajinaste S.A. Es una entidad fuerte con los siguientes atributos:

id_vivero (Clave Primaria): Identificador únido del vivero, con dominio de número entero positivo.

nombre: Nombre del vivero, con dominio de cadena de texto.

latitud: Coordenada de latitud con domino de número decimal.

longitud: Coordenada de longitud con domino de número decimal.

### Zona
Zona: Las subdivisiones físicas o funcionales dentro de un vivero específico. Entidad débil en identificación respecto a Vivero; la existencia de una zona depende directamente de su vivero. Sus atributos son:

id_zona (Clave Parcial): Identificador local de la zona dentro del vivero. De dominio un número entero positivo.

nombre: Nombre de la zona, con dominio de cadena de texto.

latitud: Coordenada de latitud con domino de número decimal.

longitud: Coordenada de longitud con domino de número decimal. 

### Producto
Producto: Representa los artículos que comercializa la empresa en sus viveros. Es una entidad fuerte con los siguientes atributos:

id_producto (Clave Primaria): Código interno del producto, con dominio de cadena de caracteres o entero.

nombre: Nombre del producto, con dominio de cadena de texto.

tipo: Categorización del producto, con dominio de texto restringido a enumeración.

precio: Precio de venta, con dominio de moneda/decimal positivo con dos decimales.

### Empleado
Empleado: Representa al personal que trabaja en la empresa. Los empleados realizan sus labores asignados a distintas zonas/viveros según la época del año y son responsables de gestionar ventas. Es una entidad fuerte con los siguientes atributos:

id_empleado (Clave Primaria): Número de ficha de empleado, con dominio de números enteros.

dni_nif: Documento de identificación fiscal o de identidad, con dominio de texto de 9 caracteres con reglamento establecido.

nombre: Nombre del trabajador, con dominio de cadena de texto.

apellidos: Apellidos del trabajador, con dominio de cadena de texto.

### Cliente
Cliente: Representa a cualquier persona física o jurídica que realiza compras en la red de viveros de la empresa. Es una entidad fuerte con los siguientes atributos:

id_cliente (Clave Primaria): Identificador general del cliente, con dominio de números enteros.

nombre: Nombre o Razón Social, con dominio de cadena de texto.

apellidos: Apellidos del trabajador, con dominio de cadena de texto.

email: Dirección de correo electrónico de contacto, con dominio de cadena de texto.

### Cliente_Plus
Cliente_Plus: Representa a los clientes pertenecientes al programa de fidelización Tajinaste plus. Entidad débil; sus atributos son:

id_cliente (Clave Primaria): Identificador general del cliente, con dominio de números enteros.

fecha_ingreso_plus: Fecha en la que el cliente se adhirió al programa Tajinaste Plus, con dominio de fecha (DD-MM-AAAA).

### Pedido
Pedido: Representa las transacciones de compras realizadas por los clientes. Es una entidad fuerte con los siguientes atributos:

id_pedido (Clave Primaria): Código del comprobante de venta, con dominio de números enteros.

fecha: Marca temporal de emisión del pedido, con dominio de fecha (DD-MM-AAAA).

importe_total: Suma total calculada de la venta, con dominio de moneda/decimal positivo con dos decimales.

### Bonificación
Bonificación: Representa los beneficios o recompensas económicas/puntos que se acreditan mensualmente a un cliente según al volumen acumulado de compras. Es una entidad fuerte con los siguientes atributos:

id_bonificacion (Clave Primaria): Código interno del abono de bonificación, con dominio de números enteros.

mes_año: Periodo mensual al que corresponde al beneficio, con dominio de fecha (DD-MM-AAAA).

volumen_compras: Suma acumulada de las compras del cliente en dicho mes, con dominio de moneda/decimal positivo con dos decimales.

monto_bonificacion: Importe asignado de descuento o crédito, con dominio de moneda/decimal positivo con dos decimales.

## Descripción de las Relaciones y Cardinalidades

### Tiene (Vivero-Zona)
Asocia cada vivero con sus áreas distintas zonas. Un vivero puede tener una o muchas zonas (1:N), Una zona pertenece obligatoriamente a un Vivero (1:1).

### Stock (Zona-Producto)
Controla la cantidad física disponible de cada artículo en una zona específica. Una zona puede almacenar cero o varios Productos(0:N), un producto puede estar almacenado en cero o varias Zonas (0:M).

### Histórico (Empleado-Zona)
Controla la cantidad física disponible de cada artículo en una zona específica. Un empleado puede haber estado destinado a cero o muchas Zonas a lo largo del tiempo (0:N), y una Zona puede haber contado con cero o muchos empleados asignados en distintos épocas (0:M).

### Gestiona (Empleado - Pedido)
Asigna la responsabilidad de una venta a un empleado específico para auditar su cumplimiento de objetivos de venta. Un empleado puede gestionar cero o varios pedidos (0:N), un pedido tiene un empleado responsable (1:1).

### Contiene (Pedido - Producto)
Detalla los artículos que integran la compra de un pedido. Un pedido debe incluir uno o varios productos(1:N). Un producto puede estar incluido en cero o muchos pedidos(0:M).

### Realiza (Cliente Plus - pedido)
Vincula los pedidos gestionados con el cliente correspondiente. Un cliente plus puede realizar uno o varios pedidos desde que ingresó al programa (1:N) y un pedido es realizado por un único Cliente Plus (1:1).

### Contiene (Pedido - Producto)
Detalla la línea de artículos que integran la compra de un pedido. Un pedido debe incluir uno o varios Productos (1:N) y un producto puede estar inculuido en cero o muchos pedidos (0:M).

### Recibe (Cliente_Plus - Bonificación)
Registra la asignación mensual de bonificaciones a los clientes del programa Tajinaste Plus. Un cliente plus puede recibir cero o muchas bonificiaciones a lo largo del tiempo (0:N) y una bonificación es otorgada a un único cliente plus (1:1).

## Restricciones Semánticas

### Restricción 1: Un empleado nunca puede estar asignado a dos viveros/zonas de forma simultánea.
En la relación Histórico no pueden existir dos registros para un mismo id_empleado donde los rangos de fechas se solapen. Aquel registro  con fecha_fin = Null se considera el destino activo.

### Restricción 2: Solo se auditan los pedidos de clientes Tajinaste Plus desde su ingreso al programa.
Para cualquier pedido realizado por un cliente Tajinaste Plis, la propiedad PEDIDO.fecha debe ser igual o posterior a CLIENTE_PLUS.fecha_ingreso.

### Restricción 3: Las coordenadas de una zona deben encontrarse dentro del área geográfica delimitada por el vivero al que pertenece.
ZONA.latitud y ZONA.longitud deben encontrarse en un radio o margen geomético coherente respecto a VIVERO.latitud y VIVERO.longitud.


<img width="1442" height="998" alt="Diagrama sin título drawio" src="https://github.com/user-attachments/assets/031287a1-95ca-41a0-9dc5-801a8aa03719" />


