---
title: 設備網路設定 Analytics Platform System |Microsoft Docs
description: Analytics Platform System (APS) 設備是內建，而且修正一份在所有伺服器和 IHV 的工廠適用於裝置的 IP 位址設定。 設備的傳遞，就必須重新設定外部 （乙太網路） IP 位址以符合特定的客戶資料中心的需求。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 341db2791f99d72d293fe00dbf92c1f59df444ca
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51697916"
---
# <a name="appliance-network-configuration-for-analytics-platform-system"></a>Analytics Platform System 的設備網路設定
Analytics Platform System (APS) 設備是內建，而且修正一份在所有伺服器和 IHV 的工廠適用於裝置的 IP 位址設定。 設備的傳遞，就必須重新設定外部 （乙太網路） IP 位址以符合特定的客戶資料中心的需求。  
  
> [!NOTE]  
> PDW V1 需要 8 IP 外部 (*客戶面向*) 位址，以提供每個控制項的外部連線能力機架的節點。 PDW 2012 (V2) 增強網路通訊，藉由公開透過 IP 位址從外部應用裝置的每個元件。 此方法提供更強大的設計可以降低成本、 增加彈性，以及可增強資料移動、 載入資料，與 Hadoop 整合。 所需的 IP 位址數目取決於設備中的節點數目。 為了符合這個較大的 IP 位址區塊，客戶應該設定不同的子網路，適用於 PDW。 在這個子網路中，會有足夠 IP 位址空間 （最多 250 個位址） 可容納最多 5 個 PDW 機架的元件。  
  
**網路組態**頁面可讓您檢視 Analytics Platform System appliance 對外公開的網路設定的節點。 此頁面會處於唯讀狀態。  
  
![DWConfig 應用裝置網路](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>若要更新您的應用裝置上的網路設定  
變更的網狀架構網域和工作負載網域的 IP 位址，藉由編輯**AplianceInfo.xml**檔案，然後執行 安裝程式。 這是一種離線作業。 PDW 區域將 IP 位址變更期間會自動停止。  
  
> [!NOTE]  
> 網域名稱會提供在安裝期間，並指定最多 6 個的英數字元、 以字母開頭。 命名系統經常會建立網狀架構網域開始使用 f #，開頭為 p 的 PDW 工作負載網域此格式會假設整個說明檔主題，但並非必要。 <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>若要變更分析平台系統的 IP 位址  
  
1.  使用**遠端桌面**應用程式中，連接到**HST01**使用工作負載的網域系統管理員帳戶。  
  
2.  HST01 在節點上，開啟應用裝置資訊檔案，在**c:\pdwinst\media\AplianceInfo.xml**。  
  
    > [!NOTE]  
    > 如果檔案不存在，可能需要建立新的檔案。  
  
3.  視需要更新的乙太網路的 IP 值並儲存檔案。  
  
4.  在命令提示字元視窗中，執行下列安裝命令來更新 IP 位址的 PDW 區域中，使用 P/F/H 網域名稱和系統管理員密碼。  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>製造商的參考  
如需 Dell 應用裝置的詳細資訊，請參閱：  
  
-   PowerConnect 參數指示[Dell PowerConnect 6200 系列系統 CLI 參考指南](https://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   iDRAC/BMC[整合 Dell 遠端存取控制器 7 (iDRAC7) 版本 1.30.30 使用者指南](https://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   PDU 的**Dell 計量 Rack PDU**`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>另請參閱  
[啟動組態管理員 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
