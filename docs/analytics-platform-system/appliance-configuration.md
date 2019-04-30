---
title: 組態檢查清單-Analytics Platform System |Microsoft Docs
description: 檢查清單提供為您自己的環境設定 Analytics Platform System 所需的工作。 這些組態工作是必要的才能使用設備。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ada3d2f782a33caf5334361a9682c53cf7cdec95
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63276054"
---
# <a name="appliance-configuration-checklists-for-analytics-platform-system"></a>Analytics Platform System appliance 組態檢查清單
檢查清單提供為您自己的環境設定 Analytics Platform System 所需的工作。 這些組態工作是必要的才能使用設備。  
  
> [!WARNING]  
> 使用 Analytics Platform System**Configuration Manager**是最佳的方式，以及唯一支援的方式，來執行此工具中可用的工作。  
  
## <a name="BeforeTasks"></a>開始之前  
  
### <a name="prerequisites"></a>先決條件  
  
1.  設備必須安裝在資料中心，並開啟電源。  
  
2.  請確定您具有 ihv 提供所提供的下列資訊：  
  
    -   PDW 控制節點的外部 IP 位址 (*PDW_region-* CTL01)  
  
    -   應用裝置的網域名稱  
  
    -   使用者名稱和設備網域系統管理員密碼  
  
3.  取得受信任的憑證。 您將在稍後的步驟，以允許用戶端連線到匯入這**管理主控台**與安全的連線。 將憑證儲存到受密碼保護 PFX 檔案中的 [控制] 節點中。  
  
4.  啟動**Configuration Manager**，使用下列步驟：  
  
    1.  使用**遠端桌面**連接至 PDW 控制節點 (*PDW_region*-CTL01)。 （您可能需要連接的外部 IP 位址，如 CTL01）。  
  
    2.  啟動**Configuration Manager**從**開始**PDW 控制節點的功能表。 Configuration Manager 中的第一個畫面會顯示應用裝置拓撲中，由 ihv 提供所建立。 它是由您的 SQL Server PDW 軟體視為屬於您的應用裝置的硬體節點的清單。 此外，您應該不需要變更任何應用裝置拓撲螢幕上的設定。  
  
## <a name="CMTasks"></a>執行 Configuration Manager 工作  
SQL Server PDW**Configuration Manager** (PDWCM) 是 SQL Server PDW 系統管理員使用來執行應用裝置層級的作業，以及變更設備層級設定為設備系統管理工具。 例如，使用 PDWCM 重設密碼、 設定時區、 變更 IP 位址、 設定 SSL 憑證，啟用通過防火牆的遠端存取、 啟動或停止應用裝置，以及設定立即檔案初始化。  
  
使用**Configuration Manager**進行下列設定工作。  
  
|組態工作|描述|  
|----------------------|---------------|  
|熟悉的實體元件名稱|[PDW 與設備的網狀架構實體元件&#40;Analytics Platform System&#41;](pdw-and-appliance-fabric-physical-components.md)|  
|啟動 SQL Server PDW 組態管理員|[啟動組態管理員 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)|  
|變更網域系統管理員密碼|應用裝置有私人 Windows Active Directory 網域服務用來驗證應用裝置內的節點。<br /><br />Ihv 提供設定的預設網域系統管理員密碼與設備。 這必須是安全的密碼變更。<br /><br />**Configuration Manager**唯一支援的方法變更網域系統管理員密碼。<br /><br />如需詳細資訊，請參閱 <<c0> [ 密碼重設&#40;Analytics Platform System&#41;](password-reset.md)。</c0>|  
|變更的密碼**sa**登入|SQL Server PDW 具有名為系統管理員身份登入**sa**。 **Sa**登入擁有所有權限。 它可以授與、 拒絕或撤銷任何權限。 它也可以查看所有的系統檢視表。<br /><br />如需詳細資訊，請參閱 <<c0> [ 密碼重設&#40;Analytics Platform System&#41;](password-reset.md)。</c0>|  
|設定設備時區|設定所有的應用裝置節點的時間 （本機或其他所需的時間）。<br /><br />如需詳細資訊，請參閱 <<c0> [ 設備時區設定&#40;Analytics Platform System&#41;](appliance-time-zone-configuration.md)。</c0>|  
|指定 SQL Server PDW 應用裝置對外開放的網路設定|[設備網路設定&#40;Analytics Platform System&#41;](appliance-network-configuration.md)|  
|安全性憑證匯入系統管理員主控台|憑證可以透過 HTTPS 來提供安全通訊端層 (SSL) 連線[使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。 根據預設，**管理主控台**包含自我簽署的憑證所提供的隱私權，但不是伺服器驗證。 此憑證也會傳回錯誤，指出 Internet Explorer:「 有 」 這個網站的安全性憑證有問題的使用者的連線時。 雖然此連線進行加密進行中的資料，用戶端與伺服器之間，連線就是仍然有來自攻擊者的風險。<br /><br />SQL Server PDW 系統管理員，應立即取得憑證鏈結至信任的憑證授權單位辨識用戶端，才能有安全的連線，並移除 Internet Explorer 會報告錯誤。 這需要對應 [控制] 節點的虛擬 IP 位址 （建議選項） 的完整的網域名稱，或憑證名稱符合使用者輸入其瀏覽器的位址值軸存取管理主控台。<br /><br />使用**Configuration Manager**新增或移除受信任的憑證。 直接使用 Microsoft Windows HTTP 服務的憑證組態工具 (`winHttpCertCfg.exe`) 來管理憑證不受支援。<br /><br />如需詳細資訊，請參閱 <<c0> [ 佈建 PDW 憑證&#40;Analytics Platform System&#41;](pdw-certificate-provisioning.md)。</c0>|
|功能參數|會顯示相關分析平台系統 AU7 中引進的功能參數的資訊。 使用此頁面來更新或啟用/停用功能和 Analytics Platform System 中的設定。 功能參數值的變更需要重新啟動服務。<br /><br />如需詳細資訊，請參閱 < [PDW 功能參數&#40;Analytics Platform System&#41;](appliance-feature-switch.md)。|
|啟用或停用 Windows 防火牆規則來允許或防止在 SQL Server PDW 應用裝置上的特定連接埠存取。|Ihv 提供將設定和啟用防火牆規則所需的設備，以正常運作。 在大部分情況下將不會啟用或停用防火牆規則。<br /><br />如需詳細資訊，請參閱 < [PDW 防火牆設定&#40;Analytics Platform System&#41;](pdw-firewall-configuration.md)。|  
|啟動及停止 SQL Server PDW 應用裝置|停止或啟動 SQL Server PDW 應用裝置。 如需詳細資訊，請參閱 < [PDW 服務狀態&#40;Analytics Platform System&#41;](pdw-services-status.md)。|  
|使用檢閱檔案立即初始化選項**權限**對話方塊|立即檔案初始化是 SQL Server 功能，可讓資料更快速執行的檔案作業。 只有在網路服務帳戶授與 SE_MANAGE_VOLUME_NAME 特殊權限，它會啟用 SQL Server PDW 上。 根據預設，它被已關閉。<br /><br />如需詳細資訊，請參閱 <<c0> [ 立即檔案初始化設定&#40;Analytics Platform System&#41;](instant-file-initialization-configuration.md)。</c0>|  
|從備份還原 master 資料庫|刪除目前**主要**資料庫，並以備份取代。 如需詳細資訊，請參閱 <<c0> [ 還原 Master 資料庫&#40;Analytics Platform System&#41;](restore-the-master-database.md)。</c0>|  
  
## <a name="AddTasks"></a>執行其他設定工作  
在執行之後**Configuration Manager**工作，執行下列其他設定工作的清單。 其中有些工作是選擇性的。  
  
|組態工作|描述|  
|----------------------|---------------|  
|協力廠商防毒軟體可以安裝並設定 SQL Server PDW 應用裝置的面向外部的節點上。<br /><br />(選擇性)|如需詳細資訊，請參閱 <<c0> [ 防毒軟體&#40;Analytics Platform System&#41;](antivirus-software.md)。</c0>|  
|可以變更 DSRM 密碼。<br /><br />(選擇性)|如需詳細資訊，請參閱 <<c0> [ 設定登入目錄服務還原模式中的 AD 節點的系統管理員密碼&#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)。</c0>|  
|設定要接收軟體更新設備<br /><br />(建議使用)|應用裝置必須設定為接收 SQL Server PDW 和基礎的軟體更新。<br /><br />如需詳細資訊，請參閱 <<c0> [ 設定 Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md)。</c0> 如需 WSUS 的相關資訊，請參閱 <<c0> [ 軟體服務&#40;Analytics Platform System&#41;](software-servicing.md)。</c0>|  
|設定外部資料，例如 Hadoop 或 Azure blob 儲存體的連線。<br /><br />(選擇性)|如需詳細資訊，請參閱 <<c0> [ 設定外部資料的 PolyBase 連線&#40;Analytics Platform System&#41;](configure-polybase-connectivity-to-external-data.md)。</c0>|  
|設定防毒軟體<br /><br />(選擇性)|協力廠商防毒解決方案可用來保護對外公開的節點，但並非必要。 請依照下列中的指導方針。|  
|設定備份和載入伺服器上的 InfiniBand 網路介面卡<br /><br />(選擇性)|若要設定備份並載入伺服器連接至 SQL Server PDW 使用 InfiniBand 網路，您需要設定網路介面卡，以允許應用裝置 DNS 來解析 InfiniBand 連線至的目前作用中的 InfiniBand 網路。|  
|設定將遙測資料傳送給 Microsoft<br /><br />(選擇性)|若要設定將遙測資料傳送到 Microsoft Analytics Platform System，您需要在控制節點上執行 PowerShell 指令碼。 特定的指示，請參閱[傳送遙測意見反應給 Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)。|  
  
## <a name="see-also"></a>另請參閱  
[防毒軟體&#40;Analytics Platform System&#41;](antivirus-software.md)  
[InfiniBand 網路介面卡設定&#40;SQL Server PDW&#41;](configure-infiniband-network-adapters.md)  
  
