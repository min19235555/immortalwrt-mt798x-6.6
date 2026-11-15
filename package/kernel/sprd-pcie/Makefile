#
# Quectel SPRD (UNISOC) PCIe EP driver for RM500U/RM520N class modules.
#
# Upstream: https://github.com/usdyg/quectel-sprd-pcie
# The driver registers a private PCIe protocol on top of the module's
# 16c3:abcd endpoint and creates an Ethernet (or raw-IP) netdevice.
#
include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=quectel-sprd-pcie
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/usdyg/quectel-sprd-pcie.git
PKG_SOURCE_DATE:=2026-05-31
PKG_SOURCE_VERSION:=35c32481633f6f703a3d76390099c2794d52a5fb
PKG_MIRROR_HASH:=skip

include $(INCLUDE_DIR)/package.mk

define KernelPackage/sprd-pcie
  SUBMENU:=WWAN Support
  TITLE:=Quectel SPRD/UNISOC PCIe endpoint driver
  DEPENDS:=@PCI_SUPPORT +kmod-mii
  FILES:=$(PKG_BUILD_DIR)/sprd_pcie.ko
  AUTOLOAD:=$(call AutoLoad,90,sprd_pcie)
endef

define KernelPackage/sprd-pcie/description
  PCIe host driver for Quectel 5G modules based on UNISOC chipsets
  (RM500U-CN/RM500U-CNV and similar). The module exposes a Synopsys
  DWC_usb3/PCIe bridge (16c3:abcd) and this driver implements the
  SIP C / SIPA data path on top of it, creating a netdevice.
endef

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		$(KERNEL_MAKE_FLAGS) \
		M="$(PKG_BUILD_DIR)" \
		modules
endef

$(eval $(call KernelPackage,sprd-pcie))
