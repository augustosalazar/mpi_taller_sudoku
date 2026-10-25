# Informe de resultados

Completa este informe después de implementar las tres tareas MPI. Ejecuta las comparaciones con el mismo archivo `seeds.txt`, en el mismo equipo y con el contenedor del taller.

## Entorno

- Equipo y CPU lógicas visibles en el contenedor:
- Versión del contenedor:
- Cantidad de repeticiones por medición: 3
- Valor común de `N` elegido:

## Cómo elegir un único `N` por equipo

Desde la carpeta del proyecto, ejecuta:

```text
docker run --rm -v "${PWD}:/app" augustosalazar/slim-mpi:2 python /app/detectar_procesos_mpi.py
```

El programa cuenta números primos con distintos valores de `N`. Usa las CPU lógicas del contenedor como slots MPI, mide hasta `nproc` y calcula cuál fue más rápido. Al final imprime **`N RECOMENDADO`**: copia ese valor y úsalo en las tres implementaciones MPI. No necesitas calcularlo.

## Comparación final con el mismo `N`

Repite tres veces cada ejecución y registra la mediana. Mantén fijo el `N` elegido en todas las filas MPI. Incluye `--allow-run-as-root --use-hwthread-cpus --oversubscribe` en `mpiexec`, igual que en la calibración, para permitir valores de `N` mayores que los slots detectados.

| Implementación | Caso | Procesos | Mediana del tiempo total (s) | Aceleración frente a secuencial | Resultado correcto |
| --- | --- | ---: | ---: | ---: | --- |
| Secuencial | Todos los IDs | 1 |  | 1,00 |  |
| MPI por tableros | Todos los IDs | N |  |  |  |
| MPI por ramas | Todos los IDs, uno después de otro | N |  |  |  |
| MPI híbrido | Todos los IDs | N |  |  |  |

Calcula la aceleración como `tiempo secuencial / tiempo MPI`. Mide el tiempo MPI desde el inicio del reparto hasta recibir todos los resultados necesarios.

## Conclusiones

- ¿Qué estrategia obtuvo el menor tiempo para los 30 tableros? ¿Cuánto mejoró respecto a la versión secuencial?
- ¿Cómo afectaron la comunicación y las diferencias de duración entre tableros?
- ¿Cómo se comparó repartir tableros con resolverlos en orden y repartir las ramas de cada uno?
