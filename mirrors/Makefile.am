# Default mirrors
pkgdata_MIRRORS = default

# Mirrors in Asia (excl. China and Russia)
pkgdata_ASIA_MIRRORS = mirror.albony.xyz mirror.bardia.tech          \
mirrors.cbrx.io linux.domainesia.com mirror.nevacloud.com            \
mirror.textcord.xyz tmx.xvx.my.id  mirrors.nguyenhoang.cloud         \
mirror.freedif.org

# Mirrors in China
pkgdata_CHINA_MIRRORS = mirrors.tuna.tsinghua.edu.cn                 \
mirror.iscas.ac.cn mirrors.nju.edu.cn mirrors.pku.edu.cn             \
mirrors.ustc.edu.cn mirrors.bfsu.edu.cn	mirrors.aliyun.com           \
mirrors.cqupt.edu.cn mirror.nyist.edu.cn mirrors.sau.edu.cn	         \
mirrors.sdu.edu.cn mirrors.sustech.edu.cn mirrors.zju.edu.cn         \
mirror.sjtu.edu.cn mirrors.qvq.net.cn

# Mirrors in Europe
pkgdata_EUROPE_MIRRORS = grimler.se mirror.neoterm.dev                \
repo.theworkjoy.com neoterm.librehat.com mirror.mwt.me                \
neoterm.mentality.rip mirrors.sahilister.in neoterm.cdn.lumito.net     \
neoterm.astra.in.ua neoterm.3san.dev mirror.accum.se                   \
md.mirrors.hacktegic.com ftp.fau.de is.mirror.flokinet.net           \
ro.mirror.flokinet.net mirrors.medzik.dev mirrors.cfe.re             \
mirror.sunred.org mirror.autkin.net mirror.bouwhuis.network          \
mirror.leitecastro.com 

# Mirrors in North America
pkgdata_NORTH_AMERICA_MIRRORS = plug-mirror.rcac.purdue.edu          \
dl.kcubeterm.com mirrors.uneoterm.dev mirror.fcix.net mirror.mwt.me   \
mirror.vern.cc mirror.csclub.uwaterloo.ca mirror.quantum5.ca

# Mirrors in Oceania
pkgdata_OCEANIA_MIRRORS = mirror.endianness.com

# Mirrors in South America
pkgdata_SOUTH_AMERICA_MIRRORS = mirrors.rda.run

# Mirrors in Russia
pkgdata_RUSSIA_MIRRORS = mirror.mephi.ru repository.su


# Removed, renamed or moved mirrors
# Mirrors files are marked as conffiles and they are manually deleted
# in preinst step of package upgrade as conffiles removed in a newer
# version of the package are only deleted if package is purged and
# would otherwise be left as is after package upgrades and would still
# get used during mirror selection.
pkgdata_MIRRORS_REMOVED = \
asia/packages.nscdn.top \
china/mirrors.dgut.edu.cn \
china/mirrors.hit.edu.cn \
china/mirrors.njupt.edu.cn \
china/mirrors.scau.edu.cn \
europe/cdn.lumito.net \
europe/mirror.neoterm.dv \
europe/neoterm.sahilister.in \
north_america/repo.theworkjoy.com \
oceania/mirrors.wale.id.au \
russia/mirror.surf



define install-mirror-rule
install-$1:
	$$(MKDIR_P) $$(DESTDIR)$$(sysconfdir)/neoterm/mirrors/$1
	for f in $$(pkgdata_$2_MIRRORS); do \
		$(INSTALL) -m 644 $(srcdir)/$1/$$$$f \
		$(DESTDIR)$(sysconfdir)/neoterm/mirrors/$1; \
	done
endef

define uninstall-mirror-rule
uninstall-$1:
	for f in $$(pkgdata_$2_MIRRORS); do \
		rm -f $(DESTDIR)$(sysconfdir)/neoterm/mirrors/$1/$$$$f; \
	done
	-rmdir $(DESTDIR)$(sysconfdir)/neoterm/mirrors/$1
endef

$(eval $(call install-mirror-rule,asia,ASIA))
$(eval $(call install-mirror-rule,china,CHINA))
$(eval $(call install-mirror-rule,europe,EUROPE))
$(eval $(call install-mirror-rule,north_america,NORTH_AMERICA))
$(eval $(call install-mirror-rule,oceania,OCEANIA))
$(eval $(call install-mirror-rule,south_america,SOUTH_AMERICA))
$(eval $(call install-mirror-rule,russia,RUSSIA))

$(eval $(call uninstall-mirror-rule,asia,ASIA))
$(eval $(call uninstall-mirror-rule,china,CHINA))
$(eval $(call uninstall-mirror-rule,europe,EUROPE))
$(eval $(call uninstall-mirror-rule,north_america,NORTH_AMERICA))
$(eval $(call uninstall-mirror-rule,oceania,OCEANIA))
$(eval $(call uninstall-mirror-rule,south_america,SOUTH_AMERICA))
$(eval $(call uninstall-mirror-rule,russia,RUSSIA))



install-default: $(pkgdata_MIRRORS)
	$(MKDIR_P) $(DESTDIR)$(sysconfdir)/neoterm/mirrors
	for f in $(pkgdata_MIRRORS); do \
		$(INSTALL) -m 644 $(srcdir)/$$f \
		$(DESTDIR)$(sysconfdir)/neoterm/mirrors; \
	done

uninstall-default:
	for f in $(pkgdata_MIRRORS); do \
		rm -f $(DESTDIR)$(sysconfdir)/neoterm/mirrors/$$f; \
	done
	-rmdir $(DESTDIR)$(sysconfdir)/neoterm/mirrors



uninstall-removed-mirrors:
	for f in $(pkgdata_MIRRORS_REMOVED); do \
		rm -f $(DESTDIR)$(sysconfdir)/neoterm/mirrors/$$f; \
	done



create-deb-control-files:
	sh -c "cd $$(dirname $(DESTDIR)$(sysconfdir)); find $$(basename $(DESTDIR)$(sysconfdir))/neoterm/mirrors -type f" >> ../conffiles;
	printf "# Delete removed mirrors\nfor f in %s; do\n    if test -f \"%s/etc/neoterm/mirrors/\$$f\"; then\n        echo \"Deleting removed mirror: \$$f\"; rm -f \"%s/etc/neoterm/mirrors/\$$f\";\n    fi\ndone" "$(pkgdata_MIRRORS_REMOVED)" "$(neoterm_prefix)" "$(neoterm_prefix)" >> ../preinst;



install-data-local: uninstall-removed-mirrors install-default install-asia install-china install-europe install-north_america install-oceania install-south_america install-russia create-deb-control-files

uninstall-local: uninstall-removed-mirrors uninstall-default uninstall-asia uninstall-china uninstall-europe uninstall-north_america uninstall-oceania uninstall-south_america uninstall-russia

EXTRA_DIST = $(pkgdata_MIRRORS) $(pkgdata_ASIA_MIRRORS)		\
$(pkgdata_CHINA_MIRRORS) $(pkgdata_EUROPE_MIRRORS)		\
$(pkgdata_NORTH_AMERICA_MIRRORS) $(pkgdata_OCEANIA_MIRRORS)	\
$(pkgdata_SOUTH_AMERICA_MIRRORS)
