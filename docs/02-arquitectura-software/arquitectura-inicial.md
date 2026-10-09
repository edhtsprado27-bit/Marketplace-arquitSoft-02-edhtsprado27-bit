# Arquitectura Inicial del Sistema

## Diagrama de Arquitectura en Capas

```mermaid
flowchart TD
    subgraph ACTORES ["ACTORES"]
        Cliente["Cliente"]
        Seller["Seller"]
        Admin["Administrador"]
    end

    subgraph PRESENTACION ["PRESENTACIÓN"]
        Web["Aplicación Web API REST"]
    end

    subgraph NEGOCIO ["LÓGICA DE NEGOCIO"]
        Usuarios["Usuarios"]
        Sellers["Sellers"]
        Catalogo["Catálogo"]
        Carrito["Carrito"]
        Pedidos["Pedidos"]
    end

    subgraph DATOS ["DATOS"]
        BD[("Base de Datos")]
    end

    subgraph EXTERNOS ["SISTEMAS EXTERNOS"]
        Pago["Pasarela de Pago"]
        ERP["ERP"]
        Envio["Servicio de Envío"]
    end

    ACTORES --> PRESENTACION
    PRESENTACION --> NEGOCIO
    NEGOCIO --> DATOS
    DATOS --> Pago
    DATOS --> ERP
    DATOS --> Envio