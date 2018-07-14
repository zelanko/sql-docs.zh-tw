---
title: 啟用和停用 AlwaysOn 可用性群組 (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], disabling
- Availability Groups [SQL Server], enabling
ms.assetid: 7c326958-5ae9-4761-9c57-905972276a8f
caps.latest.revision: 58
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8cfcbdb8e61941a651539bd545b5067a1df5b63a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185351"
---
# <a name="enable-and-disable-alwayson-availability-groups-sql-server"></a>啟用和停用 AlwaysOn 可用性群組 (SQL Server)
  啟用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 是伺服器執行個體使用可用性群組的必要條件。 您必須在將要裝載一個或多個可用性群組之可用性複本的每個 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 執行個體上啟用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能，才能建立及設定任何可用性群組。  
  
> [!IMPORTANT]  
>  如果您刪除然後重新建立 WSFC 叢集，則必須在原始 WSFC 叢集上裝載可用性複本的每個 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 執行個體，停用然後重新啟用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能。  
  
-   **開始之前：**  
  
     [必要條件](#Prerequisites)  
  
     [Security](#Security)  
  
-   **如何：**  
  
    -   [判斷 AlwaysOn 可用性群組是否已啟用](#IsEnabled)  
  
    -   [啟用 AlwaysOn 可用性群組](#EnableAOAG)  
  
    -   [停用 AlwaysOn 可用性群組](#DisableAOAG)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 啟用 AlwaysOn 可用性群組的必要條件  
  
-   此伺服器執行個體必須位於 Windows Server 容錯移轉叢集 (WSFC) 節點上。  
  
-   伺服器執行個體必須執行支援 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]的 SQL Server 版本。 如需詳細資訊，請參閱＜ [Features Supported by the Editions of SQL Server 2014](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)＞。  
  
-   一次只在一個伺服器執行個體啟用 AlwaysOn 可用性群組。 啟用 AlwaysOn 可用性群組之後，等到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]再繼續進行到另一個伺服器執行個體重新啟動服務。  
  
 如需建立及設定可用性群組的其他必要條件的資訊，請參閱 <<c0> [ 必要條件、 限制和建議的 AlwaysOn 可用性群組&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)。</c0>  
  
###  <a name="Security"></a> 安全性  
 執行個體上啟用 AlwaysOn 可用性群組時[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，伺服器執行個體已在 WSFC 叢集上的完整控制權。  
  
####  <a name="Permissions"></a> 權限  
 需要本機電腦的 **Administrator** 群組成員資格和 WSFC 叢集的完整控制。 透過使用 PowerShell 啟用 AlwaysOn 時，請使用 **[以系統管理員身分執行]** 選項開啟命令提示字元視窗。  
  
 需要 Active Directory 建立物件和管理物件權限。  
  
##  <a name="IsEnabled"></a> 判斷 AlwaysOn 可用性群組是否已啟用  
  
-   [SQL Server Management Studio](#SSMS1Procedure)  
  
-   [Transact-SQL](#Tsql1Procedure)  
  
-   [PowerShell](#PowerShell1Procedure)  
  
###  <a name="SSMS1Procedure"></a> 使用 SQL Server Management Studio  
 **若要判斷是否已啟用 AlwaysOn 可用性群組**  
  
1.  在物件總管中，以滑鼠右鍵按一下伺服器執行個體，然後按一下 [屬性]。  
  
2.  在 **[伺服器屬性]** 對話方塊中，按一下 **[一般]** 頁面。 **[為已啟用 HADR]** 屬性會顯示下列其中一個值：  
  
    -   如果 AlwaysOn 可用性群組已啟用，則為**True**  
  
    -   如果 AlwaysOn 可用性群組已停用，則為**False**  
  
###  <a name="Tsql1Procedure"></a> 使用 Transact-SQL  
 **若要判斷是否已啟用 AlwaysOn 可用性群組**  
  
1.  使用下列 [SERVERPROPERTY](/sql/t-sql/functions/serverproperty-transact-sql) 陳述式：  
  
    ```  
    SELECT SERVERPROPERTY ('IsHadrEnabled');  
    ```  
  
     `IsHadrEnabled` 伺服器屬性設定會指出 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體是否已啟用 AlwaysOn 可用性群組，如下所示：  
  
    -   如果`IsHadrEnabled`= 1，已啟用 AlwaysOn 可用性群組。  
  
    -   如果`IsHadrEnabled`= 0 時，會停用 AlwaysOn 可用性群組。  
  
    > [!NOTE]  
    >  如需詳細資訊`IsHadrEnabled`伺服器屬性，請參閱 < [SERVERPROPERTY &#40;TRANSACT-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)。  
  
###  <a name="PowerShell1Procedure"></a> 使用 PowerShell  
 **若要判斷是否已啟用 AlwaysOn 可用性群組**  
  
1.  將目錄切換到 (`cd`) 要判斷 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 是否已啟用的伺服器執行個體。  
  
2.  輸入下列 PowerShell `Get-Item` 命令：  
  
    ```  
    PS SQLSERVER:\SQL\NODE1\DEFAULT> get-item . | select IsHadrEnabled  
    ```  
  
    > [!NOTE]  
    >  若要檢視 cmdlet 的語法，請使用`Get-Help`指令程式在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]PowerShell 環境。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="EnableAOAG"></a> 啟用 AlwaysOn 可用性群組  
 **若要啟用 AlwaysOn，使用：**  
  
-   [SQL Server 組態管理員](#SQLCM2Procedure)  
  
-   [PowerShell](#PScmd2Procedure)  
  
###  <a name="SQLCM2Procedure"></a> 使用 SQL Server 組態管理員  
 **若要啟用 AlwaysOn 可用性群組**  
  
1.  連接到 Windows Server 容錯移轉叢集 (WSFC) 節點裝載[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]您要啟用 AlwaysOn 可用性群組的執行個體。  
  
2.  指向 [開始]  功能表上的 [所有程式] ，然後依序指向 [ [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]] 和 [組態工具] ，再按一下 [SQL Server 組態管理員] 。  
  
3.  在  **SQL Server 組態管理員**，按一下**SQL Server 服務**，以滑鼠右鍵按一下 SQL Server (**<*`instance name`*>)**，其中**< *`instance name`* >** 是您要啟用 AlwaysOn 可用性群組中，本機伺服器執行個體的名稱和按一下 **屬性。**  
  
4.  選取 **[AlwaysOn 高可用性]** 索引標籤。  
  
5.  確認 [Windows 容錯移轉叢集名稱] 欄位包含本機容錯移轉叢集的名稱。 如果此欄位為空白，表示此伺服器執行個體目前不支援 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。 有可能本機電腦不是叢集節點，WSFC 叢集已經關閉，或者此版本 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 不支援 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。  
  
6.  選取 **[啟用 AlwaysOn 可用性群組]** 核取方塊，然後按一下 **[確定]**。  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 組態管理員會儲存您的變更。 然後您必須手動重新啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務。 這讓您可以選擇最適合您業務需求的重新啟動時間。 當[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服務重新啟動時，AlwaysOn 就會啟用，而`IsHadrEnabled`伺服器屬性會設定為 1。  
  
###  <a name="PScmd2Procedure"></a> 使用 SQL Server PowerShell  
 **若要啟用 AlwaysOn**  
  
1.  將目錄切換到 (`cd`) 要啟用 AlwaysOn 可用性群組的伺服器執行個體。  
  
2.  使用`Enable-SqlAlwaysOn`cmdlet 啟用 AlwaysOn 可用性群組。  
  
     若要檢視 cmdlet 的語法，請使用`Get-Help`指令程式在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]PowerShell 環境。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
    > [!NOTE]  
    >  如需有關如何控制資訊是否`Enable-SqlAlwaysOn`cmdlet 會重新啟動[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服務，請參閱[何時 Cmdlet 重新啟動 SQL Server 服務？](#WhenCmdletRestartsSQL)稍後在本主題中。  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../../powershell/sql-server-powershell-provider.md)  
  
####  <a name="ExmplEnable-SqlHadrServic"></a> 範例：Enable-SqlAlwaysOn  
 下列 PowerShell 命令會在 SQL Server 執行個體 (電腦\\執行個體) 上啟用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。  
  
```  
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Computer\Instance  
```  
  
##  <a name="DisableAOAG"></a> 停用 AlwaysOn 可用性群組  
  
-   **您停用 AlwaysOn 之前：**  
  
     [建議](#Recommendations)  
  
-   **若要停用 AlwaysOn，使用：**  
  
    -   [SQL Server 組態管理員](#SQLCM3Procedure)  
  
    -   [PowerShell](#PScmd3Procedure)  
  
-   **後續操作：**[停用 AlwaysOn 之後  ](#FollowUp)  
  
> [!IMPORTANT]  
>  一次只在一個伺服器執行個體上停用 AlwaysOn。 停用 AlwaysOn 可用性群組之後，等到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務重新啟動後才能在另一個伺服器執行個體繼續進行。  
  
###  <a name="Recommendations"></a> 建議  
 在伺服器執行個體上停用 AlwaysOn 之前，我們建議您執行下列動作：  
  
1.  如果伺服器執行個體目前裝載要保留之可用性群組的主要複本，建議手動將可用性群組容錯移轉至已同步處理的次要複本 (如果可能的話)。 如需詳細資訊，請參閱[執行可用性群組的已規劃手動容錯移轉 &#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)。  
  
2.  移除所有本機次要複本。 如需詳細資訊，請參閱[將次要複本從可用性群組移除 &#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)。  
  
###  <a name="SQLCM3Procedure"></a> 使用 SQL Server 組態管理員  
 **若要停用 AlwaysOn**  
  
1.  連接到 Windows Server 容錯移轉叢集 (WSFC) 節點，此節點裝載您要停用 AlwaysOn 可用性群組的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體。  
  
2.  指向 **[開始]** 功能表上的 **[所有程式]**，然後依序指向 [ [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)]] 和 **[組態工具]**，再按一下 **[SQL Server 組態管理員]**。  
  
3.  在  **SQL Server 組態管理員**，按一下**SQL Server 服務**，以滑鼠右鍵按一下 SQL Server (**<*`instance name`*>)**，其中**< *`instance name`* >** 是您要停用 AlwaysOn 可用性群組，本機伺服器執行個體的名稱和按一下 **屬性**。  
  
4.  在 [AlwaysOn 高可用性]索引標籤上，取消選取 [啟用 AlwaysOn 可用性群組]  核取方塊，然後按一下 [確定] 。  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 組態管理員會儲存您的變更並重新啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務。 當 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務重新啟動時，AlwaysOn 就會停用，而且 `IsHadrEnabled` 伺服器屬性會設定為 0，表示 AlwaysOn 可用性群組已停用。  
  
5.  我們建議您閱讀本主題稍後的＜ [待處理：停用 AlwaysOn 之後](#FollowUp)＞資訊。  
  
###  <a name="PScmd3Procedure"></a> 使用 SQL Server PowerShell  
 **若要停用 AlwaysOn**  
  
1.  將目錄切換到 (`cd`) 要停用 AlwaysOn 可用性群組、目前啟用的伺服器執行個體。  
  
2.  使用`Disable-SqlAlwaysOn`cmdlet 啟用 AlwaysOn 可用性群組。  
  
     例如，下列命令會停用 AlwaysOn 可用性群組上的 SQL Server 執行個體 (*電腦*\\*執行個體*)。  此命令需要重新啟動執行個體，而且系統將提示您確認重新啟動。  
  
    ```  
    Disable-SqlAlwaysOn -Path SQLSERVER:\SQL\Computer\Instance  
    ```  
  
    > [!IMPORTANT]  
    >  如需有關如何控制資訊是否`Disable-SqlAlwaysOn`cmdlet 會重新啟動[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]服務，請參閱[何時 Cmdlet 重新啟動 SQL Server 服務？](#WhenCmdletRestartsSQL)稍後在本主題中。  
  
     若要檢視 cmdlet 的語法，請使用`Get-Help`指令程式在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]PowerShell 環境。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
 **若要設定和使用 SQL Server PowerShell 提供者**  
  
-   [SQL Server PowerShell 提供者](../../../powershell/sql-server-powershell-provider.md)  
  
###  <a name="FollowUp"></a> 後續操作： 停用 AlwaysOn 之後  
 停用 AlwaysOn 可用性群組，執行個體之後[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]必須重新啟動。 SQL Server 組態管理員會自動重新啟動伺服器執行個體。 但是，如果您使用 `Disable-SqlAlwaysOn` 指令程式，則需要手動重新啟動伺服器執行個體。 如需詳細資訊，請參閱 [sqlservr Application](../../../tools/sqlservr-application.md)。  
  
 在重新啟動的伺服器執行個體：  
  
-   在 SQL Server 啟動時，可用性資料庫不會啟動，因此無法存取。  
  
-   唯一支援的 AlwaysOn[!INCLUDE[tsql](../../../includes/tsql-md.md)]陳述式[DROP AVAILABILITY GROUP](/sql/t-sql/statements/drop-availability-group-transact-sql)。 不支援 CREATE AVAILABILITY GROUP、ALTER AVAILABILITY GROUP，以及 ALTER DATABASE 的 SET HADR 選項。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中繼資料和 WSFC 中的 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 組態資料不受 AlwaysOn 可用性群組停用所影響。  
  
 如果您在裝載一個或多個可用性群組之可用性複本的每個伺服器執行個體上永久停用 AlwaysOn 可用性群組，建議您完成下列步驟：  
  
1.  如果您在停用 AlwaysOn 之前未移除本機可用性複本，請針對裝載可用性複本的伺服器執行個體刪除 (卸除) 每個可用性群組。 如需刪除可用性群組的相關資訊，請參閱[移除可用性群組 &#40;SQL Server&#41;](remove-an-availability-group-sql-server.md)。  
  
2.  若要移除遺留的中繼資料，在做為原始 WSFC 叢集一部分的伺服器執行個體上，刪除 (卸除) 每個受影響的可用性群組。  
  
3.  任何主要資料庫仍會繼續可供所有連接存取，但是主要和次要資料庫之間的資料同步處理會停止。  
  
4.  次要資料庫會進入 RESTORING 狀態。 您可以刪除它們，或透過使用 RESTORE WITH RECOVERY 還原它們。 但是，還原的資料庫不再參與可用性群組資料同步處理。  
  
##  <a name="WhenCmdletRestartsSQL"></a> Cmdlet 在何時重新啟動 SQL Server 服務  
 在目前執行中的伺服器執行個體上，使用 `Enable-SqlAlwaysOn` 或 `Disable-SqlAlwaysOn` 變更目前的 AlwaysOn 設定，可能會導致 SQL Server 服務重新啟動。 重新啟動行為取決於下列條件：  
  
|指定 -NoServiceRestart 參數|指定 -Force 參數|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務是否重新啟動？|  
|--------------------------------------------|---------------------------------|---------------------------------------------------------|  
|否|否|根據預設。 但指令程式會出現提示，如下所示：<br /><br /> **若要完成這個動作，我們必須重新啟動伺服器執行個體 '<執行個體名稱>' 的 SQL Server 服務。您要繼續嗎?**<br /><br /> **[Y] 是 [N] 否 [S] 暫停 [?] 說明 (預設為 "Y")：**<br /><br /> 如果指定 **N** 或 **S**，就不會重新啟動服務。|  
|否|是|服務會重新啟動。|  
|是|否|服務不會重新啟動。|  
|是|是|服務不會重新啟動。|  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組概觀&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)  
  
  
