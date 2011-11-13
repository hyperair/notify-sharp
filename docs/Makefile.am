DOC_UPDATER = @MONODOCER@ -delete
DOC_ASSEMBLER = @MDASSEMBLER@ --out notify-sharp-docs --ecma

ASSEMBLIES = \
	$(top_builddir)/src/notify-sharp.dll

ASSEMBLIES_BUILD = $(foreach asm,$(ASSEMBLIES),$(addprefix -assembly:,$(asm)))

if BUILD_DOCS

monodocdir = $(DOCDIR)
monodoc_DATA = \
	notify-sharp-docs.zip \
	notify-sharp-docs.tree \
	$(srcdir)/notify-sharp-docs.source

all:

update-docs: $(ASSEMBLIES)
	$(DOC_UPDATER) $(ASSEMBLIES_BUILD) -path:en

notify-sharp-docs.zip notify-sharp-docs.tree: $(srcdir)/en/*/*.xml $(srcdir)/en/*.xml
	$(DOC_ASSEMBLER) $(srcdir)/en

endif

EXTRA_DIST = \
	$(srcdir)/en/*.xml \
	$(srcdir)/en/*/*.xml \
	$(srcdir)/notify-sharp-docs.source

DISTCLEANFILES = \
	notify-sharp-docs.zip \
	notify-sharp-docs.tree

MAINTAINERCLEANFILES = \
	Makefile.in

