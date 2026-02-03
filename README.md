# clase-12
**repaso considerando una app de mascotas**

class Mascota:
  def __init__(self,nombre,edad):
    #atributos privados (encapsulamiento)
    self._nombre = nombre
    self._edad = edad

  #getters

  def get_nombre(self):
    return self._nombre

  def get_edad(self):
    return self._edad

  #setters

  def set_nombre(self,nuevo_nombre):
   self._nombre = nuevo_nombre

  #metodo comun para todas las mascotas

  def presentarse(self):
    print(f"soy {self._nombre} y tengo {self._edad} años.")

***ahora vamos a crear un perro y un gato, sino que vamos a heredar la estructura de mascota***

class perro(Mascota):
  def hablar(self):
    print("¡guau!")

class gato(Mascota):
  def hablar(self):
    print("¡miau!")

polimorfismo significa muchas formas,es decir una misma funcion "hablar" responde de forma diferente en todas las mascotas.

si bien las mascotas son distintas se usa un solo metodo en comun

def hacer_hablar(mascota):
  mascota.hablar()#aca sucede el polimorfismo


firulais = perro("firulais",5)
mishi = gato("mishi",3)

hacer_hablar(firulais)
hacer_hablar(mishi)

*encapsulamiento*

**encapsular es proteger. marcamos atributos como privados para evitar que el usuario del codigo cambie sin querer.**

print(firulais.get_nombre())
firulais.set_nombre

firulais._nombre

**reutilizar codigo**

pensar segmentos de codigo que sean comunes a los objetivos

firulais.presentarse()
mishi.presentarse()

"""
APP QUE GESTIONA ESTUDIANTES Y NOTAS
"""
# Clase alumno - representa el nombre, edad, lista de notas

class Alumno:
  def __init__(self, nombre, edad):
    self._nombre = nombre
    self._edad = edad
    self._notas = []

  def get_nombre(self):
    return self._nombre

  def get_edad(self):
    return self._edad

  def get_notas(self):
    return self._notas

  # SETTER

  def set_nombre(self, nuevo_nombre):
    self._nombre = nuevo_nombre

  def set_edad(self, nueva_edad):

    if nueva_edad > 0:
      self._edad = nueva_edad
    else:
      print("Edad inválida, no se actualizó")

  # MÉTODO DE COMPORTAMIENTO

  def agregar_nota(self, nota):
    if 0 <= nota <= 10:
      self._nota.append(nota)
    else:
      print("Nota fuera del rango")

  def calcular_promedio(self):
    if len(self._notas) == 0:
      return None

    suma = sum(self._notas)
    promedio = suma / len(self._notas)

    return promedio

  def esta_aprobado(self):
    promedio = self.calcular_promedio()
    if promedio is None:
      return False
    return promedio >= 6

  def mostrar_detalle(self):
    print(f"Alumno: {self._nombre} ({self._edad} años)")
    print(f"Notas: {self._notas}")

    promedio = self.calcular_promedio()
    if promedio is None:
      print("Promedio: sin notas cargadas")
      print("Estado: sin calificar")
    else:
      print(f"Promedio: {promedio:.2f}")
      if self.esta_aprobado():
        print("Estado: aprobado")
      else:
        print("Estado: desaprobado")

class curso:
  def __init_(self,nombre_curso):
   self._nombre_curso = nombre_curso
   self._alumnos = []

  def agregar_alumno(self,alumno):
    self.alumnos.append(alumno)
    print(f"alumno '{alumno.get_nombre()}' agregado al curso")

  def buscar_alumno_por_nombre(self,nombre):
    for alumno in self._alumnos:
      if alumno.get_nombre().lower() == nombre.lower():
        return alumno
        return None
  def listar_alumnos(self):
    if len(self._alumnos) == 0:
      print("El curso está vacío")
      return

    print(f"\nAlumnos del curso {self._nombre_curso}")

    for i, alumno in enumerate(self._alumnos, start = 1):
      print(f"{i}. {alumno.get_nombre()} ({alumno.get_edad} años)")

  def mostrar_detalle_curso(self):
    print(f"nombre del curso {self.nombre_curso}")
    print(f"alumnos del curso {self.alumnos}")
    """
    Muestra el detalle de todos los alumnos del curso,
    usando el método mostrar_detalle() de cada Alumno
    Acá se va a reutilizar métodos
    """

  def calcular_promedio_general(self):

    """
    Calcula el promedio general del curso
    Es decir, el promedio de todos los promedios de los alumnos
    """

funciones del menu

def mostrar_menu():
  print("1. Agregar alumno")
  print("2. Listar alumnos")
  print("3. Cargar nota a un alumno")
  print("4. Mostrar detalle de un alumno")
  print("5. Mostrar detalle de TODO el curso")
  print("6. Ver promedio general del curso")
  print("7. Salir")


main

#Creamos un curso

  nombre_curso = input("Ingrese el nombre del curso")
  curso = nombre_curso

  opcion = 0

  while opcion !=7:
    mostrar_menu()
    try:
      opcion = int(input("Elegi una opción: "))
    except ValueError:
      print("Por favor, ingrese un número válido")
      continue


    if opcion == 1:
      nombre = input("Ingrese el nombre del alumno")
      try:
        edad = int(input("Ingrese la edad"))
      except ValueError:
        print("Edad inválida, vuelva al menú")
        continue

      nuevo_alumno = Alumno(nombre,edad)
      curso.agregar_alumno(nuevo_alumno)

    if opcion == 2:
      curso.listar_alumnos()

    elif opcion == 3:
      nombre = input("Ingrese el nombre del alumno que desea ingresar nota")
      alumno = curso.buscar_alumno_por_nombre(nombre)
      if alumno is None:
        print("No se encontró dicho alumno")
      else:
        try:
          nota = float(input("Ingrese la nota de 0-10:"))
        except ValueError:
          print("Nota inválida.")
          continue


        alumno.agregar_nota(nota)
        print("Nota agregada correctamente")
    elif opcion == 4:
      nombre = input("Nombre del alumno: ")
      alumno = curso.buscar_alumno_por_nombre(nombre)
      if alumno is None:
        print("No se encontró un alumno con ese nombre")
      else:
        alumno.mostrar_detalle()

    elif opcion == 5:
      curso.mostrar_detalle_curso()

    elif opcion == 6:
      promedio_general = curso.calcular_promedio_general()
      if promedio_general is None:
        print("No se pudo calcular")
      else:
        print("El promedio general es",promedio_general)
    elif opcion == 7:
      print("Saliendo del programa")
