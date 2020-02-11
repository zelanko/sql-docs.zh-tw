---
title: 設備網路設定
description: 分析平臺系統（AP）應用裝置已建立並設定為所有伺服器中的一組修正 IP 位址，以及來自 IHV 工廠的適用裝置。 當設備傳遞時，必須重新設定外部（乙太網路） IP 位址，以符合特定客戶的資料中心需求。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: af892cbb43b42953732bda59d371e3e22855413b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401415"
---
# <a name="appliance-network-configuration-for-analytics-platform-system"></a>Analytics Platform System 的設備網路設定
分析平臺系統（AP）應用裝置已建立並設定為所有伺服器中的一組修正 IP 位址，以及來自 IHV 工廠的適用裝置。 當設備傳遞時，必須重新設定外部（乙太網路） IP 位址，以符合特定客戶的資料中心需求。  
  
> [!NOTE]  
> PDW V1 需要8個 IP 外部（*客戶面向*）位址，以提供對每個控制機架節點的外部連線能力。 PDW 2012 （V2）藉由透過 IP 位址從外部公開設備的每個元件，來增強網路通訊。 這種方法提供更健全的設計，可降低成本並增加彈性，並增強資料移動、資料載入和 Hadoop 整合。 所需的 IP 位址數目取決於設備中的節點數目。 為了容納這個較大的 IP 位址區塊，客戶應該為 PDW 設定個別的子網。 在此子網中，將會有足夠的 IP 位址空間（最多250個位址），以容納最多5個 PDW 機架的元件。  
  
[**網路**設定] 頁面可讓您針對分析平臺系統裝置上的節點，查看對外的網路設定。 此頁面是唯讀的。  
  
![DWConfig 應用裝置網路](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>更新設備上的網路設定  
藉由編輯**AplianceInfo** ，然後執行安裝程式，來變更網狀架構網域和工作負載網域的 IP 位址。 這是一種離線作業。 在 IP 位址變更期間，將會自動停止 PDW 區域。  
  
> [!NOTE]  
> 系統會在安裝期間提供功能變數名稱，並指定最多6個英數位元（以字母開頭）。 常見的命名系統會建立從 F 開始的網狀架構網域，這是以 P 開頭的 PDW 工作負載網域。這種格式在說明檔主題中是假設的，但並非必要。 <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>變更分析平臺系統的 IP 位址  
  
1.  使用**遠端桌面**應用程式，使用工作負載網域系統管理員帳戶連線到**HST01** 。  
  
2.  在 [HST01] 節點上，開啟位於**c:\pdwinst\media\AplianceInfo.xml**的設備資訊檔案。  
  
    > [!NOTE]  
    > 如果檔案不存在，則可能需要建立新的檔案。  
  
3.  視需要更新乙太網路 IP 值，然後儲存檔案。  
  
4.  在 [命令提示字元] 視窗中，使用 P/F/H 功能變數名稱和系統管理員密碼，執行下列安裝程式命令來更新 PDW 區域的 IP 位址。  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>製造商參考  
如需有關 Dell 設備的詳細資訊，請參閱：  
  
-   PowerConnect 交換器指示[Dell PowerConnect 6200 系列系統 CLI 參考指南](https://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   iDRAC/BMC[整合的 Dell 遠端存取控制器7（iDRAC7）版本1.30.30 使用者指南](https://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   PDU 的**Dell 計量付費機架 PDU**`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>另請參閱  
[啟動 Configuration Manager &#40;分析平臺系統&#41;](launch-the-configuration-manager.md)  
  
