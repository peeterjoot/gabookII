THISDIR := gabookII
THISBOOK := $(THISDIR)

export BOOKSUBVER := 1
export BOOKMAJVER := 0
# This isn't a good way to version.  It depends on the local git reflog history count.
export REVCOUNTSTART := 1

include ../latex/make.bookvars

FIGURES := ../figures/gabook

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
