# run all targets sequentially
.NOTPARALLEL:

# this variable marks this file has been included
BUILDYS_COMMON_INCLUDED=1

BUILDSYS_COMMON_ROOT := $(dir $(realpath $(lastword $(MAKEFILE_LIST))))

# use given customer's debian directory
DEB_CUSTOMER ?= internal

# dput configuration
DPUT_DISTRIBUTION := citationtech
DPUT_CONFIG := dput.cf

deb: deb_prepare
	@(dpkg-buildpackage -b -j`grep -c ^processor /proc/cpuinfo`)

debclean: deb_prepare
	@(unset MAKELEVEL; unset MAKEFLAGS;	fakeroot ./debian/rules clean)

dput: deb_prepare
	dput -c $(join $(BUILDSYS_COMMON_ROOT),dput.cf) $(DPUT_DISTRIBUTION) $(call deb_changes_file)

dversion: deb_prepare
	@echo $(call deb_version)

dch: deb_prepare
	@dch -i --no-auto-nmu

# notice no quotes around deb_tag -> we get package name and package version as
# separates args
dtag: deb_prepare
	@$(BUILDSYS_COMMON_ROOT)/dtag.sh $(call deb_tag)

.PHONY: deb debclean dput dtag deb_prepare

deb_prepare:
	@if ! /usr/bin/test -a debian; then \
		ln -sfT debian.$(DEB_CUSTOMER) debian; \
	elif /usr/bin/test -h debian; then \
		ln -sfT debian.$(DEB_CUSTOMER) debian; \
	fi

# supporting macros
define deb_changes_file
$(shell (dpkg-parsechangelog; \
	echo -n "Architecture: "; dpkg-architecture -qDEB_BUILD_ARCH) \
	| gawk '/^Version:/ { version=$$2; } /^Source:/ { source=$$2; } /^Architecture:/ { arch=$$2; } END { printf("../%s_%s_%s.changes\n", source, version, arch); }')
endef

define deb_tag
$(shell dpkg-parsechangelog | \
	gawk '/^Version:/ { version=$$2; } /^Source:/ { source=$$2; } END { printf("%s %s\n", source, version); }')
endef

define deb_version
$(shell dpkg-parsechangelog | \
	gawk '/^Version:/ { print $$2; }')
endef


tar:
	@($(BUILDSYS_COMMON_ROOT)/make-tarball.sh -j`grep -c ^processor /proc/cpuinfo`)
