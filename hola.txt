from tkinter import *
from tkinter import messagebox, Label, Button, PhotoImage, LEFT
from PIL import Image, ImageTk

def send_data():
    # Obtener los datos de los campos de entrada
    DNIs_data = DNIs.get()
    Nombre_data = Nombre.get()
    Fecha_data = Fecha.get()
    print(DNIs_data, "\t", Nombre_data, "\t", Fecha_data)

    # Guardar los datos en un archivo de texto
    with open("user.txt", "a") as file:
        file.write(f"{DNIs_data}\t{Nombre_data}\t{Fecha_data}\n")

    print("Registrado con éxito. DNI: {} | Nombre: {} | Fecha de Nacimiento: {}".format(DNIs_data, Nombre_data, Fecha_data))

    # Limpiar los campos de entrada después de enviar los datos
    DNIs_entry.delete(0, END)
    Nombre_entry.delete(0, END)
    Fecha_entry.delete(0, END)
    messagebox.showinfo("Guardado", "Registrado con éxito")

def show_position(event):
    # Actualizar el label con las coordenadas del mouse
    position_label.config(text=f"Posición del mouse: x={event.x}, y={event.y}")

# Configuración de la ventana principal
mywindows = Tk()
mywindows.geometry("600x600")
mywindows.title("Formulario de Registro Python y Tkinter")
mywindows.resizable(False, False)

# Vincular el movimiento del mouse a la función para mostrar la posición
mywindows.bind("<Motion>", show_position)

# Cargar la fuente personalizada
custom_font_path = "BEBASNEUE.OTF"
custom_font_size = 14

# Cargar imagen de fondo
bg_image = Image.open("background.png")
bg_photo = ImageTk.PhotoImage(bg_image)

# Etiqueta de imagen para el fondo
background_label = Label(mywindows, image=bg_photo)
background_label.place(relwidth=1, relheight=1)

# Título del formulario
main_title = Label(text="Formulario de Registro", compound=LEFT, font=(custom_font_path, custom_font_size), bg="#e7fdd3", fg="black", width="100", height="2")
main_title.pack()

# Etiqueta para mostrar las coordenadas del mouse
position_label = Label(mywindows, text="Posición del mouse: x=0, y=0", font=("Arial", 12), bg="#e7fdd3", fg="black")
position_label.pack(pady=10)

# Etiquetas y campos de entrada con imágenes
dni_image = Image.open("dni_icon.png").resize((30,30))
dni_photo = ImageTk.PhotoImage(dni_image)

# Etiquetas y campos de entrada
DNI_label = Label(mywindows, image=dni_photo, text=" DNI,Cedula,Pasaporte", compound=LEFT, font=(custom_font_path, custom_font_size), bg="#e7fdd3", fg="black", width=240, anchor=W)
DNI_label.place(x=22, y=60)

username_image = Image.open("nombre_icon.png").resize((30,30))
username_photo = ImageTk.PhotoImage(username_image)

username_label = Label(image=username_photo, text=" Nombre Completo", compound=LEFT, font=(custom_font_path, custom_font_size), bg="#e7fdd3", fg="black", width=240, anchor=W)
username_label.place(x=22, y=120)

date_image = Image.open("fecha_icon.png").resize((30,30))
date_photo = ImageTk.PhotoImage(date_image)

Date_label = Label(image=date_photo, text=" Fecha de Nacimiento", compound=LEFT, font=(custom_font_path, custom_font_size), bg="#e7fdd3", fg="black", width=240, anchor=W)
Date_label.place(x=22, y=190)

# Variables para almacenar los datos de entrada
DNIs = StringVar()
Nombre = StringVar()
Fecha = StringVar()

# Campos de entrada de texto
DNIs_entry = Entry(textvariable=DNIs, width=40)
DNIs_entry.place(x=22, y=95)

Nombre_entry = Entry(textvariable=Nombre, width=40)
Nombre_entry.place(x=22, y=160)

Fecha_entry = Entry(textvariable=Fecha, width=40)
Fecha_entry.place(x=22, y=230)

# Botón de envío con imagen
send_image = Image.open("send_icon.png").resize((200,63))
send_photo = ImageTk.PhotoImage(send_image)

# Botón de envío
submit_btn = Button(mywindows, image=send_photo, text=" Enviar Info", font=("cambria", 15), compound=CENTER, command=send_data, fg="#e7fdd3", bd=0, relief=FLAT)
submit_btn.place(x=314, y=475)

# Ejecutar la ventana principal
mywindows.mainloop()