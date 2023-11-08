# Aplicacion de editor de texto

## Python


from tkinter import * # importamos la libreria tk que sera la base de todo
from tkinter.filedialog import askopenfilename # importamos para interactuar con el explorador de archivos
from tkinter.filedialog import asksaveasfilename # Importamos para interactuar con el explorador de archivos a la hora de "guardar como..."
from tkinter.messagebox import askquestion  # Importamos para mostrar una ventana emergente (diálogo) que presenta al usuario una pregunta con dos opciones
import webbrowser  # Importamos el módulo webbrowser para interactuar con el navegador
#------------------------------------------------------------------------------------------------------ 
# Opciones de "Archivo"
# Funcion "Archivo Nuevo"
def Archivonuevo():
    Guardarcomo() # LLamamos y re utilizamos la funcion "Guardar como" ya que basicamente seria lo mismo porque puedes guardar un archivo que contenga o no algo adentro
# Muestra una ventana emergente
    ventana_nuevo_archivo = Toplevel(ventana)
    ventana_nuevo_archivo.title("Lector y Editor de Archivos de Texto")
    etiqueta = Label(ventana_nuevo_archivo, text="Archivo creado")
    etiqueta.pack(padx=20, pady=20) 
# Agregar un archivo actual global para rastrear el archivo abierto
archivo_actual = None
# Funcion "Abrir archivo"
def Abrir():
    global archivo_actual
    archivo_actual = askopenfilename()
    if archivo_actual:
        print(f"Archivo seleccionado: {archivo_actual}")
        with open(archivo_actual, 'r') as file:
            contenido = file.read()
            texto.delete('1.0', END)
            texto.insert(END, contenido)           
# Función "Guardar"
# Guardar el contenido en el archivo actual
def Guardar():
    if archivo_actual:
        contenido = texto.get('1.0', END)
        with open(archivo_actual, 'w') as file:
            file.write(contenido)
        print(f"Archivo guardado: {archivo_actual}")
# Función "Guardar Como"
# Guardar el contenido en un archivo con la extensión adecuada
def Guardarcomo():
    contenido = texto.get('1.0', END)
    archivo = asksaveasfilename(defaultextension=".txt", filetypes=[("Archivos de texto", "*.txt"), ("Archivos Python", "*.py"), ("Archivos C++", "*.cpp")])

    if archivo:
        if archivo.endswith(".py"):
            # Si es un archivo .py, asegúrate de que el contenido se guarde como código Python
            with open(archivo, 'w') as file:
                file.write(contenido)
        elif archivo.endswith(".cpp"):
            # Si es un archivo .cpp, asegúrate de que el contenido se guarde como código C++
            with open(archivo, 'w') as file:
                file.write(contenido)
        else:
            # Para otros tipos de archivo, guárdalos como texto simple
            with open(archivo, 'w') as file:
                file.write(contenido)
        print(f"Archivo guardado como: {archivo}")
# Funcion "Salir"
# Función para confirmar la salida
def ConfirmarSalir():
    respuesta = askquestion("Salir", "¿Quieres salir?")
    if respuesta == "yes":
        ventana.destroy()
#------------------------------------------------------------------------------------------------------    
# Opciones de "Editar"
# Función para copiar texto al portapapeles
def Copiar():
    selected_text = texto.get("sel.first", "sel.last")
    if selected_text:
        ventana.clipboard_clear()
        ventana.clipboard_append(selected_text)
# Función para pegar texto desde el portapapeles
def Pegar():
    try:
        texto.insert(INSERT, ventana.clipboard_get())
    except TclError:
        pass
# Función para cortar texto
def Cortar():
    selected_text = texto.get("sel.first", "sel.last")
    if selected_text:
        ventana.clipboard_clear()
        ventana.clipboard_append(selected_text)
        texto.delete("sel.first", "sel.last")
# Función para deshacer
def Deshacer():
    try:
        texto.edit_undo()
    except TclError:
        pass
# Función para rehacer
def Rehacer():
    try:
        texto.edit_redo()
    except TclError:
        pass
#------------------------------------------------------------------------------------------------------ 
# Opciones de "Ayuda"
# Funcion "Informacion"
def Informacion():
    ventana_informacion = Toplevel(ventana)
    ventana_informacion.title("Informacion")
    # Agrega etiquetas 
    Titulo = Label(ventana_informacion, text="Informacion:")
    Titulo.pack(padx=20, pady=10)
    etiqueta_informacion = Label(ventana_informacion, text="Esta es una aplicacion de Editor de Texto en Python con la librería Tkinter ofrece una plataforma")
    etiqueta_informacion.pack(padx=20, pady=10)
    etiqueta2_informacion = Label(ventana_informacion, text="versatil y amigable para crear, editar y gestionar documentos de texto. Esta aplicación incluye")
    etiqueta2_informacion.pack(padx=20, pady=10)
    etiqueta3_informacion = Label(ventana_informacion, text="una serie de caracteristicas esenciales para mejorar la experiencia del usuario, como la")
    etiqueta3_informacion.pack(padx=20, pady=10)
    etiqueta4_informacion = Label(ventana_informacion, text="capacidad de abrir, leer, modificar y guardar archivos de texto de manera sencilla.")
    etiqueta4_informacion.pack(padx=20, pady=10)
    Detalles = Label(ventana_informacion, text="Detalles:")
    Detalles.pack(padx=20, pady=10)  
    version = Label(ventana_informacion, text="Version 1.0.0")
    version.pack(padx=20, pady=10)  
    version = Label(ventana_informacion, text="Licencia aprobada")
    version.pack(padx=20, pady=10) 
# Función "MostrarManualUsuario"
def MostrarManualUsuario():
    # Crea una nueva ventana para mostrar el enlace
    ventana_manual = Toplevel(ventana)
    ventana_manual.title("Manual de Usuario")
    # Crea una etiqueta con el enlace
    etiqueta_enlace = Label(ventana_manual, text="Manual de Usuario:")
    etiqueta_enlace.pack(padx=20, pady=10)
    # Crea un enlace que abre el navegador al hacer clic
    enlace = Label(ventana_manual, text="https://acortar.link/eGLZHf", cursor="hand2")
    enlace.pack(padx=20, pady=10)
    def abrir_enlace(event):
        webbrowser.open("https://acortar.link/eGLZHf")
    enlace.bind("<Button-1>", abrir_enlace)   
# Funcion "integrantes"
def Integrantes():
    ventana_integrantes = Toplevel(ventana)
    ventana_integrantes.title("Integrantes")
    # Agrega etiquetas 
    etiqueta_nombre = Label(ventana_integrantes, text="Nombre: Eric Alexander Barillas Orozco")
    etiqueta_carnet = Label(ventana_integrantes, text="Carnet: 7690-22-18539")
    etiqueta_nombre.pack(padx=20, pady=10)
    etiqueta_carnet.pack(padx=20, pady=10)
#------------------------------------------------------------------------------------------------------ 
# Funcion "TemaOscuro"
# Colores para el tema claro
colorfondo = "white"
colortexto = "black"
# Colores para el tema oscuro
colorfondooscuro = "black"
colortextooscuro = "white"
# Función "TemaOscuro"
def CambiarTema():
    global colorfondo, colortexto
    if colorfondo == "white":
        colorfondo, colortexto = colorfondooscuro, colortextooscuro
    else:
        colorfondo, colortexto = "white", "black"
    ventana.configure(bg=colorfondo)
    texto.configure(bg=colorfondo, fg=colortexto)
#------------------------------------------------------------------------------------------------------ 
# Opciones de "color de texto"
# Funcion "Color de texto"
def CambiarColorTexto(color):
    global colortexto, texto
    if color == "Verde":
        colortexto = "green"
    elif color == "Rojo":
        colortexto = "red"
    elif color == "Azul":
        colortexto = "blue"
    texto.configure(fg=colortexto)
#------------------------------------------------------------------------------------------------------ 
# Crear una instancia de la ventana principal
ventana = Tk()
# Configurar el título de la ventana
ventana.title("Lector y Editor de Archivos de Texto")
# Configurar las dimensiones de la ventana
ventana.geometry("800x600")  # Cambia el tamaño de la ventana según tus necesidades
# Agregar un widget de texto
texto = Text(ventana, undo=True) # Al incluir undo=True, habilitas la funcionalidad de deshacer y rehacer en el widget de texto
texto.pack(fill=BOTH, expand=1)  # Agrega el widget de texto y lo expande para llenar la ventana
# Declarar menu
menu = Menu(ventana)
ventana.config(menu=menu)
#------------------------------------------------------------------------------------------------------ 
# Listas del menu
# Listas de archivo
Archivo = Menu(menu, tearoff=0)
Archivo.add_command(label="Nuevo Archivo...", command = Archivonuevo)
Archivo.add_command(label="Abrir Archivo...", command = Abrir)
Archivo.add_separator()
Archivo.add_command(label="Guardar", command = Guardar)
Archivo.add_command(label="Guardar como...", command= Guardarcomo)
Archivo.add_separator()
Archivo.add_command(label="Salir", command = ConfirmarSalir)
# Listas de editor
Editor = Menu(menu, tearoff=0)
Editor.add_command(label="Deshacer", command= Deshacer)
Editor.add_command(label="Rehacer", command= Rehacer)
Editor.add_separator()
Editor.add_command(label="Cortar", command = Cortar)
Editor.add_command(label="Copiar", command = Copiar)
Editor.add_command(label="Pegar", command =  Pegar)
# Listas de ayuda
Ayuda = Menu(menu, tearoff=0)
Ayuda.add_command(label="Informacion", command=Informacion)
Ayuda.add_command(label="Manual de usuario", command=MostrarManualUsuario)
Ayuda.add_command(label="Integrantes", command=Integrantes)
# Listas de temas
Temas = Menu(menu, tearoff=0)
Temas.add_command(label="Tema Oscuro", command=CambiarTema)
# Listas de color de texto
Colortexto = Menu(menu, tearoff=0)
Colortexto.add_command(label="Verde", command=lambda: CambiarColorTexto("Verde"))
Colortexto.add_command(label="Rojo", command=lambda: CambiarColorTexto("Rojo"))
Colortexto.add_command(label="Azul", command=lambda: CambiarColorTexto("Azul"))
#------------------------------------------------------------------------------------------------------ 
# Mostrar nuestro menú dentro de la ventana
menu.add_cascade(label="Archivo", menu=Archivo)
menu.add_cascade(label="Editor", menu=Editor)
menu.add_cascade(label="Ayuda", menu=Ayuda)
menu.add_cascade(label="Temas", menu=Temas)
menu.add_cascade(label="Color de texto", menu=Colortexto)
#------------------------------------------------------------------------------------------------------ 
# Esto inicia la aplicación
ventana.mainloop()
