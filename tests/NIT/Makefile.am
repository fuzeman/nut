EXTRA_DIST = nit.sh README

if WITH_CHECK_NIT
check: check-NIT
else
check:
	@echo "NO-OP: $@ in `pwd` is inactive by default. Run 'configure --enable-check-NIT' or 'make check-NIT' explicitly" >&2
endif

# Run in builddir, use script from srcdir
# Avoid running "$<" - not all make implementations handle that
check-NIT: $(abs_srcdir)/nit.sh
	"$(abs_srcdir)/nit.sh"

# Make sure pre-requisites for NIT are fresh as we iterate
check-NIT-devel: $(abs_srcdir)/nit.sh
	@cd .. && ( $(MAKE) -s cppnit$(EXEEXT) || echo "OPTIONAL C++ test client test will be skipped" )
	@cd "$(top_builddir)/clients" && $(MAKE) -s upsc$(EXEEXT) upsrw$(EXEEXT) upsmon$(EXEEXT)
	@cd "$(top_builddir)/server" && $(MAKE) -s upsd$(EXEEXT)
	@cd "$(top_builddir)/drivers" && $(MAKE) -s dummy-ups$(EXEEXT)
	@$(MAKE) check-NIT

MAINTAINERCLEANFILES = Makefile.in .dirstamp

clean-local:
	rm -rf tmp
