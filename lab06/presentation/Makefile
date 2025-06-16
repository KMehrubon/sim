HTML = presentation.html
PDF  = presentation.pdf
SRC  = presentation.md

REVEALJS = https://cdn.jsdelivr.net/npm/reveal.js

all: $(HTML) $(PDF)

$(HTML): $(SRC)
	pandoc $< -t revealjs -s -o $@ --slide-level=2 -V revealjs-url=$(REVEALJS) -V theme=moon

$(PDF): $(SRC)
	pandoc $< -t beamer -o $@

clean:
	rm -f $(HTML) $(PDF)
