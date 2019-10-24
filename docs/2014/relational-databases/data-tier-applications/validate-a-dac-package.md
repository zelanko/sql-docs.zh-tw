---
title: 驗證 DAC 封裝 | Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- data-tier application [SQL Server], validate
- data-tier application [SQL Server], compare
- validate DAC
- compare DACs
- data-tier application [SQL Server], view
- view DAC
ms.assetid: 726ffcc2-9221-424a-8477-99e3f85f03bd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 56655f7d75635668d266b44853fc29969fd741ed
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782673"
---
# <a name="validate-a-dac-package"></a>驗證 DAC 封裝
  最好先檢閱 DAC 封裝的內容，再將它部署至實際執行環境，以及先驗證升級動作，再升級現有 DAC。 當您部署的封裝之前不是在組織內開發時，特別會是這個情況。  
  
1.  **Before you begin:**  [Prerequisites](#Prerequisites)  
  
2.  **使用下列項目，升級 DAC**  [檢視 DAC 內容](#ViewDACContents)、 [檢視資料庫變更](#ViewDBChanges)、 [檢視升級動作](#ViewUpgradeActions)、 [Compare DACs](#CompareDACs)  
  
##  <a name="Prerequisites"></a> Prerequisites  
 建議您不要部署來源不明或來源不受信任的 DAC 封裝。 這類 DAC 可能包含惡意程式碼，因此可能會執行非預期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，或是修改結構描述而造成錯誤。 使用來源不明或來源不受信任的 DAC 之前，請先將它部署到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的隔離測試執行個體，並在資料庫上執行 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)，然後檢查資料庫中的程式碼，例如預存程序或其他使用者定義的程式碼。  
  
##  <a name="ViewDACContents"></a> 檢視 DAC 內容  
 有兩個機制可檢視資料層應用程式 (DAC) 封裝的內容。 您可以在 SQL Server Developer Tools 中將 DAC 封裝匯入 DAC 專案。 您可以將封裝的內容解除封裝到資料夾中。  
  
 **在 SQL Server Developer Tools 中檢視 DAC**  
  
1.  開啟 [檔案] 功能表，選取 [開新檔案]，然後選取 [專案...]。  
  
2.  選取 **[SQL Server]** 專案範本，並指定 **[名稱]** 、 **[位置]** 及 **[方案名稱]** 。  
  
3.  在 [方案總管] 中，以滑鼠右鍵按一下專案節點，然後選取 [屬性...]。  
  
4.  在 [專案設定] 索引標籤的 [輸出類型] 區段中，選取 [資料層應用程式 (.dacpac 檔案)] 核取方塊，然後關閉屬性對話方塊。  
  
5.  在 [方案總管] 中，以滑鼠右鍵按一下專案節點，然後選取 [匯入資料層應用程式...]。  
  
6.  使用方案總管開啟 DAC 中的所有檔案，例如伺服器選取原則和部署前後指令碼。  
  
7.  使用 **[結構描述檢視]** 檢閱結構描述中的所有物件，特別是檢閱函數或預存程序這類物件中的程式碼時。  
  
 **檢視資料夾中的 DAC**  
  
-   遵循 [Unpack a DAC Package](unpack-a-dac-package.md)中的指示，將 DAC 封裝解壓縮至資料夾。  
  
-   在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的 [ [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器] 中開啟 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]指令碼以檢視其內容。  
  
-   使用記事本這類工具檢視文字檔的內容。  
  
##  <a name="ViewDBChanges"></a> 檢視資料庫變更  
 將 DAC 的目前版本部署至實際執行環境之後，直接對相關聯資料庫進行的變更可能會與新版 DAC 中所定義的結構描述衝突。 升級至新版 DAC 之前，請確認是否已經對資料庫進行這類變更。  
  
 **使用精靈檢視資料庫變更**  
  
1.  執行 [升級資料層應用程式精靈]，同時指定目前部署的 DAC 以及含有新版 DAC 的 DAC 封裝。  
  
2.  在 **[偵測變更]** 頁面上，檢閱已對資料庫進行之變更的報表。  
  
3.  如果您不想要繼續升級，請選取 **[取消]** 。  
  
4.  如需使用精靈的詳細資訊，請參閱 [升級資料層應用程式](upgrade-a-data-tier-application.md)。  
  
### <a name="view-database-changes-by-using-powershell"></a>使用 PowerShell 檢視資料庫變更
  
1.  建立 SMO Server 物件，並將它設定為包含要檢視之 DAC 的執行個體。  
  
2.  開啟 `ServerConnection` 物件，並連接到相同的執行個體。  
  
3.  指定變數中的 DAC 名稱。  
  
4.  使用 `GetDatabaseChanges()` 方法擷取 `ChangeResults` 物件，並將該物件以管道傳送至文字檔以產生新的、已刪除和已變更之物件的簡單報表。  
  
### <a name="view-database-changes-example-powershell"></a>檢視資料庫變更範例 (PowerShell)
  
 下列範例報告在已部署的 DAC (名稱為 MyApplicaiton) 中所做的任何資料庫變更。  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Specify the DAC instance name.  
$dacName  = "MyApplication"  
  
## Generate the change list and save to file.  
$dacChanges = $dacstore.GetDatabaseChanges($dacName) | Out-File -Filepath C:\DACScripts\MyApplicationChanges.txt  
```  
  
##  <a name="ViewUpgradeActions"></a> 檢視升級動作  
 使用新版 DAC 封裝升級從舊版 DAC 封裝部署的 DAC 之前，可以產生一份報表，其中包含會在升級期間執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，然後檢閱這些陳述式。  
  
 **使用精靈來報告升級動作**  
  
1.  執行 [升級資料層應用程式精靈]，同時指定目前部署的 DAC 以及含有新版 DAC 的 DAC 封裝。  
  
2.  在 **[摘要]** 頁面上，檢閱升級動作的報表。  
  
3.  如果您不想要繼續升級，請選取 **[取消]** 。  
  
4.  如需使用精靈的詳細資訊，請參閱 [升級資料層應用程式](upgrade-a-data-tier-application.md)。  
  
 **使用 PowerShell 來報告升級動作**  
  
1.  建立 SMO Server 物件，並將它設定為包含已部署之 DAC 的執行個體。  
  
2.  開啟 `ServerConnection` 物件，並連接到相同的執行個體。  
  
3.  使用 `System.IO.File` 以載入 DAC 封裝檔案。  
  
4.  指定變數中的 DAC 名稱。  
  
5.  使用 `GetIncrementalUpgradeScript()` 方法以取得升級要執行的 Transact-SQL 陳述式清單，並將該清單以管道傳送至文字檔。  
  
6.  關閉用來讀取 DAC 封裝檔案的檔案資料流。  
  
### <a name="view-upgrade-actions-example-powershell"></a>檢視升級動作範例 (PowerShell)
  
 下列範例報告 Transact-SQL 陳述式，可執行以將 DAC (名稱為 MyApplicaiton) 升級至 MyApplicationVNext.dacpac 檔案中所定義的結構描述。  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = Get-Item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplicationVNext.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Specify the DAC instance name.  
$dacName  = "MyApplication"  
  
## Generate the upgrade script and save to file.  
$dacstore.GetIncrementalUpgradeScript($dacName, $dacType) | Out-File -Filepath C:\DACScripts\MyApplicationUpgrade.sql  
  
## Close the filestream to the new DAC package.  
$fileStream.Close()  
```  
  
##  <a name="CompareDACs"></a> Compare DACs  
 在升級 DAC 之前，最好先檢閱目前 DAC 與新 DAC 之間的資料庫和執行個體層級物件的差異。 如果您沒有目前 DAC 封裝的複本，您可以從目前的資料庫擷取封裝。  
  
 如果您在 SQL Server Developer Tools 中將這兩個 DAC 封裝匯入至 DAC 專案，則可以使用結構描述比較工具來分析這兩個 DAC 的差異。  
  
 您也可以將 DAC 解除封裝至不同的資料夾。 然後您可以使用差異工具 (如 WinDiff 公用程式) 來分析差異。  
  
## <a name="see-also"></a>請參閱  
 [資料層應用程式](data-tier-applications.md)   
 [部署資料層應用程式](deploy-a-data-tier-application.md)   
 [升級資料層應用程式](upgrade-a-data-tier-application.md)  
