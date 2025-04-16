[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/5g0zSLVN)
[![Open in Codespaces](https://classroom.github.com/assets/launch-codespace-2972f46106e565e64193e422d61a12cf1da4916b45550586e14ef0a7c637dd04.svg)](https://classroom.github.com/open-in-codespaces?assignment_repo_id=19207112)

print("Practica 4")
print("Jose Javier Perez Ledesma")

import string # Se importa el modulo string que contiene una lista de signos de puntuacion

# Cargar palabras válidas en un diccionario
def cargar_diccionario():
    dicc = {}
    try:
        with open("palabras.txt", "r", encoding="utf-8") as f: # Abre al archivo palabras.txt que contiene una palabra valida por linea 
            for linea in f: # el utf-8 se utiliza para representar caracteres como secuencia de bytes para que los archivos de texto puedan leerse por computadoras
                dicc[linea.strip().lower()] = 0 # Cada palabra se combierte en minuscula y se guarda como clave en un diccionario
    except:
        print("No se pudo abrir 'palabras.txt'") # Si el archivo no se puede abrir muestra un errror y termina el programa 
        exit()
    return dicc

# Revisar un archivo de texto
def revisar_texto(dicc):
    nombre = input("Nombre del archivo a revisar: ") # Solicitamnos el nombre del archivo a revisar
    try:
        with open(nombre, "r", encoding="utf-8") as f: # Intenta abrir el archivo y lee todo su contenido
            texto = f.read()
    except:
        print("No se pudo abrir el archivo.") # Si falla mustra un mensaje de error y sale la funcion
        return

    for signo in string.punctuation: # Elimina todos los signos de puntuacion del texto
        texto = texto.replace(signo, "")
    
    errores = []
    for palabra in texto.lower().split(): # combierte todo el texto a minuscula y lo divide en palabras
        if palabra not in dicc and palabra not in errores: # verifica si cada palabra esta en el diccionario 
            errores.append(palabra) # Si no esta y no se ha detectado antes, se guarda en la lista de errores

    if errores:
        print("Errores encontrados:") # Muestra las palabras desconocidas
        for e in errores:
            print("-", e)
    else:
        print("No hay errores de ortografía.") # Si no hay errores lo indica

# Programa principal
revisar_texto(cargar_diccionario()) # Carga el diccionario y pasa ese diccionario a la funcion revisar texto
