---
title: "PowerShell scripting in Analysis Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 60bb9610-7229-42eb-a95f-a377268a8720
caps.latest.revision: 44
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 44
---
# PowerShell scripting in Analysis Services
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 包括 PowerShell 元件，可巡覽、管理及查詢 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器、表格式及多維度物件：  
  
-   **SQLAS** 提供者可用於物件階層導覽，並會在您具有 Analysis Services 的任何本機執行個體時提供使用 (與伺服器模式無關)。  
  
-   **SQLASCMDLETS** 模組提供工作特定的 Cmdlet (例如備份、還原、處理)，以及可接受任何 ASSL/XMLA 或表格式模型指令碼語言 (TMSL) 查詢或指令碼輸入檔的一般用途 [Invoke-ASCmd Cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)。  
  
 這兩個元件會實作 Analysis Services 管理物件 ([Microsoft.AnalysisServices 命名空間](http://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx)) 管理介面的子集，提供用於管理及建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的 Cmdlet。  這兩者都是 SQL Server **SQLPS** 根模組的延伸模組。 若要使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] PowerShell 元件，請從匯入 **SQLPS** 開始。 您可以在 [Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md)找到語法和所有 Cmdlet 的範例。  如需如何以 PowerShell 使用 AMO 類型建立表格式資料庫的範例，請參閱 [AMO PowerShell Example](../../analysis-services/powershell/amo-powershell-example.md)。  
  
##  <a name="bkmk_prereq"></a> 步驟 1：安裝 PowerShell 元件  
 取得 PowerShell 的建議方法是安裝 SQL Server Management Studio (SSMS)。 此方法提供適用於 SQL Server 的 PowerShell 模組和 Analysis Services Management (AMO) 資料提供者。 SSMS 也會為您提供工具，能夠輕鬆地產生 XMLA 和 TMSL 輸入，進而運用在 PowerShell。  
  
 請考慮安裝 Analysis Services 的本機執行個體。 本機執行個體讓您即使未曾使用 **SQLAS** 提供者裝載資料庫，也能透過其導覽物件階層。  
  
1.  請前往  [Download SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/mt238290.aspx) (下載 SQL Server Management Studio) 取得最新版 Management Studio。 Management Studio 最新版本 包括已更新的 AMO，對於建立於相容性層級 1200 的表格式模型支援表格式中繼資料物件定義。  
  
2.  安裝 Management Studio 後，請開啟 PowerShell 視窗。 不一定要是管理視窗。  
  
3.  輸入 `Get-Module -ListAvailable` 以確認清單中有 **SQLPS** 和 **SQLASCMDLETS** 模組。  
  
     除非您也安裝了 Analysis Services 的本機執行個體 (表格式或多維度模式)，否則不會看到 **SQLAS**。  
  
4.  輸入 `Get-Command -Module sqlascmdlets` 以產生 Analysis Services 管理中使用的 Cmdlet 清單。  
  
     即使遺漏**SQLASCMDLETS** 提供者，依然可以使用 **SQLASCMDLETS** 。  
  
    -   [Add-RoleMember 指令程式](../../analysis-services/powershell/add-rolemember-cmdlet.md)  
  
    -   [Backup-ASDatabase 指令程式](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)  
  
    -   [Invoke-ASCmd Cmdlet](../../analysis-services/powershell/invoke-ascmd-cmdlet.md) **-inputfile**  
  
    -   [Invoke-ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)  
  
    -   [Invoke-ProcessCube 指令程式](../../analysis-services/powershell/invoke-processcube-cmdlet.md)  
  
    -   [Invoke-ProcessDimension 指令程式](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)  
  
    -   [Invoke-ProcessPartition 指令程式](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)  
  
    -   [Invoke-ProcessTable Cmdlet](../../analysis-services/powershell/invoke-processtable-cmdlet.md)  
  
    -   [Merge-Partition 指令程式](../../analysis-services/powershell/merge-partition-cmdlet.md)  
  
    -   [New-RestoreFolder 指令程式](../../analysis-services/powershell/new-restorefolder-cmdlet.md)  
  
    -   [New-RestoreLocation 指令程式](../../analysis-services/powershell/new-restorelocation-cmdlet.md)  
  
    -   [Remove-RoleMember 指令程式](../../analysis-services/powershell/remove-rolemember-cmdlet.md)  
  
    -   [Restore-ASDatabase 指令程式](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)  
  
> [!NOTE]  
>  Windows PowerShell 預設會安裝在較新版的 Windows 作業系統上。 建議為 4.0 或更新版本。  
  
## 步驟 2：載入元件已啟動互動式工作階段  
 安裝元件後，加以載入便會啟動互動式工作階段。  
  
1.  輸入 `Import-Module sqlps -DisableNameChecking`，  
  
     載入 SQL Server PowerShell 元件，包括 Analysis Services 的元件，並隱藏動詞名稱無效的警告。  
  
2.  輸入 `sqlserver:`  
  
     您應該會看到提示變更為 **PS SQLSERVER:\\>**。  
  
3.  如果 Analysis Services 安裝在本機，則可以巡覽物件階層。 輸入 `cd sqlas` 即可開啟 **SQLAS** 提供者。  
  
4.  鍵入 `dir` 以列出 Analysis Services 執行個體。 提供者不會區分表格式和多維度執行個體。  
  
## Permissions  
 互動式 PowerShell 工作階段會在加以啟動的人員安全性識別下執行。 大多數工作都會要求啟動工作階段的人員同時也是 Analysis Services 伺服器管理員。  
  
 排定的 PowerShell 工作應該視為自動作業。 執行排程器 (例如 SQL Server Agent 服務) 的帳戶很可能必須是 Analysis Services 系統管理員 (取決於工作)。  
  
 本機資料的資料夾 (例如預設備份或資料目錄) 已經設有檔案系統權限，可讓本機執行個體讀取及寫入位置。  
  
 遠端系統管理 (尤其是從未安裝 Analysis Services 的用戶端電腦管理時) 會要求執行動作的遠端 Analysis Services 伺服器執行個體擁有檔案系統權限，可在還原期間讀取檔案，或在備份期間寫入檔案。  
  
## 指令碼輸入檔案：ASSL/XMLA 或 TMSL  
 若您使用 **invoke-ascmd** 執行指令碼，伺服器模式、資料庫類型和相容性層級都會影響您建構指令碼的方式。  
  
-   位於 1050-1103 相容性層級的多維度資料庫和表格式資料庫會回應以 XMLA (使用 Analysis Services 物件定義專屬的 ASSL 延伸模組) 撰寫的指令碼。  
  
-   SQL Server 2016 (相容性層級 1200) 的表格式資料庫會回應 TMSL 指令碼。  
  
 若您在同一個 SQL Server 2016 執行個體混用表格式模型版本，請記得使用正確的指令碼。  
  
> [!NOTE]  
>  指令碼可在 SQL Server Management Studio 中產生，並依需要修改。 位於 1200 相容性層級的表格式資料庫是以 TMSL 撰寫指令碼。 其他則都是以 XMLA/ASSL 撰寫。 表格式模式中的 SQL Server 2016 執行個體支援這兩種指令碼撰寫語言。  
  
## 本機和遠端系統管理  
 透過 PowerShell 指令碼和命令的 Analysis Services 本機系統管理較為簡單，有以下兩個原因：  
  
-   可使用 **SQLAS** 提供者導覽物件階層。  
  
-   允許 Analysis Services 從備份或還原工作的預設資料夾讀取的檔案權限已經就位，並假設您使用這些資料夾當作資料庫位置，還會對作業使用本機伺服器執行個體。  
  
 需要額外組態才能管理遠端執行個體。 下列步驟假設您已完成 Management Studio 的安裝步驟，但服務執行個體位於遠端電腦上。 您必須要有 Analysis Services 伺服器的系統管理員權限。  
  
 因為 Analysis Services 位於遠端，所以沒有 **SQLAS** 可供本機導覽物件階層。 若您從本機資料夾還原檔案，而不是從 Analysis Services 執行個體，就必須建立共用，並將檔案的讀取權限授與伺服器。  
  
1.  開啟系統管理員 PowerShell 視窗。  
  
2.  輸入 `Set-ExecutionPolicy RemoteUnsigned`  
  
3.  在檔案總管中，確認儲存資料檔案的所有資料夾都已共用，而且 Analysis Services 執行個體具有內容的讀取權限。  
  
##  <a name="bkmk_vers"></a> Analysis Services 的支援版本和模式  
 下表顯示不同內容中 Analysis Services PowerShell 的可用性。  
  
|內容|PowerShell 功能可用性|  
|-------------|-------------------------------------|  
|多維度執行個體與資料庫|支援本機和遠端管理。<br /><br /> 合併資料分割需要本機連接。|  
|表格式執行個體與資料庫|在所有相容性層級均獲本機和遠端系統管理支援。<br /><br /> 位於 1200 相容性層級的表格式模型，其 SQLAS Cmdlet 以 JSON 而非 XMLA 使用 Tabular Model Scripting Language (TMSL)。|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 執行個體與資料庫|有限支援。 您可以使用 HTTP 連接和 SQLAS 提供者來檢視執行個體與資料庫資訊。<br /><br /> 但是，不支援使用指令程式。 您無法使用 Analysis Services PowerShell 備份與還原記憶體內部 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫，也不得加入或移除角色、處理資料，或執行任意的 XMLA 指令碼。<br /><br /> 基於組態目的，[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 具有個別提供的內建 PowerShell 支援。 如需詳細資訊，請參閱[Power Pivot for SharePoint 的 PowerShell 參考](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md)。|  
|本機 Cube 的原生連接<br /><br /> “Data Source=c:\backup\test.cub”|不支援。|  
|SharePoint 中 BI 語意模型 (.bism) 連接檔案的 HTTP 連接<br /><br /> “Data Source=http://server/shared_docs/name.bism”|不支援。|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料庫的內嵌連線<br /><br /> “Data Source=$Embedded$”|不支援。|  
|Analysis Services 預存程序中的本機伺服器內容<br /><br /> “Data Source=*”|不支援。|  
  
## 使用 PowerShell 的伺服器管理工作範例  
 **列出伺服器屬性**  
  
 伺服器屬性會以數種方式公開。  若您熟悉以 msmdsrv. ini 或 Management Studio 屬性頁公開的屬性，就會從下方範例看到屬性實際上是從不同物件傳回。  
  
 此指令碼會載入 AMO 伺服器物件。 若您需要完整的屬性名稱，可以執行此指令碼以傳回清單。  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.connect("server-name\instance-name")  
$as.serverproperties  
  
```  
  
 此指令碼會傳回執行個體層級的屬性和方法。 您可以在此清單中讀到 **ServerMode**、 **Version**、 **ProductName**或 **ProductLevel**等值。  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as | get-member  
  
```  
  
 **取得伺服器模式**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.ServerMode  
```  
  
 **取得預設相容性層級**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.DefaultCompatibilityLevel  
```  
  
 **取得資料庫清單**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.databases  
```  
  
 **變更連接埠號碼**  
  
 此指令碼會為具名執行個體建立物件、宣告連接埠、設定連接埠、更新伺服器執行個體、將物件中斷連線，以及重新啟動服務。 您可以開啟新的連線並傳回連接埠，當作驗證步驟。  
  
 您也可以在 msmdsrv.ini 檔案或 Management Studio 的伺服器 [一般屬性] 頁面中驗證連接埠。  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.connect("server-name\instance-name")  
$port = $as.serverproperties['Port']  
$port | select *  
$port.Value = [int]55555  
$as.Update()  
$as.Disconnect()  
restart-service 'MSOLAP$TABULAR'  
$as.connect("server-name\instance-name")  
$port | select *  
  
```  
  
## 請參閱＜  
 [將伺服器系統管理員權限授與 Analysis Services 執行個體](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Analysis Services 中表格式模型的相容性層級](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [表格式模型指令碼語言 &#40;TMSL&#41; 參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [安裝 SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)   
 [使用 PowerShell 管理表格式模型](http://go.microsoft.com/fwlink/?linkID=227685)   
 [設定 Internet Information Services &#40;IIS&#41; 8.0 上 Analysis Services 的 HTTP 存取](../../analysis-services/instances/configure http access to analysis services on iis 8.0.md)  
  
  