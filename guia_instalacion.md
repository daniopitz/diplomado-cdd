# Guía de instalación del entorno de trabajo

Diplomado en Ciencia de Datos Aplicada, Módulo 1: Introducción y fundamentos
estadísticos. Universidad Técnica Federico Santa María.

En este módulo trabajaremos con Python, Jupyter y las librerías NumPy, Pandas y
Matplotlib, entre otras. Esta guía deja todo instalado y funcionando en su
computador personal. Si le es posible, **inténtela antes de la primera clase**
(martes 25 de agosto), pero solo si puede: no es un requisito, y la revisaremos
paso a paso en esa clase. Lo importante es llegar a la **clase 2** (jueves 27
de agosto) **con el entorno funcionando**, porque desde ahí trabajaremos con
código en todas las clases. Instalar el entorno local no es obligatorio: también
puede trabajar en Google Colab (ver el plan alternativo, al final de la guía).

Si algo no funciona, anote el mensaje de error y el paso en que apareció, y
escríbanos antes de la clase 2. Tendremos ayudantes para resolver este tipo de
dudas; pronto publicaremos más información. Al final de la guía hay una sección
de problemas frecuentes y un plan alternativo en la nube por si su computador
tiene restricciones de instalación.

Tiempo estimado: 15 a 20 minutos, con conexión a internet.

## Qué vamos a instalar

- **uv**: un administrador de entornos y paquetes de Python. Se encarga de
  descargar Python, crear el entorno del curso e instalar las librerías, todo con
  un par de comandos. No necesita tener Python instalado previamente.
- **git** (recomendado): para clonar el repositorio del curso y recibir el
  material nuevo cada semana. Sin git también se puede: el repositorio se
  descarga como ZIP.
- **El entorno del módulo**: Python 3.12 con NumPy, Pandas, Matplotlib, Seaborn,
  SciPy, statsmodels, scikit-learn y JupyterLab. Las versiones exactas vienen
  fijadas en el repositorio, así todo el curso trabaja con el mismo entorno.

## Paso 1: instalar uv

Abra una terminal y ejecute el comando correspondiente a su sistema.

En macOS o Linux (aplicación Terminal):

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

En macOS, si ya usa Homebrew, también sirve `brew install uv`.

En Windows (abrir PowerShell):

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Después de instalar, **cierre la terminal y abra una nueva** para que el comando
quede disponible. Verifique la instalación con:

```bash
uv --version
```

Debería ver el número de versión (por ejemplo `uv 0.8.x`). Si aparece un error de
comando no encontrado, revise la sección de problemas frecuentes.

## Paso 2: descargar el repositorio del curso y crear el entorno

Todo el material del módulo (notebooks, datos, esta guía) vive en el
repositorio [github.com/daniopitz/diplomado-cdd](https://github.com/daniopitz/diplomado-cdd).
Clónelo y cree el entorno:

```bash
git clone https://github.com/daniopitz/diplomado-cdd.git
cd diplomado-cdd
uv sync
```

Si no tiene git, descargue el repositorio como ZIP (botón verde `Code` >
`Download ZIP` en GitHub), descomprímalo, entre a la carpeta desde la terminal
y ejecute `uv sync`.

`uv sync` lee los archivos `pyproject.toml` y `uv.lock` del repositorio e
instala Python 3.12 y las mismas versiones de las librerías para todo el curso.
La descarga toma unos minutos la primera vez.

## Paso 3: abrir un notebook y verificar

Elija el editor que le acomode:

- **VS Code (el que se usa en las clases)**: abra la carpeta del curso
  (`Archivo > Abrir carpeta`), instale las extensiones "Python" y "Jupyter" de
  Microsoft, abra un notebook y seleccione como kernel el intérprete de Python
  de la subcarpeta `.venv`. No necesita ejecutar ningún comando adicional.
- **JupyterLab (opcional, si no usa VS Code)**: desde la carpeta del curso
  ejecute `uv run jupyter lab`; se abre en el navegador y no requiere
  configurar nada más.

Para verificar, cree un notebook nuevo y ejecute esta celda:

```python
import numpy as np
import pandas as pd
import matplotlib

print("NumPy", np.__version__)
print("Pandas", pd.__version__)
print("Matplotlib", matplotlib.__version__)

pd.DataFrame({"comuna": ["Santiago", "Providencia", "Maipú"],
              "viajes": [120, 95, 210]})
```

Si ve las tres versiones impresas y una tabla con tres comunas, el entorno quedó
listo.

Para volver a trabajar cualquier otro día, basta con abrir la carpeta del curso
en su editor. Cada semana, `git pull` trae el material nuevo (o vuelva a
descargar el ZIP); si cambian las dependencias, `uv sync` deja el entorno al
día.

## Problemas frecuentes

- **`uv: command not found` o `uv no se reconoce`**: la terminal abierta es
  anterior a la instalación. Cierre todas las terminales, abra una nueva y
  reintente. En Windows, use PowerShell (no el símbolo de sistema clásico).
- **En Windows, error de política de ejecución en PowerShell**: ejecute el
  comando de instalación tal como aparece en el paso 1, que incluye
  `-ExecutionPolicy ByPass` justamente para esto.
- **Red corporativa con proxy o antivirus que bloquea descargas**: intente desde
  otra red (por ejemplo la de su casa). Si el bloqueo persiste, use el plan
  alternativo en la nube y escríbanos.
- **macOS pide instalar "herramientas de línea de comandos"**: acepte la
  instalación que propone el sistema y reintente el paso 1 (esas herramientas
  incluyen git).
- **`git` no está instalado**: en Windows se descarga de
  [git-scm.com](https://git-scm.com); en macOS viene con las herramientas de
  línea de comandos. O use la descarga ZIP del paso 2.

## Plan alternativo: Google Colab

Si no puede o prefiere no instalar programas, puede seguir el módulo con
[Google Colab](https://colab.research.google.com),
que ejecuta notebooks en la nube y ya trae NumPy, Pandas y Matplotlib
instalados. Solo necesita una cuenta de Google. Los notebooks del curso se
abren con los enlaces del README del repositorio.

Importante: los cambios sobre el enlace del curso no quedan guardados. Antes de
trabajar, guarde su propia copia con `Archivo > Guardar una copia en Drive` y
organice sus copias en una carpeta del curso en su Google Drive.

Colab sirve perfectamente para las clases: los notebooks del curso leen los
datos por URL, así que no hay que subir nada.

### Subir datos propios a Colab

Esto se necesita solo al trabajar con datos propios, por ejemplo los del
proyecto Capstone.

- **Archivos sueltos**: botón de subir del panel de archivos (icono de carpeta,
  a la izquierda) o arrastrarlos al panel. Se pueden seleccionar varios a la
  vez. Quedan en `/content/`, el directorio de trabajo del notebook.
- **Carpetas completas**: el panel no acepta carpetas; comprímala a `.zip`,
  suba el zip y descomprímalo desde una celda:

  ```python
  !unzip -q eod_stgo.zip -d .
  ```

  (en la terminal de Colab, el mismo comando sin el `!`).
- **Persistencia**: los archivos subidos viven solo mientras dura la sesión de
  Colab; al cerrarla, o si expira por inactividad, se pierden y hay que
  subirlos de nuevo. Para no volver a subirlos cada vez, monte su Google Drive
  (ver la sección siguiente).

### Montar Google Drive en Colab

Montar el Drive conecta su Google Drive a la sesión de Colab, como si fuera una
carpeta más del computador. Es la opción recomendada para los datos del
proyecto: se suben una sola vez a Drive y quedan disponibles en cualquier
sesión futura.

1. Suba la carpeta de datos a su Google Drive en el navegador
   ([drive.google.com](https://drive.google.com)), por ejemplo a una carpeta
   `diplomado`. El navegador sí acepta arrastrar carpetas completas a Drive.
2. En el notebook de Colab, ejecute esta celda y autorice el acceso cuando se
   lo pida (una vez por sesión):

   ```python
   from google.colab import drive
   drive.mount("/content/drive")
   ```

3. Su Drive queda disponible en `/content/drive/MyDrive/` (que corresponde a
   "Mi unidad"). Desde ahí se lee con la ruta completa, por ejemplo:

   ```python
   viajes = pd.read_csv("/content/drive/MyDrive/diplomado/eod_stgo/viajes.csv",
                        sep=";", decimal=",", low_memory=False)
   ```

El montaje hay que repetirlo en cada sesión nueva (la autorización es rápida),
pero los archivos ya no se vuelven a subir. Cuidado al borrar dentro de
`/content/drive/`: ahí está su Drive real, no una copia.

## En resumen

Intente llegar a la clase 1 con una de las dos opciones funcionando:

- **Entorno local**: uv instalado (`uv --version` responde), repositorio del
  curso descargado, entorno creado (`uv sync` terminó sin errores) y la celda
  de verificación muestra las versiones y la tabla (en VS Code o JupyterLab).
- **Google Colab**: puede abrir los notebooks con los enlaces del README y
  guardar su copia en su Google Drive.

Nos vemos el martes 25 de agosto a las 18:00.
