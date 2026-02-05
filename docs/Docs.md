# Diseño de Arquitectura y Base de Datos para Delivereats 
Gerhard Benjamin Ardon Valdez
202004796
Seminario de sistemas 2 A
---
La práctica se basa en el proyecto Delivereats, una plataforma de delivery diseñada con arquitectura de microservicios.

## Requerimientos Funcionales (RF)

| **ID**   | **Requerimiento** | **Criterio de aceptación** |
|------|---------------|-------------------------|
| RF1  | registro de usuarios con email, contraseña hasheada y rol | el sistema crea el usuario, valida que el email sea único y almacena la contraseña en forma segura; rol cliente, restaurante, repartidor o administrador |
| RF2  | inicio de sesión y emisión de jwt | el sistema valida credenciales y devuelve un token jwt con user id, email y rol; rol cliente, restaurante, repartidor o administrador |
| RF3  | validación y revocación de tokens | el api gateway valida el jwt en cada petición y rechaza accesos inválidos; rol todos |
| RF4  | gestión de roles por administrador | el rol administrador puede asignar o actualizar roles y el cambio queda registrado en auditoría |
| RF5  | crud de restaurantes | el rol administrador puede crear, leer, actualizar y eliminar restaurantes; la eliminación es lógica por defecto |
| RF6  | crud de ítems de menú | el rol restaurante puede crear, leer, actualizar y eliminar ítems de menú asociados a su negocio |
| RF7  | listado público de restaurantes con filtros | el rol cliente puede consultar restaurantes con paginación y filtros por tipo de comida, horario y calificación |
| RF8  | creación de orden desde carrito | el rol cliente puede generar una orden con estado inicial creada y recibe order id, total y timestamp |
| RF9  | máquina de estados de órdenes | el sistema aplica transiciones válidas entre estados creada, en proceso, lista, en camino y entregado; rol cliente, restaurante y repartidor |
| RF10 | cancelación de orden con motivo | el rol cliente, restaurante o repartidor puede cancelar una orden en estados permitidos y se notifica al cliente |
| RF11 | gestión de órdenes por restaurante | el rol restaurante puede listar órdenes, aceptarlas, rechazarlas, marcarlas como lista y finalizarlas |
| RF12 | aceptación de órdenes por repartidor | el rol repartidor puede listar órdenes en estado lista y aceptar una de forma atómica evitando doble asignación |
| RF13 | actualización de estado de entrega | el rol repartidor puede actualizar la orden a en camino, entregado o cancelado con motivo |
| RF14 | publicación de eventos asíncronos | el sistema publica eventos de creación y actualización de órdenes en un bus para consumo por otros servicios |
| RF15 | envío de notificaciones por correo | el notification service envía correos al rol cliente con información mínima de la orden en cada evento |
| RF16 | reintentos de notificación | el notification service reintenta tres veces el envío de correos y registra errores si persisten |
| RF17 | api gateway | el api gateway expone rutas rest, valida jwt, enruta a microservicios y aplica rate limiting básico; rol todos |
| RF18 | auditoría de eventos críticos | el sistema registra login, cambios de estado y operaciones crud con timestamp y actor; rol administrador |




## Requerimientos No Funcionales (RNF)


| **ID**    | **Requerimiento** | **Criterio de aceptación** |
|-------|---------------|-------------------------|
| RNF1  | escalabilidad | el sistema debe poder crecer horizontal o verticalmente para soportar mayor carga sin afectar la operación |
| RNF2  | rendimiento | el sistema debe responder de forma eficiente a las solicitudes de los usuarios y servicios internos |
| RNF3  | disponibilidad | el sistema debe estar accesible de manera continua y minimizar tiempos de inactividad |
| RNF4  | tolerancia a fallos | el sistema debe manejar errores y fallos de componentes sin interrumpir el servicio general |
| RNF5  | seguridad | el sistema debe proteger la información de usuarios y transacciones mediante autenticación, autorización y cifrado |
| RNF6  | privacidad | el sistema debe garantizar el uso responsable de los datos personales conforme a normativas aplicables |
| RNF7  | mantenibilidad | el sistema debe ser fácil de actualizar, corregir y mejorar sin afectar la operación existente |
| RNF8  | portabilidad | el sistema debe poder ejecutarse en diferentes entornos de infraestructura y nube sin cambios significativos |
| RNF9  | respaldo y recuperación | el sistema debe contar con mecanismos de respaldo y recuperación de datos ante fallos o pérdidas |
| RNF10 | usabilidad | la interfaz debe ser clara, coherente y fácil de usar para todos los roles definidos |
| RNF11 | observabilidad | el sistema debe generar registros, métricas y alertas que permitan monitorear su estado y desempeño |
| RNF12 | cumplimiento | el sistema debe respetar políticas organizacionales, estándares técnicos y regulaciones legales aplicables |

## Diagrama de Arquitectura de Alto Nivel

## Diagrama de Despliegue

## Diagrama de Base de Datos
![Diagrama de Base de Datos](../PRACTICA1/assets/Untitled.png)
## Diagrama de Actividades