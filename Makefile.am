###############################################################################
## Makefile for French--frp
###############################################################################

LANG1=fra
LANG2=frp
PREFIX1=$(LANG1)-$(LANG2)
PREFIX2=$(LANG2)-$(LANG1)

BASENAME=apertium-$(PREFIX1)

TARGETS_COMMON =		\
	$(PREFIX1).automorf.bin	\
	$(PREFIX1).prob		\
	$(PREFIX1).rlx.bin	\
	$(PREFIX1).autobil.bin	\
	$(PREFIX1).autolex.bin	\
	$(PREFIX1).autosep1.bin	\
	$(PREFIX1).autosep2.bin	\
	$(PREFIX1).autogen.bin	\
	$(PREFIX1).autopgen.bin	\
	$(PREFIX1).t1x.bin	\
	$(PREFIX1).t2x.bin	\
	$(PREFIX1).t3x.bin	\
	$(PREFIX2).automorf.bin	\
	$(PREFIX2).prob		\
	$(PREFIX2).rlx.bin	\
	$(PREFIX2).autobil.bin	\
	$(PREFIX2).autolex.bin	\
	$(PREFIX2).autosep1.bin	\
	$(PREFIX2).autosep2.bin	\
	$(PREFIX2).autogen.bin	\
	$(PREFIX2).autopgen.bin	\
	$(PREFIX2).t1x.bin	\
	$(PREFIX2).t2ax.bin	\
	$(PREFIX2).t2bx.bin	\
	$(PREFIX2).t2cx.bin	\
	$(PREFIX2).t3x.bin

# This include defines goals for install-modes, .deps/.d, autobil.prefixes and .mode files:
@ap_include@

###############################################################################
## Monolingual transducers
###############################################################################

# -------------------
# French analysis:
# -------------------

.deps/$(LANG1).automorf.bin: $(AP_SRC1)/$(LANG1).automorf.bin .deps/.d
	cp $< $@

$(PREFIX1).automorf.bin: .deps/$(LANG1).automorf.bin $(PREFIX1).autobil.bin
	lt-trim $^ $@

# -------------------
# French generation:
# ---------------------


$(PREFIX2).autogen.bin: $(AP_SRC1)/$(LANG1).autogen.bin
	cp $< $@

# -------------------
# frp analysis:
# -------------------

.deps/$(LANG2).automorf.bin: $(AP_SRC2)/$(LANG2).automorf.bin .deps/.d
	cp $< $@

$(PREFIX2).automorf.bin: .deps/$(LANG2).automorf.bin $(PREFIX2).autobil.bin
	lt-trim $^ $@

# -------------------
# frp generation:
# ---------------------


$(PREFIX1).autogen.bin: $(AP_SRC2)/$(LANG2).autogen.bin
	cp $< $@

###############################################################################
## Multiwords
###############################################################################

$(PREFIX1).autosep1.bin: $(BASENAME).$(PREFIX1).l1x
	lsx-comp lr $< $@
$(PREFIX1).autosep2.bin: $(BASENAME).$(PREFIX1).l2x
	lsx-comp lr $< $@

$(PREFIX2).autosep1.bin: $(BASENAME).$(PREFIX2).l1x
	lsx-comp lr $< $@
$(PREFIX2).autosep2.bin: $(BASENAME).$(PREFIX2).l2x
	lsx-comp lr $< $@

###############################################################################
## Tagger models
###############################################################################

$(PREFIX1).prob: $(AP_SRC1)/$(LANG1).prob
	cp $< $@

$(PREFIX2).prob: $(AP_SRC2)/$(LANG2).prob
	cp $< $@

###############################################################################
## Disambiguation rules
###############################################################################

$(PREFIX1).rlx.bin: $(AP_SRC1)/apertium-$(LANG1).$(LANG1).rlx
	cg-comp $< $@

$(PREFIX2).rlx.bin: $(AP_SRC2)/apertium-$(LANG2).$(LANG2).rlx
	cg-comp $< $@

###############################################################################
## Bilingual dictionaries
###############################################################################

$(PREFIX1).autobil.bin: $(BASENAME).$(PREFIX1).dix
	apertium-validate-dictionary $<
	lt-comp lr $< $@

$(PREFIX2).autobil.bin: $(BASENAME).$(PREFIX1).dix
	apertium-validate-dictionary $<
	lt-comp rl $< $@

###############################################################################
## Lexical selection rules
###############################################################################

.deps/%.lrx: %.metalrx .deps/.d
	apertium-metalrx $< $@

$(PREFIX1).autolex.bin: .deps/$(BASENAME).$(PREFIX1).lrx
	lrx-comp $< $@

$(PREFIX2).autolex.bin: .deps/$(BASENAME).$(PREFIX2).lrx
	lrx-comp $< $@

###############################################################################
## Structural transfer rules
###############################################################################


$(PREFIX1).t1x.bin: $(BASENAME).$(PREFIX1).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t2x.bin: $(BASENAME).$(PREFIX1).t2x
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX1).t3x.bin: $(BASENAME).$(PREFIX1).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@


$(PREFIX2).t1x.bin: $(BASENAME).$(PREFIX2).t1x
	apertium-validate-transfer $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t2ax.bin: $(BASENAME).$(PREFIX2).t2ax
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t2bx.bin: $(BASENAME).$(PREFIX2).t2bx
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t2cx.bin: $(BASENAME).$(PREFIX2).t2cx
	apertium-validate-interchunk $<
	apertium-preprocess-transfer $< $@

$(PREFIX2).t3x.bin: $(BASENAME).$(PREFIX2).t3x
	apertium-validate-postchunk $<
	apertium-preprocess-transfer $< $@

###############################################################################
## Postgeneration dictionaries
###############################################################################

$(PREFIX1).autopgen.bin: $(AP_SRC2)/$(LANG2).autopgen.bin
	cp $< $@

$(PREFIX2).autopgen.bin: $(AP_SRC1)/$(LANG1).autopgen.bin
	cp $< $@

###############################################################################
## Distribution
###############################################################################

EXTRA_DIST=					\
		./deps/$(BASENAME).$(PREFIX1).lrx	\
		./deps/$(BASENAME).$(PREFIX2).lrx	\
		$(BASENAME).$(PREFIX1).dix	\
		$(BASENAME).$(PREFIX1).t1x	\
		$(BASENAME).$(PREFIX1).t2x	\
		$(BASENAME).$(PREFIX1).t3x	\
		$(BASENAME).$(PREFIX2).t1x	\
		$(BASENAME).$(PREFIX2).t2ax	\
		$(BASENAME).$(PREFIX2).t2bx	\
		$(BASENAME).$(PREFIX2).t2cx	\
		$(BASENAME).$(PREFIX2).t3x	\
		modes.xml

###############################################################################
## Installation
###############################################################################

apertium_fra_frpdir=$(prefix)/share/apertium/$(BASENAME)/

# Files which should be installed to $(prefix)/share/apertium/$(BASENAME)/:
apertium_fra_frp_DATA=	\
	$(TARGETS_COMMON)				\
	$(BASENAME).$(PREFIX1).dix			\
	$(BASENAME).$(PREFIX1).l1x			\
	$(BASENAME).$(PREFIX1).l2x			\
	$(BASENAME).$(PREFIX1).metalrx			\
	$(BASENAME).$(PREFIX1).t1x			\
	$(BASENAME).$(PREFIX1).t2x			\
	$(BASENAME).$(PREFIX1).t3x			\
	$(BASENAME).$(PREFIX2).metalrx			\
	$(BASENAME).$(PREFIX2).t1x			\
	$(BASENAME).$(PREFIX2).t2ax			\
	$(BASENAME).$(PREFIX2).t2bx			\
	$(BASENAME).$(PREFIX2).t2cx			\
	$(BASENAME).$(PREFIX2).t3x


# All modes are created by the same goal, listing several will just give problems with make -j2
noinst_DATA=modes/$(PREFIX1).mode \
	.deps/$(LANG1).automorf.bin \
	.deps/$(LANG2).automorf.bin

install-data-local: install-modes

###############################################################################
## Cleanup
###############################################################################

CLEANFILES = $(TARGETS_COMMON)
clean-local:
	-rm -rf .deps modes

###############################################################################
## Test
###############################################################################

test: all
	echo "Apertium est un logiciel de traduction automatique." | apertium -d . fra-frp | tee .test-mt
	@echo "Apertium est una programerie de traduccion ôtomatica." > .test-ref
	@diff .test-ref .test-mt
	echo "Apertium est una programerie de traduccion ôtomatica." | apertium -d . frp-fra | tee .test-mt
	@echo "Apertium est un logiciel de traduction automatique." > .test-ref
	@diff .test-ref .test-mt
	@rm .test-ref .test-mt
