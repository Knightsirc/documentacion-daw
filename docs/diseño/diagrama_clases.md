# Diseño del Sistema: Diagrama de Clases

A continuación se describe la estructura de clases principal del núcleo del sistema (Backend).

```mermaid
classDiagram
    class Usuario {
        +String id
        +String nombre
        +String email
        +String passwordHash
        +login()
        +logout()
    }

    class Proyecto {
        +String id
        +String titulo
        +String descripcion
        +Date fechaCreacion
        +agregarTarea()
        +eliminarTarea()
    }

    class Tarea {
        +String id
        +String titulo
        +String estado
        +String prioridad
        +actualizarEstado()
    }

    Usuario "1" --> "*" Proyecto : gestiona / participa
    Proyecto "1" --> "*" Tarea : contiene
