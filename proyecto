# Usando pila (stack), matrices y funciones auxiliares

# Función auxiliar: verifica si una posición es valida
def es_posicion_valida(fila, columna, filas_totales, columnas_totales, laberinto, visitados):
    # Verificar que está dentro de los límites
    if fila < 0 or fila >= filas_totales or columna < 0 or columna >= columnas_totales:
        return False
    
    # Verificar que no es pared
    if laberinto[fila][columna] == '#':
        return False
    
    # Verificar que no fue visitado
    if (fila, columna) in visitados:
        return False
    
    # Si todo está bien, retornar True
    return True


# Función auxiliar: obtener los vecinos válidos de una posición
def obtener_vecinos(fila, columna, filas_totales, columnas_totales, laberinto, visitados):
    # Definir las 4 direcciones posibles, arriba(-1, 0), abajo(1, 0), izquierda(0, -1), derecha(0, 1)
    direcciones = [(-1, 0), (1, 0), (0, -1), (0, 1)]
    
    # Lista para guardar los vecinos válidos
    vecinos = []
    
    # Probar cada dirección
    for diferencia_fila, diferencia_columna in direcciones:
        # Calcular la nueva posición
        nueva_fila = fila + diferencia_fila
        nueva_columna = columna + diferencia_columna
        
        # Verificar si la nueva posición es válida
        if es_posicion_valida(nueva_fila, nueva_columna, filas_totales, columnas_totales, laberinto, visitados):
            # Agregar a la lista de vecinos
            vecinos.append((nueva_fila, nueva_columna))
    
    # Retornar los vecinos válidos
    return vecinos


# Función auxiliar: marcar el camino en la matriz
def marcar_camino(laberinto, pasos):
    # Recorrer todos los pasos del camino
    for fila, columna in pasos:
        # Solo marcar si es espacio libre
        if laberinto[fila][columna] == '.':
            laberinto[fila][columna] = '*'


# Función auxiliar: mostrar la matriz del laberinto
def mostrar_laberinto(laberinto):
    # Recorrer cada fila de la matriz
    for fila in laberinto:
        # Convertir la lista de caracteres en texto
        print("".join(fila))


# Función principal: resolver el laberinto usando pila
def resolver_laberinto(laberinto, filas_totales, columnas_totales, posicion_inicio, posicion_fin):
    # Crear la pila con el estado inicial
    # Cada estado contiene: (fila, columna, pasos anteriores)
    pila = [(posicion_inicio[0], posicion_inicio[1], [])]
    
    # Conjunto para guardar las posiciones ya visitadas
    visitados = {posicion_inicio}
    
    # Mientras la pila tenga elementos
    while pila:
        # Sacar el último elemento de la pila
        fila_actual, columna_actual, pasos_anteriores = pila.pop()
        
        # Verificar si llegamos a la posición final
        if (fila_actual, columna_actual) == posicion_fin:
            # Marcar el camino en la matriz
            marcar_camino(laberinto, pasos_anteriores)
            # Retornar True indicando que encontramos solución
            return True
        
        # Obtener los vecinos válidos de la posición actual
        vecinos = obtener_vecinos(fila_actual, columna_actual, filas_totales, columnas_totales, laberinto, visitados)
        
        # Procesar cada vecino
        for nueva_fila, nueva_columna in vecinos:
            # Agregar a visitados
            visitados.add((nueva_fila, nueva_columna))
            
            # Crear la lista de nuevos pasos agregando la posición actual
            nuevos_pasos = pasos_anteriores + [(fila_actual, columna_actual)]
            
            # Agregar el nuevo estado a la pila
            pila.append((nueva_fila, nueva_columna, nuevos_pasos))
    
    # Si la pila se vacía sin encontrar la solución, retornar False
    return False



# ENTRADA: Leer la primera línea con filas y columnas
linea_primera = input()

# Convertir a números
filas_totales = int(linea_primera.split()[0])
columnas_totales = int(linea_primera.split()[1])

# Crear la matriz del laberinto
laberinto = []

# Inicializar las posiciones de inicio y fin
posicion_inicio = None
posicion_fin = None

# Leer cada fila del laberinto
for numero_fila in range(filas_totales):
    # Leer una línea del laberinto
    linea_laberinto = input()
    
    # Convertir en lista de caracteres (matriz)
    fila_caracteres = list(linea_laberinto)
    
    # Buscar las posiciones de 'S' y 'E'
    for numero_columna in range(len(fila_caracteres)):
        if fila_caracteres[numero_columna] == 'S':
            posicion_inicio = (numero_fila, numero_columna)
        
        if fila_caracteres[numero_columna] == 'E':
            posicion_fin = (numero_fila, numero_columna)
    
    # Agregar la fila a la matriz
    laberinto.append(fila_caracteres)



# Resolver el laberinto
if resolver_laberinto(laberinto, filas_totales, columnas_totales, posicion_inicio, posicion_fin):
    # Si encontró solución, mostrar el laberinto
    mostrar_laberinto(laberinto)
else:
    # Si no hay solución
    print("No existe solución")
