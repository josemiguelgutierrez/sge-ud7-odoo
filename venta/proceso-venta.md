# Proceso de venta

Esta es la venta que hice en el vídeo, del presupuesto a la factura pagada. Cada paso lo hizo el usuario de su puesto, ninguno lo hice con el administrador.

**Cliente:** Cervecería Lúpulo Bravo S.L.
**Fecha:** 7 de noviembre de 2026

## Lo que se vendió

| Producto | Cantidad | Precio | Descuento | Importe |
|---|---|---|---|---|
| Camiseta personalizada | 20 | 14,90 € | 10 % | 268,20 € |
| Sudadera con capucha personalizada | 10 | 32,00 € | No | 320,00 € |
| Diseño de logotipo | 1 | 80,00 € | No | 80,00 € |

Base imponible 668,20 €, IVA 21 % 140,32 € y total **808,52 €**. Condiciones de pago a 30 días.

## Paso a paso

| Paso | Qué hice | Usuario | Documento | Estado |
|---|---|---|---|---|
| 1 | Crear el presupuesto con 3 líneas, una con descuento, con las condiciones de pago a 30 días y una fecha de validez, y sacar el PDF | Marta García Sánchez, comercial | S00002 | Presupuesto |
| 2 | Confirmar el presupuesto | José Miguel Gutiérrez López, responsable de ventas | S00002 | Pedido de venta |
| 3 | Validar la entrega en Inventario con la cantidad hecha igual a la pedida, y comprobar que bajaba el stock | José Miguel Gutiérrez López, responsable de ventas | WH/OUT/00002 | Hecho |
| 4 | Crear la factura desde el pedido, revisarla y publicarla | Carmen Ruiz Moreno, facturación | INV/2026/00002 | Registrado |
| 5 | Registrar el pago por banco | Carmen Ruiz Moreno, facturación | INV/2026/00002 | Pagado |
| 6 | Comprobar el estado final del pedido | José Miguel Gutiérrez López, responsable de ventas | S00002 | Completamente facturado |

## Cómo cambió el stock

Al validar la entrega solo salieron del almacén los productos físicos. El diseño de logotipo no aparece en la entrega porque es un servicio.

| Producto | Antes | Después |
|---|---|---|
| Camiseta personalizada | 98 | 78 |
| Sudadera con capucha personalizada | 40 | 30 |

## Documentos impresos desde Odoo

- [Presupuesto](presupuesto.pdf)
- [Factura](factura.pdf)