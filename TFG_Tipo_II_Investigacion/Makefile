MAIN=tfg_uvigo
ifeq ($(OS),Windows_NT)
    PYTHON ?= py
else
    PYTHON ?= python3
endif

all: pdf clean_aux

pdf:
	pdflatex -interaction=nonstopmode $(MAIN).tex
	biber $(MAIN)
	pdflatex -interaction=nonstopmode $(MAIN).tex
	pdflatex -interaction=nonstopmode $(MAIN).tex

docx:
	@echo "Generando version Word (docx) con Pandoc..."
	-pandoc $(MAIN).tex -o $(MAIN).docx --resource-path=.:src:src/images:src/chapters --toc
	@echo "Conversion finalizada. Nota: El formato visual sera distinto al PDF."

docx-hd: pdf clean_aux
	@echo "Generando version Word HD desde el PDF (alta fidelidad visual)..."
	$(PYTHON) pdf2word.py $(MAIN)
	@echo "Conversion HD finalizada: $(MAIN).docx"

clean_aux:
	@echo "----------------------------------------"
	@echo "Eliminando archivos basura de la compilacion..."
	-@rm -f *.aux *.bbl *.blg *.idx *.ilg *.ind *.lof *.lot *.out *.toc *.log *.fls *.fdb_latexmk *.synctex.gz *.run.xml *.bcf
	-@rm -f src/*.aux
	-@rm -f src/chapters/*.aux
	@echo "Compilacion limpia terminada."

clean: clean_aux
	-@rm -f $(MAIN).pdf $(MAIN).docx

.PHONY: all pdf docx docx-hd clean_aux clean
