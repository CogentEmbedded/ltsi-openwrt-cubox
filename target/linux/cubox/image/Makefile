#
# Copyright (C) 2009-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/image.mk

define Image/BuildKernel
	$(LINUX_DIR)/scripts/dtc/dtc -O dtb -o $(KDIR)/dove-cubox.dtb $(LINUX_DIR)/arch/arm/boot/dts/dove-cubox.dts
	cat $(LINUX_DIR)/arch/arm/boot/zImage $(KDIR)/dove-cubox.dtb > $(KDIR)/$(IMG_PREFIX)-zImage
	/bin/sh $(LINUX_DIR)/scripts/mkuboot.sh -A arm -O linux -C none -T kernel -a 0x00008000 -e 0x00008000 -n 'Linux' -d $(KDIR)/$(IMG_PREFIX)-zImage $(BIN_DIR)/$(IMG_PREFIX)-uImage
endef

define Image/Build/squashfs
	$(call prepare_generic_squashfs,$(KDIR)/root.squashfs)
	dd if=$(KDIR)/root.$(1) of=$(BIN_DIR)/$(IMG_PREFIX)-$(1).img bs=128k conv=sync
endef

define Image/Build
	$(call Image/Build/$(1),$(1))
endef

$(eval $(call BuildImage))
