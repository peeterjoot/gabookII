THISDIR := gabookII
THISBOOK := gabookII

BIBLIOGRAPHY_PATH := classicthesis_mine
HAVE_OWN_CONTENTS := 1
HAVE_OWN_TITLEPAGE := 1
MY_CLASSICTHESIS_FRONTBACK_FILES += ../latex/classicthesis_mine/FrontBackmatter/Index.tex
MY_CLASSICTHESIS_FRONTBACK_FILES += ../latex/classicthesis_mine/FrontBackmatter/ContentsAndFigures.tex
#BOOKTEMPLATE := ../latex/classicthesis_mine/ClassicThesis2.tex
BOOKTEMPLATE := ../latex/classicthesis_mine/ClassicThesis3.tex

#ORIG_LISTING_DIRS += ../algebra

include make.revision
include ../latex/make.bookvars

#ONCEFLAGS := -justonce

FIGURES := ../figures/gabook

SOURCE_DIRS += electrodynamics
SOURCE_DIRS += emstress
SOURCE_DIRS += $(FIGURES)
SOURCE_DIRS += fourier
SOURCE_DIRS += lorentzforce
SOURCE_DIRS += qm
SOURCE_DIRS += relativity


# comment this out for online pdf version (uncomment for KDP)
#PRINT_VERSION := 1

#SUBFIGDIR := bw
#ifndef SUBFIGDIR
#SUBFIGDIR := color
#endif

ifdef PRINT_VERSION
SUBFIGDIR := bw
else
SUBFIGDIR := color
endif

ifndef PRINT_VERSION
PARAMS += --no-print
endif
PARAMS += -subfig $(SUBFIGDIR)
DISTEXTRA := $(SUBFIGDIR)
ifdef PRINT_VERSION
DISTEXTRA := $(DISTEXTRA).kdp
endif

PARAMS += --lettersize

#LOCAL_LISTING_FILES += levi.pl

FIGURES += ../figures/$(THISBOOK)/$(SUBFIGDIR)
FIGURES += ../figures/$(THISBOOK)
SOURCE_DIRS += $(FIGURES)

PRIMARY_SOURCES := $(shell grep input chapters.tex | sed 's/%.*//;s/.*{//;s/}.*//;')
PRIMARY_SOURCES += FrontBackmatter/preface.tex

METAFLAGS := --chapter=mychapter

#GENERATED_SOURCES += mathematica.tex
#GENERATED_SOURCES += cronology.tex
#GENERATED_SOURCES += backmatter.tex

EPS_FILES := $(foreach dir,$(FIGURES),$(wildcard $(dir)/*.eps))
PDFS_FROM_EPS := $(subst eps,pdf,$(EPS_FILES))
#$(error PDFS_FROM_EPS $(PDFS_FROM_EPS))

THISBOOK_DEPS += $(PDFS_FROM_EPS)

CLEAN_TARGETS += *.sp FrontBackmatter/*.sp

DO_SPELL_CHECK := $(shell cat spellcheckem.txt)

include ../latex/make.rules

$(THISBOOK).pdf :: parameters.sty

vpath %.png $(ORIG_FIGURE_DIRS)
#vpath %.pl $(ORIG_LISTING_DIRS)

eps:
	@echo $(EPS_FILES)

pdfeps:
	@echo $(PDFS_FROM_EPS)

eps2pdf: $(PDFS_FROM_EPS)

# FIXME: this should be an automatic dependency, but currently isn't.
#$(THISBOOK).pdf :: mmacells.sty

#$(THISBOOK).pdf :: classicthesis.sty $(EXTERNAL_DEPENDENCIES)
$(THISBOOK).pdf :: $(EXTERNAL_DEPENDENCIES)

.PHONY: spellcheck
spellcheck: $(patsubst %.tex,%.sp,$(filter-out $(DONT_SPELL_CHECK),$(DO_SPELL_CHECK)))

%.sp : %.tex
	spellcheck $^
	touch $@

#listings/%.pl: %.pl
#	mkdir -p $(@D)
#	cp $< $@

mmacells/mmacells.sty:
	git clone https://github.com/jkuczm/mmacells

bib:
	rm -f Bibliography.bib myrefs.bib
	make Bibliography.bib myrefs.bib

mmacells.sty: mmacells/mmacells.sty
	cp $^ $@

# hack for: HAVE_OWN_TITLEPAGE
clean ::
	git checkout FrontBackmatter/Titlepage.tex

#backmatter.tex: ../latex/classicthesis_mine/backmatter2.tex
#	rm -f $@
#	ln -s ../latex/classicthesis_mine/backmatter2.tex backmatter.tex

mathematica.tex : ../METADATA ../mathematica/METADATA
	(cd .. ; ./METADATA -mathematica -latex -gabook $(REDACTED) > $(THISBOOK)/mathematica.tex)
