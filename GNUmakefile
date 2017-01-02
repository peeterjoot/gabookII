THISDIR := gabookII
THISBOOK := $(THISDIR)
BASEVER := d77ceaa

include ../latex/make.bookvars

FIGURES := ../../figures/gabook

SOURCE_DIRS += electrodynamics
SOURCE_DIRS += emstress
SOURCE_DIRS += $(FIGURES)
SOURCE_DIRS += fourier
SOURCE_DIRS += lorentzforce
SOURCE_DIRS += qm
SOURCE_DIRS += relativity

#ONCEFLAGS := -justonce

include ../latex/make.rules

#vpath %.png $(ORIG_FIGURE_DIRS)
