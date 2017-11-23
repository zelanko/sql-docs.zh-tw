---
title: "應用裝置設定 (Analytics Platform System)"
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
ms.assetid: 064e7485-7026-4acf-8084-f5d30757d177
caps.latest.revision: "43"
ms.openlocfilehash: ebb797e3fdb24bad79857f83c163dbf92a439883
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="appliance-configuration"></a>應用裝置組態
檢查清單提供您自己的環境設定 Analytics Platform System 所需的工作。 您可以使用此應用裝置之前，會需要這些組態工作。  
  
> [!WARNING]  
> 使用 Analytics Platform System**Configuration Manager**最佳的方式，而唯一支援的方法，來執行此工具中可用的工作。  
  
## <a name="BeforeTasks"></a>開始之前  
  
### <a name="prerequisites"></a>必要條件  
  
1.  應用裝置必須安裝在資料中心和電源已開啟。  
  
2.  請確定您已由您 IHV 提供下列資訊：  
  
    -   PDW 控制節點的外部 IP 位址 (*PDW_region-*CTL01)  
  
    -   應用裝置的網域名稱  
  
    -   使用者名稱和應用裝置的網域系統管理員密碼  
  
3.  取得受信任的憑證。 您將在稍後的步驟，以允許用戶端連線到匯入這個**管理主控台**與安全的連線。 將憑證儲存到受密碼保護 PFX 檔案中的控制節點。  
  
4.  啟動**Configuration Manager**，使用下列步驟：  
  
    1.  使用**遠端桌面**連接至 PDW 控制節點 (*PDW_region*-CTL01)。 （您可能需要連接的外部 IP 位址與 CTL01）。  
  
    2.  啟動**Configuration Manager**從**啟動**功能表 PDW 控制節點。 Configuration Manager 中的第一個畫面會顯示應用裝置拓撲，您 IHV 所建立。 它是由 SQL Server PDW 軟體辨識為屬於您的應用裝置的硬體節點的清單。 您應該不需要變更任何應用裝置拓撲螢幕上的設定。  
  
## <a name="CMTasks"></a>執行 Configuration Manager 工作  
SQL Server PDW**Configuration Manager** (PDWCM) 是 SQL Server PDW 系統管理員使用可執行應用裝置層級作業，而且變更應用裝置層級設定為設備系統管理工具。 例如，使用 PDWCM 重設密碼，請設定時區、 變更 IP 位址，設定 SSL 憑證，啟用通過防火牆的遠端存取、 啟動或停止應用裝置，並設定立即檔案初始化。  
  
使用**Configuration Manager**執行下列設定工作。  
  
|組態工作|Description|  
|----------------------|---------------|  
|熟悉實體元件名稱|[PDW 和應用裝置網狀架構的實體元件 &#40;Analytics Platform System &#41;](pdw-and-appliance-fabric-physical-components.md)|  
|啟動 SQL Server PDW 組態管理員|[啟動組態管理員 &#40;Analytics Platform System &#41;](launch-the-configuration-manager.md)|  
|變更網域系統管理員密碼|應用裝置有私用 Windows Active Directory 網域服務用來驗證應用裝置內的節點。<br /><br />您 IHV 設定與預設網域系統管理員密碼應用裝置。 這必須是安全的密碼變更。<br /><br />**Configuration Manager**唯一支援的方式來變更網域系統管理員密碼。<br /><br />如需詳細資訊，請參閱[密碼重設 &#40;Analytics Platform System &#41;](password-reset.md).|  
|變更密碼**sa**登入|SQL Server PDW 具有系統管理員登入名為**sa**。 **Sa**登入擁有的所有權限。 它可以授與、 拒絕或撤銷權限。 它也可以查看所有的系統檢視表。<br /><br />如需詳細資訊，請參閱[密碼重設 &#40;Analytics Platform System &#41;](password-reset.md).|  
|設定應用裝置時區|設定所有的應用裝置節點的時間 （本機或其他所需時間）。<br /><br />如需詳細資訊，請參閱[應用裝置的時區組態 &#40;Analytics Platform System &#41;](appliance-time-zone-configuration.md).|  
|指定 SQL Server PDW 應用裝置的對外網路設定|[應用裝置網路組態 &#40;Analytics Platform System &#41;](appliance-network-configuration.md)|  
|匯入的安全性憑證管理主控台|憑證可以透過 HTTPS 來提供安全通訊端層 (SSL) 連線[使用系統管理員主控台 &#40; 監視的應用裝置Analytics Platform System &#41;](monitor-the-appliance-by-using-the-admin-console.md). 根據預設，**管理主控台**包含自我簽署的憑證所提供的隱私權，但不是伺服器驗證。 此憑證也會傳回錯誤，指出 Internet Explorer: 「 有 」 這個網站的安全性憑證有問題時在使用者連接。 雖然此連線進行加密用戶端與伺服器之間傳遞資料，連線仍然是遭受攻擊的風險。<br /><br />SQL Server PDW 系統管理員應該立即取得憑證，以辨識用戶端，才能有安全的連線，並移除 Internet Explorer 會報告此錯誤的受信任的憑證授權單位鏈結。 這需要對應的控制節點的虛擬 IP 位址 （建議選項） 的完整的網域名稱或使用者輸入其瀏覽器位址的值相符的憑證名稱列來存取管理主控台。<br /><br />使用**Configuration Manager**新增或移除受信任的憑證。 直接使用 Microsoft Windows HTTP 服務的憑證組態工具 (`winHttpCertCfg.exe`) 管理的憑證不受支援。<br /><br />如需詳細資訊，請參閱[PDW 憑證佈建 &#40;Analytics Platform System &#41;](pdw-certificate-provisioning.md).|  
|啟用或停用 Windows 防火牆規則來允許或防止存取 SQL Server PDW 應用裝置上的特定連接埠。|您 IHV 會設定，並啟用防火牆規則所需的設備，才能正確運作。 在大部分情況下將不會啟用或停用防火牆規則。<br /><br />如需詳細資訊，請參閱[PDW 防火牆組態 &#40;Analytics Platform System &#41;](pdw-firewall-configuration.md).|  
|啟動及停止 SQL Server PDW 應用裝置|停止或啟動 SQL Server PDW 應用裝置。 如需詳細資訊，請參閱[PDW 服務狀態 &#40;Analytics Platform System &#41;](pdw-services-status.md).|  
|檢閱使用立即檔案初始化選項**權限**對話方塊|立即檔案初始化是 SQL Server 功能，可讓資料檔案作業更快速地執行。 只有當網路服務帳戶授與 SE_MANAGE_VOLUME_NAME 特殊權限，它會啟用 SQL Server PDW 上。 它是預設關閉。<br /><br />如需詳細資訊，請參閱[立即檔案初始化組態 &#40;Analytics Platform System &#41;](instant-file-initialization-configuration.md).|  
|從備份還原 master 資料庫|刪除目前**主要**資料庫，並以備份取代。 如需詳細資訊，請參閱[還原 Master 資料庫 &#40;Analytics Platform System &#41;](restore-the-master-database.md).|  
  
## <a name="AddTasks"></a>執行其他設定工作  
在執行之後**Configuration Manager**工作，執行下列其他設定工作的清單。 其中有些工作是選擇性的。  
  
|組態工作|Description|  
|----------------------|---------------|  
|協力廠商防毒軟體可以安裝並設定 SQL Server PDW 應用裝置的對外公開的節點上。<br /><br />(選擇性)|如需詳細資訊，請參閱[防毒軟體 &#40;Analytics Platform System &#41;](antivirus-software.md).|  
|可以變更的 DSRM 密碼。<br /><br />(選擇性)|如需詳細資訊，請參閱[設定登入目錄服務還原模式 &#40; DSRM &#41; &#40; AD 節點的系統管理員密碼Analytics Platform System &#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md).|  
|設定應用裝置，以接收軟體更新<br /><br />(建議使用)|應用裝置必須設定為接收到的 SQL Server PDW 和基礎的軟體更新。<br /><br />如需詳細資訊，請參閱[設定 Windows Server Update Services &#40;WSUS &#41;&#40;Analytics Platform System &#41;](configure-windows-server-update-services-wsus.md). 如需 WSUS 的相關資訊，請參閱[軟體服務 &#40;Analytics Platform System &#41;](software-servicing.md).|  
|設定外部資料，例如 Hadoop 或 Azure blob 儲存體的連線。<br /><br />(選擇性)|如需詳細資訊，請參閱[設定 PolyBase 連線到外部資料 &#40;Analytics Platform System &#41;](configure-polybase-connectivity-to-external-data.md).|  
|設定防毒軟體<br /><br />(選擇性)|協力廠商防毒解決方案可以用來保護對外開放的節點，但是不需要。 請依照下列中的指導方針。|  
|備份及載入伺服器上設定 InfiniBand 網路介面卡<br /><br />(選擇性)|若要設定備份並載入伺服器連接到 SQL Server PDW 使用 InfiniBand 網路，您需要設定以允許 DNS 來解析 InfiniBand 連接到目前作用中的 InfiniBand 網路應用裝置的網路介面卡。|  
|設定將遙測資料傳送給 Microsoft<br /><br />(選擇性)|若要設定將遙測資料傳送到 Microsoft Analytics Platform System，您需要的控制節點上執行 PowerShell 指令碼。 如需特定指示，請參閱[傳送遙測意見反應給 Microsoft &#40;SQL Server PDW &#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md).|  
  
## <a name="see-also"></a>請參閱＜  
[防毒軟體 &#40;Analytics Platform System &#41;](antivirus-software.md)  
[設定 InfiniBand 網路介面卡 &#40;SQL Server PDW &#41;](configure-infiniband-network-adapters.md)  
  
