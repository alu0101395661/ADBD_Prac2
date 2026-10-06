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
