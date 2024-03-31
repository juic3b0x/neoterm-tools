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

man_MANS = neoterm.1

neoterm.1.md: ${srcdir}/neoterm.1.md.in
	@echo "Creating neoterm.1.md"
	@sed -e "s%[@]NEOTERM_PREFIX[@]%$(neoterm_prefix)%g" \
	    -e "s%[@]NEOTERM_HOME[@]%${neoterm_android_home}%g" \
	${srcdir}/neoterm.1.md.in > neoterm.1.md

neoterm.1: neoterm.1.md
	@echo "Generating neoterm.1"
	@pandoc --standalone --to man --output neoterm.1 neoterm.1.md
