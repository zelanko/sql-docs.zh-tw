---
title: 設定可用性複本的備份 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- backup priority
- backup on secondary replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], backup on secondary replicas
- active secondary replicas [SQL Server], backup on
- automated backup preference
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 74bc40bb-9f57-44e4-8988-1d69c0585eb6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 95f1e2cec530ee65dce60ceea1679281a9d3ba5c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "72783000"
---
# <a name="configure-backup-on-availability-replicas-sql-server"></a>設定可用性複本的備份 (SQL Server)
  本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中的 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]或 PowerShell，針對 AlwaysOn 可用性群組設定次要複本的備份。  
  
> [!NOTE]  
>  如需在次要複本上進行備份的簡介，請參閱使用中[次要：在次要複本上備份（AlwaysOn 可用性群組）](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)。  
  
 
  

  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 必要條件  
 您必須連接到裝載主要複本的伺服器執行個體。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
  
|工作|權限|  
|----------|-----------------|  
|若要在建立可用性群組時設定次要複本的備份|需要 **系統管理員 (sysadmin)** 固定伺服器角色的成員資格，以及 CREATE AVAILABILITY GROUP 伺服器權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。|  
|若要修改可用性群組或可用性複本|需要可用性群組的 ALTER AVAILABILITY GROUP 權限、CONTROL AVAILABILITY GROUP 權限、ALTER ANY AVAILABILITY GROUP 權限或 CONTROL SERVER 權限。|  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **若要設定次要複本的備份**  
  
1.  在 [物件總管] 中，連接到裝載主要複本的伺服器執行個體，然後按一下伺服器名稱以展開伺服器樹狀目錄。  
  
2.  依序展開 **[AlwaysOn 高可用性]** 節點和 **[可用性群組]** 節點。  
  
3.  按一下您想要設定其備份喜好設定的可用性群組，然後選取 **[屬性]** 命令。  
  
4.  在 **[可用性群組屬性]** 對話方塊中，選取 **[備份喜好設定]** 頁面。  
  
5.  在 **[應該在何處執行備份?]** 面板上，選取可用性群組的自動備份喜好設定，它有下列幾種：  
  
     **慣用次要**  
     指定應該在次要複本上進行備份，但是主要複本是唯一線上複本的情況例外。 在此情況下，應該在主要複本上進行備份。 這是預設選項。  
  
     **僅次要**  
     指定絕對不能在主要複本上執行備份。 如果主要複本是唯一的線上複本，不應該進行備份。  
  
     `Primary`  
     指定備份一定要在主要複本上進行。 如果當您在次要複本上執行備份時，需要不支援的備份功能 (例如建立差異備份)，這個選項會很實用。  
  
    > [!IMPORTANT]  
    >  如果您計畫要使用記錄傳送來準備可用性群組的任何次要資料庫，請將自動備份喜好設定設為 `Primary`，直到所有次要資料庫都已經準備完成並且聯結至可用性群組為止。  
  
     **任何複本**  
     指定當您選擇要執行備份的複本時，您希望備份作業忽略可用性複本的角色。 請注意，備份作業可能會評估其他因素，例如每個可用性複本的備份優先權，搭配其操作狀態和連接狀態。  
  
    > [!IMPORTANT]  
    >  不會強制執行自動備份喜好設定。 這個喜好設定的解譯取決於您在給定可用性群組之資料庫的備份作業中所編寫的邏輯 (如果有的話)。 自動備份喜好設定對於特定備份沒有任何影響。 如需詳細資訊，請參閱本主題稍後的＜ [後續操作：設定次要複本的備份之後](#FollowUp) ＞。  
  
6.  您可以使用 **[複本備份優先權]** 方格來變更可用性複本的備份優先權。 此方格顯示裝載可用性群組複本的每個伺服器執行個體的目前備份優先權。 方格資料行如下所示：  
  
     **伺服器實例**  
     裝載可用性複本之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的名稱。  
  
     **備份優先權 (最低 = 1，最高 = 100)**  
     指定在這個複本上執行備份的優先權 (相對於相同可用性群組中的其他複本)。 這個值是 0 到 100 範圍之間的整數。 1 表示最低優先權，100 表示最高優先權。 如果 [備份優先權]**** = 1，則只有當目前沒有更高優先權的可用性複本可用時，才會選擇此可用性複本來執行備份。  
  
     **排除複本**  
     決定是否絕對不要選擇這個可用性複本來執行備份。 例如，這對於您永遠不希望將備份容錯移轉到其中的遠端可用性複本十分有用。  
  
7.  若要認可變更，請按一下 **[確定]**。  
  
 **存取備份喜好設定頁面的其他方式**  
  
-   [使用新增可用性群組對話方塊 &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [使用 [將複本加入可用性群組中精靈] &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用新增可用性群組對話方塊 &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要設定次要複本的備份**  
  
1.  連接到裝載主要複本的伺服器執行個體。  
  
2.  若為新的可用性群組，請使用 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-availability-group-transact-sql) 陳述式。 如果您要修改現有的可用性群組，請使用 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql) 陳述式。  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> 使用 PowerShell  

### <a name="to-configure-backup-on-secondary-replicas"></a>若要設定次要複本的備份
  
1.  將預設值 (`cd`) 設定為裝載主要複本的伺服器執行個體。  
  
2.  (選擇性) 設定您要加入或修改之每個可用性複本的備份優先權。 裝載主要複本的伺服器執行個體會使用這個優先權來決定哪個複本應該服務可用性群組中資料庫的自動備份要求 (系統會選擇優先權最高的複本)。 這個優先權可以是 0 和 100 (含) 之間的任何數字。 如果優先權為 0，就表示系統不應該將複本視為服務備份要求的候選。  預設值為 50。  
  
     將可用性複本加入至可用性群組時，請使用 `New-SqlAvailabilityReplica` 指令程式。 修改現有的可用性複本時，請使用 `Set-SqlAvailabilityReplica` 指令程式。 不論是哪一種情況`BackupPriority`，請指定*n*參數，其中*n*是介於0到100之間的值。  
  
     例如，下列命令會將可用性複本 `MyReplica` 的備份優先權設定為 `60`。  
  
    ```powershell
    Set-SqlAvailabilityReplica -BackupPriority 60 -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
3.  (選擇性) 設定您要建立或修改之可用性群組的自動備份喜好設定。 這個喜好設定會指出備份作業在選擇要在何處執行備份時應該如何評估主要複本。 預設設定是慣用次要複本。  
  
     建立可用性群組時，請使用 `New-SqlAvailabilityGroup` 指令程式。 修改現有的可用性群組時，請使用 `Set-SqlAvailabilityGroup` 指令程式。 在任何一種情況中，請指定 `AutomatedBackupPreference` 參數。  
  
     其中  
  
     `Primary`  
     指定備份一定要在主要複本上進行。 如果當您在次要複本上執行備份時，需要不支援的備份功能 (例如建立差異備份)，這個選項會很實用。  
  
    > [!IMPORTANT]  
    >  如果您計畫要使用記錄傳送來準備可用性群組的任何次要資料庫，請將自動備份喜好設定設為 `Primary`，直到所有次要資料庫都已經準備完成並且聯結至可用性群組為止。  
  
     `SecondaryOnly`  
     指定絕對不能在主要複本上執行備份。 如果主要複本是唯一的線上複本，不應該進行備份。  
  
     `Secondary`  
     指定應該在次要複本上進行備份，但是主要複本是唯一線上複本的情況例外。 在此情況下，應該在主要複本上進行備份。 此為預設行為。  
  
     `None`  
     指定當您選擇要執行備份的複本時，您希望備份作業忽略可用性複本的角色。 請注意，備份作業可能會評估其他因素，例如每個可用性複本的備份優先權，搭配其操作狀態和連接狀態。  
  
    > [!IMPORTANT]  
    >  不會強制執行 `AutomatedBackupPreference`。 這個喜好設定的解譯取決於您在給定可用性群組之資料庫的備份作業中所編寫的邏輯 (如果有的話)。 自動備份喜好設定對於特定備份沒有任何影響。 如需詳細資訊，請參閱本主題稍後的＜ [後續操作：設定次要複本的備份之後](#FollowUp) ＞。  
  
     例如，下列命令會將可用性群組 `MyAg` 的 `AutomatedBackupPreference` 屬性設定為 `SecondaryOnly`。 這個可用性群組中資料庫的自動備份永遠不會在主要複本上進行，但是會重新導向至備份優先權設定最高的次要複本。  
  
    ```powershell
    Set-SqlAvailabilityGroup -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg `  
     -AutomatedBackupPreference SecondaryOnly  
    ```  
  
> [!NOTE]  
>  若要檢視指令程式的語法，請在 `Get-Help` PowerShell 環境中使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 指令程式。 如需詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
若要設定及使用 SQL Server PowerShell 提供者，請參閱[SQL Server PowerShell 提供者](../../../powershell/sql-server-powershell-provider.md)並[取得說明 SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。
  
##  <a name="follow-up-after-configuring-backup-on-secondary-replicas"></a><a name="FollowUp"></a>後續操作：在次要複本上設定備份之後  
 若要針對給定可用性群組將自動備份喜好設定納入考量，您必須在備份優先權大於零 (>0) 之裝載可用性複本的每個伺服器執行個體上，針對可用性群組中的資料庫編寫備份作業的指令碼。 若要判斷目前的複本是否為慣用的備份複本，請在您的備份指令碼中使用 [sys.fn_hadr_backup_is_preferred_replica](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql) 函數。 如果目前伺服器執行個體所裝載的可用性複本是慣用的備份複本，此函數會傳回 1。 如果不是，函數會傳回 0。 透過在每個可用性複本上執行簡單的指令碼來查詢這個函數，您就可以判斷哪個複本應該執行給定的備份作業。 例如，備份作業指令碼的一般程式碼片段看起來可能像是：  
  
```  
IF (NOT sys.fn_hadr_backup_is_preferred_replica(@DBNAME))  
BEGIN  
      Select 'This is not the preferred replica, exiting with success';  
      RETURN 0 - This is a normal, expected condition, so the script returns success  
END  
BACKUP DATABASE @DBNAME TO DISK=<disk>  
   WITH COPY_ONLY;  
```  
  
 使用這類邏輯編寫備份作業的指令碼，可讓您指定備份作業以相同排程在每個可用性複本上執行。 每一個作業都會查看相同的資料，以判斷應該執行哪一個作業，如此一來，只有其中一個排程作業會實際進行到備份階段。  萬一發生容錯移轉，指令碼或作業都不需要修改。 此外，如果您重新設定可用性群組以加入可用性複本，備份作業管理只需要複製或排程備份作業。 如果您移除可用性複本，只需從原先裝載該複本的伺服器執行個體刪除備份作業。  
  
> [!TIP]  
>  如果您使用[維護計畫精靈](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)來建立指定的備份作業，此作業就會自動包含呼叫並檢查 **sys.fn_hadr_backup_is_preferred_replica** 函數的指令碼邏輯。 不過，此備份作業不會傳回「這不是慣用的複本...」訊息。請務必在裝載可用性群組之可用性複本的每一個伺服器執行個體上，為每個可用性資料庫建立作業。  
  
##  <a name="to-obtain-information-about-backup-preference-settings"></a><a name="ForInfoAboutBuPref"></a>取得備份喜好設定的相關資訊  
 下列檢視表可用於取得次要備份的相關資訊。  
  
|檢視|資訊|相關資料行|  
|----------|-----------------|----------------------|  
|[sys.fn_hadr_backup_is_preferred_replica](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)|目前的複本是否為慣用的備份複本？|不適用。|  
|[sys.availability_groups](/sql/relational-databases/system-catalog-views/sys-availability-groups-transact-sql)|自動備份喜好設定|**automated_backup_preference**<br /><br /> **automated_backup_preference_desc**|  
|[sys.availability_replicas](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)|給定可用性複本的備份優先權|**backup_priority**|  
|[sys.dm_hadr_availability_replica_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql)|複本是否為伺服器執行個體的本機複本？<br /><br /> 目前的角色<br /><br /> 操作狀態<br /><br /> 連接狀態<br /><br /> 可用性複本的同步處理健全狀況|**is_local**<br /><br /> **role**、 **role_desc**<br /><br /> **operational_state**、 **operational_state_desc**<br /><br /> **connected_state**、 **connected_state_desc**<br /><br /> **synchronization_health**、 **synchronization_health_desc**|  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 相關內容  
  
-   [Microsoft SQL Server AlwaysOn 高可用性和災害復原方案指南](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [SQL Server AlwaysOn 團隊部落格：官方 SQL Server AlwaysOn 團隊部落格](https://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>另請參閱  
 [AlwaysOn 可用性群組 &#40;SQL Server 的總覽&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [使用中次要：在次要複本上備份 (AlwaysOn 可用性群組)](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md) 
