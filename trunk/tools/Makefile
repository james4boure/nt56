# use host target
CC        = gcc
GCC       = gcc
CXX       = g++
AS        = as
AR        = ar
LD        = ld
NM        = nm
OBJCOPY   = objcopy
RANLIB    = ranlib
STRIP     = strip
STRIPTOOL = $(STRIP)
SSTRIP_NAME = ELFkickers-3.1

CFLAGS    = -Wall -O2
LDFLAGS   =

-include $(LINUX_CONFIG)

# Go installation
GO_VERSION = 1.15.2
GO_TAR = go$(GO_VERSION).linux-amd64.tar.gz
GO_URL = https://mirrors.ustc.edu.cn/golang/$(GO_TAR)
GO_DIR = trunk/tools/go

$(GO_DIR)/$(GO_TAR):
	mkdir -p $(GO_DIR)
	curl --create-dirs -L $(GO_URL) -o $(GO_DIR)/$(GO_TAR)

all: $(GO_DIR)/$(GO_TAR)
	make -C trunk/tools/mkimage
	mkdir -p trunk/tools/sstrip
	make -C trunk/tools/$(SSTRIP_NAME)
	make -C trunk/tools/lzma
ifeq ($(CONFIG_RT2880_ROOTFS_IN_FLASH),y)
	make -C trunk/tools/mksquashfs_xz
endif

clean:
	if [ -f trunk/tools/$(SSTRIP_NAME)/Makefile ] ; then \
		make -C trunk/tools/$(SSTRIP_NAME) clean ; \
	fi ;
	rm -rf trunk/tools/sstrip
	make -C trunk/tools/mkimage clean
	make -C trunk/tools/lzma clean
	make -C trunk/tools/mksquashfs_xz clean
