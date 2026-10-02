# Estilo Arquitectónico Global del Sistema

## Estilo Seleccionado: Monolito Modular en Capas
Para el **Sistema Web Integral de Licencias de Conducir Clase B en Huamanga**, se ha seleccionado el estilo **Monolito Modular organizadamente estructurado en Capas**, comunicado mediante API REST hacia una aplicación cliente web SPA.

### Justificación
1. **Unidad de Despliegue Única:** Facilita la administración de infraestructura de bajo costo en Render/Docker sin la complejidad ni la sobrecarga de red de los microservicios.
2. **Cohesión Modular:** Los módulos (*Identidad*, *Orientación*, *Expediente*, *Agenda*, *Simulacro*, *Seguimiento*) están lógicamente aislados y solo se comunican mediante interfaces o servicios de aplicación.
3. **Evolución Progresiva:** Si en el futuro un módulo requiere escalar independientemente, su bajo acoplamiento permitirá extraerlo hacia un servicio independiente sin rehacer el núcleo.

## Diagrama de la Arquitectura Global (Mermaid)

```mermaid
flowchart TD
    subgraph CLIENTES ["ACTORES / CLIENTES"]
        Ciudadano["Ciudadano / Postulante"]
        Admin["Administrador de Plataforma"]
        Orientador["Orientador / Soporte"]
    end

    subgraph FRONTEND ["CAPA DE PRESENTACIÓN WEB (SPA)"]
        UI["Cliente Web Responsive\n(React + TypeScript + Tailwind CSS)"]
    end

    subgraph BACKEND ["MONOLITO BACKEND - LICENCIAS B (Java 21 / Spring Boot)"]
        MW["Middlewares (Security, JWT, Cross-Cutting, CORS, Logger)"]

        subgraph PRESENTACION ["1. CAPA DE PRESENTACIÓN / API REST"]
            C_Identidad["Identidad Controller"]
            C_Orientacion["Orientación Controller"]
            C_Expediente["Expediente Controller"]
            C_Agenda["Agenda Controller"]
            C_Simulacro["Simulacro Controller"]
            C_Seguimiento["Seguimiento Controller"]
        end

        subgraph NEGOCIO ["2. CAPA DE LÓGICA DE NEGOCIO / SERVICIOS"]
            S_Identidad["Identidad Service"]
            S_Orientacion["Orientación Service"]
            S_Expediente["Expediente Service"]
            S_Agenda["Agenda Service"]
            S_Simulacro["Simulacro Service"]
            S_Seguimiento["Seguimiento Service"]
        end

        subgraph DATOS ["3. CAPA DE ACCESO A DATOS / INFRAESTRUCTURA"]
            R_Identidad["Identidad Repository"]
            R_Orientacion["Orientación Repository"]
            R_Expediente["Expediente Repository"]
            R_Agenda["Agenda Repository"]
            R_Simulacro["Simulacro Repository"]
            R_Seguimiento["Seguimiento Repository"]
        end
    end

    subgraph PERSISTENCIA ["PERSISTENCIA DE DATOS"]
        BD[("PostgreSQL 16\n(Usuarios, Checklist, Agenda, Auditoría)")]
        Storage[("MinIO / AWS S3\n(Documentos Privados)")]
    end

    subgraph EXTERNOS ["SERVICIOS EXTERNOS (ADAPTADORES)"]
        Notif["Servicio de Notificaciones\n(SMTP / Web Push)"]
        Mapas["OpenStreetMap\n(Ubicación de Oficinas)"]
        MuniRef["Referencias Públicas\n(Muni Huamanga / MTC)"]
    end

    CLIENTES -->|HTTPS| UI
    UI -->|JSON / HTTPS REST| MW
    MW --> PRESENTACION

    C_Identidad --> S_Identidad
    C_Orientacion --> S_Orientacion
    C_Expediente --> S_Expediente
    C_Agenda --> S_Agenda
    C_Simulacro --> S_Simulacro
    C_Seguimiento --> S_Seguimiento

    S_Identidad --> R_Identidad
    S_Orientacion --> R_Orientacion
    S_Expediente --> R_Expediente
    S_Agenda --> R_Agenda
    S_Simulacro --> R_Simulacro
    S_Seguimiento --> R_Seguimiento

    DATOS --> BD
    S_Expediente --> Storage
    S_Agenda --> Notif
    S_Orientacion --> Mapas
    S_Orientacion -.->|Enlace Informativo| MuniRef
