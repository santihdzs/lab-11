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

## Bloque D — Tabla de mutantes

Rama `experimento-mutantes`, mutantes acumulados, corriendo locales + instrumentadas después de cada uno.

| Mutante | Cambio | Prueba nueva en rojo |
|---|---|---|
| 1 | `..` → `until` en `tituloValido` | `un_titulo_de_3_y_uno_de_60_caracteres_son_validos` |
| 2 | `<` → `<=` en `tiempoRelativo` | `a_los_59_minutos_todavia_son_minutos_y_a_los_60_ya_es_una_hora` |
| 3 | Sin `if (!uiState.puedePublicar) return` | `tocar_publicar_dos_veces_manda_un_solo_aviso` |
| 4 | `contentDescription = null` en `TarjetaAviso` | `la_imagen_elegida_se_anuncia_y_se_puede_quitar` |
| 5 | `LADO_MAX` 1280 → 12800 | Ninguna: **sobrevive** (nadie mide el tamaño de la imagen) |

Mutante 5 lo atrapa ahora `una_foto_grande_sale_con_1280_px_en_su_lado_mas_largo` (D4): `expected:<1280> but was:<3000>`.
