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


# We have two variants of our motd message loaded by login script:
#   1. motd.sh: A dynamic motd that is executed with bash and echos a
#      motd message with escape sequences, optionally with a terminal logo.
#   2. motd: A static motd that is just read as is with cat and displayed.

# The motd-playstore is an additional motd that will only be displayed
# if the neoterm-app version is very old (like the version found on playstore)
sysconf_DATA = motd.sh motd motd-playstore

CLEANFILES = motd.sh motd


do_subst = sed -e "s%[@]NEOTERM_PREFIX[@]%$(neoterm_prefix)%g"

define process-rule
$1: $1.in Makefile
	@echo "Creating $1"
	@$$(do_subst) < $(srcdir)/$1.in > $1
endef

$(eval $(call process-rule,motd.sh))


motd:
	@echo "Creating motd file"

	@echo "Welcome to NeoTerm!" > motd
	@echo "" >> motd
	@echo "Docs:       https://repo.theworkjoy.com/docs" >> motd
	@echo "Donate:     https://repo.theworkjoy.com/donate" >> motd
	@echo "Community:  https://repo.theworkjoy.com/community" >> motd

	@echo "" >> motd
	@echo "Working with packages:" >> motd
	@echo "" >> motd
	@echo " - Search:  pkg search <query>" >> motd
	@echo " - Install: pkg install <package>" >> motd
	@echo " - Upgrade: pkg upgrade" >> motd

    ifeq ($(NEOTERM_PACKAGE_MANAGER),apt)
		@echo "" >> motd
		@echo "Subscribing to additional repositories:" >> motd
		@echo "" >> motd
		@echo " - Root:    pkg install root-repo" >> motd
		@echo " - X11:     pkg install x11-repo" >> motd
		@echo "" >> motd
		@echo "For fixing any repository issues," >> motd
		@echo "try 'neoterm-change-repo' command." >> motd
    endif

	@echo "" >> motd
	@echo "Report issues at https://repo.theworkjoy.com/issues" >> motd
