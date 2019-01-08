---
title: 建立 SQL Server 公用程式控制點 (SQL Server 公用程式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.create.ucp.progress.F1
- SQL12.SWB.create.ucp.welcome.F1
- SQL12.SWB.create.ucp.Summary.F1
- SQL12.SWB.create.ucp.validation.F1
- SQL12.SWB.create.ucp.instancename.F1
- SQL12.SWB.create.ucp.agentconfiguration.F1
helpviewer_keywords:
- Create UCP
- UCP
ms.assetid: d5335124-1625-47ce-b4ac-36078967158c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c027b6648da799be5a2b9381a0f19dc437563242
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377660"
---
# <a name="create-a-sql-server-utility-control-point-sql-server-utility"></a>建立 SQL Server 公用程式控制點 (SQL Server 公用程式)
  企業可以擁有多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式，每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式都可以管理多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體和資料層應用程式。 每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式都只能有一個公用程式控制點 (UCP)。 您必須針對每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式建立新的 UCP。 每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體和每一個資料層應用程式都只是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式的成員，而且是由單一 UCP 所管理。  
  
 UCP 每隔 15 分鐘就會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體收集組態和效能資訊。 這項資訊會儲存在 UCP 的公用程式管理資料倉儲 (UMDW) 中，而 UMDW 檔案名稱為 sysutility_mdw。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 效能資料會與原則相比較，有助於識別資源使用瓶頸及合併機會。  
  
## <a name="before-you-begin"></a>開始之前  
 在建立 UCP 之前，請先檢閱下列需求和建議事項。  
  
 在這一版中，UCP 及所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體都必須滿足以下需求：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須是 10.50 或更高的版本。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體類型必須是 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式必須在單一 Windows 網域或具有雙向信任關係的多個網域上運作。  
  
-   UCP 上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶及 SQL Server 的所有受管理的執行個體都必須具有 Active Directory 使用者的讀取權限。  
  
 在此版本中，UCP 必須滿足下列需求：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體必須是受支援的版本。 如需的版本所支援的功能清單[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 支援的 SQL Server 2014 的版本功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
-   我們建議您使用區分大小寫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體來主控 UCP。  
  
 請考慮在 UCP 電腦上採用下列容量規劃建議：  
  
-   在一般的案例中，UCP 上的 UMDW 資料庫 (sysutility_mdw) 所使用的磁碟空間大約是每年每個 SQL Server 受管理的執行個體 2 GB。 這個估計會根據受管理的執行個體所收集的資料庫和系統物件數目而有所不同。 UMDW (sysutility_mdw) 磁碟空間成長率在頭兩天最高。  
  
-   在一般的案例中，UCP 上的 msdb 所使用的磁碟空間大約是每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]受管理的執行個體 20 MB。 請注意，這個估計會根據資源使用量原則以及受管理的執行個體所收集的資料庫和系統物件數目而有所不同。 一般來說，當原則違規數目增加，以及動態資源的移動時間間隔增加時，磁碟空間使用量也會增加。  
  
-   請注意，要等到受管理的執行個體的資料保留期限過期之後，從 UCP 移除受管理的執行個體才會減少 UCP 資料庫所使用的磁碟空間。  
  
 在這一版中，所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體都必須滿足以下需求：  
  
-   我們建議如果使用不區分大小寫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體來主控 UCP，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體也應該不區分大小寫。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式監視不支援 FILESTREAM 資料。  
  
 如需詳細資訊，請參閱 < [SQL Server 的最大容量規格](../../sql-server/maximum-capacity-specifications-for-sql-server.md)並[支援的 SQL Server 2014 的版本功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
### <a name="remove-previous-utility-control-points-before-installing-a-new-one"></a>移除先前的公用程式控制點，然後再安裝新的公用程式控制點  
 如果您要在曾經設定為公用程式控制點 (UCP) 的 SQL Server 執行個體上安裝 UCP，就必須先移除所有 SQL Server 受管理的執行個體並移除該 UCP，然後再進行此作業。 您可以透過執行 **sp_sysutility_ucp_remove** 預存程序，完成移除作業。  
  
 執行此程序前，請注意下列需求：  
  
-   此程序必須在成為 UCP 的電腦上執行。  
  
-   此程序必須由擁有系統管理員 (sysadmin) 權限的使用者執行，而這些是建立 UCP 所需的相同權限。  
  
-   您必須從 UCP 中移除所有 SQL Server 受管理的執行個體。 請注意，UCP 就是 SQL Server 受管理的執行個體。 如需詳細資訊，請參閱[How to:從 SQL Server 公用程式移除 SQL Server 的執行個體](https://go.microsoft.com/fwlink/?LinkId=169392)。  
  
 您可以使用這個程序，從 SQL Server 公用程式中移除 SQL Server UCP。 完成此作業之後，您就可以再次於 SQL Server 執行個體上建立 UCP。  
  
 請使用 SQL Server Management Studio 來連接至 UCP，然後執行這個指令碼：  
  
```  
EXEC msdb.dbo.sp_sysutility_ucp_remove;  
```  
  
> [!NOTE]  
>  如果已移除 UCP 的 SQL Server 執行個體具有非公用程式資料收集組，此程序就不會卸除 sysutility_mdw 資料庫。 如果發生這種情況，您就必須先手動卸除 sysutility_mdw 資料庫，然後才能再次建立 UCP。  
  
 每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體和每一個資料層應用程式都只是一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式的成員，而且是由單一 UCP 所管理。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式概念的詳細資訊，請參閱 [SQL Server 公用程式的功能與工作](sql-server-utility-features-and-tasks.md)。  
  
 UCP 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式的中央推理點。 您可以使用 UCP 來檢視從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料層應用程式收集而來的組態與效能資訊，並執行一般容量規劃活動。 UCP 是從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式註冊及移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的啟動點。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中註冊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體後，您可以監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體與資料層應用程式的資源健全狀況，以確認合併機會及隔離資源瓶頸。 如需詳細資訊，請參閱 [監視 SQL Server 公用程式中的 SQL Server 執行個體](monitor-instances-of-sql-server-in-the-sql-server-utility.md)。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組與非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組會一起受到支援。 也就是說，當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Managed 執行個體為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式的成員時，可以受到其他收集組的監視。 但是請注意，受管理的執行個體上的所有收集組都會將其資料上傳到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式管理資料倉儲。 如需詳細資訊，請參閱[在相同 SQL Server 執行個體上執行公用程式和非公用程式收集組的考量事項](run-utility-and-non-utility-collection-sets-on-same-sql-instance.md)和[設定公用程式控制點資料倉儲 &#40;SQL Server 公用程式&#41;](configure-your-utility-control-point-data-warehouse-sql-server-utility.md)。  
  
## <a name="wizard-steps"></a>精靈步驟  
 ![](../../database-engine/media/create-ucp.gif "Create_UCP")  
  
 下列章節提供有關建立新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 之精靈工作流程中每一頁的詳細資訊。 若要啟動此精靈來建立新的 UCP，請從 SSMS 的 [檢視] 功能表中開啟公用程式總管窗格，然後按一下公用程式總管窗格上方的 [建立 UCP] 按鈕 ![](../../database-engine/media/create-ucp.gif "Create_UCP")。  
  
 按一下以下清單中的連結可導覽到精靈中頁面的詳細資料。  
  
 如需有關這項作業之 PowerShell 指令碼的詳細資訊，請參閱 [範例](#PowerShell_create_UCP)。  
  
-   [建立 UCP 精靈簡介](#Welcome)  
  
-   [指定執行個體](#Instance_name)  
  
-   [連接對話方塊](#Connection_dialog)  
  
-   [公用程式收集組帳戶](#Agent_configuration)  
  
-   [驗證規則](#Validation_rules)  
  
-   [摘要](#Summary)  
  
-   [建立公用程式控制點](#Creating_UCP)  
  
##  <a name="Welcome"></a> 建立 UCP 精靈簡介  
 如果您開啟公用程式總管，而且沒有連接的公用程式控制點，您必須連接到其中一個控制點或建立新的控制點。  
  
 **連接到現有的 UCP** - 如果您的部署中已經有公用程式控制點，您可以按一下公用程式總管窗格上方的 [連接到公用程式] 按鈕 ![](../../database-engine/media/connect-to-utility.gif "Connect_to_Utility") 來連線。 若要連接到現有的 UCP，您必須擁有系統管理員認證，或是具有公用程式讀取者角色成員的身分。 請注意，每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式上只能有一個 UCP，而且您也只能夠從一個 SSMS 執行個體連接到一個 UCP。  
  
 **建立新的 UCP** - 若要建立新的公用程式控制點，請按一下公用程式總管窗格上方的 [建立 UCP] 按鈕 ![](../../database-engine/media/create-ucp.gif "Create_UCP")。 若要建立新的 UCP，您必須指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱，並在連接對話方塊中提供系統管理員認證。 請注意，每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式只能有一個 UCP。  
  
##  <a name="Instance_name"></a> 指定執行個體  
 指定有關您建立之 UCP 的下列資訊：  
  
-   **執行個體名稱** - 若要從連線對話方塊選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，請按一下 [連線...]。使用以下格式提供電腦名稱和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱：ComputerName\InstanceName。  
  
-   **公用程式名稱** - 指定將用來識別網路上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式的名稱。  
  
 若要繼續進行，請按 **[下一步]**。  
  
##  <a name="Connection_dialog"></a> 連接對話方塊  
 在 [連接到伺服器] 對話方塊中，確認伺服器類型、電腦名稱及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱資訊。 如需詳細資訊，請參閱[連接到伺服器 &#40;Database Engine&#41;](../../ssms/f1-help/connect-to-server-database-engine.md)。  
  
> [!NOTE]  
>  如果連接已加密，將會使用加密的連接。 如果連接未加密， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式會使用加密的連接重新連接。  
  
 若要繼續，請按一下 [連線...]。  
  
##  <a name="Agent_configuration"></a> 公用程式收集組帳戶  
 指定要執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組的 Windows 網域帳戶。 此帳戶會當做 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 帳戶來使用。 另外，您也可以使用現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶。 若要通過驗證需求，請使用下列方針來指定帳戶。  
  
 如果您指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶選項：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶必須是非內建帳戶 (如 LocalSystem、NetworkService 或 LocalService) 的 Windows 網域帳戶。  
  
 若要繼續進行，請按 **[下一步]**。  
  
##  <a name="Validation_rules"></a> 驗證規則  
 在這一版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，以下條件必須在即將建立 UCP 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上成立：  
  
|驗證規則|更正動作|  
|---------------------|-----------------------|  
|您必須在即將建立公用程式控制點的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上擁有系統管理員權限。|使用具有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上系統管理員權限的帳戶登入。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本必須是 10.50 或更高的版本。|指定要主控 UCP 的另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體必須是受支援的版本。 如需的版本所支援的功能清單[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 支援的 SQL Server 2014 的版本功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。|指定要主控 UCP 的另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體不得為使用任何其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP 所註冊的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。|請指定不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體以裝載 UCP，或者從 UCP (目前為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的受管理的執行個體) 解除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的註冊。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體不得主控公用程式控制點。|指定要主控 UCP 的另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。|  
|指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體必須啟用 TCP/IP。|為指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體啟用 TCP/IP。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體不得擁有名為 "sysutility_mdw" 的資料庫。|建立 UCP 作業將會建立名為 "sysutility_mdw" 的公用程式管理資料倉儲 (UMDW)。 此作業會要求在執行驗證規則時，該名稱不能存在於電腦上。 若要繼續，您必須移除或重新命名任何名為 "sysutility_mdw" 的資料庫。 如需重新命名作業的詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)。|  
|必須停止指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的收集組。|在指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上建立 UCP 時，請停止已經存在的收集組。 如果資料收集器已停用，請啟用它，並停止任何執行中的收集組，然後針對建立 UCP 作業重新執行驗證規則。<br /><br /> 若要啟用資料收集器：<br /><br /> 在 [物件總管] 中，展開 **[管理]** 節點。<br /><br /> 以滑鼠右鍵按一下 **[資料收集]**，然後按一下 **[啟用資料收集]**。<br /><br /> 若要停止收集組：<br /><br /> 在 [物件總管] 中，依序展開 [管理] 節點、 **[資料收集]** 和 **[系統資料收集組]**。<br /><br /> 以滑鼠右鍵按一下您要停止的收集組，然後按一下 **[停止資料收集組]**。<br /><br /> 訊息方塊會顯示此動作的結果，而此收集組圖示上的紅色圓圈會指示此收集組已經停止。|  
|必須在指定的執行個體上啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務。 如果指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體，那麼必須將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務設定為手動啟動。 否則，必須將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務設定為自動啟動。|啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務。 如果指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體，那麼請將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務設定為手動啟動。 否則，請將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務設定為自動啟動。|  
|WMI 必須正確設定。|若要針對 WMI 組態進行疑難排解，請參閱 [疑難排解 SQL Server 公用程式](../../database-engine/troubleshoot-the-sql-server-utility.md)。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 帳戶不得為內建帳戶，例如 Network Service。|如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 帳戶為內建帳戶 (如 Network Service)，請將此帳戶重新指派給具有系統管理員權限的 Windows 網域帳戶。|  
|如果您選取 Proxy 帳戶選項， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 帳戶必須是有效的 Windows 網域帳戶。|指定有效的 Windows 網域帳戶。 若要確保此帳戶是有效的，請使用 Windows 網域帳戶登入指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。|  
|如果您選取服務帳戶選項， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶不得為內建帳戶，例如 Network Service。|如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶為內建帳戶 (如 Network Service)，請將此帳戶重新指派給 Windows 網域帳戶。|  
|如果您選取服務帳戶選項， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶必須是有效的 Windows 網域帳戶。|指定有效的 Windows 網域帳戶。 若要確保此帳戶是有效的，請使用 Windows 網域帳戶登入指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。|  
  
 如果驗證結果中有失敗的情況，請更正阻礙問題，然後按一下 **[重新執行驗證]** 確認電腦組態。  
  
 若要儲存驗證報表，請按一下 **[儲存報表]** 然後指定檔案的位置。  
  
 若要繼續進行，請按 **[下一步]**。  
  
##  <a name="Summary"></a> 摘要  
 摘要頁面會顯示您提供之有關 UCP 的資訊：  
  
-   主控 UCP 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式的名稱。  
  
-   將用於執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式資料收集工作的帳戶名稱。  
  
 若要變更 UCP 組態設定，請按 **[上一步]**。 若要繼續進行，請按 **[下一步]**。  
  
##  <a name="Creating_UCP"></a> 建立公用程式控制點  
 在建立 UCP 作業的期間，此精靈會顯示步驟並提供狀態：  
  
-   正在準備 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體以建立 UCP。  
  
-   正在建立公用程式管理資料倉儲 (UMDW)。  
  
-   正在初始化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UMDW；UMDW 檔案名稱為 sysutility_mdw。  
  
-   正在設定 UCP。  
  
-   正在設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式收集組。  
  
 若要儲存有關建立 UCP 作業的報表，請按一下 **[儲存報表]** 然後指定檔案的位置。  
  
 若要完成精靈，請按一下 **[完成]**。  
  
 完成建立 UCP 精靈之後，SSMS 中的 [公用程式總管] 導覽窗格會顯示 UCP 的節點，以及其底下針對部署的資料層應用程式、受管理的執行個體和公用程式管理的節點。 UCP 會自動變成受管理的執行個體。  
  
 資料收集程序會立即開始，但是最多需要 30 分鐘的時間，資料才會第一次出現在 [公用程式總管] 內容窗格的儀表板和視點內。 資料收集會持續每隔 15 分鐘進行一次。 初始資料將來自 UCP 本身。 也就是說，UCP 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中的第一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體。  
  
 若要顯示儀表板，請從 SSMS 功能表按一下 **[檢視]** ，然後選取 **[公用程式總管內容]** 。 若要重新整理資料，請以滑鼠右鍵按一下 [公用程式總管] 窗格中的公用程式名稱，然後選取 [重新整理]。  
  
 如需如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中註冊其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的詳細資訊，請參閱[註冊 SQL Server 的執行個體 &#40;SQL Server 公用程式&#41;](enroll-an-instance-of-sql-server-sql-server-utility.md)。 若要從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中移除當做 受管理的執行個體的 UCP，請在 **[公用程式總管]** 窗格中選取 **[受管理的執行個體]** 來填入受管理的執行個體的清單檢視，然後以滑鼠右鍵按一下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [公用程式總管內容] **清單檢視中的** 執行個體名稱，再選取 **[將執行個體設為未受管理]**。  
  
##  <a name="PowerShell_create_UCP"></a> 使用 PowerShell 建立新的公用程式控制點  
 使用下列範例建立新的公用程式控制點：  
  
```  
> $UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\UCP-Name";  
> $SqlStoreConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
> $Utility = [Microsoft.SqlServer.Management.Utility.Utility]::CreateUtility("Utility", $SqlStoreConnection, "ProxyAccount", "ProxyAccountPassword");  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 公用程式的功能與工作](sql-server-utility-features-and-tasks.md)   
 [疑難排解 SQL Server 公用程式](../../database-engine/troubleshoot-the-sql-server-utility.md)  
  
  
