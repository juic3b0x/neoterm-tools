# Copyright (C) 2022 NeoTerm

# This file is part of neoterm-tools.

# neoterm-tools is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.

# neoterm-tools is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with neoterm-tools.  If not, see
# <https://www.gnu.org/licenses/>.

SUBDIRS = . scripts doc mirrors motds

CONFFILES = \
etc/motd \
etc/motd.sh \
etc/motd-playstore \
etc/profile.d/init-neoterm-properties.sh \
etc/neoterm-login.sh

do_subst = sed -e "s%[@]NEOTERM_PREFIX[@]%$(neoterm_prefix)%g" \
	       -e "s%[@]NEOTERM_APP_PACKAGE[@]%${neoterm_app_package}%g" \
	       -e "s%[@]NEOTERM_BASE_DIR[@]%${neoterm_base_dir}%g" \
	       -e "s%[@]NEOTERM_CACHE_DIR[@]%${neoterm_cache_dir}%g" \
	       -e "s%[@]NEOTERM_HOME[@]%${neoterm_android_home}%g" \
	       -e "s%[@]PACKAGE_VERSION[@]%${PACKAGE_VERSION}%g" \
	       -e "s%[@]NEOTERM_PACKAGE_FORMAT[@]%${NEOTERM_PACKAGE_FORMAT}%g" \
	       -e "s%[@]NEOTERM_PACKAGE_MANAGER[@]%${NEOTERM_PACKAGE_MANAGER}%g"

define sed-rule
$1: $1.in Makefile
	@echo "Creating $1"
	@$$(do_subst) < $(srcdir)/$1.in > $1
endef

# Login script
sysconf_DATA = neoterm-login.sh

# profile.d script
pkgdata_PROFILE = init-neoterm-properties.sh

pkgdata_EXAMPLES = neoterm.properties

$(eval $(call sed-rule,init-neoterm-properties.sh))

$(eval $(call sed-rule,neoterm-login.sh))



create-deb-control-files:
	printf "" > conffiles
	for f in $(CONFFILES); do \
		printf "%s\n" "$$f" >> conffiles; \
	done
	printf "#!%s/bin/bash\n\n" "${neoterm_prefix}" > preinst



install-data-local: create-deb-control-files $(pkgdata_PROFILE)
	$(MKDIR_P) $(DESTDIR)$(datarootdir)/examples/neoterm
	for f in $(pkgdata_EXAMPLES); do \
		$(INSTALL) -m 644 $(srcdir)/$$f \
		$(DESTDIR)$(datarootdir)/examples/neoterm; \
	done
	$(MKDIR_P) $(DESTDIR)$(sysconfdir)/profile.d
	for f in $(pkgdata_PROFILE); do \
		$(INSTALL) -m 644 $$f \
		$(DESTDIR)$(sysconfdir)/profile.d; \
	done

uninstall-local:
	for f in $(pkgdata_EXAMPLES); do \
		rm -f $(DESTDIR)$(datarootdir)/examples/neoterm/$$f; \
	done
	-rmdir $(DESTDIR)$(datarootdir)/examples/neoterm
	for f in $(pkgdata_PROFILE); do \
		rm -f $(DESTDIR)$(sysconfdir)/profile.d/$$f; \
	done
	-rmdir $(DESTDIR)$(sysconfdir)/profile.d

EXTRA_DIST = $(pkgdata_DATA) $(pkgdata_PROFILE) $(pkgdata_EXAMPLES)
