# Drivers Arquitectónicos

Factores determinantes (requisitos, atributos de calidad o restricciones) que impactan de forma significativa en las decisiones del diseño de arquitectura.

| ID | Driver Arquitectónico | Origen | ¿Por qué influye en la arquitectura? |
| :--- | :--- | :--- | :--- |
| **DA01** | Soporte a alta concurrencia en campañas comerciales. | AC03 - Escalabilidad | Condiciona la estrategia de escalamiento de infraestructura, balanceo y despliegue del sistema. |
| **DA02** | Tiempos de respuesta rápidos en procesamiento. | AC01 - Rendimiento | Impacta en las decisiones de diseño de APIs, estrategias de almacenamiento en caché y consultas a la base de datos. |
| **DA03** | Protección estricta de datos de usuarios y compras. | AC04 - Seguridad | Determina el uso de protocolos seguros (HTTPS, TLS), autenticación mediante tokens (JWT) y cifrado de datos. |
| **DA04** | Integración externa con pasarela de pago. | RC04 - Pasarela de pago | Condiciona la arquitectura para soportar llamadas asíncronas, webhooks e integración segura con servicios de terceros. |
| **DA05** | Comunicación mediante arquitectura API REST. | RC03 - API REST | Establece una separación clara entre la capa de presentación frontend y los componentes de la lógica de negocio backend. |

