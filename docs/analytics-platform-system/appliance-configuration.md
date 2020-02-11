---
title: 設定檢查清單
description: 針對您自己的環境設定分析平臺系統所需的工作，提供檢查清單。 您必須先進行這些設定工作，才能使用設備。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 80fc899400be167badaae9d617d43a61e0d346b5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401458"
---
# <a name="appliance-configuration-checklists-for-analytics-platform-system"></a>分析平臺系統的設備設定檢查清單
針對您自己的環境設定分析平臺系統所需的工作，提供檢查清單。 您必須先進行這些設定工作，才能使用設備。  
  
> [!WARNING]  
> 流量分析平臺系統**Configuration Manager**是執行工具中所提供工作的最佳方式，以及唯一支援的方法。  
  
## <a name="BeforeTasks"></a>開始之前  
  
### <a name="prerequisites"></a>Prerequisites  
  
1.  設備必須安裝在資料中心並開啟電源。  
  
2.  請確定您具有下列資訊（由您的 IHV 提供）：  
  
    -   PDW 控制節點的外部 IP 位址（*PDW_region*CTL01）  
  
    -   設備功能變數名稱  
  
    -   設備網域系統管理員的使用者名稱和密碼  
  
3.  取得受信任的憑證。 您會在稍後的步驟中匯入此功能，以允許用戶端使用安全連線連接到**管理主控台**。 將憑證儲存至受密碼保護的 PFX 檔案中的控制節點。  
  
4.  使用下列步驟啟動**Configuration Manager**：  
  
    1.  使用 [**遠端桌面**] 連接至 PDW 控制節點（*PDW_region*CTL01）。 （您可能需要與 CTL01 的外部 IP 位址連線。）  
  
    2.  從 [PDW 控制項] 節點的 [**開始**] 功能表啟動**Configuration Manager** 。 Configuration Manager 的第一個畫面會顯示您的 IHV 所建立的設備拓朴。 這是您的 SQL Server PDW 軟體所識別的硬體節點清單，屬於您的設備。 您應該不需要變更 [設備拓朴] 畫面上的任何設定。  
  
## <a name="CMTasks"></a>執行 Configuration Manager 工作  
SQL Server PDW**Configuration Manager** （PDWCM）是一種裝置管理工具，SQL Server PDW 系統管理員用來執行設備層級的作業，以及變更設備層級的設定。 例如，使用 PDWCM 來重設密碼、設定時區、變更 IP 位址、設定 SSL 憑證、啟用透過防火牆的遠端存取、啟動或停止設備，以及設定立即檔案初始化。  
  
使用**Configuration Manager**執行下列設定工作。  
  
|組態工作|描述|  
|----------------------|---------------|  
|熟悉實體元件名稱|[PDW 和設備網狀架構實體元件 &#40;分析平臺系統&#41;](pdw-and-appliance-fabric-physical-components.md)|  
|啟動 SQL Server PDW Configuration Manager|[啟動 Configuration Manager &#40;分析平臺系統&#41;](launch-the-configuration-manager.md)|  
|變更網域系統管理員密碼|設備具有私用 Windows Active Directory Domain Services，可用來驗證設備中的節點。<br /><br />您的 IHV 會使用預設網域系統管理員密碼來設定設備。 這需要變更為安全的密碼。<br /><br />**Configuration Manager**是變更網域系統管理員密碼的唯一支援方式。<br /><br />如需詳細資訊，請參閱[密碼重設 &#40;分析平臺系統&#41;](password-reset.md)。|  
|變更**sa**登入的密碼|SQL Server PDW 具有名為**sa**的系統管理員登入。 **Sa**登入具有擁有權限。 它可以授與、拒絕或撤銷任何許可權。 它也可以查看所有系統檢視。<br /><br />如需詳細資訊，請參閱[密碼重設 &#40;分析平臺系統&#41;](password-reset.md)。|  
|設定設備時區|設定所有設備節點的時間（本機或其他所需時間）。<br /><br />如需詳細資訊，請參閱[&#41;的設備時區設定 &#40;分析平臺系統](appliance-time-zone-configuration.md)。|  
|指定 SQL Server PDW 設備的外部面向網路設定|[&#40;分析平臺系統&#41;的設備網路設定](appliance-network-configuration.md)|  
|匯入管理主控台的安全性憑證|憑證可以[使用管理主控台 &#40;分析平臺系統&#41;](monitor-the-appliance-by-using-the-admin-console.md)，提供透過 HTTPS 到監視設備的安全通訊端層（SSL）連線。 根據預設，**管理主控台**會包含提供隱私權的自我簽署憑證，但不包括伺服器驗證。 此憑證也會在 Internet Explorer 中傳回錯誤，指出：「此網站的安全性憑證有問題」（當使用者連接時）。 雖然此連接會加密用戶端與伺服器之間的傳輸中資料，但連線仍然會有攻擊者的風險。<br /><br />SQL Server PDW 系統管理員應該立即取得憑證，以連結至用戶端所識別的受信任憑證授權單位單位，以便擁有安全連線並移除 Internet Explorer 報告的錯誤。 這需要對應控制節點之虛擬 IP 位址（建議）的完整功能變數名稱，或符合使用者在其瀏覽器位址列中所輸入之值的憑證名稱，才能存取管理主控台。<br /><br />使用**Configuration Manager**來新增或移除受信任的憑證。 不支援直接使用 Microsoft Windows HTTP Services 憑證設定工具`winHttpCertCfg.exe`（）來管理憑證。<br /><br />如需詳細資訊，請參閱[PDW 憑證提供 &#40;分析平臺系統&#41;](pdw-certificate-provisioning.md)。|
|功能切換|顯示分析平臺系統 AU7 中引進之功能參數的相關資訊。 使用此頁面來更新或啟用/停用分析平臺系統中的功能和設定。 變更功能切換值需要重新開機服務。<br /><br />如需詳細資訊，請參閱[PDW 功能切換 &#40;分析平臺系統&#41;](appliance-feature-switch.md)。|
|啟用或停用 Windows 防火牆規則，以允許或防止存取 SQL Server PDW 應用裝置上的特定埠。|您的 IHV 會設定並啟用應用程式正常運作所需的防火牆規則。 在大部分情況下，您不會啟用或停用防火牆規則。<br /><br />如需詳細資訊，請參閱[PDW 防火牆設定 &#40;分析平臺系統&#41;](pdw-firewall-configuration.md)。|  
|啟動和停止 SQL Server PDW 設備|停止或啟動 SQL Server PDW 設備。 如需詳細資訊，請參閱[PDW 服務狀態 &#40;分析平臺系統&#41;](pdw-services-status.md)。|  
|使用 [**許可權**] 對話方塊來審查立即檔案初始化選項|立即檔案初始化是一項 SQL Server 功能，可讓資料檔案作業更快速地執行。 只有在已將 SE_MANAGE_VOLUME_NAME 許可權授與網路服務帳戶時，才會在 SQL Server PDW 上啟用此功能。 根據預設，它是關閉的。<br /><br />如需詳細資訊，請參閱[立即檔案初始化設定 &#40;分析平臺系統&#41;](instant-file-initialization-configuration.md)。|  
|從備份還原 master 資料庫|刪除目前的**master**資料庫，並將它取代為備份。 如需詳細資訊，請參閱[將 Master 資料庫 &#40;分析平臺系統還原&#41;](restore-the-master-database.md)。|  
  
## <a name="AddTasks"></a>執行其他設定工作  
執行**Configuration Manager**工作之後，請執行下列其他設定工作清單。 其中某些工作是選擇性的。  
  
|組態工作|描述|  
|----------------------|---------------|  
|協力廠商防毒軟體可以在 SQL Server PDW 設備上針對外部面向節點進行安裝和設定。<br /><br />(選用)|如需詳細資訊，請參閱[防毒軟體 &#40;分析平臺系統&#41;](antivirus-software.md)。|  
|DSRM 的密碼可以變更。<br /><br />(選用)|如需詳細資訊，請參閱[在目錄服務還原模式中設定用來登入 AD 節點的管理員密碼 &#40;DSRM&#41; &#40;分析平臺系統&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)。|  
|設定設備以接收軟體更新<br /><br />(建議使用)|設備必須設定為接收 SQL Server PDW 和基礎軟體的更新。<br /><br />如需詳細資訊，請參閱[&#40;WSUS&#41; &#40;分析平臺系統&#41;設定 Windows Server Update Services ](configure-windows-server-update-services-wsus.md)。 如需 WSUS 的相關資訊，請參閱[軟體服務 &#40;分析平臺系統&#41;](software-servicing.md)。|  
|設定對外部資料（例如 Hadoop 或 Azure blob 儲存體）的連線能力。<br /><br />(選用)|如需詳細資訊，請參閱[設定 PolyBase 與外部資料的連線 &#40;分析平臺系統&#41;](configure-polybase-connectivity-to-external-data.md)。|  
|設定防毒軟體<br /><br />(選用)|協力廠商防毒軟體可以用來保護外部對向節點，但不是必要的。 遵循中的指導方針。|  
|在備份和載入伺服器上設定不會的網路介面卡<br /><br />(選用)|若要設定備份和載入伺服器，以使用不受的網路連線到 SQL Server PDW，您需要設定網路介面卡，讓設備 DNS 能夠將無法使用的連線解析成目前作用中的「未受處理」網路。|  
|設定以將遙測資料傳送給 Microsoft<br /><br />(選用)|若要設定分析平臺系統將遙測資料傳送給 Microsoft，您需要在控制節點上執行 PowerShell 腳本。 如需特定指示，請參閱[將遙測意見反應傳送給 Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)。|  
  
## <a name="see-also"></a>另請參閱  
[防毒軟體 &#40;分析平臺系統&#41;](antivirus-software.md)  
[設定不會 &#40;SQL Server PDW 的網路介面卡&#41;](configure-infiniband-network-adapters.md)  
  
