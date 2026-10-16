# Trabajo Práctico N° 2 — Tienda Móvil con Carrito y Pago Simulado

- **Materia:** Proyecto y Desarrollo de Software para Plataformas Móviles
- **Docente:** Prof. Leonardo Martínez
- **Modalidad:** Grupal (2 integrantes)

---

## Objetivo General

Desarrollar una aplicación móvil nativa utilizando **React Native y Expo**, integrada con un **backend funcional** de desarrollo propio. La aplicación deberá presentar un catálogo de productos de un rubro a elección del equipo, permitir visualizar el detalle de cada producto, gestionar un carrito de compras mediante estado y concretar un flujo de **pago simulado** procesado por el servidor. La aplicación deberá funcionar en entorno de PRODUCCIÓN.

---

## Requisitos del Proyecto

### Temática y Diseño

- **Rubro libre:** El equipo puede elegir libremente la temática de la tienda (indumentaria, tecnología, librería, gastronomía, hardware, etc.).
- **Identidad visual:** Los estilos deben ser coherentes con el rubro elegido, cuidando la legibilidad, el contraste, las tarjetas de producto y la distribución de los elementos en pantalla.

### Requisitos obligatorios del Frontend (Expo + React Native)

1. **Navegación con `expo-router` (Stack):**
   - Implementar navegación mediante **Stack** (`app/_layout.jsx`).
   - Utilizar **navegación estática** entre vistas (por ejemplo, del catálogo al carrito/checkout).
   - Utilizar **navegación dinámica** mediante rutas con parámetros (por ejemplo, `app/detalle/[id].jsx`) y lectura de datos con el hook **`useLocalSearchParams`**.

2. **Hooks de React y Navegación:**
   - **`useState`**: Para gestionar el estado de los productos, los ítems agregados al carrito, los campos del formulario de pago y los estados de carga/confirmación. *(Se puede combinar con Context de React para compartir el estado del carrito entre pantallas).*
   - **`useEffect`**: Para realizar la petición inicial al backend al montar la pantalla del catálogo.
   - **`useRouter` / `<Link>` y `useLocalSearchParams`**: Para el flujo de navegación y recepción de parámetros entre pantallas.

3. **Componentes Nativos y Dependencias obligatorias:**
   - **`react-native-safe-area-context`**: Uso obligatorio de `<SafeAreaView>` para asegurar que la interfaz respete las áreas seguras del dispositivo.
   - **`FlatList`**: Para renderizar el listado de productos del catálogo de manera optimizada (utilizando `keyExtractor` y `renderItem`).
   - **`ScrollView`**: Para envolver pantallas cuyo contenido pueda exceder el alto del dispositivo (como el detalle del producto o el resumen y formulario de pago).
   - **`Image`**: Para renderizar las imágenes de los productos provenientes del backend.
   - **`Pressable` o `TouchableOpacity`**: Para la creación de botones interactivos personalizados (agregar al carrito, modificar cantidades, confirmar compra, etc.).
   - **`TextInput`**: Para la carga de datos del comprador en la instancia de pago simulado (nombre, dirección, método de pago o datos simulados de tarjeta/alias).
   - **`ActivityIndicator` y `Modal` (o `Alert`)**: Para dar feedback visual durante la carga de datos y al procesar/confirmar el pago.
   - **Componetizacion**: Es necesario dividir la interface en componentes reutilizables a traves de props.

4. **Renderizado Condicional:**
   - Mostrar un indicador de carga (`ActivityIndicator` o mensaje) mientras se esperan los datos del backend.
   - Mostrar una vista o mensaje específico cuando el **carrito esté vacío**, deshabilitando u ocultando la opción de pagar.
   - Mostrar en pantalla el comprobante o mensaje de éxito una vez finalizado el pago simulado.

5. **Estilos:**
   - Uso obligatorio de **`StyleSheet.create`** y maquetación con **Flexbox**.

---

### Requisitos del Backend

- **Lenguaje y Base de Datos a elección:** El grupo puede construir el backend en el lenguaje, framework y motor de base de datos que prefiera (Node.js/Express, Python/FastAPI, PHP, etc.).
- **Mínimo de productos:** La base de datos deberá contar con al menos **20 productos** precargados con: `id`, `nombre`, `descripcion`, `precio`, `imagen` (URL), `categoria` y `stock`.
- **Endpoints mínimos requeridos (JSON):**
  1. **`GET /productos`**: Retorna el listado completo de productos disponibles.
  2. **`GET /productos/:id`** *(Opcional si los datos se envían por parámetros en la ruta, o recomendado para consultar el detalle actualizado del producto)*.
  3. **`POST /checkout` (o `POST /ordenes`)**: Recibe los datos del comprador, el listado de productos seleccionados en el carrito y el monto total. Valida que el pedido sea correcto y devuelve una confirmación (código `200` o `201`) junto con un identificador o número de orden simulado.

---

## Flujo de Usuario Mínimo (Pantallas)

1. **Pantalla 1 — Catálogo Principal (`app/index.jsx`):**
   - Encabezado con el nombre de la tienda y un botón/acceso rápido al carrito (indicando la cantidad de productos agregados).
   - Listado de productos utilizando `FlatList`.
   - Al tocar un producto, navega de forma dinámica a su pantalla de detalle.
   - Filtros básicos de categoría y/o precios.

2. **Pantalla 2 — Detalle del Producto (`app/detalle/[id].jsx`):**
   - Contenedor con `ScrollView`.
   - Recepción del parámetro con `useLocalSearchParams`.
   - Visualización de imagen ampliada, nombre, precio, descripción completa y botón **"Agregar al carrito"**.

3. **Pantalla 3 — Carrito y Pago Simulado (`app/carrito.jsx`):**
   - Visualización de los productos seleccionados, con posibilidad de eliminar ítems o vaciar el carrito, y cálculo automático del **total a pagar**.
   - Si el carrito está vacío, mostrar el estado correspondiente mediante renderizado condicional.
   - Formulario con `TextInput` para los datos del comprador y el pago simulado.
   - Botón **"Confirmar y Pagar"** que envía la petición `POST` al backend, muestra el número de orden generada y limpia el carrito.

---

## Pautas de Entrega y Defensa

1. **Repositorio en GitHub:**
   - El trabajo debe entregarse en un único repositorio público de GitHub con la siguiente estructura sugerida:

     ```text
     /
     ├── frontend/       # Proyecto Expo (React Native)
     ├── backend/        # Código fuente del servidor y API
     ├── database/       # Script .sql o archivo de datos iniciales (seed)
     └── README.md       # Integrantes, temática e instrucciones de ejecución
     ```

2. **Archivo `README.md`:**
   - Nombre de los 2 integrantes del grupo.
   - Nombre y temática de la tienda.
   - Tecnologías utilizadas en el backend.
   - Pasos claros para levantar el backend, la base de datos y la app de Expo.

3. **Defensa Oral:**
   - Ambos integrantes deberán exponer el funcionamiento de la aplicación en vivo y responder preguntas sobre el código tanto del frontend como del backend. Se verificará la participación de ambos en el historial de commits del repositorio.

---

## Rúbrica de Evaluación

| Criterio | Descripción | Puntaje |
| :--- | :--- | :---: |
| **Backend Funcional y Consumo de API** | Servidor operativo que entrega el catálogo (`GET`) y procesa la orden de compra (`POST`). Correcta integración desde React Native con `fetch` y `useEffect`. | **2.5 pts** |
| **Componentes Nativos y Safe Area** | Uso correcto de `FlatList`, `ScrollView`, `SafeAreaView` (`react-native-safe-area-context`), `Image`, `Pressable`/`TouchableOpacity` y `TextInput`. | **2.5 pts** |
| **Lógica de Carrito y Pago Simulado** | Manejo de estado con `useState` (y/o `Context`), cálculo del total, alta/baja de ítems y flujo completo de pago simulado con confirmación. | **2.0 pts** |
| **Navegación y Renderizado Condicional** | Implementación del `Stack` en `expo-router`, navegación estática y dinámica con `useLocalSearchParams`, y manejo de vistas condicionales (carga, carrito vacío, éxito). | **1.5 pts** |
| **Estilos, Diseño y Trabajo en Equipo** | Interfaz prolija con `StyleSheet`, coherencia visual, estructura ordenada del repositorio y defensa oral del equipo. | **1.5 pts** |
| **Total** |  | **10 pts** |
