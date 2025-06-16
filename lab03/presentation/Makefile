SRC = presentation.md
HTML = presentation.html
PDF_BEAMER = presentation.pdf
PPTX = presentation.pptx
PRINTABLE_HTML = printable_presentation.html
REVEALJS_URL = https://cdn.jsdelivr.net/npm/reveal.js
REVEALJS_THEME = moon
PPTX_TEMPLATE = template.pptx  # если нет шаблона, убрать --reference-doc

.PHONY: all html pdf-beamer pptx printable pdf-html serve clean

# Собрать всё
all: html pdf-beamer pptx printable

# Reveal.js HTML
html: $(HTML)

$(HTML): $(SRC)
	pandoc $< -t revealjs -s -o $@ \
		--slide-level=2 \
		-V revealjs-url=$(REVEALJS_URL) \
		-V theme=$(REVEALJS_THEME)

# PDF Beamer
pdf-beamer: $(PDF_BEAMER)

$(PDF_BEAMER): $(SRC)
	pandoc $< -t beamer -o $@

# PowerPoint (с шаблоном, если он есть)
pptx: $(PPTX)

$(PPTX): $(SRC)
	pandoc $< -t pptx -o $@ --reference-doc=$(PPTX_TEMPLATE)

# HTML с локальными путями к изображениям
printable: $(HTML)
	python3 -c "\
import bs4, os; \
soup = bs4.BeautifulSoup(open('$(HTML)', encoding='utf-8'), 'html.parser'); \
[img.attrs.update({'src': img['data-src']}) or img.attrs.pop('data-src') for img in soup.select('img[data-src]')]; \
open('$(PRINTABLE_HTML)', 'w', encoding='utf-8').write(str(soup))"

# Инструкция по PDF из HTML
pdf-html:
	@echo ""
	@echo "=== Экспорт Reveal.js в PDF ==="
	@echo "1. make serve"
	@echo "2. Открой в браузере:"
	@echo "   http://localhost:8000/$(PRINTABLE_HTML)?print-pdf"
	@echo "3. Ctrl+P → Сохранить как PDF"
	@echo "4. Включи галочку 'Печатать фоновые рисунки'"
	@echo "================================"

# Локальный сервер
serve:
	python3 -m http.server

# Очистка
clean:
	rm -f $(HTML) $(PDF_BEAMER) $(PPTX) $(PRINTABLE_HTML)
