# Sistema de Compras Online - Microservicios

Este proyecto es una descomposición de un sistema monolítico de compras en línea a una arquitectura basada en microservicios.

## 📦 Requisitos

- Docker
- Docker Compose

## 🚀 Instrucciones de Despliegue

### Clona el repositorio

```bash
git clone https://github.com/usuario/nombre-repo.git
cd nombre-repo
```

### Construye e inicia los servicios

```bash
docker-compose up --build
```

### Verifica que todos los servicios estén en funcionamiento

Accede a los siguientes endpoints en tu navegador o herramienta de prueba (Postman, curl, etc.):

- `http://localhost:8001/products`
- `http://localhost:8002/orders`
- `http://localhost:8003/payments`
- `http://localhost:8004/customers`
- `http://localhost:8005/returns`
- `http://localhost:8006/analytics`
- `http://localhost/api` → Entrada del API Gateway

## 📚 Servicios Incluidos


| Servicio          | Puerto | URL Ejemplo              |
| ----------------- | ------ | ------------------------ |
| product-service   | 8001   | `/products`              |
| order-service     | 8002   | `/orders`                |
| payment-service   | 8003   | `/payments`              |
| customer-service  | 8004   | `/customers`             |
| returns-service   | 8005   | `/returns`               |
| analytics-service | 8006   | `/reports`, `/forecasts` |
| api-gateway       | 80     | `/api/...`               |

## 🛠️ Estructura del Proyecto

```
├── services/
│   ├── product-service/
│   ├── order-service/
│   ├── payment-service/
│   ├── customer-service/
│   ├── returns-service/
│   └── analytics-service/
├── gateway/
├── docker-compose.yml
├── README.md
├── architecture-diagram.png
└── report.pdf
```

## 🧠 Notas Finales

- Cada servicio tiene su propia base de datos.
- Comunicación entre servicios es vía HTTP REST y RabbitMQ.
- El gateway centraliza acceso, autenticación y rutas.
