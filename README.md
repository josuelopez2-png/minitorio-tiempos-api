Descripción del caso

El algoritmo diseñado resuelve la necesidad de un equipo de desarrollo de software para monitorear y evaluar el rendimiento de una interfaz de programación de aplicaciones (API)[span_1](start_span)[span_1](end_span). El sistema permite analizar el comportamiento de un conjunto de N llamadas HTTP mediante la recolección de sus tiempos de respuesta expresados en milisegundos[span_2](start_span)[span_2](end_span).

* *Entradas:* El usuario debe ingresar la cantidad total de llamadas a evaluar (N)[span_3](start_span)[span_3](end_span). Posteriormente, para cada llamada, se introduce su respectivo tiempo de respuesta en milisegundos[span_4](start_span)[span_4](end_span).
* *Procesamiento:* El algoritmo valida de forma estricta que cada tiempo ingresado sea un valor real mayor a cero[span_5](start_span)[span_5](end_span). En caso de detectar un valor inválido, exige la reintroducción del dato[span_6](start_span)[span_6](end_span). Luego, almacena los datos en un arreglo y realiza un recorrido general para calcular la sumatoria total de los tiempos (necesaria para determinar el tiempo promedio de respuesta) y contar cuántas de estas solicitudes superaron el umbral crítico de 200 milisegundos[span_7](start_span)[span_7](end_span).
* *Salidas:* Al finalizar, el algoritmo expone de manera clara el tiempo promedio de respuesta de la API y la cantidad exacta de peticiones catalogadas como "respuestas lentas[span_8](start_span)"[span_8](end_span).

---

## Pseudocódigo

```text
ALGORITMO MonitoreoTiemposAPI

VARIABLES
    N : ENTERO
    tiempos : ARREGLO [100] DE REAL
    tiempo_ingresado : REAL
    suma : REAL
    promedio : REAL
    respuestas_lentas : ENTERO
    i : ENTERO

INICIO
    // Leer y validar la cantidad de llamadas a procesar
    ESCRIBIR "¿Cuántas llamadas a la API desea analizar? (máximo 100): "
    LEER N
    
    // Cargar el arreglo con validación de datos en cada ingreso
    PARA i DE 1 HASTA N CON PASO 1 HACER
        ESCRIBIR "Ingrese el tiempo de respuesta de la llamada ", i, " (en ms): "
        LEER tiempo_ingresado
        
        // Validación de consistencia: tiempos mayores a 0 ms
        MIENTRAS tiempo_ingresado <= 0 HACER
            ESCRIBIR "Error: El tiempo de respuesta debe ser mayor a 0 ms."
            ESCRIBIR "Ingrese nuevamente el tiempo para la llamada ", i, ": "
            LEER tiempo_ingresado
        FIN_MIENTRAS
        
        tiempos[i] <- tiempo_ingresado
    FIN_PARA

    // Inicialización de acumulador y contador antes del ciclo de procesamiento
    suma <- 0
    respuestas_lentas <- 0

    // Recorrido del arreglo para cálculos estadísticos
    PARA i DE 1 HASTA N CON PASO 1 HACER
        suma <- suma + tiempos[i]
        
        // Verificar si supera el umbral crítico de respuestas lentas
        SI tiempos[i] > 200 ENTONCES
            respuestas_lentas <- respuestas_lentas + 1
        FIN_SI
    FIN_PARA

    // Cálculo del promedio y despliegue de métricas finales
    promedio <- suma / N
    
    ESCRIBIR "--- RESULTADOS DEL MONITOREO ---"
    ESCRIBIR "Tiempo promedio de respuesta: ", promedio, " ms"
    ESCRIBIR "Cantidad de respuestas lentas (> 200 ms): ", respuestas_lentas
