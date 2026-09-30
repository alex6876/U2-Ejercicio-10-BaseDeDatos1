# Ejercicio 10 — Base de Datos de Gestión de Flota de Vehículos, Viajes y Mantenimiento



Proyecto enfocado en la modelación Entidad-Relación (DER / MER) e implementación de base de datos relacional para un sistema de gestión de flota de transporte, administrando vehículos, choferes, cargas de combustible, mantenimientos preventivos/correctivos en talleres mecánicos, asignación de viajes y trayectos de carga.

---

## Descripción

El sistema modela una estructura de datos relacional para la administración logística de una flota de vehículos de transporte. Permite registrar y realizar el seguimiento de los vehículos y su odómetro/kilometraje, administrar la información de los choferes habilitados, controlar los consumos y cargas de combustible, programar e historializar mantenimientos mecánicos en talleres externos o propios, y coordinar los viajes de carga asignando choferes y vehículos específicos.

---

## Funcionalidades e Implementación

### Entidades y Atributos

* Vehiculo:


* id_Patente: Clave primaria identificadora única del vehículo (dominio/patente).


* NroChasis: Número identificador de chasis del vehículo.


* Año fabricación: Año de fabricación de la unidad.


* Marca: Marca del vehículo.


* Modelo: Modelo del vehículo.


* Kilometraje Actual: Lectura actual del odómetro del vehículo.




* Chofer:


* id_Legajo: Clave primaria identificadora del chofer o conductor.


* DNI: Documento Nacional de Identidad.


* nombre: Nombre completo del conductor.


* Fecha nacimiento: Fecha de nacimiento del chofer.


* Categoria Licencia: Tipo o clase de licencia de conducir que posee.


* vencimiento licencia: Fecha de expiración del carnet/licencia de habilitación.




* Carga de combustible:


* id_Carga: Clave primaria identificadora de la transacción de combustible.


* id_Patente: Clave foránea referenciando al vehículo abastecido.


* fecha: Fecha y/o hora del repostaje.


* litro Cargados: Cantidad de litros de combustible cargados.


* Costo x litros: Valor unitario por litro cargado.


* odometro: Lectura del odómetro/kilometraje al momento del abastecimiento.




* Mantenimiento:


* id_Matenimiento: Clave primaria identificadora de la orden o registro de mantenimiento.


* id_Patente: Clave foránea referenciando al vehículo ingresado a taller.


* id_CUIT: Clave foránea referenciando al taller mecánico responsable.


* Tipo: Tipo de intervención (ej. preventivo, correctivo, revisión).


* Fecha ingreso: Fecha de ingreso al servicio técnico.


* descripción trabajo: Detalle técnico de las tareas o reparaciones realizadas.


* Costo Total: Importe total abonado por la intervención mecánica.




* Taller Mecanico:


* id_CUIT: Clave primaria única tributaria o identificador del taller.


* nombre: Razón social o nombre del taller mecánico.


* direccion: Ubicación o domicilio físico del taller.


* telefono: Número telefónico de contacto.


* especialidad: Rama o especialidad del taller (ej. motor, electricidad, frenos).




* Viaje:


* id_Viaje: Clave primaria identificadora del viaje/flete.


* Fecha hora salida: Momento estipulado o real de partida.


* FechaHora llegada: Momento de finalización o arribo.


* Origen: Ciudad o punto inicial de partida.


* Destino: Ciudad o punto final de entrega.


* Carga: Descripción o tipo de mercadería transportada.


* id_Patente: Clave foránea del vehículo asignado para el trayecto.




* Asignación - viaje:


* id_Viaje: Clave foránea referenciando al viaje a realizar.


* id_Legajo: Clave foránea referenciando al chofer asignado.


* RolChofer: Rol desempeñado en la ruta (ej. conductor principal, acompañante/relevo).


* Hora conducción: Registro de horas conducidas por el chofer en dicho viaje.


* Observación: Notas o novedades del desempeño o ruta.





---

## Relaciones del Modelo

1. Vehiculo ↔ Carga de combustible (Relación 1:N / N:1):


* Un vehículo registra múltiples cargas de combustible a lo largo del tiempo, pero cada carga corresponde a una única unidad.




2. Vehiculo ↔ Mantenimiento (Relación 1:N):


* Un vehículo ingresa a mantenimiento en múltiples oportunidades para revisiones o reparaciones.




3. Taller Mecanico ↔ Mantenimiento (Relación 1:N / N:1):


* Un taller mecánico efectúa múltiples órdenes de mantenimiento para los vehículos de la flota.




4. Vehiculo ↔ Viaje (Relación 1:N):


* Un vehículo realiza múltiples viajes de transporte, pero cada viaje específico utiliza un vehículo asignado.




5. Chofer ↔ Viaje (Relación N:M via Asignación - viaje):


* Un chofer puede realizar múltiples viajes y un viaje puede requerir uno o más choferes (titular/relevo). La relación se resuelve operativamente a través de la entidad intermedia `Asignación - viaje`.




6. Chofer ↔ Asignación - viaje (Relación 1:N):


* Un chofer posee registros de asignación a distintos viajes programados.




7. Viaje ↔ Asignación - viaje (Relación 1:N):


* Un viaje contiene una o más asignaciones de personal de conducción.
