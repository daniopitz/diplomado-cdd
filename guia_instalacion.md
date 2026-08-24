# Guía de instalación del entorno de trabajo

Diplomado en Ciencia de Datos Aplicada, Módulo 1: Introducción y fundamentos
estadísticos. Universidad Técnica Federico Santa María.

En este módulo trabajaremos con Python, Jupyter y las librerías NumPy, Pandas y
Matplotlib, entre otras. Esta guía deja todo instalado y funcionando en su
computador personal. **La revisaremos paso a paso en la primera clase** (martes
25 de agosto), así que no es necesario hacer nada antes; si quiere adelantarse,
puede seguirla por su cuenta. Lo importante es llegar a la **clase 2** (jueves 27
de agosto) **con el entorno funcionando**, porque desde ahí trabajaremos con
código en todas las clases.

Si algo no funciona, no se preocupe: anote el mensaje de error y el paso en que
apareció, y lo revisamos en la clase 1, o escríbanos antes de la clase 2. Al
final de la guía hay una sección de problemas frecuentes y un plan alternativo en
la nube por si su computador tiene restricciones de instalación.

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

## Paso 3: abrir JupyterLab y verificar

Desde la misma carpeta, ejecute:

```bash
uv run jupyter lab
```

Se abrirá JupyterLab en su navegador. Cree un notebook nuevo (botón Python 3) y
ejecute esta celda:

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
listo. Puede cerrar JupyterLab con Ctrl+C en la terminal.

Para volver a trabajar cualquier otro día, basta con entrar a la carpeta y
repetir `uv run jupyter lab`. Cada semana, `git pull` trae el material nuevo
(o vuelva a descargar el ZIP); si cambian las dependencias, `uv sync` deja el
entorno al día.

## Alternativa: VS Code

Si prefiere trabajar en Visual Studio Code, abra la carpeta del curso
(`Archivo > Abrir carpeta`), instale la extensión "Jupyter" de Microsoft, y al
abrir un notebook seleccione como kernel el intérprete de Python de la
subcarpeta `.venv`. El resto funciona igual.

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

Si su computador es administrado por su empresa y no permite instalar programas,
puede seguir el módulo con [Google Colab](https://colab.research.google.com),
que ejecuta notebooks en la nube y ya trae NumPy, Pandas y Matplotlib
instalados. Solo necesita una cuenta de Google. Los notebooks del curso se
pueden subir a Colab con `Archivo > Subir notebook`.

Colab sirve perfectamente para las clases; la única diferencia es que los
archivos de datos hay que subirlos a la sesión o montarlos desde Google Drive,
lo que veremos en clase si alguien lo necesita.

## Antes de la clase 2, en resumen

1. uv instalado (`uv --version` responde).
2. Repositorio del curso descargado y entorno instalado (`uv sync` terminó
   sin errores).
3. JupyterLab abre y la celda de verificación muestra las versiones y la tabla.

Nos vemos el martes 25 de agosto a las 18:00.
