# Usuarios, grupos y permisos

He creado los usuarios de TintaViva para que cada uno solo pueda hacer lo que necesita en su trabajo, que es lo que se llama mínimo privilegio. Aquí no pongo contraseñas, solo el correo con el que entra cada uno.

## Tipos de usuario

- **Interno:** es un trabajador de la empresa que usa Odoo por dentro. Los tres trabajadores son internos.
- **Portal:** es un cliente que entra desde fuera y solo ve sus presupuestos, pedidos y facturas. No ve ninguna app. Se lo he puesto a Lucía, que es clienta.
- **Público:** es alguien que entra a la web sin cuenta. No he creado ninguno porque TintaViva no usa la web.

## Usuarios

| Usuario | Correo de acceso | Puesto | Tipo | Permisos por módulo | Grupo propio | Por qué |
|---|---|---|---|---|---|---|
| Marta García Sánchez | marta.garcia@tintaviva.es | Comercial | Interno | Ventas: solo sus documentos. Productos: ver. Contacto: no. Contabilidad: no. Inventario: no | TintaViva / Comercial junior | Ella solo hace presupuestos y solo tiene que ver los suyos. No necesita ver la contabilidad ni el almacén |
| José Miguel Gutiérrez López | josemiguel.gutierrez@tintaviva.es | Responsable de ventas | Interno | Ventas: administrador. Contacto: creación. Exportar: sí. Inventario: usuario. Contabilidad: no | Ninguno | Yo veo todos los presupuestos, confirmo los pedidos y valido las entregas en el almacén. No facturo |
| Carmen Díaz Vela | carmen.diaz@tintaviva.es | Administración y facturación | Interno | Contabilidad: facturación. Ventas: no. Inventario: no. Contacto: no | TintaViva / Facturación de pedidos | Ella hace las facturas y registra los pagos, pero no se encarga de las ventas |
| Lucía García Montes | lucia.garcia@correo.es | Clienta | Portal | Ninguna app | Ninguno | Es clienta, así que solo puede ver sus cosas desde el portal |

El administrador solo lo he usado para configurar Odoo. Ningún paso de la venta lo hago con él.

## Grupo propio 1: TintaViva / Comercial junior

Lo hice para que la comercial pueda trabajar con los clientes, crearlos y editarlos, pero sin poder borrarlos, porque al borrar un cliente se pierde su historial. Tampoco puede cambiar los productos ni sus precios.

- **Hereda de:** Ventas / Usuario: Solo mostrar documentos propios. Así tiene todo lo que tiene un comercial normal sin tener que poner los permisos uno a uno.
- **Usuario:** Marta García Sánchez.

| Derecho de acceso | Modelo | Leer | Escribir | Crear | Borrar |
|---|---|---|---|---|---|
| Comercial junior - Contactos | Contacto `res.partner` | Sí | Sí | Sí | No |
| Comercial junior - Productos | Producto `product.template` | Sí | No | No | No |

## Grupo propio 2: TintaViva / Facturación de pedidos

Cuando probé con Carmen me di cuenta de que no podía abrir los pedidos de venta, y entonces no podía hacer la factura desde el pedido. No quería darle todo Ventas porque ella no lleva las ventas, así que hice este grupo para que solo pueda ver los pedidos y facturarlos.

- **Hereda de:** Contabilidad / Facturación. Así puede hacer facturas y registrar pagos.
- **Menús:** Ventas, Ventas / A facturar y Ventas / A facturar / Pedidos a facturar. Es el único camino que ve dentro de Ventas.
- **Usuaria:** Carmen Díaz Vela.

| Derecho de acceso | Modelo | Leer | Escribir | Crear | Borrar |
|---|---|---|---|---|---|
| Facturación - Pedidos | Pedido de venta `sale.order` | Sí | Sí | No | No |
| Facturación - Líneas de pedido | Línea de pedido de venta `sale.order.line` | Sí | Sí | No | No |
| Facturación - Crear factura | Factura de anticipo de venta `sale.advance.payment.inv` | Sí | Sí | Sí | No |

Con esto Carmen puede ver los pedidos y darle a Crear factura, pero no puede crear pedidos nuevos ni borrarlos.

## Comprobación de permisos

Entré con cada usuario para ver que todo funcionaba bien.

| Usuario | Lo que puede hacer | Lo que no puede hacer |
|---|---|---|
| Marta | Entrar en Ventas, hacer presupuestos, crear y editar clientes y ver productos | Ver Contabilidad e Inventario, borrar clientes, cambiar productos y ver los presupuestos de otros |
| José Miguel | Ver todos los presupuestos, confirmar pedidos y validar entregas en Inventario | Ver Contabilidad y hacer facturas |
| Carmen | Entrar en Facturación, ver los pedidos a facturar, hacer y publicar facturas y registrar pagos | Hacer presupuestos o pedidos y entrar en Inventario |
| Lucía | Ver sus presupuestos, pedidos y facturas en el portal | Entrar en ninguna app de Odoo |