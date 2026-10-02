# Estilo Arquitectónico: Monolito Modular en Capas

## Diagrama de la Arquitectura Global

![Diagrama Monolito Modular](./diagrama-monolito.png)

## Reglas de la Arquitectura
1. Cada capa solo invoca a la capa inmediatamente inferior.
2. Un módulo no accede al repository ni a las tablas de otro módulo.
3. La comunicación entre módulos se hace llamando a su service.
4. Todo se ejecuta en un único proceso Node.js con una única BD.