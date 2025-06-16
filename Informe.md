# Informe Técnico: Rediseño de Sistema de Compras Online con Microservicios

## 1. Justificación del Rediseño

El sistema original, basado en una arquitectura monolítica, presentaba varios desafíos:

- **Escalabilidad limitada**: Todos los módulos estaban acoplados.
- **Dificultades de mantenimiento**: Cambios en una parte requerían pruebas globales.
- **Despliegue lento y riesgoso**: No era posible actualizar funcionalidades de forma aislada.

La solución fue rediseñar el sistema aplicando principios de **arquitectura de microservicios**, donde cada servicio implementa una funcionalidad específica, se despliega de forma independiente y se comunica por HTTP REST o mensajería asíncrona (RabbitMQ).

## 2. Descripción de los Servicios


| Servicio            | Descripción                                                                |
| ------------------- | --------------------------------------------------------------------------- |
| `product-service`   | Gestiona productos: alta, baja, modificación, consultas.                   |
| `order-service`     | Maneja pedidos: creación, actualización de estado, historial de órdenes. |
| `payment-service`   | Procesa pagos, interactúa con pasarela de pagos, maneja reembolsos.        |
| `returns-service`   | Procesa devoluciones y cambios, incluye lógica de reembolso.               |
| `customer-service`  | Maneja datos del cliente, revisiones de productos y seguimiento de pedidos. |
| `analytics-service` | Genera reportes de ventas y predicciones para proveedores y admins.         |
| `api-gateway`       | Unifica acceso externo, enruta peticiones, incluye posibles filtros y auth. |
| `rabbitmq`          | Cola de mensajes para desacoplar eventos como pagos y devoluciones.         |

Cada microservicio tiene su propia base de datos, eliminando dependencias internas.

## 3. Diagrama de Arquitectura

El diagrama `architecture-diagram.png` adjunto representa:

- Comunicación REST entre gateway y servicios.
- Comunicación asíncrona mediante eventos por RabbitMQ.
- Base de datos por microservicio (por ejemplo: `orders_db`, `products_db`, etc).
- Conexiones externas con Payment Gateway y Shipping Service mediante APIs.

## 4. Lecciones Aprendidas y Desafíos

### Desafíos

- **Diseño de contratos entre servicios**: importante mantener estabilidad.
- **Sincronización de datos**: se optó por consistencia eventual y comunicación basada en eventos.
- **Orquestación del sistema**: se resolvió mediante Docker Compose y rabbitMQ para integración de eventos.

### Lecciones

- La separación de responsabilidades permite despliegues más rápidos y seguros.
- Los servicios pueden escalar según demanda real.
- El uso de colas de mensajes mejora la resiliencia y la respuesta del sistema.
- Un gateway centralizado permite seguridad, logging y control de acceso unificado.
