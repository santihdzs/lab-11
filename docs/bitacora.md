# Bitácora — Práctica 11: Avisos con pruebas

Matrícula: A01787550

## Ejercicio 0 — ¿Local o instrumentada?

| Promesa | Tipo | Por qué |
|---|---|---|
| Título de 2 letras no se publica | Local | `AvisoValidator` es Kotlin puro |
| «hace 1 h», no «hace 60 min» | Local | `tiempoRelativo` es Kotlin puro |
| Subir la imagen antes que el aviso | Instrumentada | El ViewModel usa compresor y fotos temporales (`Context`, `Uri`) |
| Un solo aviso con doble toque | Instrumentada | Mismo ViewModel |
| Decir la verdad si el servidor rechaza | Instrumentada | Mismo ViewModel |
| TalkBack anuncia la imagen | Instrumentada | Hay que dibujar la pantalla (Compose) |

## Ejercicio C3 — Lo que la prueba no ve

- **¿Suficiente?** No. TalkBack dice «Imagen del aviso» en todas; no se sabe qué muestra cada una.
- **Mejor:** incluir el título: «Imagen del aviso Feria de proyectos».
- **Cómo probarlo:** dibujar `TarjetaAviso` con un aviso de título conocido y buscar `onNodeWithContentDescription("Imagen del aviso Feria de proyectos")`.
