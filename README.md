# cajas-del-campo
"Cajas del Campo" es una plataforma digital que conecta a campesinos y productores locales con consumidores finales a través de un modelo de suscripción de cajas de productos agrícolas.

-------------------------------------------
1. DESCRIPCIÓN GENERAL DEL PROYECTO
-------------------------------------------

"Cajas del Campo" es una plataforma digital que conecta a campesinos y productores locales con consumidores finales a través de un modelo de suscripción de cajas de productos agrícolas.

**Propuesta de Valor:**
- **Para el Cliente:** Ofrecer productos frescos, naturales y a un precio justo, eliminando intermediarios. Brinda la comodidad de recibir una caja de mercado en casa y la satisfacción de apoyar directamente la economía local y el consumo sostenible.
- **Para el Campesino:** Proporcionar un canal de venta directa, asegurando un ingreso más estable y justo por sus productos, y dándoles visibilidad en el mercado digital.

La aplicación funcionará como un e-commerce por suscripción donde los usuarios podrán elegir, personalizar y gestionar la entrega periódica de sus cajas de productos del campo.

-------------------------------------------
2. ARQUITECTURA Y STACK TECNOLÓGICO
-------------------------------------------

La aplicación se desarrollará siguiendo una arquitectura desacoplada con un frontend (cliente) y un backend (servidor) que se comunican a través de una API REST.

**2.1. Arquitectura MVC (Modelo-Vista-Controlador)**

Esta arquitectura se aplicará principalmente en el backend (Node.js) para organizar el código de manera lógica y escalable.

- **Modelo (Model):** Representa la estructura de los datos y la lógica de negocio. Se encargará de interactuar con la base de datos. Aquí se definirán los esquemas de los usuarios, productos, suscripciones, etc. Se utilizará un ORM (Object-Relational Mapping) como Sequelize o un ODM (Object-Document Mapping) como Mongoose para facilitar esta interacción.

- **Vista (View):** Es la representación de los datos, es decir, la interfaz de usuario (UI). En nuestra arquitectura, la "Vista" es manejada completamente por el frontend de React. El backend no renderizará HTML directamente, sino que enviará los datos en formato JSON a React para que este los presente al usuario.

- **Controlador (Controller):** Actúa como intermediario entre el Modelo y la Vista. Recibe las peticiones HTTP del cliente (React), procesa la solicitud (ej: validar datos), interactúa con el Modelo para consultar o modificar la base de datos y envía una respuesta (generalmente en formato JSON) de vuelta a la Vista.

**Flujo de una petición:**
1. El usuario interactúa con la interfaz en React (Vista).
2. React realiza una petición HTTP (ej: GET, POST) a un endpoint específico del backend.
3. El enrutador del backend (Express.js) dirige la petición al Controlador correspondiente.
4. El Controlador procesa la lógica, llama al Modelo para acceder a los datos.
5. El Modelo interactúa con la base de datos y devuelve los datos al Controlador.
6. El Controlador formatea la respuesta y la envía como JSON al cliente (React).
7. React recibe los datos y actualiza la Vista para mostrarlos al usuario.

**2.2. Stack Tecnológico**

- **Frontend (Cliente):**
  - **Framework:** React.js
  - **Lenguaje:** JavaScript / TypeScript (recomendado para escalabilidad).
  - **Gestión de Estado:** React Context API (para aplicaciones simples) o Redux Toolkit (para estado complejo).
  - **Enrutamiento:** React Router.
  - **Peticiones HTTP:** Axios.
  - **Estilos:** Styled-Components, Tailwind CSS o un framework de componentes como Material-UI.

- **Backend (Servidor):**
  - **Entorno de ejecución:** Node.js
  - **Framework:** Express.js (para la creación de la API REST).
  - **Lenguaje:** JavaScript / TypeScript.
  - **Base de Datos:** PostgreSQL (recomendado por su robustez para datos relacionales y transaccionales como ventas y suscripciones).
  - **ORM:** Sequelize (para mapear los modelos de datos de PostgreSQL a objetos en JavaScript/TypeScript).

- **Autenticación:**
  - **Estrategia:** JSON Web Tokens (JWT) para gestionar sesiones seguras.
  - **OAuth 2.0:** Integración con Google para "Iniciar Sesión con Google".

-------------------------------------------
3. FUNCIONALIDADES DE LA APLICACIÓN
-------------------------------------------

**3.1. Módulo de Usuario (Cliente)**

1.  **Autenticación y Registro:**
    -   Registro mediante formulario de correo y contraseña.
    -   Inicio de sesión con credenciales.
    -   Inicio de sesión/registro rápido con Google (OAuth 2.0).
    -   Funcionalidad de "Olvidé mi contraseña" vía email.

2.  **Gestión de Perfil:**
    -   El usuario podrá ver y modificar su información personal: nombre, apellido, teléfono.
    -   Gestionar múltiples direcciones de envío.
    -   Administrar sus métodos de pago (CRUD): asociar nuevas tarjetas, PSE, y otros medios a través de una pasarela de pago.

3.  **Suscripciones:**
    -   Explorar los diferentes tipos de "cajas" o planes de suscripción disponibles.
    -   Suscribirse a un plan, seleccionando frecuencia de entrega (semanal, quincenal, mensual).
    -   Ver el historial de sus suscripciones activas y pasadas.
    -   Pausar, cancelar o reactivar una suscripción.
    -   Ver detalles de su próxima entrega.

4.  **Pagos:**
    -   Integración con una pasarela de pagos (ej. PayU, Stripe) que soporte:
        -   Tarjetas de crédito/débito.
        -   PSE (Pagos Seguros en Línea).
        -   Google Pay.
        -   Factura de Claro (si la pasarela de pago lo permite como método de pago alternativo).
    -   Visualización del historial de pagos y facturas.

**3.2. Módulo de Administración (Admin)**

Este módulo será una interfaz web accesible solo para personal autorizado.

1.  **Dashboard (Panel de Control):**
    -   Visualización de métricas clave en tiempo real:
        -   Ingresos totales (diarios, semanales, mensuales).
        -   Número de suscriptores activos.
        -   Nuevas suscripciones vs. cancelaciones.
        -   Productos más vendidos.
    -   Gráficos y reportes para el análisis de ventas.

2.  **Gestión de Clientes (CRUD):**
    -   Ver un listado de todos los clientes registrados.
    -   Buscar y filtrar clientes por nombre, correo, etc.
    -   Ver los detalles de un cliente específico (información personal, direcciones, historial de suscripciones y pedidos).
    -   Desactivar o eliminar cuentas de clientes.

3.  **Gestión de Campesinos (CRUD):**
    -   Añadir nuevos campesinos a la plataforma.
    -   Editar la información de los campesinos (nombre, ubicación, historia, datos de contacto).
    -   Asociar productos a cada campesino.

4.  **Gestión de Productos (CRUD):**
    -   Crear nuevos productos (ej: Tomate, Lechuga, Papa).
    -   Editar detalles del producto (nombre, descripción, unidad de medida, precio base).
    -   Asignar productos a uno o varios campesinos.
    -   Gestionar el stock o la disponibilidad por temporada.

5.  **Gestión de Suscripciones (CRUD):**
    -   Ver todas las suscripciones de la plataforma.
    -   Modificar manualmente la suscripción de un cliente (ej: cambiar plan, actualizar fecha de entrega).
    -   Crear suscripciones manualmente para un cliente.
    -   Cancelar suscripciones a petición del cliente.
