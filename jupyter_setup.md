# 🚀 Configuración de Jupyter Lab con UV <img src="../img/sergio_portrait_square.png" alt="Sergio Benito" align="right" width="100">

- **Autor:** Sergio Benito Martín
- **Contacto:** pontia@sergiobenito.com
- **Última actualización:** 22/05/2025

Este documento describe el proceso para configurar Jupyter Lab dentro del proyecto UV y cómo crear/personalizar un kernel específico para el entorno virtual del proyecto.

## 🌱 Creación del entorno virtual con UV

Antes de configurar Jupyter Lab, necesitas crear un entorno virtual utilizando UV:

```bash
# Navegar al directorio del proyecto
cd ruta/a/tu/proyecto

# Crear el entorno virtual
uv venv --python 3.11 env-pontia-ml

# Activar el entorno virtual
source env-pontia-ml/bin/activate

# Instalar dependencias desde el archivo requirements.txt
uv pip install -r requirements.txt
```

ℹ️ El archivo `requirements.txt` ya ha sido preparado y generado para facilitar el trabajo de la gestión de librerías. Sin embargo, si necesitas actualizar las dependencias después de modificar `requirements.txt`:

```bash
uv pip install -r requirements.txt --upgrade
```

También podrías añadir otras librerías o modificar las existentes del entorno virtual si lo deseases.

## 🔧 Crear un kernel para Jupyter

Se utilizarán las funcionalidades de de UV para utilizar Jupyter, en caso de que se prefiera utilizar directamente Jupyter ir a [Anexo I](#anexo-i). Para ello tendremos que basarnos en el comando `uv run --active --with jupyter ...` que permite ejecutar mediante `run` un script / aplicación concreta, en este caso `Jupyter`.

Para crear un kernel personalizado que use tu entorno virtual de UV:

```bash
# Activar el entorno virtual
source env-pontia-ml/bin/activate

# Crear un kernel con nombre personalizado
uv run --active ipython kernel install --user --env VIRTUAL_ENV env-pontia-ml --name=env-pontia-ml

```

## 🚀 Iniciar Jupyter Lab

Para iniciar Jupyter Lab desde el entorno virtual:

```bash
# Activar el entorno virtual
source env-pontia-ml/bin/activate

# Iniciar Jupyter Lab
uv run --active --with jupyter jupyter lab
```

Para salir tendrás que usar la siguiente combinación de teclas:
- Windows / Linux: `Ctrl+C`
- Mac: `Control+C`

Luego pulsar a la tecla `Y` (haciendo referencia a que deseas cerrar Jupyter) y darle a `Enter`.

<h2 id='anexo-i'>💡 Anexo I: Usar Jupyter sin UV</h2>
Para utilizar Jupyter no es necesario hacerlo a través de UV, por tanto aquí se dan los comandos principales para añadir el entorno virtual al kernel de Jupyter:

```bash
python -m ipykernel install --user --name=NOMBRE_ENTORNO --display-name="NOMBRE_MOSTRADO"

# En este caso será con el nombre de nuestro entorno virtual sería
python -m ipykernel install --user --name=env-pontia-ml --display-name="Entorno Pontia ML"
```

Donde:
- `NOMBRE_ENTORNO`: Es un identificador técnico para el kernel (sin espacios, por ejemplo: "env-pontia-ml")
- `NOMBRE_MOSTRADO`: Es el nombre que aparecerá en la interfaz de Jupyter (puede contener espacios, por ejemplo: "Entorno Pontia ML")

```bash
# Activar el entorno virtual
source env-pontia-ml/bin/activate

# Visualiza los kernels que tienes cargados en Jupyter
jupyter kernelspec list

# Eliminar kernel anterior (si existe)
jupyter kernelspec remove env-pontia-ml

# Crear nuevo kernel con nombres personalizados
python -m ipykernel install --user --name=mi_proyecto_ml --display-name="Mi Proyecto de Machine Learning"

# Iniciar Jupyter Lab
jupyter lab
```

Al crear nuevos notebooks en Jupyter Lab, podrás seleccionar el kernel con el nombre mostrado que has definido.

<h2 id='anexo-ii'>✏️ Anexo II: Personalizar nombres existentes</h2>

Si ya has creado un kernel y deseas cambiar su nombre:

1. Primero, lista los kernels disponibles:

```bash
uv run --active --with jupyter kernelspec list
```

2. Elimina el kernel existente:

```bash
uv run --active --with jupyter kernelspec remove NOMBRE_ENTORNO_ACTUAL
```

3. Se añadiría con el comando visto previamente:

```bash
uv run --active ipython kernel install --user --env VIRTUAL_ENV new-virtual-env --name=new-virtual-env
```

## 📑 Useful info
- UV official documentation 
    - [Managing packages](https://docs.astral.sh/uv/pip/packages/#installing-a-package)
    - [Using Python environments](https://docs.astral.sh/uv/pip/environments/)
    - [Using uv with Jupyter](https://docs.astral.sh/uv/guides/integration/jupyter/)