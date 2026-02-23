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
