import re
import random

def menu():
    """Despliega el menú de opciones."""
    print("=== Menú===")
    print("1. Identificar tipo de gramática")
    print("2. Derivar cadenas de la gramática")
    print("3. Calcular longitud máxima de cadenas")
    print("4. Salir")

def validar_regla(regla):
    """Verifica si la regla está en el formato 'A -> aB'."""
    if '->' not in regla:
        print(f"Regla inválida: {regla}. Debe estar en el formato 'A -> aB'.")
        return False

    izquierda, derecha = regla.split('->', 1)
    izquierda = izquierda.strip()
    derecha = derecha.strip()

    if not (izquierda.isalpha() and izquierda.isupper() and len(izquierda) == 1):
        print(f"Regla inválida: {regla}. La parte izquierda debe ser una sola letra mayúscula.")
        return False

    if not derecha:
        print(f"Regla inválida: {regla}. La parte derecha no puede estar vacía.")
        return False

    return True

def es_regular(gramatica):
    """Determina si una gramática es regular."""
    for regla in gramatica:
        izquierda, derecha = regla.split('->', 1)
        izquierda = izquierda.strip()
        derecha = derecha.strip()

        if not re.fullmatch(r'[a-z]*[A-Z]?', derecha):
            return False
    return True

def derivar_cadenas(gramatica, simbolo_inicial, max_pasos=5):
    """Genera cadenas válidas a partir de una gramática dada."""
    # Crear un diccionario con las reglas: { 'S': ['aSb', 'ε'] }
    reglas = {}
    for regla in gramatica:
        izquierda, derecha = regla.split('->', 1)
        izquierda = izquierda.strip()
        derecha = derecha.strip()
        if izquierda not in reglas:
            reglas[izquierda] = []
        reglas[izquierda].append(derecha)

    cadena = simbolo_inicial

    # Realizar derivaciones hasta el límite de pasos
    for _ in range(max_pasos):
        nueva_cadena = ""
        derivado = False  # Marca si se realizó una sustitución

        for simbolo in cadena:
            if simbolo in reglas:
                # Filtrar las producciones para evitar usar `ε` si hay otras opciones
                opciones = [p for p in reglas[simbolo] if p != 'ε']
                if opciones:
                    produccion = random.choice(opciones)
                else:
                    produccion = 'ε'

                # Reemplazar el símbolo con la producción seleccionada
                nueva_cadena += produccion
                derivado = True
            else:
                nueva_cadena += simbolo  # Mantener los terminales sin cambio

        cadena = nueva_cadena.replace('ε', '')  # Eliminar `ε` de la cadena

        if not derivado:
            break  # Si no hubo más derivaciones, terminar

    return cadena

def longitud_maxima(gramatica):
    """Calcula la longitud máxima de las cadenas derivables."""
    for regla in gramatica:
        if re.search(r'[A-Z] -> .*[A-Z]', regla):
            return -1  # Hay recursión o posibilidad infinita
    return sum(len(regla.split('->')[1].strip()) for regla in gramatica)

def main():
    while True:
        menu()
        opcion = input("Seleccione una opción: ")

        if opcion == '1':
            print("Ingrese las reglas de la gramática (una por línea, 'fin' para terminar):")
            gramatica = []
            while True:
                regla = input().strip()
                if regla.lower() == 'fin':
                    break
                if validar_regla(regla):
                    gramatica.append(regla)

            if es_regular(gramatica):
                print("La gramática es Regular.")
            else:
                print("La gramática es Independiente de Contexto.")

        elif opcion == '2':
            print("Ingrese las reglas de la gramática (una por línea, 'fin' para terminar):")
            gramatica = []
            while True:
                regla = input().strip()
                if regla.lower() == 'fin':
                    break
                if validar_regla(regla):
                    gramatica.append(regla)

            simbolo_inicial = input("Ingrese el símbolo inicial: ").strip()
            cadena = derivar_cadenas(gramatica, simbolo_inicial)
            print(f"Cadena derivada: {cadena}")

        elif opcion == '3':
            print("Ingrese las reglas de la gramática (una por línea, 'fin' para terminar):")
            gramatica = []
            while True:
                regla = input().strip()
                if regla.lower() == 'fin':
                    break
                if validar_regla(regla):
                    gramatica.append(regla)

            longitud = longitud_maxima(gramatica)
            if longitud == -1:
                print("La gramática puede generar cadenas de longitud infinita.")
            else:
                print(f"La longitud máxima de las cadenas es: {longitud}")

        elif opcion == '4':
            print("Saliendo del programa.")
            break

        else:
            print("Opción no válida. Intente de nuevo.")

if __name__ == "__main__":
    main()
