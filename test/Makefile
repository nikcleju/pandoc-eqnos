
v2.2 = 2.2.3.2
v2.1 = 2.1.3
v2.0 = 2.0.6
v1.19 = 1.19.2
v1.18 = 1.18
v1.17 = 1.17.2
v1.16 = 1.16.0.2
v1.15 = 1.15.2

PANDOC-2.2 = pandoc-$(v2.2)
PANDOC-2.1 = pandoc-$(v2.1)
PANDOC-2.0 = pandoc-$(v2.0)
PANDOC-1.19 = pandoc-$(v1.19)
PANDOC-1.18 = pandoc-$(v1.18)
PANDOC-1.17 = pandoc-$(v1.17)
PANDOC-1.16 = pandoc-$(v1.16)
PANDOC-1.15 = pandoc-$(v1.15)

PYTHON-2.7 = python2.7
PYTHON-3.6 = python3.6

# mathml needed for \mathrm{}
PDFFLAGS = --variable geometry:margin=1in --standalone --mathml \
           --variable urlcolor=blue
HTMLFLAGS = --standalone --mathml --variable urlcolor=blue


all: pdf html docx

pdf: out/test-2.2.pdf \
     out/test-2.2-py2.7.pdf \
     out/test-2.2-py3.6.pdf \
     out/test-2.2-cleveref.pdf \
     out/test-2.1.pdf \
     out/test-2.0.pdf \
     out/test-1.19.pdf \
     out/test-1.18.pdf \
     out/test-1.17.pdf \
     out/test-1.16.pdf \
     out/test-1.15.pdf

html: out/test-2.2.html

docx: out/test-2.2.docx


out/test-%.html: test.md
	@if [ ! -d $(dir $@) ]; then mkdir -p $(dir $@); fi
	$(PANDOC-$*) $< --filter pandoc-eqnos $(HTMLFLAGS) -o $@

out/test-%-py2.7.pdf: test.md
	@if [ ! -d $(dir $@) ]; then mkdir -p $(dir $@); fi
	$(PANDOC-$*) $< -t json | $(PYTHON-2.7) ../pandoc_eqnos.py latex --pandocversion=$(v$*) | $(PANDOC-$*) -f json $(PDFFLAGS) -o $@

out/test-%-py3.6.pdf: test.md
	@if [ ! -d $(dir $@) ]; then mkdir -p $(dir $@); fi
	$(PANDOC-$*) $< -t json | $(PYTHON-3.6) ../pandoc_eqnos.py latex --pandocversion=$(v$*) | $(PANDOC-$*) -f json $(PDFFLAGS) -o $@

out/test-%-cleveref.pdf: test.md
	@if [ ! -d $(dir $@) ]; then mkdir -p $(dir $@); fi
	$(PANDOC-$*) $< --filter pandoc-eqnos $(PDFFLAGS) --include-in-header=cleveref.tex -o $@

out/test-%.pdf: test.md
	@if [ ! -d $(dir $@) ]; then mkdir -p $(dir $@); fi
	$(PANDOC-$*) $< --filter pandoc-eqnos $(PDFFLAGS) -o $@

out/test-%.docx: test.md
	@if [ ! -d $(dir $@) ]; then mkdir -p $(dir $@); fi
	$(PANDOC-$*) $< --filter pandoc-eqnos -o $@


.PHONY: clean

clean:
	rm -rf out
