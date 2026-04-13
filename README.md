# 🎓 Plantillas TFG UVigo - ESEI (Modalidades I y II)

![LaTeX](https://img.shields.io/badge/LaTeX-008080?style=for-the-badge&logo=latex&logoColor=white)
![UVigo](https://img.shields.io/badge/UVigo-ESEI-blue?style=for-the-badge)

Este repositorio contiene las plantillas oficiales actualizadas según la **"Guía para a elaboración e estrutura da documentación do TFG"** de la ESEI (UVigo). Facilito el código en LaTeX para redactar memorias de alta calidad tipográfica y un estándar profesional en TFGs. Aunque el objetivo principal es generar un PDF impecable, también se incluye soporte experimental para exportar el contenido a formato Word (`.docx`) para revisiones con tutores.

---

## 📂 Organización del Repositorio

El proyecto se divide en dos carpetas autónomas. Elige la que corresponda a tu modalidad de TFG:

### 🔷 [TFG_Tipo_I_Software](./TFG_Tipo_I_Software)
- **Para**: Proyectos con desarrollo de software o hardware.
- **Estructura**: 22 secciones oficiales (Arquitectura, Diseño, Pruebas, Manual, etc.).
- **Uso**: Entra en la carpeta y compila `tfg_uvigo.tex`.

### 🔶 [TFG_Tipo_II_Investigacion](./TFG_Tipo_II_Investigacion)
- **Para**: Proyectos de investigación o análisis (sin desarrollo técnico predominante).
- **Estructura**: 17 secciones oficiales (Marco Teórico, Contexto, etc.).
- **Uso**: Entra en la carpeta y compila `tfg_uvigo.tex`.

---


## 🚀 Cómo empezar

1. **Clona el repositorio**:
   ```bash
   git clone https://github.com/maurozelenka/latex-uvigo-tfg.git
   ```
2. Abre la carpeta correspondiente a tu tipo de TFG.
3. Edita la metadata (Título, Autor, Tutor) en el archivo `tfg_uvigo.tex`.
4. Escribe tu contenido en los archivos dentro de `src/chapters/`.
5. Compila el documento. Tienes varias opciones dependiendo de tus herramientas:

### Opción A: Usando Make (¡Recomendado!) 🏆
Es la forma más rápida y limpia de trabajar. El `Makefile` incluido compila todo y limpia los archivos temporales automáticamente.

#### 🪟 Windows (Powershell/CMD)
```powershell
# Entra en la carpeta y ejecuta make
cd TFG_Tipo_I_Software
make
```

#### 🍎 macOS / 🐧 Linux (Terminal)
```bash
# Entra en la carpeta y ejecuta make
cd TFG_Tipo_I_Software
make
```

---

### Opción B: Usando Latexmk (Automatizado) 🤖
Detecta cuántas pasadas son necesarias y limpia los archivos auxiliares al terminar. *(Requiere tener **Perl** instalado en el sistema)*.

#### 🪟 Windows / 🍎 macOS / 🐧 Linux
```bash
# El parámetro -c borra los archivos basura automáticamente tras compilar
latexmk -pdf -c tfg_uvigo.tex
```

---

### Opción C: Comandos manuales (Tradicional) ✍️
Si prefieres el control total, recuerda limpiar los archivos temporales al finalizar.

#### 🪟 Windows (Powershell)
```powershell
# Compilación
pdflatex tfg_uvigo.tex
biber tfg_uvigo
pdflatex tfg_uvigo.tex
pdflatex tfg_uvigo.tex

# Limpieza manual de basura
Remove-Item -Force *.aux, *.log, *.toc, *.lof, *.lot, *.out, *.bbl, *.blg, *.bcf, *.run.xml
```

#### 🍎 macOS / 🐧 Linux (Terminal)
```bash
# Compilación
pdflatex tfg_uvigo.tex
biber tfg_uvigo
pdflatex tfg_uvigo.tex
pdflatex tfg_uvigo.tex

# Limpieza manual de basura
rm -f *.aux *.log *.toc *.lof *.lot *.out *.bbl *.blg *.bcf *.run.xml
```

---

### Opción D: Exportar a Word 📝
Si tu tutor necesita revisar el trabajo en formato Word, tienes dos niveles de calidad:

#### `make docx` — Conversión básica (Pandoc)
Extrae el texto y la estructura desde el código LaTeX. Rápido pero con formato visual muy básico.
```bash
make docx
```
> Requiere tener [Pandoc](https://pandoc.org/) instalado.

#### `make docx-hd` — Conversión HD (¡Recomendado!) 🏆
Convierte el PDF generado a Word manteniendo la **fidelidad visual completa**: portada, imágenes, márgenes y tipografía. Funciona con el mismo principio que herramientas online como iLovePDF, pero ejecutándose **localmente en tu equipo**.
```bash
make docx-hd
```
> Requiere tener **Python** y las librerías necesarias instaladas: `pip install -r requirements.txt`

> [!TIP]
> Si usas **VS Code**, la extensión [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) es excelente para previsualizar el PDF en tiempo real.

---

## 💡 ¿Por qué se compila 4 veces?
Si revisas el `Makefile` o los comandos manuales, verás que procesamos el documento varias veces. Esto es necesario en LaTeX para:
1.  **Pasada 1**: Detectar todas las etiquetas, citas y secciones (genera archivos `.aux`).
2.  **Pasada 2 (Biber)**: Procesar la bibliografía y enlazarla con las citas encontradas.
3.  **Pasada 3**: Insertar la bibliografía y actualizar las citas en el texto (esto puede mover el contenido de sitio).
4.  **Pasada 4**: Corregir definitivamente los números de página en el Índice y las referencias cruzadas tras los cambios de página.

> [!TIP]
> Si usas **VS Code**, la extensión [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) es excelente para previsualizar el PDF en tiempo real.


---

## 🛠️ Requisitos por Plataforma

### 🪟 Windows
1.  **Distribución**: [MiKTeX](https://miktex.org/) (Recomendado) o TeX Live.
2.  **Make**: Viene incluido en *Git for Windows*. También puedes instalarlo con `choco install make`.
3.  *(Opcional)* **Word HD**: Python + `pip install -r requirements.txt`

### 🍎 macOS
1.  **Distribución**: [MacTeX](https://www.tug.org/mactex/).
2.  **Make**: Viene con las *Xcode Command Line Tools* (`xcode-select --install`).
3.  *(Opcional)* **Word HD**: Python + `pip install -r requirements.txt`

### 🐧 Linux
1.  **Distribución**: `texlive-full`.
2.  **Make**: `sudo apt install build-essential`.
3.  *(Opcional)* **Word HD**: Python + `pip install -r requirements.txt`

---

*¡Espero que tengas suerte desarrollando tu TFG!* 