#
# Download realtek r8168 linux driver from official site:
# [https://www.realtek.com/component/zoo/category/network-interface-controllers-10-100-1000m-gigabit-ethernet-pci-express-software]
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=r8168
PKG_VERSION:=8.049.02
PKG_RELEASE:=22

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/BROBIRD/openwrt-r8168.git
PKG_SOURCE_DATE:=2021-10-08
PKG_SOURCE_VERSION:=2b969c15afe403a685fc7ee069620782241e3ad6
PKG_MIRROR_HASH:=skip

PKG_BUILD_DIR:=$(KERNEL_BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

MAKE_PATH:=src

include $(INCLUDE_DIR)/package.mk

define KernelPackage/r8168
  TITLE:=Driver for Realtek r8168 chipsets
  SUBMENU:=Network Devices
  VERSION:=$(LINUX_VERSION)+$(PKG_VERSION)-$(BOARD)-$(PKG_RELEASE)
  DEPENDS:=
  FILES:= $(PKG_BUILD_DIR)/src/r8168.ko
  AUTOLOAD:=$(call AutoProbe,r8168)
  
endef

define Package/r8168/description
  This package contains a driver for Realtek r8168 chipsets.
endef

R8168_MAKEOPTS= -C $(PKG_BUILD_DIR)/src \
	PATH="$(TARGET_PATH)" \
	ARCH="$(LINUX_KARCH)" \
	CROSS_COMPILE="$(TARGET_CROSS)" \
	TARGET="$(HAL_TARGET)" \
	TOOLPREFIX="$(KERNEL_CROSS)" \
	TOOLPATH="$(KERNEL_CROSS)" \
	KERNELPATH="$(LINUX_DIR)" \
	KERNELDIR="$(LINUX_DIR)" \
	LDOPTS=" " \
	DOMULTI=1

define Build/Compile
	$(MAKE) $(R8168_MAKEOPTS) modules
endef

$(eval $(call KernelPackage,r8168))