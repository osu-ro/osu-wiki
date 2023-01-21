---
no_native_review: true
---

# Precisión

La precisión es una medida percentil de la capacidad de un jugador para golpear [objetos](/wiki/Hit_object) a tiempo. Hay tres tipos de precisión que un jugador puede tener: la precisión del beatmap, que depende de las puntuaciones obtenidas; la precisión general del jugador, que se pondera para permitir que las mejores puntuaciones se destaquen más; y la precisión de los [puntos de rendimiento (pp)](/wiki/Performance_points) del jugador, que depende de la precisión de la puntuación enviada.

## Modos de juego

### ![](/wiki/shared/mode/osu.png) osu!

![Precisión = (300 \* número de 300s + 100 \* número de 100s + 50 \* número de 50s) / (300 \* (número de 300s + número de 100s + número de 50s + número de fallos))](img/accuracy_osu_updated.png "Fórmula de precisión para osu!")

En osu!, la precisión se calcula ponderando el [juicio](/wiki/Gameplay/Judgement) obtenido de cada objeto por su valor y dividido por la cantidad máxima posible.

Referencia para un círculo:

```
300 -> 300 / 300 = 1   = 100.00%
100 -> 100 / 300 = 1/3 =  33.33%
50  ->  50 / 300 = 1/6 =  16.67%
0   ->   0 / 300 = 0   =   0.00%
```

### ![](/wiki/shared/mode/taiko.png) osu!taiko

![Precisión = (número de GREATs + 0.5 \* número de GOODs) / (número de GREATs + número de GOODs + número de fallos)](img/accuracy_taiko_updated.png "Fórmula de precisión para osu!taiko")

En osu!taiko, la precisión se calcula tomando la suma de la precisión de la nota (qué tan cerca estuvo de tocar la nota a tiempo) dividida por el número total de notas anotadas hasta el momento. Las precisiones de las notas están etiquetadas como GREAT (良) (cuenta como 100%), GOOD (可) (cuenta como 50%) (mitad), y MISS/BAD (不可) (cuenta como 0%, lo que también rompe el combo). Los redobles de tambor y los spinners no influyen en la precisión.

### ![](/wiki/shared/mode/catch.png) osu!catch

![Precisión = (número de frutas capturadas + número de gotas atrapadas + número de gotitas atrapadas) / (número de todas las frutas + número de todas las gotas + número de todas las gotitas)](img/accuracy_catch_updated.png "Fórmula de precisión para osu!catch")

En osu!catch, la precisión se calcula dividiendo el número total de objetos que no sean spinners entre el número total de objetos que no sean spinners. Todos los objetos tienen el mismo valor; a excepción de los plátanos, ya que son parte de los spinners.

*Notas para usuarios de la API:*

- El número de gotas capturadas se devuelve como `count100`.
- El número de gotitas capturadas se devuelve como `count50`.
- El número de frutas perdidas *y* gotas acumuladas se devuelve como `countMiss`.
- El número de gotitas perdidas se devuelve como `countKatu`.
- `countGeki` no debe usarse para calcular la precisión en absoluto. Es la cantidad de frutas capturadas con finalización de combo.

### ![](/wiki/shared/mode/mania.png) osu!mania

En osu!mania, la precisión se calcula de forma similar a [osu!](#osu!). Sin embargo, la sponderación de los rainbow 300s (también conocidos como resultados MAX) depende de si ScoreV2 está activo.

Sin ScoreV2 activo, los rainbow 300 y los gold 300 tienen el mismo peso de 300:

![Precisión = (300 \* (número de MAXs + número de 300s) + 200 \* número de 200s + 100 \* número de 100s + 50 \* número de 50s) / (300 \* (número de MAXs + número de 300s + número de 200s + número de 100s + número de 50s + número de fallos))](img/accuracy_mania_updated_score_v1.png "Fórmula de precisión para osu!mania con ScoreV1")

ScoreV2 aumenta la ponderación de los rainbow 300 a 305:

![Precisión = 305 \* number of MAXs + 300 \* number of 300s + 200 \* number of 200s + 100 \* number of 100s + 50 \* number of 50s) / (305 \* (number of MAXs + number of 300s + number of 200s + number of 100s + number of 50s + number of fallos))](img/accuracy_mania_updated_score_v2.png "Fórmula de precisión para osu!mania con ScoreV2")

*Notas para usuarios de la API:*

- El número de rainbow 300s se devuelve como `countGeki`.
- El número de 200s se devuelve como `countKatu`.

## Gráfico de rendimiento

![Gráfico de rendimiento](img/performance_graph.png "Gráfico de rendimiento")

El gráfico de rendimiento es un gráfico que muestra el rendimiento del jugador (basado en su barra de vida) en el transcurso de una jugada (tiempo). Se puede mostrar información adicional al pasar el cursor del juego sobre ella.

*Nota: La información adicional solo se puede ver después de jugar un beatmap o ver una repetición. Después de salir de la [pantalla de resultados](/wiki/Client/Interface#pantalla-de-resultados), esta información no se guardará.*

### Precisión

Al pasar el cursor sobre el gráfico de rendimiento, se muestra un texto emergente con una clasificación de `Error` y `Tasa inestable`.

Debido a la forma en que se implementan los mods [DT](/wiki/Game_modifier/Double_Time) y [HT](/wiki/Game_modifier/Half_Time), los valores de tasa de error e inestabilidad se multiplicarán por el mismo factor que la canción. Para obtener los valores reales cuando juegues con el mod DT, divide los resultados entre 1.5. Del mismo modo, multiplica los resultados por 1.33 cuando juegues con el mod HT.

#### Error

`Error` siempre mostrará dos valores que representan qué tan lejos estaban en promedio los primeros golpeos y qué tan lejos estaban en promedio los últimos golpeos. Cuanto más alto sea el valor de [dificultad general](/wiki/Beatmapping/Overall_difficulty) del beatmap, más bajos tendrán que ser los valores de error para hacerlo bien al jugar el beatmap.

#### Tasa inestable

`Tasa inestable` representa la consistencia del tiempo de los aciertos, donde los números más bajos son mejores (los mejores jugadores a menudo obtienen puntajes por debajo de 100). Tenga en cuenta que el valor mide la consistencia, no la precisión, por lo que acertar constantemente 15 ms antes es lo mismo que acertar siempre a tiempo. La fórmula es esencialmente la desviación estándar de los errores de golpeo (en milisegundos), multiplicada por 10. El [código de muestra](https://gist.github.com/peppy/3a11cb58c856b6af7c1916422f668899) está disponible como referencia y muestra cómo osu-stable calcula los valores de tasa inestables.

### Giros

*Nota: Los giros solo se usa para el modo de juego [osu!](/wiki/Game_mode/osu!).*

Además de la precisión, en el mismo texto emergente también se ve alguna información sobre los spinners.

#### Velocidad

La velocidad representa el promedio de RPM (revoluciones por minuto) en todos los spinners en el beatmap. `Max` es el RPM más alto que el jugador logró en cualquiera de los spinners del beatmap.
