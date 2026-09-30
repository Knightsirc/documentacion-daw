# Análisis de Requisitos

## 1. Requisitos Funcionales (RF)
* **RF-01 (Autenticación):** El sistema debe permitir el registro e inicio de sesión de usuarios mediante correo electrónico/contraseña y proveedores OAuth (Google, GitHub).
* **RF-02 (Gestión de Tareas):** Los usuarios con rol de Administrador o Gestor deben poder crear, asignar, editar y eliminar tareas dentro de un proyecto.
* **RF-03 (Tablero Kanban):** La interfaz debe mostrar las tareas en columnas dinámicas: *Por Hacer*, *En Progreso* y *Completado*.

## 2. Requisitos No Funcionales (RNF)
* **RNF-01 (Rendimiento):** Las peticiones al API REST deben responder en un tiempo menor a 200 ms bajo condiciones normales de tráfico.
* **RNF-02 (Seguridad):** Las contraseñas deben almacenarse utilizando el algoritmo de hash `bcrypt` con un factor de trabajo mínimo de 12.
* **RNF-03 (Disponibilidad):** La plataforma debe garantizar una disponibilidad del 99.9% medido de forma mensual.
