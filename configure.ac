dnl  Autoconf script for neoterm-tools
dnl To rebuild the 'configure' script from this, execute the command
dnl	autoconf
dnl in the directory containing this script.
dnl
dnl Copyright (C) 2024 NeoTerm
dnl
dnl  This file is part of neoterm-tools.
dnl
dnl  neoterm-tools is free software: you can redistribute it
dnl  and/or modify it under the terms of the GNU General Public
dnl  License as published by the Free Software Foundation, either
dnl  version 3 of the License, or (at your option) any later version.
dnl
dnl  neoterm-tools is distributed in the hope that it will be
dnl  useful, but WITHOUT ANY WARRANTY; without even the implied
dnl  warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
dnl  See the GNU General Public License for more details.
dnl
dnl  You should have received a copy of the GNU General Public License
dnl  along with neoterm-tools.  If not, see
dnl  <https://www.gnu.org/licenses/>.

AC_PREREQ([2.69])
AC_INIT([neoterm-tools], [1.41.3], [support@theworkjoy.com])

AM_INIT_AUTOMAKE([foreign])

AC_PROG_MAKE_SET

copyright="Copyright (C) 2024 NeoTerm."
if test "${NEOTERM_APP_PACKAGE+set}" = set; then
  neoterm_app_package="$NEOTERM_APP_PACKAGE"
else
  neoterm_app_package="io.neoterm"
fi
if test "${NEOTERM_BASE_DIR+set}" = set; then
  neoterm_base_dir="$NEOTERM_BASE_DIR"
else
  neoterm_base_dir="/data/data/$neoterm_app_package/files"
fi
if test "${NEOTERM_CACHE_DIR+set}" = set; then
  neoterm_cache_dir="$NEOTERM_CACHE_DIR"
else
  neoterm_cache_dir="/data/data/$neoterm_app_package/cache"
fi
if test "${NEOTERM_PREFIX+set}" = set; then
  neoterm_prefix="$NEOTERM_PREFIX"
else
  neoterm_prefix="$neoterm_base_dir/usr"
fi
if test "${NEOTERM_ANDROID_HOME+set}" = set; then
  neoterm_android_home="$NEOTERM_ANDROID_HOME"
else
  neoterm_android_home="$neoterm_base_dir/home"
fi
if test "${NEOTERM_PACKAGE_FORMAT+set}" = set; then
  neoterm_package_format="$NEOTERM_PACKAGE_FORMAT"
else
  neoterm_package_format="debian"
fi
if test "${NEOTERM_PACKAGE_MANAGER+set}" = set; then
  neoterm_package_manager="$NEOTERM_PACKAGE_MANAGER"
else
  neoterm_package_manager="apt"
fi

AC_DEFINE_UNQUOTED(COPYRIGHT, ["$copyright"],
  [Short copyright string for this version of neoterm-tools.])
AC_DEFINE_UNQUOTED(NEOTERM_APP_PACKAGE, ["$neoterm_app_package"],
  [NeoTerm namespace])
AC_DEFINE_UNQUOTED(NEOTERM_BASE_DIR, ["$neoterm_base_dir"],
  [Base directory of neoterm application])
AC_DEFINE_UNQUOTED(NEOTERM_CACHE_DIR, ["$neoterm_cache_dir"],
  [Cache directory of neoterm application])
AC_DEFINE_UNQUOTED(NEOTERM_PREFIX, ["$neoterm_prefix"],
  [NeoTerm prefix])
AC_DEFINE_UNQUOTED(NEOTERM_ANDROID_HOME, ["$neoterm_android_home"],
  [NeoTerm home directory])
AC_DEFINE_UNQUOTED(NEOTERM_PACKAGE_FORMAT, ["$neoterm_package_format"],
  [Packaging format (debian or pacman)])
AC_DEFINE_UNQUOTED(NEOTERM_PACKAGE_MANAGER, ["$neoterm_package_manager"],
  [Package manager (apt or pacman)])

AC_SUBST(neoterm_app_package)
AC_SUBST(neoterm_base_dir)
AC_SUBST(neoterm_cache_dir)
AC_SUBST(neoterm_prefix)
AC_SUBST(neoterm_android_home)
AC_SUBST(neoterm_package_format)
AC_SUBST(neoterm_package_manager)

AC_PROG_LN_S

AC_CONFIG_FILES([Makefile scripts/Makefile doc/Makefile
mirrors/Makefile motds/Makefile])

AC_OUTPUT
