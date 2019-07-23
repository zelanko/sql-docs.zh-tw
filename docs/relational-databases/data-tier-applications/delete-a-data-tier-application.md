---
title: 刪除資料層應用程式 | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.deletedacwizard.deletedac.f1
- sql13.swb.deletedacwizard.summary.f1
- sql13.swb.deletedacwizard.introduction.f1
- sql13.swb.deletedacwizard.choosemethod.f1
helpviewer_keywords:
- How to [DAC], delete
- data-tier application [SQL Server], delete
- wizard [DAC], delete
- delete DAC
ms.assetid: 16fe1c18-4486-424d-81d6-d276ed97482f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 17e12a45f8f5aa9e94936a85f62d21c88ccb8c08
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134834"
---
# <a name="delete-a-data-tier-application"></a>刪除資料層應用程式
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  您可以使用 [刪除資料層應用程式精靈] 或 Windows PowerShell 指令碼來刪除資料層應用程式。 您可以指定是否要保留、卸離或卸除相關聯的資料庫。  
  
-   **開始之前：** [限制事項](#LimitationsRestrictions)、[權限](#Permissions)  
  
-   **若要升級 DAC，請使用下列方式：** [註冊資料層應用程式精靈](#UsingDeleteDACWizard)、[PowerShell](#DeleteDACPowerShell)  
  
## <a name="before-you-begin"></a>開始之前  
 當您刪除資料層應用程式 (DAC) 執行個體時，可以選擇三個選項中的一個，指定要使用與資料層應用程式相關聯之資料庫執行的動作。 所有的三個選項都會刪除 DAC 定義中繼資料。 這些選項的差異在於它們使用與資料層應用程式相關聯之資料庫執行的動作。 精靈不會刪除與 DAC 或資料庫相關聯的任何執行個體層級物件，例如登入。  
  
|選項|資料庫動作|  
|------------|----------------------|  
|刪除註冊|相關聯的資料庫會保持不變。|  
|卸離資料庫|相關聯的資料庫會遭到卸離。 Database Engine 執行個體無法參考資料庫，但是資料和記錄檔保持不變。|  
|刪除資料庫|相關聯的資料庫會遭到卸除。 資料和記錄檔會遭到刪除。|  
  
###  <a name="LimitationsRestrictions"></a> 限制事項  
 在刪除 DAC 之後還原 DAC 定義中繼資料或資料庫沒有任何自動化的機制。 您手動重建 DAC 執行個體的方式取決於刪除選項。  
  
|選項|如何重建 DAC 執行個體|  
|------------|-------------------------------------|  
|刪除註冊|從原狀的資料庫註冊 DAC。|  
|卸離資料庫|使用 **sp_attachdb** 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]重新附加資料庫，然後從資料庫註冊新的 DAC 執行個體。|  
|刪除資料庫|從刪除 DAC 之前所做的完整備份還原資料庫，然後從資料庫註冊新的 DAC 執行個體。|  
  
> [!WARNING]  
>  從已還原或重新附加的資料庫註冊 DAC 來重建 DAC 執行個體時，將無法重新建立原始 DAC 的某些部分，例如伺服器選取原則。  
  
###  <a name="Permissions"></a> 權限  
 DAC 只能由系統管理員 ( **sysadmin** ) 或伺服器管理員 ( **serveradmin** ) 固定伺服器角色的成員或資料庫擁有者刪除。 名為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sa **的內建** 系統管理員帳戶也可以啟動精靈。  
  
##  <a name="UsingDeleteDACWizard"></a> 使用刪除資料層應用程式精靈  
 **使用精靈刪除 DAC**  
  
1.  在 **[物件總管]** 中，展開含有要刪除的 DAC 之執行個體的節點。  
  
2.  展開 **[管理]** 節點。  
  
3.  展開 **資料層應用程式** 節點。  
  
4.  以滑鼠右鍵按一下要刪除的 DAC，然後選取 [刪除資料層應用程式…]   
  
5.  完成精靈對話方塊：  
  
    1.  [簡介](#Introduction)  
  
    2.  [選擇方法](#Choose_method)  
  
    3.  [摘要](#Summary)  
  
    4.  [刪除資料層應用程式](#Delete_datatier_application)  
  
##  <a name="Introduction"></a> 簡介頁面  
 此頁面描述刪除資料層應用程式的步驟。  
  
 **不要再顯示此頁面。** - 按一下此核取方塊，之後就不會再顯示此頁面。  
  
 **下一步 >** - 繼續進行 [選擇方法]  頁面。  
  
 **取消** - 結束精靈，不刪除資料層應用程式或資料庫。  
  
 [使用刪除資料層應用程式精靈](#UsingDeleteDACWizard)  
  
##  <a name="Choose_method"></a> 選擇方法頁面  
 使用此頁面來指定用於處理與要刪除的 DAC 相關聯之資料庫的選項。  
  
 **刪除註冊** - 移除定義資料層應用程式的中繼資料，但讓相關聯的資料庫保持不變。  
  
 **卸離資料庫** - 移除定義資料層應用程式的中繼資料，並卸離相關聯的資料庫。  
  
 該 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體無法再參考資料庫，但資料和記錄檔保持不變。  
  
 **刪除資料庫** - 移除定義 DAC 的中繼資料，並卸除相關聯的資料庫。  
  
 資料庫的資料和記錄檔會遭到永久刪除。  
  
 **< 上一步** - 回到 [簡介]  頁面。  
  
 **下一步 >** - 繼續進行 [摘要]  頁面。  
  
 **取消** - 結束精靈，不刪除 DAC 或資料庫。  
  
 [使用刪除資料層應用程式精靈](#UsingDeleteDACWizard)  
  
##  <a name="Summary"></a> 摘要頁面  
 使用此頁面來檢閱刪除 DAC 執行個體時，精靈將會採取的動作。  
  
 **檢閱選項摘要** - 檢閱顯示在方塊中的 DAC、資料庫與刪除方法。 如果資訊正確，選取 **[下一步]** 或 **[完成]** 來刪除 DAC。 如果 DAC 和資料庫資訊不正確，選取 **[取消]** ，然後選取正確的 DAC。 如果刪除方法不正確，選取 **[上一步]** ，返回 **[選擇方法]** 頁面，然後選取其他方法。  
  
 **< 上一步** - 回到 [選擇方法]  頁面以選擇其他刪除方法。  
  
 **下一步 >** - 使用您在上一頁選擇的方法刪除 DAC 執行個體，然後繼續進行 [刪除資料層應用程式]  頁面。  
  
 **取消** - 結束精靈，不刪除 DAC 執行個體。  
  
 [使用刪除資料層應用程式精靈](#UsingDeleteDACWizard)  
  
##  <a name="Delete_datatier_application"></a> 刪除資料層應用程式頁面  
 此頁面會報告刪除作業成功或失敗。  
  
 **刪除 DAC** - 報告為刪除 DAC 執行個體所採取的每個動作成功或失敗。 檢閱資訊以判斷每個動作成功或失敗。 發生錯誤的所有動作在 **[結果]** 資料行中都會有一個連結。 選取連結來檢視該動作的錯誤報告。  
  
 **儲存報表** - 選取此按鈕可以將刪除報告儲存到 HTML 檔案。 此檔案會報告每個動作的狀態，包括所有動作所產生的所有錯誤。 預設資料夾為 Windows 帳戶之文件資料夾中的 SQL Server Management Studio\DAC Packages 資料夾。  
  
 **完成** - 結束精靈。  
  
 [使用刪除資料層應用程式精靈](#UsingDeleteDACWizard)  
  
##  <a name="DeleteDACPowerShell"></a> 使用 PowerShell 刪除 DAC  
 **使用 PowerShell 指令碼刪除 DAC**  
  
1.  建立 SMO Server 物件，並將它設定為包含要刪除之 DAC 的執行個體。  
  
2.  開啟 **ServerConnection** 物件，並連接到相同的執行個體。  
  
3.  使用 **add_DacActionStarted** 和 **add_DacActionFinished** 訂閱 DAC 升級事件。  
  
4.  指定要刪除的 DAC。  
  
5.  請根據適用的刪除選項，使用下列其中一組程式碼：  
  
    -   若要刪除 DAC 註冊但讓資料庫保持不變，請使用 **Unmanage()** 方法。  
  
    -   若要刪除 DAC 註冊並卸離資料庫，請使用 **Uninstall()** 方法並指定 **DetachDatabase**。  
  
    -   若要刪除 DAC 註冊並卸除資料庫，請使用 **Uninstall()** 方法並指定 **DropDatabase**。  
  
### <a name="example-deleting-the-dac-but-leaving-the-database-powershell"></a>刪除 DAC 但保留資料庫的範例 (PowerShell)  
 下列範例使用 **Unmanage()** 方法刪除 DAC 但讓資料庫保持不變，以刪除名為 MyApplication 的 DAC。  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Subscribe to the DAC delete events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "MyApplication"  
  
## Only delete the DAC definition from msdb, the associated database remains active.  
$dacstore.Unmanage($dacName)  
```  
  
 [使用 PowerShell 刪除 DAC](#DeleteDACPowerShell)  
  
### <a name="example-deleting-the-dac-and-detaching-the-database-powershell"></a>刪除 DAC 並卸離資料庫的範例 (PowerShell)  
 下列範例使用 **Uninstall()** 方法刪除 DAC 並卸離資料庫，以刪除名為 MyApplication 的 DAC。  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Subscribe to the DAC delete events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "MyApplication"  
  
## Delete the DAC definition from msdb and detach the associated database.  
$dacstore.Uninstall($dacName, [Microsoft.SqlServer.Management.Dac.DacUninstallMode]::DetachDatabase)  
```  
  
 [使用 PowerShell 刪除 DAC](#DeleteDACPowerShell)  
  
### <a name="example-deleting-the-dac-and-dropping-the-database-powershell"></a>刪除 DAC 並卸除資料庫的範例 (PowerShell)  
 下列範例使用 **Uninstall()** 方法刪除 DAC 並卸除資料庫，以刪除名為 MyApplication 的 DAC。  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Subscribe to the DAC delete events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "MyApplication"  
  
## Delete the DAC definition from msdb and drop the associated database.  
## $dacstore.Uninstall($dacName, [Microsoft.SqlServer.Management.Dac.DacUninstallMode]::DropDatabase)  
```  
  
 [使用 PowerShell 刪除 DAC](#DeleteDACPowerShell)  
  
## <a name="see-also"></a>另請參閱  
 [資料層應用程式](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [資料層應用程式](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [部署資料層應用程式](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [將資料庫註冊為 DAC](../../relational-databases/data-tier-applications/register-a-database-as-a-dac.md)   
 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [資料庫卸離與附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
