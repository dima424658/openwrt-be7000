#
# Copyright (C) 2022 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ath11k-firmware
PKG_SOURCE_DATE:=2026-01-23
PKG_SOURCE_VERSION:=53f9ee68543d66894854c32e1e968cb514c0880a
PKG_MIRROR_HASH:=3a1baa8032541f6c752fc9be7eaa7f3c8df352f1d0a8e0977373904af7f2669d
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://git.codelinaro.org/clo/ath-firmware/ath11k-firmware.git

PKG_LICENSE_FILES:=LICENSE.qca_firmware

PKG_MAINTAINER:=Robert Marko <robimarko@gmail.com>

include $(INCLUDE_DIR)/package.mk

RSTRIP:=:
STRIP:=:

ATH11K_LEGACY_FW_NAME:=ath11k-legacy-firmware
ATH11K_LEGACY_FW_DATE:=2024-03-14
ATH11K_LEGACY_FW_RELEASE:=795809c7
ATH11K_LEGACY_FW_SUBDIR:=$(ATH11K_LEGACY_FW_NAME)-$(ATH11K_LEGACY_FW_DATE)~$(ATH11K_LEGACY_FW_RELEASE)
ATH11K_LEGACY_FW_SOURCE=$(ATH11K_LEGACY_FW_SUBDIR).tar.zst

define Download/$(ATH11K_LEGACY_FW_NAME)
	FILE:=$(ATH11K_LEGACY_FW_SOURCE)
	PROTO:=git
	URL:=https://github.com/quic/upstream-wifi-fw.git
	SOURCE_VERSION:=795809c7041582bd51bdfaa1f548b916ae8d4382
	MIRROR_HASH:=b55bf7204543c7ba87876e84788239b0e47ad62434c5b0d1169526cde36a9daa
	SUBDIR:=$(ATH11K_LEGACY_FW_SUBDIR)
endef

define Package/ath11k-firmware-default
  SECTION:=firmware
  CATEGORY:=Firmware
  URL:=$(PKG_SOURCE_URL)
  DEPENDS:=
endef

define Package/ath11k-firmware-ipq5018
$(Package/ath11k-firmware-default)
  TITLE:=IPQ5018 ath11k firmware
endef

define Package/ath11k-firmware-ipq5018-qcn6122
$(Package/ath11k-firmware-default)
  TITLE:=IPQ5018/QCN6122 ath11k firmware
endef

define Package/ath11k-firmware-ipq6018
$(Package/ath11k-firmware-default)
  TITLE:=IPQ6018 ath11k firmware
endef

define Package/ath11k-firmware-ipq8074
$(Package/ath11k-firmware-default)
  TITLE:=IPQ8074 ath11k firmware
endef

define Package/ath11k-firmware-ipq9574
$(Package/ath11k-firmware-default)
  TITLE:=IPQ9574 ath11k firmware
endef

define Package/ath11k-firmware-qcn9074
$(Package/ath11k-firmware-default)
  TITLE:=QCN9074 ath11k firmware
endef

define Build/Clean
	$(call Build/Clean/Default,)

	rm -rf \
		$(BUILD_DIR)/$(ATH11K_LEGACY_FW_SUBDIR)
endef

define Build/Prepare
	$(eval $(call Download,ath11k-legacy-firmware))
	
	$(call Build/Prepare/Default,)

	$(TAR) -C $(BUILD_DIR) -xf $(DL_DIR)/$(ATH11K_LEGACY_FW_SOURCE)
endef

define Build/Compile

endef

define Package/ath11k-firmware-ipq5018/install
	$(INSTALL_DIR) $(1)/lib/firmware/ath11k/IPQ5018/hw1.0
	$(INSTALL_DATA) \
		$(PKG_BUILD_DIR)/IPQ5018/hw1.0/2.6.0.1/WLAN.HK.2.6.0.1-01291-QCAHKSWPL_SILICONZ-1/* \
		$(1)/lib/firmware/ath11k/IPQ5018/hw1.0/
endef

define Package/ath11k-firmware-ipq5018-qcn6122/install
	$(INSTALL_DIR) $(1)/lib/firmware/ath11k/IPQ5018/hw1.0
	$(INSTALL_DATA) \
		$(BUILD_DIR)/$(ATH11K_LEGACY_FW_SUBDIR)/ath11k-firmware/IPQ5018_QCN6122_QCN6122/hw1.0/2.7.0.1/WLAN.HK.2.7.0.1-01744-QCAHKSWPL_SILICONZ-1/*.* \
		$(1)/lib/firmware/ath11k/IPQ5018/hw1.0/
	$(INSTALL_DIR) $(1)/lib/firmware/ath11k/QCN6122/hw1.0
	$(INSTALL_DATA) \
		$(BUILD_DIR)/$(ATH11K_LEGACY_FW_SUBDIR)/ath11k-firmware/IPQ5018_QCN6122_QCN6122/hw1.0/2.7.0.1/WLAN.HK.2.7.0.1-01744-QCAHKSWPL_SILICONZ-1/qcn6122/*.* \
		$(1)/lib/firmware/ath11k/QCN6122/hw1.0/
endef

define Package/ath11k-firmware-ipq6018/install
	$(INSTALL_DIR) $(1)/lib/firmware/IPQ6018
	$(INSTALL_DATA) \
		$(PKG_BUILD_DIR)/IPQ6018/hw1.0/2.5.0.1/WLAN.HK.2.5.0.1-03982-QCAHKSWPL_SILICONZ-3/* \
		$(1)/lib/firmware/IPQ6018/
endef

define Package/ath11k-firmware-ipq8074/install
	$(INSTALL_DIR) $(1)/lib/firmware/IPQ8074
	$(INSTALL_DATA) \
		$(PKG_BUILD_DIR)/IPQ8074/hw2.0/2.9.0.1/WLAN.HK.2.9.0.1-02146-QCAHKSWPL_SILICONZ-1/* \
		$(1)/lib/firmware/IPQ8074/
endef

define Package/ath11k-firmware-ipq9574/install
	$(INSTALL_DIR) $(1)/lib/firmware/ath11k/IPQ9574/hw1.0
	$(INSTALL_BIN) \
		$(PKG_BUILD_DIR)/IPQ9574/hw1.0/board-2.bin $(1)/lib/firmware/ath11k/IPQ9574/hw1.0/board-2.bin
endef

define Package/ath11k-firmware-qcn9074/install
	$(INSTALL_DIR) $(1)/lib/firmware/ath11k/QCN9074/hw1.0
	$(INSTALL_DATA) \
		$(PKG_BUILD_DIR)/QCN9074/hw1.0/2.9.0.1/WLAN.HK.2.9.0.1-02146-QCAHKSWPL_SILICONZ-1/* \
		$(1)/lib/firmware/ath11k/QCN9074/hw1.0/
	$(INSTALL_BIN) \
		$(PKG_BUILD_DIR)/QCN9074/hw1.0/board-2.bin $(1)/lib/firmware/ath11k/QCN9074/hw1.0/board-2.bin
endef

$(eval $(call BuildPackage,ath11k-firmware-ipq5018))
$(eval $(call BuildPackage,ath11k-firmware-ipq5018-qcn6122))
$(eval $(call BuildPackage,ath11k-firmware-ipq6018))
$(eval $(call BuildPackage,ath11k-firmware-ipq8074))
$(eval $(call BuildPackage,ath11k-firmware-ipq9574))
$(eval $(call BuildPackage,ath11k-firmware-qcn9074))
