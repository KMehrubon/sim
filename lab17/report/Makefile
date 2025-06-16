FILES = $(patsubst %.md, %.docx, $(wildcard *.md))
FILES += $(patsubst %.md, %.pdf, $(wildcard *.md))

FILTERS =
OPTIONS = --number-sections
PDF_ENGINE = --pdf-engine=lualatex
FORMAT_OPTIONS = -V lang=ru -V babel-lang=none -V usepolyglossia=true -V mainfont="Liberation Serif" -V papersize=a4
BIB_OPTIONS = --citeproc
TEMPLATE = --template=template.tex

%.docx: %.md
	pandoc "$<" $(FILTERS) $(OPTIONS) $(BIB_OPTIONS) -o "$@"

%.pdf: %.md
	pandoc "$<" $(TEMPLATE) $(PDF_ENGINE) $(FORMAT_OPTIONS) $(OPTIONS) $(BIB_OPTIONS) -o "$@"

all: $(FILES)

clean:
	-rm $(FILES) *~

cleanall: clean
