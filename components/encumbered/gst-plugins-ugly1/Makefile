#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"), version 1.0.
# You may only use this file in accordance with the terms of version
# 1.0 of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source.  A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2016-2018 Aurelien Larcher.  All rights reserved.
# Copyright 2019 Michal Nowak
#

BUILD_BITS= 32_and_64

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME= gst-plugins-ugly1
COMPONENT_VERSION= 1.16.2
COMPONENT_SUMMARY= GNOME streaming media framework plugins
COMPONENT_CLASSIFICATION= System/Multimedia Libraries
COMPONENT_FMRI= library/audio/gstreamer1/plugin/ugly
COMPONENT_SRC_NAME= gst-plugins-ugly
COMPONENT_SRC= $(COMPONENT_SRC_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE= $(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_HASH= \
  sha256:5500415b865e8b62775d4742cbb9f37146a50caecfc0e7a6fc0160d3c560fbca
COMPONENT_ARCHIVE_URL= \
  https://gstreamer.freedesktop.org/src/$(COMPONENT_SRC_NAME)/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL = https://gstreamer.freedesktop.org/
COMPONENT_LICENSE= LGPLv2

include $(WS_MAKE_RULES)/encumbered.mk
include $(WS_MAKE_RULES)/common.mk

COMPONENT_PREP_ACTION = ( cd $(SOURCE_DIR) && aclocal -I ./m4 -I./common/m4 &&\
                          autoheader &&\
                          automake -a -f -c --gnu &&\
                          autoconf )
gcc_OPT = -O2

PATH = $(PATH.gnu)

CFLAGS += -I/usr/X11/include/mesa
CFLAGS += -I/usr/X11/include

CONFIGURE_OPTIONS += --sysconfdir=/etc
CONFIGURE_OPTIONS += --disable-examples
CONFIGURE_OPTIONS += --enable-external
CONFIGURE_OPTIONS += --enable-orc
CONFIGURE_OPTIONS += --with-default-audiosrc=autoaudiosrc
CONFIGURE_OPTIONS += --with-default-audiosink=autoaudiosink
CONFIGURE_OPTIONS += --with-default-videosink=autovideosink

# CFLAGS are not passed to compiler when g-ir-scanner is used
COMPONENT_BUILD_ENV += CFLAGS="$(CFLAGS)"
COMPONENT_BUILD_ENV += CXXFLAGS="$(CXXFLAGS)"
COMPONENT_INSTALL_ENV += CFLAGS="$(CFLAGS)"
COMPONENT_INSTALL_ENV += CXXFLAGS="$(CXXFLAGS)"

COMPONENT_INSTALL_ENV += GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1

unexport SHELLOPTS
COMPONENT_TEST_TRANSFORMS= \
	'-n ' \
	'-e "/TOTAL/p" ' \
	'-e "/PASS/p" '  \
	'-e "/SKIP/p" '  \
	'-e "/XFAIL/p" ' \
	'-e "/FAIL/p" '  \
	'-e "/XPASS/p" ' \
	'-e "/ERROR/p" '

# Auto-generated dependencies
REQUIRED_PACKAGES += codec/opencore-amr
REQUIRED_PACKAGES += library/audio/gstreamer1
REQUIRED_PACKAGES += library/audio/gstreamer1/plugin/base
REQUIRED_PACKAGES += library/audio/liba52
REQUIRED_PACKAGES += library/audio/libcdio
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/video/libdvdread
REQUIRED_PACKAGES += library/video/libmpeg2
REQUIRED_PACKAGES += library/video/x264
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/orc
