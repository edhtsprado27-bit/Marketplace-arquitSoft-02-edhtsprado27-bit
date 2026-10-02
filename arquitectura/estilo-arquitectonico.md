# Estilo Arquitectónico Global del Sistema

## Descripción
Se ha seleccionado el estilo **Monolito Modular en Capas**[cite: 43, 47]. Este estilo combina la simplicidad de despliegue de una sola unidad ejecutable con una separación lógica interna modular y multicapa[cite: 43, 47, 48].

## Diagrama de la Arquitectura Global (Mermaid)

```mermaid
flowchart TD
    subgraph CLIENTES ["CLIENTES"]
        C1["Cliente"]
        C2["Seller"]
        C3["Administrador"]
    end

    subgraph PRESENTACION_WEB ["CLIENTE WEB"]
        CW["Navegador (HTML / CSS / JS)"]
    end

    subgraph BACKEND ["Monolito Marketplace Backend (Node.js / Express)"]
        subgraph MIDDLEWARE ["Middlewares Express"]
            MW["Auth (JWT) | Validación | Manejo de Errores | Logger"]
        end

        subgraph CAPA_PRESENTACION ["1. CAPA DE PRESENTACIÓN"]
            U_R["usuarios.routes.js / controller.js"]
            S_R["sellers.routes.js / controller.js"]
            C_R["catalogo.routes.js / controller.js"]
            K_R["carrito.routes.js / controller.js"]
            P_R["pedidos.routes.js / controller.js"]
        end

        subgraph CAPA_NEGOCIO ["2. CAPA DE LÓGICA DE NEGOCIO"]
            U_S["usuarios.service.js"]
            S_S["sellers.service.js"]
            C_S["catalogo.service.js"]
            K_S["carrito.service.js"]
            P_S["pedidos.service.js"]
        end

        subgraph CAPA_DATOS ["3. CAPA DE DATOS"]
            U_D["usuarios.repository.js"]
            S_D["sellers.repository.js"]
            C_D["catalogo.repository.js"]
            K_D["carrito.repository.js"]
            P_D["pedidos.repository.js"]
            ORM["Acceso a datos compartido (Sequelize / Pool DB)"]
        end
        
        MIDDLEWARE --> CAPA_PRESENTACION
    end

    subgraph BASE_DATOS ["BASE DE DATOS"]
        DB[(PostgreSQL)]
    end

    subgraph EXTERNOS ["SISTEMAS EXTERNOS"]
        PAGO["Pasarela de Pagos"]
        ENVIO["Servicio de Envíos"]
    end

    CLIENTES --> PRESENTACION_WEB
    PRESENTACION_WEB -->|"HT[200~cat << 'EOF' > arquitectura/estilo-arquitectonico.md
# Estilo Arquitectónico Global del Sistema

## Descripción
Se ha seleccionado el estilo **Monolito Modular en Capas**[cite: 43, 47]. Este estilo combina la simplicidad de despliegue de una sola unidad ejecutable con una separación lógica interna modular y multicapa[cite: 43, 47, 48].

## Diagrama de la Arquitectura Global (Mermaid)

```mermaid
flowchart TD
    subgraph CLIENTES ["CLIENTES"]
        C1["Cliente"]
        C2["Seller"]
        C3["Administrador"]
    end

    subgraph PRESENTACION_WEB ["CLIENTE WEB"]
        CW["Navegador (HTML / CSS / JS)"]
    end

    subgraph BACKEND ["Monolito Marketplace Backend (Node.js / Express)"]
        subgraph MIDDLEWARE ["Middlewares Express"]
            MW["Auth (JWT) | Validación | Manejo de Errores | Logger"]
        end

        subgraph CAPA_PRESENTACION ["1. CAPA DE PRESENTACIÓN"]
            U_R["usuarios.routes.js / controller.js"]
            S_R["sellers.routes.js / controller.js"]
            C_R["catalogo.routes.js / controller.js"]
            K_R["carrito.routes.js / controller.js"]
            P_R["pedidos.routes.js / controller.js"]
        end

        subgraph CAPA_NEGOCIO ["2. CAPA DE LÓGICA DE NEGOCIO"]
            U_S["usuarios.service.js"]
            S_S["sellers.service.js"]
            C_S["catalogo.service.js"]
            K_S["carrito.service.js"]
            P_S["pedidos.service.js"]
        end

        subgraph CAPA_DATOS ["3. CAPA DE DATOS"]
            U_D["usuarios.repository.js"]
            S_D["sellers.repository.js"]
            C_D["catalogo.repository.js"]
            K_D["carrito.repository.js"]
            P_D["pedidos.repository.js"]
            ORM["Acceso a datos compartido (Sequelize / Pool DB)"]
        end
        
        MIDDLEWARE --> CAPA_PRESENTACION
    end

    subgraph BASE_DATOS ["BASE DE DATOS"]
        DB[(PostgreSQL)]
    end

    subgraph EXTERNOS ["SISTEMAS EXTERNOS"]
        PAGO["Pasarela de Pagos"]
        ENVIO["Servicio de Envíos"]
    end

    CLIENTES --> PRESENTACION_WEB
    PRESENTACION_WEB -->|"HTTPS / JSON REST"| BACKEND

    CAPA_PRESENTACION --> CAPA_NEGOCIO
    CAPA_NEGOCIO --> CAPA_DATOS
    CAPA_DATOS --> ORM
    ORM -->|"SQL"| BASE_DATOS

    CAPA_NEGOCIO -->|"HTTPS / REST"| PAGO
    CAPA_NEGOCIO -->|"HTTPS / REST"| ENVIO

    style CLIENTES fill:#222,stroke:#fff,color:#fff
    style PRESENTACION_WEB fill:#222,stroke:#fff,color:#fff
    style BACKEND fill:#1e1e1e,stroke:#fff,color:#fff
    style CAPA_PRESENTACION fill:#2b2b2b,stroke:#fff,color:#fff
    style CAPA_NEGOCIO fill:#2b2b2b,stroke:#fff,color:#fff
    style CAPA_DATOS fill:#2b2b2b,stroke:#fff,color:#fff
    style BASE_DATOS fill:#222,stroke:#fff,color:#fff
    style EXTERNOS fill:#222,stroke:#fff,color:#fff
