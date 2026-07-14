# Curso_TAAE

Curso de tecnicas avanzadas de analisis estadistico del programa de Ciencia de Datos de la UPB.

Este repositorio usa `uv` para crear el entorno virtual e instalar las dependencias definidas en `pyproject.toml` y `uv.lock`.

## Requisitos

- Python `3.12`
- Git
- `uv`

La version objetivo del proyecto esta definida en:

- [`pyproject.toml`](./pyproject.toml)
- [`.python-version`](./.python-version)

## 1. Instalar `uv`

### Linux o macOS

Instala `uv` con el script oficial:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Si necesitas recargar la terminal despues de la instalacion:

```bash
source $HOME/.local/bin/env
```

Verifica que quedo instalado:

```bash
uv --version
```

### Windows

En PowerShell instala `uv` con el script oficial:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Cierra y abre de nuevo la terminal si el comando `uv` no aparece de inmediato, y valida la instalacion con:

```powershell
uv --version
```

## 2. Descargar el repositorio y ejecutar `uv sync`

Clona el proyecto y entra a la carpeta:

```bash
git clone https://github.com/robertohincapie/Curso_TAAE.git
cd Curso_TAAE
```

Sincroniza dependencias y crea el entorno virtual local en `.venv`:

```bash
uv sync
```

Si quieres forzar la version de Python del proyecto en equipos donde aun no este disponible, puedes usar:

```bash
uv python install 3.12
uv sync
```

## 3. Seleccionar el interprete de Python del entorno

Despues de `uv sync`, el entorno virtual queda en:

- Linux/macOS: `.venv/bin/python`
- Windows: `.venv\Scripts\python.exe`

### En VS Code

1. Abre la carpeta del proyecto.
2. Ejecuta `Ctrl+Shift+P`.
3. Busca `Python: Select Interpreter`.
4. Elige el interprete dentro de `.venv`.

Si VS Code no lo detecta automaticamente, selecciona manualmente una de estas rutas:

```text
.venv/bin/python
```

```text
.venv\Scripts\python.exe
```

### En notebooks de Jupyter

Como el proyecto ya incluye `ipykernel`, despues de ejecutar `uv sync` normalmente podras abrir los notebooks y escoger el kernel del entorno `.venv` desde tu editor.

