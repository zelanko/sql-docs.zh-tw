---
title: "應用裝置網路組態 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e2b9abe-963d-479b-a4a7-1739fcb3e249
caps.latest.revision: "27"
ms.openlocfilehash: e24ed8e992591d08628ffeb14c30a47d7fa5b54a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="appliance-network-configuration"></a>應用裝置網路組態
SQL Server PDW 應用裝置會建立並設定 IP 位址在所有伺服器和從 IHV 工廠，在適用裝置修正組。 一傳遞應用裝置，則必須重新 （乙太網路） 的外部 IP 位址設定為符合特定客戶的資料中心的需求。  
  
> [!NOTE]  
> PDW V1 需要 8 IP 外部 (*客戶對向*) 位址提供給每個控制項的外部連線能力機架的節點。 PDW 2012 (V2) 增強網路通訊，藉由公開從外部透過 IP 位址應用裝置的每個元件。 此方法提供更強固的設計以減少成本，並增加彈性，和可增強資料移動、 載入資料，與 Hadoop 整合。 所需的 IP 位址數目取決於應用裝置中的節點數目和功能，例如 HDInsight 存在。 為了符合這個較大的 IP 位址區塊，客戶應該設定不同的子網路的 PDW。 此子網路中，會有足夠 IP 位址空間 （最多 250 個位址） 可容納多達 5 PDW 機架的元件。  
  
**網路組態**頁面可讓您檢視 Analytics Platform System 應用裝置上的節點對外開放的網路設定。 此頁面是唯讀的。  
  
![DWConfig 應用裝置網路](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>若要更新您的應用裝置上的網路設定  
藉由編輯變更網狀架構網域、 工作負載網域和 HDInsight 網域的 IP 位址**AplianceInfo.xml**檔案，然後執行安裝程式。 這是一種離線作業。 PDW 和 （如果有的話） 的 HDInsight 區域將 IP 位址變更時自動停止。  
  
> [!NOTE]  
> 網域名稱在安裝期間所提供且已指定最多 6 的英數字元、 以字母開頭。 命名系統經常建立網狀架構定義域啟動 F、 P、 從 PDW 工作負載網域與開頭 H.HDInsight 網域此格式會假設整個說明檔主題，但不是必要。 <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>若要變更 Analytics Platform System 的 IP 位址  
  
1.  使用**遠端桌面**應用程式中，連接到**HST01**使用工作負載的網域系統管理員帳戶。  
  
2.  上 HST01 節點中，開啟應用裝置資訊檔案在**c:\pdwinst\media\AplianceInfo.xml**。  
  
    > [!NOTE]  
    > 如果檔案不存在，可能需要建立新的檔案。  
  
3.  乙太網路的 IP 值依需要更新，然後儲存檔案。  
  
4.  在命令提示字元視窗中，執行下列安裝程式命令來更新 IP 位址的 PDW 區域，使用 P/F H 網域名稱和系統管理員密碼。  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>製造商的參考  
如需 Dell 應用裝置的詳細資訊，請參閱：  
  
-   PowerConnect 參數指示[Dell PowerConnect 6200 系列系統 CLI 參考指南](http://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   iDRAC/BMC[整合 Dell 遠端存取控制站 7 (iDRAC7) 版本 1.30.30 使用者手冊](http://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   PDU 的**Dell 計量機架 PDU**`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>請參閱＜  
[啟動組態管理員 &#40;Analytics Platform System &#41;](launch-the-configuration-manager.md)  
  
