ASSEMBLY = notify-sharp
TARGET = $(ASSEMBLY).dll

CSFLAGS = \
	-target:library

LIBFLAGS = \
	-r:Mono.Posix \
	$(GTK_SHARP_LIBS) \
	$(DBUS_SHARP_LIBS)

CSFILES = \
	$(srcdir)/Global.cs \
	$(srcdir)/Notification.cs

all: $(TARGET)

$(TARGET): $(CSFILES) AssemblyInfo.cs
	$(GMCS) -out:$@ $(CSFLAGS) $(LIBFLAGS) $^

install-data-local:
	@if test -n '$(TARGET)'; then                       \
          echo "$(GACUTIL) /i $(TARGET) /f /gacdir $(DESTDIR)$(libdir)";    \
          $(GACUTIL) /i $(TARGET) /package $(ASSEMBLY) /f /gacdir $(libdir) /root $(DESTDIR)$(libdir) || exit 1; \
        fi

uninstall-local:
	@if test -n '$(TARGET)'; then                       \
          echo "$(GACUTIL) /u $(ASSEMBLY) /gacdir $(DESTDIR)$(libdir)";  \
          $(GACUTIL) /u $(ASSEMBLY) /package $(ASSEMBLY) /gacdir $(libdir) /root $(DESTDIR)$(libdir) || exit 1;   \
        fi

EXTRA_DIST = \
	$(CSFILES) \
	$(srcdir)/$(TARGET).config \
	$(srcdir)/AssemblyInfo.cs.in \
	$(srcdir)/notify-sharp.snk

CLEANFILES = \
	$(TARGET)

DISTCLEANFILES = \
	AssemblyInfo.cs

MAINTAINERCLEANFILES = \
	Makefile.in
