# T.A.P-ApUnTeS_En_ClAsEs

## Unidad I: Interfaz Gráfica de Usuario (GUI)

La Interfaz Gráfica de Usuario (GUI) es el conjunto de elementos visuales que permiten la comunicación entre el ser humano y la máquina. Su evolución ha permitido pasar de complejas líneas de comandos a entornos intuitivos basados en ventanas, iconos y gestos. En esta unidad, exploraremos los fundamentos teóricos de las GUI y los aplicaremos de manera práctica utilizando Flet, un framework moderno para Python que permite crear aplicaciones multiplataforma (escritorio, web y móvil) con interfaces basadas en Flutter. Flet simplifica el desarrollo al proporcionar componentes listos para usar y un modelo de programación imperativo, manteniendo la potencia y el rendimiento de Flutter.
### 1.1 Creación de Interfaz Gráfica para Usuarios
#### Definición y propósito de una GUI
Una GUI es un sistema de interacción que utiliza objetos gráficos como ventanas, botones, iconos y menús para representar información y acciones disponibles. Su propósito es hacer que el manejo de la computadora sea más intuitivo, amigable y eficiente, explotando la capacidad humana de reconocimiento visual. Flet materializa estos conceptos al permitirnos construir interfaces mediante la instanciación de controles visuales sin preocuparnos por los detalles de bajo nivel de cada plataforma.
#### Modelo de programación en Flet
Flet adopta un modelo de programación imperativo, a diferencia del enfoque declarativo de Flutter nativo. Esto significa que construimos la interfaz paso a paso, modificando propiedades de objetos en tiempo de ejecución. La documentación oficial lo explica claramente: "Flet simplifica el modelo de Flutter al combinar 'widgets' más pequeños en 'controles' listos para usar con un modelo de programación imperativo".
#### El árbol de controles
Toda interfaz en Flet se organiza como un árbol de controles. La raíz es el objeto page, que representa la ventana o vista principal. A partir de ahí, se añaden controles hijos como `Column`, `Row`, `Container`, `Text`, `ElevatedButton`, etc. Esta estructura jerárquica refleja directamente el concepto teórico del árbol de componentes.

Por ejemplo, para crear una calculadora básica, primero se crea un `Container` que actuará como fondo, luego se añade una `Column` que contendrá la pantalla y las filas de botones, y dentro de cada fila se colocan los `ElevatedButton`. Esta organización en árbol es fundamental para comprender cómo se construye y actualiza la interfaz.
#### El contenedor `Page` 
La función principal de una aplicación Flet recibe un parámetro page de tipo ft.Page. Este objeto es el punto de entrada y controla propiedades globales como el título, el tamaño de la ventana, el color de fondo y, lo más importante, contiene la colección de controles que se muestran en pantalla.
```bash
import flet as ft

def main(page: ft.Page):
    page.title = "Mi Aplicación"
    page.add(ft.Text("¡Hola, mundo!"))

ft.app(target=main)
```
#### Controles de layout
Para estructurar la interfaz, Flet proporciona varios controles de diseño:
* `Row`: coloca sus hijos en una fila horizontal.
* `Column`: coloca sus hijos en una columna vertical.
* `Container`: un rectángulo que puede decorarse con color, bordes, padding y márgenes; a menudo se usa como caja contenedora.
* `ResponsiveRow`: similar a `Row` pero con capacidades de diseño adaptable (responsive) basadas en el tamaño de la pantalla.
Estos controles permiten implementar los principios de organización y jerarquía visual que exige una buena interfaz.
#### Principios de diseño aplicados en Flet
Flet facilita la aplicación de principios de diseño como:
* Simplicidad: con pocas líneas de código se pueden crear interfaces limpias.
* Consistencia: los controles tienen comportamientos predecibles en todas las plataformas.
* Retroalimentación: mediante eventos y actualizaciones visuales.
* Jerarquía visual: usando contenedores, tamaños de fuente y colores.
### Tipos De Eventos
#### Concepto De Evento
Un evento es una acción reconocida por el software, como un clic del ratón, una pulsación de tecla o un cambio en el valor de un campo de texto. En programación orientada a eventos, la aplicación permanece a la espera de que ocurran eventos y reacciona ejecutando el código correspondiente. Flet implementa este modelo de manera natural.
#### Clasificación De Eventos En Flet
Flet ofrece una amplia variedad de eventos que se pueden clasificar según su naturaleza:
#### Eventos de componentes básicos:
* `on_click`: se dispara al hacer clic sobre un control. Es el evento más común en botones, contenedores, íconos, etc.
* `on_hover`: se activa cuando el puntero del ratón entra o sale del área del control.
* `on_long_press`: se produce al mantener presionado un elemento (táctil o ratón).
#### Eventos de cambio de estado:
* `on_change`: ocurre cuando el valor de un control cambia. Se utiliza en TextField, Checkbox, Slider, Dropdown, Radio, etc.
* `on_submit`: específico de TextField, se dispara al presionar la tecla Enter.
* `on_focus / on_blur`: cuando un control gana o pierde el foco.
#### Eventos de teclado y ratón:
* `on_keyboard_event`: a nivel de página, captura pulsaciones de teclas globales.
* `on_scroll`: en controles con desplazamiento, como ListView.
* `on_tap_down, on_tap_up, on_double_tap`: eventos táctiles o de ratón de bajo nivel.
#### Eventos de ventana y ciclo de vida:
* `on_resize`: se activa cuando la ventana cambia de tamaño.
* `on_close`: al cerrar la ventana.
* `on_app_lifecycle_state_change`: escucha cambios en el estado de la aplicación (SHOW, HIDE, PAUSE, RESUME), crucial para aplicaciones móviles y web.
#### Tipado fuerte de los eventos
Una característica avanzada de Flet es el tipado fuerte de los objetos de evento. Cada evento envía un objeto que contiene información específica del contexto. Por ejemplo, un evento `on_click` de un botón envía un `ft.ControlEvent` que tiene propiedades como `control` (el botón que generó el evento) y `page` (la página actual). Para eventos de teclado, se recibe un `ft.KeyboardEvent` con propiedades como `key`, `shift`, `ctrl`, etc. Esto permite escribir manejadores con un conocimiento preciso de los datos disponibles.
```bash

def tecla_presionada(e: ft.KeyboardEvent):
    print(f"Tecla: {e.key}, Ctrl: {e.ctrl}, Shift: {e.shift}")

page.on_keyboard_event = tecla_presionada
```
### 1.3 Manejo de Eventos (Event Handling)
#### El modelo de delegación en Flet
Flet sigue el modelo clásico de delegación de eventos: cada control expone propiedades que aceptan funciones (callables) como manejadores. Cuando el evento ocurre, Flet invoca la función asociada, pasándole un objeto con información del evento. El programador solo debe definir la función y asignarla a la propiedad correspondiente.
#### Registro de manejadores
Existen varias formas de registrar manejadores en Flet:
#### Función nombrada:
```bash
def boton_clickado(e):
    print("Botón clickeado")

btn = ft.ElevatedButton("Haz clic", on_click=boton_clickado)
```
#### Función lambda:
```bash
btn = ft.ElevatedButton("Haz clic", on_click=lambda e: print("Clic"))
```
#### Manejador asíncrono:
Cuando se necesita ejecutar operaciones asíncronas (como llamadas a redes o temporizadores), se define la función como async y se pueden usar await.
```bash
async def boton_clickado(e):
    await alguna_operacion_asincrona()
    page.add(ft.Text("Operación completada"))
```
#### La fuente del evento y el objeto `e`
Dentro del manejador, el parámetro `e` (de tipo `ft.ControlEvent` o una subclase) proporciona acceso al control que disparó el evento mediante `e.control`. Esto es especialmente útil cuando varios controles comparten el mismo manejador, ya que se puede diferenciar la acción consultando propiedades como `e.control.text` o `e.control.data`.
```bash
def menu_clickado(e):
    opcion = e.control.data
    if opcion == "nuevo":
        crear_nuevo()
    elif opcion == "abrir":
        abrir_archivo()
```
#### La importancia de `page.update()`
Un aspecto fundamental en Flet es que los cambios en las propiedades de los controles no se reflejan automáticamente en la interfaz. Después de modificar una propiedad (como `text`, `value`, `disabled`, `visible`), es necesario llamar a `page.update()` (o al método `update()` del propio control) para que los cambios se sincronicen con la vista renderizada por Flutter. Este mecanismo permite optimizar las actualizaciones agrupando múltiples modificaciones antes de una sola llamada a `update()`.
```bash
def incrementar(e):
    contador.value = int(contador.value) + 1
    page.update()  # Aquí se actualiza la interfaz
```
#### Manejo de estado
El estado de la aplicación se gestiona normalmente mediante variables en el ámbito de la función `main` o en clases que heredan de `ft.UserControl`. Cada vez que se modifica una variable que afecta a la UI, se debe llamar a `update()` para que los cambios sean visibles. Este modelo imperativo es sencillo y directo, y se adapta bien a aplicaciones de tamaño pequeño a mediano.

### 1.4 Manejo de Componentes Gráficos de Control
#### Operaciones comunes sobre controles
Flet permite manipular los controles en tiempo de ejecución mediante sus propiedades y métodos. Las operaciones más habituales incluyen:
#### Cambiar contenido:
* `control.value = nuevo_valor` para actualizar el texto o valor de un control.
* `control.text = nuevo_texto` en botones, etiquetas, etc.
#### Habilitar/deshabilitar:
* `control.disabled = True` para desactivar un control (se atenúa y no responde a eventos).
#### Mostrar/ocultar:
* `control.visible = False` para ocultar un control. Los controles ocultos no ocupan espacio en el layout (a diferencia de otros frameworks donde pueden seguir ocupando espacio).
#### Cambiar apariencia:
* `control.bgcolor = ft.Colors.BLUE` cambia el color de fondo.
* `control.color = ft.Colors.WHITE` cambia el color del texto.
* `control.width = 200, control.height = 50` redimensionan el control.
#### Gestionar opciones de listas:
Para `Dropdown`, se puede modificar la lista options añadiendo o quitando elementos: `dropdown.options.append(ft.dropdown.Option("nuevo"))`.
#### Forzar actualización:
`control.update()` actualiza solo ese control, más eficiente que `page.update()` cuando solo un elemento ha cambiado.
#### Uso de la propiedad data
Una práctica común en Flet es utilizar la propiedad data de los controles para almacenar información adicional que ayude a identificar su propósito. Esto es especialmente útil cuando varios controles comparten el mismo manejador de eventos. Por ejemplo, en una calculadora, todos los botones numéricos pueden usar el mismo manejador y distinguirse mediante data:
```bash
ft.ElevatedButton("7", on_click=boton_numero, data="7")
ft.ElevatedButton("8", on_click=boton_numero, data="8")
```
#### En el manejador:
```bash
def boton_numero(e):
    digito = e.control.data
    pantalla.value += digito
    pantalla.update()
```
#### Creación de componentes reutilizables con `UserControl`
Para aplicaciones más grandes, Flet ofrece la clase `ft.UserControl`, que permite encapsular un conjunto de controles y su lógica en un componente reutilizable. Un `UserControl` debe implementar el método `build()` que devuelve la estructura de la interfaz. También puede tener su propio estado y métodos.
Ejemplo de un contador reutilizable:
```basg
class Contador(ft.UserControl):
    def __init__(self, valor_inicial=0):
        super().__init__()
        self.valor = valor_inicial

    def build(self):
        self.texto = ft.Text(str(self.valor))
        self.boton = ft.ElevatedButton("Incrementar", on_click=self.incrementar)
        return ft.Column([self.texto, self.boton])

    def incrementar(self, e):
        self.valor += 1
        self.texto.value = str(self.valor)
        self.update()
```
Luego, este componente se puede instanciar múltiples veces en la misma página:
```bash
page.add(Contador(), Contador(5))
```
Ciclo de vida de un `UserControl`
Los `UserControl` tienen métodos especiales que se invocan en momentos clave:
* `did_mount()`: se ejecuta después de que el componente se ha añadido a la página. Ideal para iniciar tareas asíncronas o cargar datos.
* `will_unmount()`: se ejecuta justo antes de que el componente sea removido. Útil para liberar recursos, cancelar temporizadores o suscripciones.
Estos métodos permiten un control fino sobre el ciclo de vida, esencial en aplicaciones complejas.
```bash
class Temporizador(ft.UserControl):
    def did_mount(self):
        self.running = True
        self.page.run_task(self.actualizar_cada_segundo)

    async def actualizar_cada_segundo(self):
        while self.running:
            await asyncio.sleep(1)
            self.actualizar_reloj()
            self.update()

    def will_unmount(self):
        self.running = False
```
#### Arquitectura de aplicaciones con Flet
Para proyectos de mayor envergadura, se pueden adoptar patrones arquitectónicos como la separación en capas (core, gui, eventos) o un sistema de comunicación basado en eventos (pub/sub). Proyectos comunitarios como flet-app-base-architecture muestran cómo organizar el código en módulos, separando la lógica de negocio de la interfaz y utilizando eventos personalizados para la comunicación entre componentes. Aunque no es obligatorio, estas prácticas mejoran la mantenibilidad y escalabilidad de las aplicaciones.

### Conclusión
A lo largo de esta unidad, hemos explorado los fundamentos teóricos de las interfaces gráficas de usuario y hemos visto cómo se materializan en Flet, un framework que acerca la potencia de Flutter a los desarrolladores de Python. Hemos aprendido a construir interfaces mediante un árbol de controles, a manejar los distintos tipos de eventos que pueden ocurrir, a escribir manejadores que respondan a esos eventos y a manipular los componentes gráficos en tiempo de ejecución. Además, hemos conocido técnicas avanzadas como la creación de componentes reutilizables con `UserControl` y la gestión del ciclo de vida. Con estas bases, estamos preparados para desarrollar aplicaciones interactivas, modernas y multiplataforma de manera eficiente.

Referencias Bibliograficas 
* Flet. (n.d.). Introduction. Flet.dev. Retrieved February 25, 2026, from https://docs.flet.dev
* flet: Flet enables developers to easily build realtime web, mobile and desktop apps in Python. No frontend experience required. (n.d.).
* Flet. (n.d.-a). PyPI. Retrieved February 25, 2026, from https://pypi.org/project/flet/


## Unidad 2: Componentes y Librerías

En el desarrollo de software moderno, la reutilización de código y la modularización son pilares fundamentales para construir aplicaciones escalables, mantenibles y eficientes. En este contexto, los componentes y las librerías juegan un papel esencial. A continuación se desarrollan los temas teóricos de la unidad, complementados con ejemplos prácticos extraídos de los fragmentos de código proporcionados.






