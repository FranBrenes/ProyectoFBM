Diseñamos e implementamos la estructura de almacenamiento utilizando sentencias SQL estructuradas para evitar duplicidades.

<img width="603" height="226" alt="image" src="https://github.com/user-attachments/assets/d2ed6535-7746-4411-a7ec-23526b1690bf" />

Esta vista realiza un acoplamiento relacional mediante uniones de las tablas de ventas, clientes, empleados y desgloses de artículos.

<img width="547" height="245" alt="image" src="https://github.com/user-attachments/assets/7ef5fd8c-b27d-4219-ab39-52b6c02fbcde" />

<img width="580" height="80" alt="image" src="https://github.com/user-attachments/assets/d05c8d4c-dce8-43b6-a0ea-cc46100ade6a" />

Esta función recibe como parámetro de entrada el identificador único de un trabajador y devuelve un valor decimal con el acumulado total de sus ingresos generados.

<img width="612" height="349" alt="image" src="https://github.com/user-attachments/assets/1c44e845-d509-4f98-b57c-975105bb7f5c" />

SELECT CoreStack.Fn_Total_Ventas_Empleado(1) AS Total_Vendido_Empleado_1;

<img width="216" height="46" alt="image" src="https://github.com/user-attachments/assets/97c459f1-9b8d-4ad6-8461-f7bd1b0a7874" />

Este trigger se ejecuta de forma automática inmediatamente después de que se registra una nueva fila dentro de la tabla de detalles de venta. Su comportamiento consiste en realizar una modificación en la tabla de productos, restando la cantidad vendida directamente del stock del artículo correspondiente.

<img width="421" height="237" alt="image" src="https://github.com/user-attachments/assets/99ee0b6d-667f-4e62-b5ef-7b013230db2f" />

Realizamos un ciclo completo de pruebas para verificar la correcta integración de todos los elementos programados.

Paso A: Revisar el stock actual
Primero, mira cuánto stock tiene el producto 1 (Ordenador Portátil i7):

SELECT nombre, stock FROM CoreStack.Productos WHERE id_producto = 1;

<img width="203" height="44" alt="image" src="https://github.com/user-attachments/assets/08eb4e66-d7d8-4dee-be49-6c3dba6df304" />

Paso B: Ejecutar el procedimiento
Ejecuta el procedimiento para simular que el Cliente 1 le compra 3 portátiles al Empleado 1:
CALL CoreStack.Sp_Registrar_Venta(1, 1, 1, 3);

<img width="600" height="104" alt="image" src="https://github.com/user-attachments/assets/e2e28e19-0977-4bdf-a47b-f74a28dc6a92" />


Paso C: Verificar el Trigger (Descuento de Stock)
Vuelve a consultar el stock del producto 1:
SELECT nombre, stock FROM CoreStack.Productos WHERE id_producto = 1;

<img width="205" height="54" alt="image" src="https://github.com/user-attachments/assets/89b1ced6-c024-4152-83c1-c2b7759fac6f" />


