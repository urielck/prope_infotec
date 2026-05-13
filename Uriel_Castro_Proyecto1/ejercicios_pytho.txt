"""
Título: Solución de Ejercicios de Python "Estructuras Secuenciales, Condicionales y Ciclos - Estructuras de Datos: Listas, Tuplas, Diccionarios, Funciones".
Autor: Uriel Castro Campos.
Fecha de entrega: 30 de abril de 2026 """

"""==========================================
EJERCICIO 1: Área de un Triángulo
ESTRUCTURA PRINCIPAL: Secuencial
ESTRUCTURAS DE DATOS: Ninguna
USO DE FUNCIONES: Para cálculo y entrada
JUSTIFICACIÓN: Solo requiere leer datos, aplicar fórmula y mostrar resultado, sin decisiones ni ciclos

Hacer un programa en Python que resuelva la siguiente expresión aritmética 
del área de un Triángulo, donde el usuario ingresa la base y la altura. area=(base*altura)/2
=============================================="""
def obtener_area(base:float, altura:float) ->  float:
    return (base * altura) / 2

def obtener_valores(mensaje: str) -> float:
    while True:
        try:
            valor = float(input(mensaje))
            if valor <= 0:
                print("¡El valor debe ser un número positivo!")
                continue
            return valor
        except ValueError:
            print("¡Debes ingresar un número válido!")

def main():
    print("Ingresa los datos que se te piden para calcular el área de un triangulo\n")
    b = obtener_valores("\tIngresa la base: ")
    a = obtener_valores("\tIngresa la altura: ")

    print(f"\nEl área del triangulo es: {obtener_area(b, a)}") 
if __name__ == "__main__":
    main()


"""==========================================
EJERCICIO 2: Ecuación de 2o grado
ESTRUCTURA PRINCIPAL: Secuencial y Condicional
ESTRUCTURAS DE DATOS: Tupla (para devolver dos soluciones)
USO DE FUNCIONES: Si
JUSTIFICACIÓN: Secuencial para cálculo, condicional para validar discriminante o evitar división entre cero

Hacer un programa en Python que resuelva la siguiente ecuación de 2o grado. 
El usuario ingresa los valores de a, b y c. x=(-b±(b^2-4ac)^1/2)/(2a)
=============================================="""
import cmath

def obtener_ecuacion(a:float, b:float, c:float) -> tuple[complex, complex]:
    d = b**2 - 4*a*c
    complejo1 = (-b + cmath.sqrt(d)) / (2*a)
    complejo2 = (-b - cmath.sqrt(d)) / (2*a)

    return complejo1, complejo2

def obtener_valores(mensaje:str) -> float:
    while True:
        try:
            valor = float(input(mensaje))
            return valor
        except ValueError:
            print("Debe ser un número valido")
def main():
    while True:
        a1 = obtener_valores("Ingresa el valor de 'a'(distinto de cero): ")
        if a1 == 0:
            print("El valor no debe ser cero")
        else:
            break

    b1 = obtener_valores("Ingresa el valor de 'b': ")
    c1 = obtener_valores("Ingresa el valor de 'c': ")

    c1, c2 = obtener_ecuacion(a1, b1, c1)

    print(f"El valor de la ecuación es:\n \tPrimer complejo: {c1}\n \tSegundo complejo: {c2}")
if __name__ == "__main__":
    main()


"""==========================================
EJERCICIO 3: Calculo de salario semanal
ESTRUCTURA PRINCIPAL: Condicional
ESTRUCTURAS DE DATOS: Ninguna
USO DE FUNCIONES: Si
JUSTIFICACIÓN: Depende de si horas ≤ 40 o > 40 para aplicar diferentes reglas

Hacer un programa en Python que calcule el salario semanal de un obrero, según los siguientes criterios:
Si trabajó 40 horas o menos, sele paga $16 por hora.
Si trabajó más de 40 horas, se le paga $16 por las primeras 40 horas, y $20 por cada hora extra.
=============================================="""
def calculo_salarial(horas:int) -> int:
    if horas <= 40:
        return 16 * horas
    else:
        extra = horas - 40
        return (16 * 40) + (20 * extra)

def obtener_horas(mensaje: str) -> int:
    while True: 
        try:
            horas_trabajadas = int(input(mensaje))
            if 0 <= horas_trabajadas < 168:
                return horas_trabajadas
            else:
                print("Ingresa un número válido de horas trabajadas")
        except ValueError:
            print("Ingresa un número válido")

def main():
    h = obtener_horas("Ingresa el total de horas trabajadas de la semana: ")
    print(f"Salario del obrero: ${calculo_salarial(h)}")

if __name__ == "__main__":
    main()


"""==========================================
EJERCICIO 4: Clasificacion de triangulos
ESTRUCTURA PRINCIPAL: Condicional
ESTRUCTURAS DE DATOS: Ninguna
USO DE FUNCIONES: Si
JUSTIFICACIÓN: Se evalúan condiciones para determinar tipo de triángulo

#Hacer un programa en Python que clasifique el tipo de triángulo a partir de sus lados ingresados:
#Equilátero. Los 3 son iguales
#Isósceles. Tiene 2 lados iguales y un lado distinto
#Escaleno. Los 3 lados son distintos
=============================================="""
def iguales(x, y, tol=1e-9):
    return abs(x-y) < tol

def clasificacion_triangulos(a:float, b:float, c:float) -> str:
    if a + b > c and a + c > b and b + c > a:   
        if iguales(a, b) and iguales(a, c):
            return "Equilátero"
        elif iguales(a, b) or iguales(a, c) or iguales(b, c):
            return "Isósceles"
        else:
            return "Escaleno"
    else:
        return "No es un triángulo"
    
def obtener_lados(mensaje:str) -> float:
    while True:
        try:
            lado = float(input(mensaje))
            if lado <= 0:
                print("El valor debe ser un número positivo")
                continue
            return lado
        except ValueError:
            print("Ingresa un número válido")

def main():
    l_a = obtener_lados("Ingresa el valor del primer lado: ")
    l_b = obtener_lados("Ingresa el valor del segundo lado: ")
    l_c = obtener_lados("Ingresa el valor del tercer lado: ")

    tipo = f"Tipo de triángulo: {clasificacion_triangulos(l_a, l_b, l_c)}"
    print(tipo)
if __name__ == "__main__":
    main()


"""==========================================
EJERCICIO 5: Índice de Masa Corporal
ESTRUCTURA PRINCIPAL: Condicional
ESTRUCTURAS DE DATOS: Ninguna
USO DE FUNCIONES: Si
JUSTIFICACIÓN: Clasificación por rangos de valores

Hacer un programa en Python que calcule el Índice de Masa Corporal
de una persona (IMC = peso[kg] / altura^2 [m]) e indique el estado 
en el que se encuentra esa persona en función del valor de IMC.
< 16. Criterio de ingreso en hospital
de 16 a 17. Infrapeso
de 17 a 18. Bajo peso
de 18 a 25. peso normal (saludable)
de 25 a 30. Sobrepeso (obesidad de grado I)
de 30 a 35. Sobrepeso crónico (obesidad de grado II)
de 35 a 40. Obesidad premórbida (obesidad de grado III)
> 40. Obesidad mórbida (obesidad de grado IV)
=============================================="""
def calculo_indice(peso:float, altura:float) -> float:
    return peso/(altura**2)

def obtener_datos(mensaje:str) -> float:
    while True:
        try:
            dato = float(input(mensaje))
            if dato <= 0:
                print("Ingresa un valor positivo")
                continue
            return dato
        except ValueError as v:
            print(f"Ingresa un valor numérico: {v}")

def obtener_clasificacion(imc:float) -> str:
    if imc < 16:
        return "Criterio de ingreso en hospital"
    elif 16 <= imc < 17:
        return "Infrapeso"
    elif 17 <= imc < 18:
        return "Bajo de peso"
    elif 18 <= imc < 25:
        return "peso normal (saludable)"
    elif 25 <= imc < 30:
        return "Sobrepeso (obesidad de grado I)"
    elif 30 <= imc < 35:
        return "Sobrepeso crónico (obesidad de grado II)"
    elif 35 <= imc < 40:
        return "Obesidad premórbida (obesidad de grado III)"
    else:
        return "Obesidad mórbida (obesidad de grado IV)"

def main():
    p = obtener_datos("Ingresa tu peso en kilográmos: ")
    a = obtener_datos("Ingresa tu altura en métros: ")

    calculo = calculo_indice(p, a)
    clasifica = obtener_clasificacion(calculo)
    
    print(f"Tu índice de masa corporal es: {round(calculo, 2)} - {clasifica}.")
if __name__ == "__main__":
    main()


"""==========================================
EJERCICIO 6: Números pares menores a n
ESTRUCTURA PRINCIPAL: Repetitiva
ESTRUCTURAS DE DATOS: Lista
USO DE FUNCIONES: Si
JUSTIFICACIÓN: Se requiere recorrer números hasta n

Hacer un programa en Python que, por un número entero dado por el usuario, 
muestre la lista de números pares inferiores a él.
=============================================="""
def obtener_numero(mensaje:str) -> int:
    while True:
        try:
            num = int(input(mensaje))
            if num <= 2:
                print("Ingresa un número superior a dos")
                continue
            return num
        except ValueError:
            print("Ingresa un valor numérico válido")

def obtener_pares(n:int) -> list[int]:
    pares = []
    for i in range(2, n, 2):
        pares.append(i)
    return pares

def main():
    n1 = obtener_numero("Ingresa un numero entero positivo: ")
    lista = obtener_pares(n1)

    print(f"Números pares inferiores: {lista}")
if __name__ == "__main__":
    main()


"""==========================================
EJERCICIO 7: Tabla del cinco
ESTRUCTURA PRINCIPAL: Repetitiva
ESTRUCTURAS DE DATOS: Ninguna
USO DE FUNCIONES: No
JUSTIFICACIÓN: Operacion aritmetica directa.

Hacer un programa en Python que muestre los productos
del 1 al 10 de la tabla de multiplicar del número 5.
=============================================="""
for i in range(1, 11):
    resultado = 5 * i
    print(f"{5} x {i} = {resultado}")

    
"""==========================================
EJERCICIO 8: Imprime serie 1/n
ESTRUCTURA PRINCIPAL: Repetitiva
ESTRUCTURAS DE DATOS: Lista (opcional para almacenar)
USO DE FUNCIONES: Si
JUSTIFICACIÓN: Se genera una secuencia iterativa

Hacer un programa en Python que imprima la serie de la sumatoria Σ1/n, 
donde n es ingresado por el usuario.
a. Ejemplo de salida: 1/1, 1/2, 1/3, ... , 1/n
=============================================="""
def obtener_numero(mensaje:str) -> int:
    while True:
        try:
            num = int(input(mensaje))
            if num <= 0:
                print("Debes ingresar un número positivo mayor a cero")
            else:
                return num
        except ValueError:
            print("Registra un número válido")

def main():
    numero = obtener_numero("Escribe un número: ")
    resultados = [f"1/{i}" for i in range(1, numero+1)]

    print(", ".join(resultados))
if __name__ == "__main__":
    main()


"""==========================================
EJERCICIO 9: Valor de sumatoria 1/n
ESTRUCTURA PRINCIPAL: Repetitiva
ESTRUCTURAS DE DATOS: No necesaria (variable acumuladora)
USO DE FUNCIONES: Si
JUSTIFICACIÓN: Se genera una secuencia iterativa

Hacer un programa en Python que imprima el valor obtenido de la sumatoria
Σ1/n, donde n es ingresado por el usuario.
=============================================="""
def obtener_numero(mensaje:str) -> int:
    while True:
        try:
            num = int(input(mensaje))
            if num <= 0:
                print("Debes ingresar un número positivo mayor a cero")
            else:
                return num
        except ValueError:
            print("Registra un número válido")

def main():
    numero = obtener_numero("Escribe un número: ")
    suma = sum(1/i for i in range(1, numero+1))

    print(suma)
if __name__ == "__main__":
    main()


"""==========================================
EJERCICIO 10: Sumatoria n² con límite
ESTRUCTURA PRINCIPAL: Repetitiva y Condicional
ESTRUCTURAS DE DATOS: No
USO DE FUNCIONES: Si
JUSTIFICACIÓN: Repetitiva para suma, condicional para restringir n ≤ 5

Hacer un programa en Python que imprima la serie y además el valor obtenido
de la sumatoria Σn^2 , donde n es ingresado por el usuario 
(n no debe ser mayor de 5).
=============================================="""
def obtener_numero(mensaje:str) -> int:
    while True:
        try:
            num = int(input(mensaje))
            if 0 < num <= 5:
                return num
            else:
                print("Ingresa un número positivo mayor a cero")
        except ValueError:
            print("Ingresa un número válido")

def main():
    numero = obtener_numero("Ingresa un número entero: ")
    resultados = [f"{i}²" for i in range(1, numero+1)]
    suma = sum(i**2 for i in range(1, numero+1))

    print("Serie: ", ", ".join(resultados))
    print(f"Suma total de la serie: {suma}.")
if __name__ == "__main__":
    main()


"""==========================================
EJERCICIO 11: Registro de calificaciones
ESTRUCTURA PRINCIPAL: Repetitiva y Condicional
ESTRUCTURAS DE DATOS: Diccionario
USO DE FUNCIONES: Si
JUSTIFICACIÓN: Repetitiva para múltiples registros, condicional para validar entrada

Hacer un programa en Python que permita registrar las calificaciones
de varios estudiantes. Cada estudiante tiene un nombre y una lista de
calificaciones, implementa funciones para:
Agregar un estudiante
Agregar una calificación
Calcular el promedio de cada estudiante
=============================================="""
def obtener_nombre(mensaje_nombre: str) -> str:
    nombre = str(input(mensaje_nombre)).strip()
    return nombre

def obtener_calif(mensaje_calif: str) -> float:
    while True:
        try:
            calif = float(input(mensaje_calif))
            if 0 <= calif <= 10:
                return calif
            else:
                print("Ingresa un número válido de 0 a 10")
        except ValueError:
            print("Ingresa un dato numérico válido")

def main():
    estudiantes = {}

    while True:
        try:
            continuar = input("¿Deseas continuar con el registro (y/n)? ").strip().lower()

            if continuar == "y":
                nom = obtener_nombre("Ingresa el nombre del alumno: ")
                cal = obtener_calif("Ingresa la calificación del alumno: ")

                estudiantes[nom] = cal

            elif continuar == "n":
                print("Saliendo del programa")
                break

            else:
                print("Ingresa solo 'y' o 'n'")
        except ValueError:
            print("Ingresa unu caracter válido")

    print("Estudiantes registrados:")
    for nom, cal in estudiantes.items():
        print(f"{nom}: {cal}")
if __name__ == "__main__":
    main()


"""==========================================
EJERCICIO 12: Inventario de productos
ESTRUCTURA PRINCIPAL: Repetitiva y Condicional
ESTRUCTURAS DE DATOS: Diccionario y Tupla
USO DE FUNCIONES: Si
JUSTIFICACIÓN: Menú iterativo y validaciones

Crea un programa en Python para gestionar un pequeño
catálogo de productos. Cada producto tendrá:
    un código clave
    una tupla con nombre, precio y cantidad disponible
Implementa funciones para:
    Agregar productos
    Consultar un producto por código
    Calcular el valor total del inventario
=============================================="""
def obtener_codigo(mensaje: str, inventario: dict) -> str:
    while True:
        codigo = input(mensaje).strip().upper()
        if not codigo:
            print("El código no puede estar vacío")
        elif codigo in inventario:
            print("El código ya existe")
        else:
            return codigo

def obtener_texto(mensaje: str) -> str:
    while True:
        texto = input(mensaje).strip()
        if not texto:
            print("No puede estar vacío")
        else:
            return texto

def obtener_precio(mensaje: str) -> float:
    while True:
        try:
            precio = float(input(mensaje))
            if precio <= 0:
                print("El precio debe ser mayor a 0")
            else:
                return precio
        except ValueError:
            print("Ingresa un número válido")

def obtener_cantidad(mensaje: str) -> int:
    while True:
        try:
            cantidad = int(input(mensaje))
            if cantidad < 0:
                print("La cantidad no puede ser negativa")
            else:
                return cantidad
        except ValueError:
            print("Ingresa un número entero válido")

def agregar_producto(inventario: dict):
    codigo = obtener_codigo("Código del producto: ", inventario)
    nombre = obtener_texto("Nombre del producto: ")
    precio = obtener_precio("Precio: ")
    cantidad = obtener_cantidad("Cantidad: ")

    inventario[codigo] = (nombre, precio, cantidad)

def consultar_producto(inventario: dict):
    codigo = input("Ingresa el código del producto: ").strip().upper()

    if codigo in inventario:
        nombre, precio, cantidad = inventario[codigo]
        print(f"Código: {codigo}")
        print(f"Nombre: {nombre}")
        print(f"Precio: {precio}")
        print(f"Cantidad: {cantidad}")
    else:
        print("Producto no encontrado")

def valor_total(inventario: dict):
    total = 0
    for nombre, precio, cantidad in inventario.values():
        total += precio * cantidad

    print(f"\nValor total del inventario: {total}")

def main():
    inventario = {}

    while True:
        print("\n--- MENÚ ---")
        print("1. Agregar producto")
        print("2. Consultar producto")
        print("3. Valor total del inventario")
        print("4. Salir")

        opcion = input("Selecciona una opción: ").strip()

        if opcion == "1":
            agregar_producto(inventario)
        elif opcion == "2":
            consultar_producto(inventario)
        elif opcion == "3":
            valor_total(inventario)
        elif opcion == "4":
            print("Saliendo del sistema")
            break
        else:
            print("Opción inválida")

if __name__ == "__main__":
    main()


"""==========================================
EJERCICIO 13: Conteo de palabras
ESTRUCTURA PRINCIPAL: Repetitiva
ESTRUCTURAS DE DATOS: Diccionario
USO DE FUNCIONES: Si
JUSTIFICACIÓN: teración sobre palabras

Escribe una función en Python que reciba una frase y devuelva 
un diccionario con la cantidad de veces que aparece 
cada palabra. Ignora mayúsculas y signos de puntuación
=============================================="""
import string

def obtener_frase(mensaje: str) -> str:
    while True:
        frase = input(mensaje).strip()
        if not frase:
            print("La frase no puede estar vacía")
        else:
            return frase

def limpiar_texto(frase: str) -> str:
    frase = frase.lower()

    for signo in string.punctuation:
        frase = frase.replace(signo, "")

    return frase

def contar_palabras(frase: str) -> dict[str, int]:
    palabras = frase.split()
    conteo = {}

    for palabra in palabras:
        if palabra in conteo:
            conteo[palabra] += 1
        else:
            conteo[palabra] = 1

    return conteo

def mostrar_resultado(conteo: dict[str, int]):
    for palabra, cantidad in conteo.items():
        print(f"{palabra}: {cantidad}")

def main():
    frase = obtener_frase("Ingresa una frase: ")
    frase_limpia = limpiar_texto(frase)

    resultado = contar_palabras(frase_limpia)
    mostrar_resultado(resultado)

if __name__ == "__main__":
    main()


"""==========================================
EJERCICIO 14: Gestión de agenda
ESTRUCTURA PRINCIPAL: Repetitiva y Condicional
ESTRUCTURAS DE DATOS: Diccionario y Tupla
USO DE FUNCIONES: Si
JUSTIFICACIÓN: Menú mas validaciones de existencia

Crea un programa en Python para gestionar una agenda donde 
cada contacto tiene:
    un nombre (clave del diccionario)
    una tupla con teléfono y correo
Implementa funciones para:
    Agregar un contacto
    Buscar un contacto por nombre
    Actualizar datos de un contacto
=============================================="""
def obtener_nombre(mensaje: str) -> str:
    while True:
        nombre = input(mensaje).strip()
        if not nombre:
            print("El nombre no puede estar vacío")
        else:
            return nombre

def obtener_telefono(mensaje: str) -> str:
    while True:
        tel = input(mensaje).strip()
        if not tel:
            print("El teléfono no puede estar vacío")
        else:
            return tel

def obtener_correo(mensaje: str) -> str:
    while True:
        correo = input(mensaje).strip()
        if not correo:
            print("El correo no puede estar vacío")
        else:
            return correo

def agregar_contacto(agenda: dict):
    nombre = obtener_nombre("Nombre: ")

    if nombre in agenda:
        print("El contacto ya existe")
        return

    telefono = obtener_telefono("Teléfono: ")
    correo = obtener_correo("Correo: ")

    agenda[nombre] = (telefono, correo)
    print("Contacto agregado")

def buscar_contacto(agenda: dict):
    nombre = input("Nombre a buscar: ").strip()

    if nombre in agenda:
        telefono, correo = agenda[nombre]
        print(f"Nombre: {nombre}")
        print(f"Teléfono: {telefono}")
        print(f"Correo: {correo}")
    else:
        print("Contacto no encontrado")

def actualizar_contacto(agenda: dict):
    nombre = input("Nombre del contacto a actualizar: ").strip()

    if nombre in agenda:
        telefono = obtener_telefono("Nuevo teléfono: ")
        correo = obtener_correo("Nuevo correo: ")

        agenda[nombre] = (telefono, correo)
    else:
        print("Contacto no existe")

def mostrar_agenda(agenda: dict):
    if not agenda:
        print("Agenda vacía")
        return

    for nombre, (telefono, correo) in agenda.items():
        print(f"{nombre} -> Tel: {telefono}, Correo: {correo}")

def main():
    agenda = {
        "María": ("555-1234", "maria@gmail.com"),
        "Luis": ("555-5678", "luis@hotmail.com")
    }

    while True:
        print("\n--- MENÚ ---")
        print("1. Agregar contacto")
        print("2. Buscar contacto")
        print("3. Actualizar contacto")
        print("4. Mostrar agenda")
        print("5. Salir")

        opcion = input("Selecciona una opción: ").strip()

        if opcion == "1":
            agregar_contacto(agenda)
        elif opcion == "2":
            buscar_contacto(agenda)
        elif opcion == "3":
            actualizar_contacto(agenda)
        elif opcion == "4":
            mostrar_agenda(agenda)
        elif opcion == "5":
            print("Saliendo del programa")
            break
        else:
            print("Opción inválida")

if __name__ == "__main__":
    main()


"""==========================================
EJERCICIO 15: Lista y Tuplas
ESTRUCTURA PRINCIPAL: Repetitiva
ESTRUCTURAS DE DATOS: Lista y Tupla
USO DE FUNCIONES: Si
JUSTIFICACIÓN: Recorrido de lista para cálculos

Crea una función en Python que reciba una lista de números
y devuelva una tupla con los siguientes datos:
    número mayor
    número menor
    promedio
    cantidad de números pares
    cantidad de números impares
=============================================="""
def obtener_lista(mensaje: str) -> list[int]:
    while True:
        entrada = input(mensaje).strip()
        try:
            numeros = [int(x) for x in entrada.split()]
            if not numeros:
                print("Debes ingresar al menos un número")
                continue
            return numeros
        except ValueError:
            print("Ingresa solo números enteros separados por espacio")

def analizar_lista(numeros: list[int]) -> tuple[int, int, float, int, int]:
    mayor = max(numeros)
    menor = min(numeros)
    promedio = sum(numeros) / len(numeros)

    pares = 0
    impares = 0

    for n in numeros:
        if n % 2 == 0:
            pares += 1
        else:
            impares += 1

    return (mayor, menor, promedio, pares, impares)

def mostrar_resultado(resultado: tuple[int, int, float, int, int]):
    mayor, menor, promedio, pares, impares = resultado

    print("\nResultados:")
    print(f"Mayor: {mayor}")
    print(f"Menor: {menor}")
    print(f"Promedio: {round(promedio, 2)}")
    print(f"Pares: {pares}")
    print(f"Impares: {impares}")

def main():
    numeros = obtener_lista("Ingresa números separados por espacio: ")
    resultado = analizar_lista(numeros)
    mostrar_resultado(resultado)

if __name__ == "__main__":
    main()