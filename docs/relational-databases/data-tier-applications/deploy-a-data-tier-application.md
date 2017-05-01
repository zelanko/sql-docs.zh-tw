---
title: "部署資料層應用程式 | Microsoft 文件"
ms.custom: 
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.deploydacwizard.introduction.f1
- sql13.swb.deploydacwizard.deploydac.f1
- sql13.swb.deploydacwizard.summary.f1
- sql13.swb.deploydacwizard.updateconfiguration.f1
- sql13.swb.deploydacwizard.selectdac.f1
helpviewer_keywords:
- Deploy data-tier application
- deploy DAC
- data-tier application [SQL Server], deploy
- How to [DAC], deploy
- wizard [DAC], deploy
ms.assetid: c117af35-aa53-44a5-8034-fa8715dc735f
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: eeda8a1432ad975caaf74134ce598b0c70c16d29
ms.lasthandoff: 04/11/2017

---
# <a name="deploy-a-data-tier-application"></a>部署資料層應用程式
  您可以使用精靈或 PowerShell 指令碼，將 DAC 封裝中的資料層應用程式 (DAC) 部署到現有的 Database Engine 或 Azure SQL Database 執行個體。 
  
 部署程序會將 DAC 定義儲存到 **msdb** 系統資料庫 ([!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中則是 **master**) 來註冊 DAC 執行個體並建立資料庫，然後使用 DAC 內定義的所有資料庫物件來擴展該資料庫。  
 
  
## <a name="deploy-the-same-dac-package-multiple-times"></a>多次部署相同的 DAC 封裝 
 您可以將相同的 DAC 封裝部署到單一 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體多次，但是一次只能執行一個部署。 針對每個部署指定的 DAC 執行個體名稱在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體中必須是唯一的。  
  
## <a name="managed-instances"></a>受管理的執行個體  
 如果您將 DAC 部署至 Database Engine 的受管理執行個體，下次從執行個體將公用程式收集組傳送到公用程式控制點時，部署的 DAC 就會合併至 **SQL Server 公用程式**。 然後 DAC 會出現在  [公用程式總管] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **[部署的資料層應用程式]** 節點中，並在  詳細資料頁面中報告。  
  
###  <a name="database-options-and-settings"></a>資料庫選項和設定  
 根據預設，部署期間建立的資料庫將會擁有 CREATE DATABASE 陳述式中的所有預設值，但是以下項目除外：  
  
-   資料庫定序和相容性層級設定為 DAC 封裝內所定義的值。 在 SQL Server Developer Tools 中從資料庫專案建立的 DAC 封裝會使用資料庫專案中所設定的值。 從現有的資料庫中擷取的封裝會使用原始資料庫中的值。  
  
-   您可以在 **[更新組態]** 頁面上調整某些資料庫設定，例如資料庫名稱和檔案路徑。 部署至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]時，無法設定檔案路徑。  
  
 某些資料庫選項 (例如 TRUSTWORTHY、DB_CHAINING 和 HONOR_BROKER_PRIORITY) 無法在部署過程中調整。 實體屬性 (如檔案群組數目或檔案數目和大小) 無法在部署過程中更改。 部署完成之後，您可以使用 ALTER DATABASE 陳述式、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 來修改資料庫。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 DAC 可部署至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]或執行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Service Pack 4 (SP4) 或更新版本的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 執行個體。 如果您使用更新版本建立 DAC，則 DAC 可能會包含 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]不支援的物件。 您無法將這些 DAC 部署至 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]執行個體。  
    
## <a name="security-and-permissions"></a>安全性和權限
驗證登入會儲存在 DAC 封裝中，而且沒有密碼。 當您部署或升級此封裝時，此登入會建立為停用的登入，而且會產生密碼。 若要啟用登入，請使用具有 ALTER ANY LOGIN 權限的登入進行登入，並使用 ALTER LOGIN 來啟用登入，然後指派可以傳達給使用者的新密碼。 Windows 驗證登入不需要這項處理，因為這類登入的密碼不是由 SQL Server 所管理。  
  
 只有下列項目的成員才能部署 DAC：**sysadmin** 或 **serveradmin** 固定伺服器角色，或是具有 **dbcreator** 固定伺服器角色及擁有 ALTER ANY LOGIN 權限的登入。 內建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員帳戶 (名稱為 **sa** ) 也可以部署 DAC。 

將具有登入的 DAC 部署至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ，需要 loginmanager 或伺服器管理員 (serveradmin) 角色的成員資格。 將不具有登入的 DAC 部署至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ，需要 dbmanager 或伺服器管理員 (serveradmin) 角色的成員資格。  
  
## <a name="deploy-a-dac-using-the-wizard"></a>使用精靈部署 DAC  
  
1.  在 **[物件總管]**中，展開您要部署 DAC 之執行個體的節點。  
  
2.  以滑鼠右鍵按一下 [資料庫] 節點，然後選取 [部署資料層應用程式…]  
  
3.  完成精靈對話方塊，然後按一下 [完成]。
進一步了解下面的某些精靈頁面： 
     
### <a name="select-dac-package-page"></a>選取 DAC 封裝頁面  
 指定包含要部署之資料層應用程式的 DAC 封裝。 此頁面會在三種狀態之間轉換。  
    
### <a name="select-the-dac-package"></a>選取 DAC 封裝  
 選擇要部署的 DAC 封裝。 DAC 封裝必須是有效的 DAC 封裝檔案，而且必須有 .dacpac 副檔名。  
  
 **DAC 封裝** - 指定包含要部署之資料層應用程式的 DAC 封裝的路徑和檔案名稱。 您可以選取方塊右邊的 **[瀏覽]** 按鈕，瀏覽到 DAC 封裝的位置。  
  
 **應用程式名稱** - 當撰寫 DAC 或是從資料庫擷取 DAC 時，顯示指派之 DAC 名稱的唯讀方塊。  
  
 **版本** - 當撰寫 DAC 或是從資料庫擷取 DAC 時，顯示指派之版本的唯讀方塊。  
  
 **描述** - 當撰寫 DAC 或是從資料庫擷取 DAC 時，顯示撰寫之描述的唯讀方塊。  
  
### <a name="validating-the-dac-package"></a>驗證 DAC 封裝  
 將進度列顯示為確認選定檔案為有效 DAC 封裝的精靈。 如果此 DAC 封裝已經驗證，此精靈會繼續回到最後一版的 **[選取封裝]** 頁面，您可以在此頁面上檢閱驗證的結果。 如果檔案不是有效的 DAC 封裝，精靈會停留在 **[選取 DAC 封裝]**上。 請選取另一個有效的 DAC 封裝，或是取消精靈並產生新的 DAC 封裝。  
  
  ### <a name="review-policy-page"></a>檢閱原則頁面  
 檢閱評估 DAC 伺服器選取原則的結果 (如果使用的話)。 DAC 伺服器選取原則為選擇性，而且當它在 Visual Studio 中建立時會指派給 DAC。 此原則會使用伺服器選取原則 Facet 來指定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體主控 DAC 所應該符合的條件。  
  
 **原則條件的評估結果** - 顯示 DAC 部署原則的條件是否成功。 評估每個條件的結果會在個別行上報告。  
  
 將 DAC 部署至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]時，下列選取伺服器原則永遠評估為 false：作業系統版本、語言、具名管道已啟用、平台和 tcp 已啟用。  
  
 **忽略違反原則** - 使用這個核取方塊可在一個或多個原則條件失敗時繼續部署。 只有當您確定所有失敗的條件都不會阻礙 DAC 作業的成功時，才選取此選項。  
   
### <a name="update-configuration-page"></a>更新組態頁面  
 指定部署作業所建立之部署的 DAC 執行個體和資料庫名稱，並設定資料庫選項。  
  
 **資料庫名稱:** - 指定部署作業所要建立的資料庫名稱。 預設值是擷取 DAC 的來源資料庫名稱。 此名稱在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體內必須是唯一的，且必須符合 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 識別碼的規則。  
  
 如果您變更資料庫名稱，則資料檔和記錄檔的名稱也會變更，以符合新的值。  
  
 資料庫名稱也會當做 DAC 執行個體的名稱使用。 執行個體名稱會顯示在**物件總管**中 [資料層應用程式] 節點或是**公用程式總管**中 [部署的資料層應用程式] 節點底下的 DAC 節點上。  
  
 下列選項不適用於 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]，也不會在部署至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 時顯示。  
  
 **使用預設資料庫位置** - 選取此選項，可在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體的預設位置中建立資料庫資料檔和記錄檔。 檔案名稱將會使用資料庫名稱來建置。  
  
 **指定資料庫檔案** - 選取此選項可針對資料檔和記錄檔指定不同的位置或名稱。  
  
 **資料檔路徑和名稱:** - 為資料檔指定完整路徑和檔案名稱。 此方塊中會填入預設路徑和檔案名稱。 在此方塊中編輯字串來變更預設值，或使用 [瀏覽] 按鈕導覽至放置資料檔的資料夾。  
  
 **記錄檔路徑和名稱:** - 為記錄檔指定完整路徑和檔案名稱。 此方塊中會填入預設路徑和檔案名稱。 在此方塊中編輯字串來變更預設值，或使用 **[瀏覽]** 按鈕導覽至放置記錄檔的資料夾。  
  
###  <a name="Summary"></a> 摘要頁面  
 使用此頁面來檢閱部署 DAC 時，精靈將會採取的動作。  
  
 **將使用以下設定部署您的 DAC** - 檢閱顯示的資訊，以確保採取的動作將會是正確的。 此視窗會顯示您所選取的 DAC 封裝以及您針對部署的 DAC 執行個體所選取的名稱。 此視窗也會顯示當您建立與 DAC 相關聯的資料庫時，將要使用的設定。  
   
### <a name="deploy-page"></a>部署頁面  
 此頁面會報告部署作業成功或失敗。  
  
 **正在部署 DAC** - 報告為了部署 DAC 所採取的每個動作成功或失敗。 檢閱資訊以判斷每個動作成功或失敗。 發生錯誤的所有動作在 **[結果]** 資料行中都會有一個連結。 選取連結來檢視該動作的錯誤報告。  
  
 **儲存報表** - 選取此按鈕可以將部署報告儲存到 HTML 檔案。 此檔案會報告每個動作的狀態，包括所有動作所產生的所有錯誤。 預設資料夾為 Windows 帳戶之文件資料夾中的 SQL Server Management Studio\DAC Packages 資料夾。  
  
  
##  <a name="deploy-a-dac-using-powershell"></a>使用 PowerShell 刪除 DAC  
  
1.  建立 SMO Server 物件，並將它設為您要部署 DAC 的執行個體。  
  
2.  開啟 **ServerConnection** 物件，並連接到相同的執行個體。  
  
3.  使用 **System.IO.File** 以載入 DAC 封裝檔案。  
  
4.  使用 **add_DacActionStarted** 和 **add_DacActionFinished** 訂閱 DAC 部署事件。  
  
5.  設定 **DatabaseDeploymentProperties**。  
  
6.  您可以使用 **DacStore.Install** 方法來部署 DAC。  
  
7.  關閉用來讀取 DAC 封裝檔案的檔案資料流。  
  
## <a name="powershell-examples"></a>PowerShell 範例  
 下列範例使用 MyApplication.dacpac 封裝中 DAC 定義來部署 [!INCLUDE[ssDE](../../includes/ssde-md.md)]之預設執行個體上名為 MyApplication 的 DAC。  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC deployment events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Deploy the DAC and create the database.  
$dacName  = "MyApplication"  
$evaluateTSPolicy = $true  
$deployProperties = New-Object Microsoft.SqlServer.Management.Dac.DatabaseDeploymentProperties($serverconnection,$dacName)  
$dacstore.Install($dacType, $deployProperties, $evaluateTSPolicy)  
$fileStream.Close()  
```  
  
## <a name="more-information"></a>詳細資訊 
 [資料層應用程式](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [從資料庫中擷取 DAC](../../relational-databases/data-tier-applications/extract-a-dac-from-a-database.md)   
 [資料庫識別碼](../../relational-databases/databases/database-identifiers.md)  
  
  

