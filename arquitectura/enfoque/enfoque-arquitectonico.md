# Enfoque Arquitectónico: Clean Architecture (Arquitectura Limpia)

## Identificación del Enfoque

| Elemento | Descripción Aplicada al Sistema de Licencias |
| :--- | :--- |
| **Enfoque Arquitectónico** | Clean Architecture (Arquitectura Limpia) + Principios Hexagonales (Puertos y Adaptadores). |
| **Objetivo** | Aislar las reglas de negocio (*Requisitos, Evaluaciones, Agenda, Checklist*) de frameworks, interfaz de usuario y bases de datos. |
| **¿Qué problema resuelve?** | Evita que los cambios en bibliotecas de Java/Spring, librerías de UI (React) o integraciones externas (servicios de notificación/correo) afecten la lógica del trámite de licencias. |
| **Capas Definidas** | **Dominio**, **Aplicación**, **Presentación** e **Infraestructura**. |
| **Beneficios** | • Facilita la realización de pruebas unitarias al dominio sin levantar la BD.<br>• Mantiene preparado el sistema para futuras integraciones institucionales oficiales sin reescribir la lógica central.<br>• Clara separación de responsabilidades en el código. |

## Mapeo de Capas y Responsabilidades
