# atajos-de-teclado
casandra
import tkinter as tk
from tkinter import messagebox

# Crear ventana principal
ventana = tk.Tk()
ventana.title("Gestor de Tareas - Jhonnatan Chacaguasay")
ventana.geometry("400x400")
ventana.config(bg="#e8f0f2")

# Lista de tareas
tareas = []

# Función para agregar tarea
def agregar_tarea(event=None):
    tarea = entrada_tarea.get().strip()
    if tarea:
        lista_tareas.insert(tk.END, tarea)
        entrada_tarea.delete(0, tk.END)
    else:
        messagebox.showwarning("Advertencia", "Debe ingresar una tarea antes de agregar.")

# Función para marcar como completada
def completar_tarea(event=None):
    seleccion = lista_tareas.curselection()
    if seleccion:
        indice = seleccion[0]
        texto = lista_tareas.get(indice)
        if not texto.startswith("✔ "):
            lista_tareas.delete(indice)
            lista_tareas.insert(indice, "✔ " + texto)
            lista_tareas.itemconfig(indice, {'fg': 'green'})
    else:
        messagebox.showinfo("Info", "Seleccione una tarea para marcarla como completada.")

# Función para eliminar tarea
def eliminar_tarea(event=None):
    seleccion = lista_tareas.curselection()
    if seleccion:
        lista_tareas.delete(seleccion[0])
    else:
        messagebox.showinfo("Info", "Seleccione una tarea para eliminarla.")

# Función para salir
def salir(event=None):
    ventana.destroy()

# --- Elementos GUI ---

# Campo de entrada
entrada_tarea = tk.Entry(ventana, font=("Arial", 12))
entrada_tarea.pack(pady=10, padx=10, fill=tk.X)

# Botones
frame_botones = tk.Frame(ventana, bg="#e8f0f2")
frame_botones.pack()

btn_agregar = tk.Button(frame_botones, text="Agregar", command=agregar_tarea, bg="#0078D7", fg="white")
btn_agregar.grid(row=0, column=0, padx=5)

btn_completar = tk.Button(frame_botones, text="Completar", command=completar_tarea, bg="#28A745", fg="white")
btn_completar.grid(row=0, column=1, padx=5)

btn_eliminar = tk.Button(frame_botones, text="Eliminar", command=eliminar_tarea, bg="#DC3545", fg="white")
btn_eliminar.grid(row=0, column=2, padx=5)

# Lista de tareas
lista_tareas = tk.Listbox(ventana, font=("Arial", 12), selectmode=tk.SINGLE)
lista_tareas.pack(pady=10, padx=10, fill=tk.BOTH, expand=True)

# --- Atajos de teclado ---
ventana.bind('<Return>', agregar_tarea)      # Enter -> Agregar tarea
ventana.bind('<c>', completar_tarea)         # C -> Completar tarea
ventana.bind('<C>', completar_tarea)
ventana.bind('<Delete>', eliminar_tarea)     # Delete -> Eliminar tarea
ventana.bind('<d>', eliminar_tarea)          # D -> Eliminar tarea
ventana.bind('<D>', eliminar_tarea)
ventana.bind('<Escape>', salir)              # Escape -> Salir

ventana.mainloop()
