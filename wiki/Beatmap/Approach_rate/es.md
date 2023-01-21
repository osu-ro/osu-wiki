---
tags:
  - approach time
  - AR
  - reading
  - velocidad de aproximación
  - lectura
---

# Velocidad de aproximación

*Para conocer los valores sugeridos de AR, véase: [Criterios de clasificación](/wiki/Ranking_Criteria)*

La **velocidad de aproximación** (***AR***) es una configuración de dificultad del [beatmap](/wiki/Beatmap) que define cuándo los [objetos](/wiki/Hit_object) empiezan a desvanecerse en relación con cuándo deben ser golpeados o recolectados. Existe solo en [osu!](/wiki/Game_mode/osu!) y [osu!catch](/wiki/Game_mode/osu!catch).

Los valores de AR varían de 0 a 10. Las tasas de aproximación más altas significan que los objetos se mostrarán durante un período de tiempo más corto, lo que le dará menos tiempo al jugador para reaccionar. Por otro lado, las tasas de aproximación más bajas permiten más tiempo de reacción, pero pueden resultar en una cantidad abrumadora de objetos golpeados que aparecen en la pantalla a la vez.

En [osu!taiko](/wiki/Game_mode/osu!taiko) y [osu!mania](/wiki/Game_mode/osu!mania), la configuración de la velocidad de aproximación no tiene efecto. La velocidad de desplazamiento en ambos modos está controlada por la [velocidad del slider](/wiki/Gameplay/Hit_object/Slider/Slider_velocity), que depende de los [BPM](/wiki/Music_theory/Tempo) y del multiplicador de velocidad del slider. Además, en osu!mania puede ser personalizada [por el propio jugador](/wiki/Game_mode/osu!mania#cambio-de-velocidad).

## Temporización de la animación

La duración de un objeto que permanece visible en la pantalla (sin mods) oscila entre 1800 ms en AR0 y 450 ms en AR10. Los niveles de AR escalan en 120 ms por debajo de AR5 y 150 ms por encima de AR5.

Consulte la infografía y las fórmulas a continuación para obtener una descripción general:

```
                                        X = golpe/recolectado
             p r e e m p t             ↓
├───────────────────────┬───────────────┤
0 %     aparición        100 % opacidad
```

El objeto empezará a aparecer cuando `X - preemt` con:

- AR < 5: `preemt = 1200 ms + 600 ms * (5 - AR) / 5`
- AR = 5: `preemt = 1200 ms`
- AR > 5: `preemt = 1200 ms - 750 ms * (AR - 5) / 5`

La cantidad de tiempo que tarda para que el objeto desaparezca por completo, también dependerá de la velocidad de aproximación:

- AR < 5: `aparición = 800 ms + 400 ms * (5 - AR) / 5`
- AR = 5: `aparición = 800 ms`
- AR > 5: `aparición = 800 ms - 500 ms * (AR - 5) / 5`

### Tabla de comparación

![](/wiki/shared/ARTable.jpg "Comparación de ventanas de visibilidad para diferentes combinaciones de AR y modificadores del juego")

## Efectos de mods

Hay cuatro mods que alteran la velocidad de aproximación cuando se activan:

- [Easy](/wiki/Game_modifier/Easy): Reduce a la mitad el valor de AR.
- [Hard Rock](/wiki/Game_modifier/Hard_Rock): Multiplica el valor de AR por 1.4, hasta un máximo de 10.
- [Double Time](/wiki/Game_modifier/Double_Time): El valor de AR no se ve afectado, pero debido al aumento del 50 % en la velocidad del juego, los objetos permanecen en la pantalla durante un 33 % menos de tiempo.
- [Half Time](/wiki/Game_modifier/Half_Time): El valor de AR no se ve afectado, pero debido a la disminución del 25 % en la velocidad del juego, los objetos permanecen en la pantalla durante un 33 % más de tiempo.

Si bien Half Time y Double Time no cambian el valor de AR, la diferencia de velocidad conduce a un cambio aparente de AR. Los AR de HT/DT se denominan comúnmente en términos de su valor percibido. Por ejemplo, "AR 8 + DT" también se puede escribir como "AR 9.6".
