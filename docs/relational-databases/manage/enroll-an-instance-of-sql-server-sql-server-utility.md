---
title: 註冊 SQL Server 的執行個體 (SQL Server 公用程式) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.SWB.makemanaged.agentaccount.F1
- sql13.SWB.makemanaged.welcome.F1
- sql13.SWB.makemanaged.enrolling.F1
- sql13.SWB.makemanaged.instancename.F1
- sql13.SWB.makemanaged.Summary.F1
- sql13.SWB.makemanaged.progress.F1
- sql13.SWB.makemanaged.validation.F1
helpviewer_keywords:
- Enroll instance
ms.assetid: a801c619-611b-4e82-a8d8-d1e01691b7a1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ff7bffcb3a31a697300d98e0de03a7f3e3111701
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51681336"
---
# <a name="enroll-an-instance-of-sql-server-sql-server-utility"></a>註冊 SQL Server 的執行個體 (SQL Server 公用程式)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體註冊到現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內，當做 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Managed 執行個體來監視它的效能和組態。 公用程式控制點 (UCP) 每隔 15 分鐘就會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Managed 執行個體收集組態和效能資訊。 這項資訊會儲存在 UCP 的公用程式管理資料倉儲 (UMDW) 中，而 UMDW 檔案名稱為 sysutility_mdw。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 效能資料會與原則相比較，有助於識別資源使用瓶頸及合併機會。  
  
 在這一版中，UCP 及所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體都必須滿足以下需求：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須是 10.50 或更高的版本。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體類型必須是 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式必須在單一 Windows 網域或具有雙向信任關係的網域上運作。  
  
-   UCP 上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶及 SQL Server 的所有受管理的執行個體都必須具有 Active Directory 使用者的讀取權限。  
  
-   要註冊的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體不可以是 SQL Azure。  
  
 在此版本中，UCP 必須滿足下列需求：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體必須是受支援的版本。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
-   我們建議您使用區分大小寫的 SQL Server 執行個體來主控 UCP。  
  
-   請考慮在 UCP 電腦上採用下列容量規劃建議：  
  
    -   在一般的案例中，UCP 上的 UMDW 資料庫 (sysutility_mdw) 所使用的磁碟空間大約是每年每個 SQL Server 受管理的執行個體 2 GB。 這個估計會根據受管理的執行個體所收集的資料庫和系統物件數目而有所不同。 UMDW (sysutility_mdw) 磁碟空間成長率在頭兩天最高。  
  
    -   在一般的案例中，UCP 上的 msdb 所使用的磁碟空間大約是每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]受管理的執行個體 20 MB。 請注意，這個估計會根據資源使用量原則以及受管理的執行個體所收集的資料庫和系統物件數目而有所不同。 一般來說，當原則違規數目增加，以及動態資源的移動時間間隔增加時，磁碟空間使用量也會增加。  
  
    -   請注意，要等到受管理的執行個體的資料保留期限過期之後，從 UCP 移除受管理的執行個體才會減少 UCP 資料庫所使用的磁碟空間。  
  
 在這一版中，SQL Server 的所有受管理的執行個體都必須滿足以下需求：  
  
-   我們建議如果使用不區分大小寫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體來主控 UCP，則 SQL Server 的受管理的執行個體也應該不區分大小寫。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式監視不支援 FILESTREAM 資料。  
  
 如需詳細資訊，請參閱 [SQL Server 的最大容量規格](../../sql-server/maximum-capacity-specifications-for-sql-server.md) 和 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式概念的詳細資訊，請參閱 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組與非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組會一起受到支援。 也就是說，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Managed 執行個體為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式的成員時，可以受到其他收集組的監視。 但是請注意，受管理的執行個體上的所有收集組都會將其資料上傳到公用程式的管理資料倉儲。 如需詳細資訊，請參閱[在相同 SQL Server 執行個體上執行公用程式和非公用程式收集組的考量事項](../../relational-databases/manage/run-utility-and-non-utility-collection-sets-on-same-sql-instance.md)和[設定公用程式控制點資料倉儲 &#40;SQL Server 公用程式&#41;](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md)。  
  
## <a name="wizard-steps"></a>精靈步驟  
 下列章節提供有關精靈工作流程中每一頁的詳細資訊。 按一下連結，可導覽到精靈中頁面的詳細資料。 如需這項作業之 PowerShell 指令碼的詳細資訊，請參閱 PowerShell 的 [範例](#PowerShell_enroll)。  
  
-   [註冊執行個體精靈簡介](#Welcome)  
  
-   [指定 SQL Server 的執行個體](#Instance_name)  
  
-   [連接對話方塊](#Connection_dialog)  
  
-   [公用程式收集組帳戶](#Proxy_configuration)  
  
-   [SQL Server 執行個體驗證](#Validation_rules)  
  
-   [註冊執行個體的摘要](#Summary)  
  
-   [正在註冊 SQL Server 的執行個體](#Enrolling)  
  
##  <a name="Welcome"></a> 註冊執行個體精靈簡介  
 若要啟動此精靈，請在公用程式控制點上展開 [公用程式總管] 樹狀目錄，然後以滑鼠右鍵按一下 [受管理的執行個體]，並選取 [新增受管理的執行個體...]。  
  
 若要繼續進行，請按 **[下一步]**。  
  
##  <a name="Instance_name"></a> 指定 SQL Server 的執行個體  
 若要從連接對話方塊選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，請按一下 [連接...]。 使用以下格式提供電腦名稱和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱：ComputerName\InstanceName。 如需詳細資訊，請參閱[連接到伺服器 &#40;Database Engine&#41;](https://msdn.microsoft.com/library/ee9017b4-8a19-4360-9003-9e6484082d41)。  
  
 若要繼續進行，請按 **[下一步]**。  
  
##  <a name="Connection_dialog"></a> 連接對話方塊  
 在 [連接到伺服器] 對話方塊中，確認伺服器類型、電腦名稱及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱資訊。 如需詳細資訊，請參閱[連接到伺服器 &#40;Database Engine&#41;](https://msdn.microsoft.com/library/ee9017b4-8a19-4360-9003-9e6484082d41)。  
  
> [!NOTE]  
>  如果連接已加密，將會使用加密的連接。 如果連接未加密， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式會使用加密的連接重新連接。  
  
 若要繼續，請按一下 **[連接...]**。  
  
##  <a name="Proxy_configuration"></a> 公用程式收集組帳戶  
 指定要執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組的 Windows 網域帳戶。 此帳戶會當做 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 帳戶來使用。 另外，您也可以使用現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶。 若要通過驗證需求，請使用下列方針來指定帳戶。  
  
 如果您指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶選項：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶必須是非內建帳戶 (如 LocalSystem、NetworkService 或 LocalService) 的 Windows 網域帳戶。  
  
 若要繼續進行，請按 **[下一步]**。  
  
##  <a name="Validation_rules"></a> SQL Server 執行個體驗證  
 在這一版中，以下條件必須在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上成立，才能註冊到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中：  
  
|條件|更正動作|  
|---------------|-----------------------|  
|您必須在指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體和 UCP 上擁有系統管理員權限。|您必須使用具有指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體和 UCP 上系統管理員權限的帳戶登入。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本必須支援執行個體註冊。|如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 必須啟用 TCP/IP。|在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 上啟用 TCP/IP。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體不能以其他任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 註冊。|如果您指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體已經當做現有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式的一部分進行管理，您無法以不同的 UCP 註冊它。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體不得為 UCP。|如果您指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體已經是與您所連接之 UCP 不同的 UCP，您無法在這個 UCP 中註冊它。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體必須安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組。|重新安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。|  
|必須停止指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的收集組。|在指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上停止預先存在的收集組。 如果資料收集器已停用，請啟用它，並停止任何執行中的收集組，然後針對建立 UCP 作業重新執行驗證規則。<br /><br /> 若要啟用資料收集器：<br /><br /> 在 [物件總管] 中，展開 **[管理]** 節點。<br /><br /> 以滑鼠右鍵按一下 **[資料收集]**，然後按一下 **[啟用資料收集]**。<br /><br /> 若要停止收集組：<br /><br /> 在 [物件總管] 中，依序展開 [管理] 節點、 **[資料收集]** 和 **[系統資料收集組]**。<br /><br /> 以滑鼠右鍵按一下您要停止的收集組，然後按一下 **[停止資料收集組]**。<br /><br /> 訊息方塊會顯示此動作的結果，而此收集組圖示上的紅色圓圈會指示此收集組已經停止。|  
|必須在指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務。|請在指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent 服務。 如果指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體，那麼請將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務設定為手動啟動。 否則，請將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務設定為自動啟動。|  
|必須在 UCP 上啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務。|在 UCP 上啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體，那麼請將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務設定為手動啟動。 否則，請將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務設定為自動啟動。|  
|WMI 必須正確設定。|若要針對 WMI 組態進行疑難排解，請參閱 [疑難排解 SQL Server 公用程式](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 帳戶必須是 UCP 上的有效 Windows 網域帳戶。|指定有效的 Windows 網域帳戶。 若要確保此帳戶是有效的，請使用 Windows 網域帳戶登入 UCP。|  
|如果您選取 Proxy 帳戶選項， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 帳戶必須是指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上的有效 Windows 網域帳戶。|指定有效的 Windows 網域帳戶。 若要確保此帳戶是有效的，請使用 Windows 網域帳戶登入指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶不得為類似 Network Service 的內建帳戶。|將此帳戶重新指派給 Windows 網域帳戶。 若要確保此帳戶是有效的，請使用 Windows 網域帳戶登入指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶必須是 UCP 上的有效 Windows 網域帳戶。|指定有效的 Windows 網域帳戶。 若要確保此帳戶是有效的，請使用 Windows 網域帳戶登入 UCP。|  
|如果您選取服務帳戶選項， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶必須是指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上的有效 Windows 網域帳戶。|指定有效的 Windows 網域帳戶。 若要確保此帳戶是有效的，請使用 Windows 網域帳戶登入指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。|  
  
 如果驗證結果中有失敗的情況，請更正阻礙問題，然後按一下 **[重新執行驗證]** 確認電腦組態。  
  
 若要儲存驗證報表，請按一下 **[儲存報表]** 然後指定檔案的位置。  
  
 若要繼續進行，請按 **[下一步]**。  
  
##  <a name="Summary"></a> 註冊執行個體的摘要  
 摘要頁面會列出有關加入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資訊。  
  
 受管理的執行個體設定：  
  
-   SQL Server 執行個體名稱：ComputerName\InstanceName  
  
-   公用程式收集組帳戶：DomainName\UserName  
  
 若要繼續進行，請按 **[下一步]**。  
  
##  <a name="Enrolling"></a> 正在註冊 SQL Server 的執行個體  
 註冊頁面提供此作業的狀態：  
  
-   正在準備執行個體以進行註冊。  
  
-   正在建立收集資料的快取目錄。  
  
-   正在設定公用程式收集組。  
  
 若要儲存有關註冊作業的報表，請按一下 [儲存報表]，然後指定檔案的位置。  
  
 若要完成精靈，請按一下 [完成]。  
  
> [!NOTE]  
>  如果您使用 SQL Server 驗證連接到 SQL Server 執行個體進行註冊，並且指定隸屬不同於 UCP 所在位置的其他 Active Directory 網域的 Proxy 帳戶，那麼執行個體驗證會順利進行，但是註冊作業會失敗且出現下列錯誤訊息：  
>   
>  執行 Transact-SQL 陳述式或批次時發生例外狀況。 (Microsoft.SqlServer.ConnectionInfo)  
>   
>  其他資訊: 無法獲得關於 Windows NT 群組/使用者 '\<域名稱\帳戶名稱>' 的資訊，錯誤碼 0x5。 (Microsoft SQL Server，錯誤：15404)  
>   
>  如需對這個失敗進行疑難排解的詳細資訊，請參閱 [疑難排解 SQL Server 公用程式](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)。  
  
> [!IMPORTANT]  
>  請勿在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體上變更「公用程式資訊」收集組的任何屬性，也請勿手動開啟/關閉資料收集，因為資料收集是由公用程式代理程式作業所控制。  
  
 完成 [註冊執行個體] 精靈之後，請在 SSMS 的**公用程式總管**瀏覽窗格中，按一下 [受管理的執行個體] 節點。 註冊的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體會顯示在 [公用程式總管內容] 窗格中的清單檢視內。  
  
 資料收集程序會立即開始，但是最多需要 30 分鐘的時間，資料才會第一次出現在 [公用程式總管] 內容窗格的儀表板和視點內。 資料收集會持續每隔 15 分鐘進行一次。 若要重新整理資料，請以滑鼠右鍵按一下**公用程式總管**瀏覽窗格中的 [受管理的執行個體] 節點，然後選取 [重新整理]，或是以滑鼠右鍵按一下清單檢視中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱，然後選取 [重新整理]。  
  
 若要從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中移除受管理的執行個體，請在**公用程式總管**瀏覽窗格中選取 [受管理的執行個體] 來填入受管理執行個體的清單檢視，然後以滑鼠右鍵按一下 [公用程式總管內容] 清單檢視中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱，再選取 [將執行個體設為未受管理]。  
  
##  <a name="PowerShell_enroll"></a> 使用 PowerShell 註冊 SQL Server 的執行個體  
 使用下列範例，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體註冊到現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式：  
  
```  
> $UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\UCP-Name";  
> $SqlStoreConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
> $Utility = [Microsoft.SqlServer.Management.Utility.Utility]::Connect($SqlStoreConnection);  
> $Instance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\ManagedInstanceName";  
> $InstanceConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $Instance.ConnectionContext.SqlConnectionObject;  
> $ManagedInstance = $Utility.EnrollInstance($InstanceConnection, "ProxyAccount", "ProxyPassword");  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 公用程式的功能與工作](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [監視 SQL Server 公用程式中的 SQL Server 執行個體](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [疑難排解 SQL Server 公用程式](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
