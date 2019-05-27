---
title: Analysis Services PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 03/11/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 60bb9610-7229-42eb-a95f-a377268a8720
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e3c8eda71783e7211011bd6f67d9acf638c8946a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66062515"
---
# <a name="analysis-services-powershell"></a>Analysis Services PowerShell
  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 包含 Analysis Services PowerShell (SQLAS) 提供者和指令程式，讓您可以使用 Windows PowerShell 來導覽、管理和查詢 Analysis Services 物件。  
  
 Analysis Services PowerShell 是由下列項目所構成：  
  
-   用於導覽分析管理物件 (AMO) 階層的 `SQLAS` 提供者。  
  
-   用於執行 MDX、DMX 或 XMLA 指令碼的 `Invoke-ASCmd` 指令程式。  
  
-   例行作業的工作特定指令程式，例如處理、角色管理、資料分割管理、備份和還原。  
  
## <a name="in-this-article"></a>本文內容  
 [必要條件](#bkmk_prereq)  
  
 [支援的版本和模式的 Analysis Services](#bkmk_vers)  
  
 [驗證需求和安全性考量](#bkmk_auth)  
  
 [Analysis Services PowerShell 工作](#bkmk_tasks)  

如需有關語法與範例的詳細資訊，請參閱 < [Analysis Services PowerShell Reference](/sql/analysis-services/powershell/analysis-services-powershell-reference)。

##  <a name="bkmk_prereq"></a> 必要條件  
 您必須安裝 Windows PowerShell 2.0。 此元件預設安裝在較新版的 Windows 作業系統上。 如需詳細資訊，請參閱[安裝 Windows PowerShell 2.0](https://msdn.microsoft.com/library/ff637750.aspx)

<!-- ff637750.aspx above is linked to by:  (https://go.microsoft.com/fwlink/?LinkId=227613). -->
  
 您必須安裝包含 SQL Server PowerShell (SQLPS) 模組與用戶端程式庫的 SQL Server 功能。 最簡單的安裝方式是安裝 SQL Server Management Studio，其中就會自動包含 PowerShell 功能與用戶端程式庫。 SQL Server PowerShell (SQLPS) 模組包含所有 SQL Server 功能的 PowerShell 提供者和指令程式，包括 SQLASCmdlets 模組和 SQLAS 提供者 (用於導覽 Analysis Services 物件階層)。  
  
 您必須匯入**SQLPS**模組，才能使用`SQLAS`提供者和 cmdlet。 SQLAS 提供者是延伸模組的`SQLServer`提供者。 匯入 SQLPS 模組的方式有許多種。 如需詳細資訊，請參閱 [匯入 SQLPS 模組](../../2014/database-engine/import-the-sqlps-module.md)。  
  
 您必須啟用遠端管理和檔案共用，才能從遠端存取 Analysis Services 執行個體。 如需詳細資訊，請參閱 <<c0> [ 啟用遠端管理](#bkmk_remote)本主題中。  
  
##  <a name="bkmk_vers"></a> Analysis Services 的支援版本和模式  
 目前，在 Windows Server 2008 R2、Windows Server 2008 SP1 或 Windows 7 上執行的任何 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Analysis Services 版本都支援 Analysis Services PowerShell。  
  
 下表顯示不同內容中 Analysis Services PowerShell 的可用性。  
  
|內容|PowerShell 功能可用性|  
|-------------|-------------------------------------|  
|多維度執行個體與資料庫|支援本機和遠端管理。<br /><br /> 合併資料分割需要本機連接。|  
|表格式執行個體與資料庫|支援本機和遠端管理。<br /><br /> 如需詳細資訊，請參閱 2011 年 8 月部落格的相關[管理表格式模型使用 PowerShell](https://go.microsoft.com/fwlink/?linkID=227685)。|  
|PowerPivot for SharePoint 執行個體與資料庫|有限支援。 您可以使用 HTTP 連接和 SQLAS 提供者來檢視執行個體與資料庫資訊。<br /><br /> 但是，不支援使用指令程式。 您不得使用 Analysis Services PowerShell 備份與還原記憶體中 InMemory PowerPivot 資料庫，也不得加入或移除角色、處理資料，或執行任意的 XMLA 指令碼。<br /><br /> 基於組態目的，PowerPivot for SharePoint 具有個別提供的內建 PowerShell 支援。 如需詳細資訊，請參閱 < [powerpivot for SharePoint 的 PowerShell 參考](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)。|  
|本機 Cube 的原生連接<br /><br /> "Data Source=c:\backup\test.cub"|不支援。|  
|SharePoint 中 BI 語意模型 (.bism) 連接檔案的 HTTP 連接<br /><br /> "Data Source=http://server/shared_docs/name.bism"|不支援。|  
|PowerPivot 資料庫的內嵌連接<br /><br /> "Data Source=$Embedded$"|不支援。|  
|Analysis Services 預存程序中的本機伺服器內容<br /><br /> "Data Source=*"|不支援。|  
  
##  <a name="bkmk_auth"></a> 驗證需求和安全性考量  
 連接至 Analysis Services 時，您必須使用 Windows 使用者識別建立連接。 在大部分情況下，您是使用 Windows 整合式安全性建立連接，其中目前的使用者識別會設定用來執行伺服器作業的安全性內容。 不過，當您設定 Analysis Services 的 HTTP 存取時，其他驗證方法會變成可以使用。 本節說明連接類型如何決定您可以使用的驗證選項。  
  
 Analysis Services 連接的特性會以原生連接或 HTTP 連接來辨別。 原生連接是從用戶端應用程式到伺服器的直接連接。 在 PowerShell 工作階段中，PowerShell 用戶端會使用 OLE DB Provider for Analysis Services 直接連接至 Analysis Services 執行個體。 原生連接一律是使用 Windows 整合式安全性所建立，其中 Analysis Services PowerShell 會以目前使用者的身分執行。 Analysis Services 不支援模擬。 如果您要以特定使用者的身分執行作業，則必須以該使用者的身分啟動 PowerShell 工作階段。  
  
 HTTP 連接則是間接透過 IIS 建立，讓其他驗證選項 (例如基本驗證) 連接至 Analysis Services 執行個體。 IIS 支援模擬，因此您可以提供一個連接字串，其中包含建立連接時 IIS 將用來模擬的認證。 若要提供認證，您可以使用-Credential 參數。  
  
 **使用-Credential 參數在 PowerShell 中**  
  
 -Credential 參數會採用 PSCredential 物件，指定使用者名稱和密碼。 在 Analysis Services PowerShell 中，-Credential 參數可對 Analysis Services 中的連線要求，而不是現有連接的內容中執行的 cmdlet 的 cmdlet。 提出連接連接要求的指令程式包括 Invoke-ASCmd、Backup-ASDatabase 和 Restore-ASDatabase。 這些 cmdlet，如-Credential 參數可以使用，假設符合下列準則：  
  
1.  伺服器會設定成 HTTP 存取，也就是說，IIS 會處理連接、讀取使用者名稱和密碼，並在連接到 Analysis Services 時模擬該使用者識別。 如需詳細資訊，請參閱 [設定 Internet Information Services &#40;IIS&#41; 8.0 上 Analysis Services 的 HTTP 存取](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)(Microsoft BI 驗證及識別委派)。  
  
2.  針對 Analysis Services HTTP 存取建立的 IIS 虛擬目錄會設定成基本驗證。  
  
3.  認證物件所提供的使用者名稱和密碼會解析 Windows 使用者識別。 Analysis Services 會以目前使用者的身分使用此識別。 如果使用者不是 Windows 使用者，或缺少執行所要求之作業的足夠權限，則要求將會失敗。  
  
 若要建立認證物件，您可以使用 Get-Credential 指令程式，向操作員收集認證。 接著，您可以在命令中使用連接至 Analysis Services 的認證物件。 下列範例將說明其中一個方法。 在此範例中，本機執行個體的連接會設定成 HTTP 存取。  
  
```  
PS SQLSERVER:\SQLAS\HTTP_DS> $cred = Get-credential adventureworks\dbadmin  
PS SQLSERVER:\SQLAS\HTTP_DS> Invoke-ASCmd -Inputfile:"c:\discoverconnections.xmla" -Credential:$cred  
```  
  
 使用基本驗證時，您應該一律搭配 SSL 使用 HTTPS，才能透過加密的連接傳送使用者名稱和密碼。 如需詳細資訊，請參閱 <<c0> [ 設定安全通訊端層在 IIS 7.0](https://go.microsoft.com/fwlink/?linkID=184299)並[設定基本驗證 (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=230776)。  
  
 請記住，您在 PowerShell 中所提供的認證、查詢和命令會原封不動地傳遞至傳輸層。 在指令碼中加入敏感內容會增加惡意插入攻擊的風險。  
  
 **當做 Microsoft.Secure.String 物件提供密碼**  
  
 有些作業 (例如備份與還原) 支援您在命令中提供密碼時所啟用的加密選項。 提供密碼會向 Analysis Services 發出加密或解密備份檔的訊號。 在 Analysis Services 中，此密碼會當做安全的字串物件具現化。 下列範例說明如何在執行階段向操作員收集密碼。  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default> $pwd = read-host -AsSecureString -Prompt "Password"  
Password: ****  
PS SQLSERVER:\SQLAS\Localhost\default> $pwd -is [System.IDisposable]   
True  
```  
  
 您現在可以備份或還原加密的資料庫，並將 $pwd 變數傳遞給密碼參數。 若要檢視結合此說明與其他 cmdlet 的完整範例，請參閱[Backup-asdatabase 指令程式](/sql/analysis-services/powershell/backup-asdatabase-cmdlet)並[Restore-asdatabase cmdlet](/sql/analysis-services/powershell/restore-asdatabase-cmdlet)。
  
 後續步驟是，從工作階段中移除密碼和變數。  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default> $pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default> Remove-Variable -Name pwd  
```  
  
##  <a name="bkmk_tasks"></a> Analysis Services PowerShell 工作  
 您可以從 Windows PowerShell 管理命令介面或 Windows 命令提示字元執行 Analysis Services PowerShell。 不支援從 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 執行 Analysis Services PowerShell。  
  
 本節將描述使用 Analysis Services PowerShell 的一般工作。  
  
-   [載入 Analysis Services 提供者和 Cmdlet](#bkmk_load)  
  
-   [啟用遠端管理](#bkmk_remote)  
  
-   [連接到 Analysis Services 物件](#bkmk_connect)  
  
-   [管理服務](#bkmk_admin)  
  
-   [取得 Analysis Services PowerShell 的說明](#bkmk_help)  
  
###  <a name="bkmk_load"></a> 載入 Analysis Services 提供者和 Cmdlet  
 Analysis Services 提供者是 SQL Server 根提供者的延伸模組，它會在您匯入 SQLPS 模組之後變成可用狀態。 系統會同時載入 Analysis Services 指令程式。不過，如果您想要使用指令程式而不使用提供者，也可以單獨載入它們。  
  
-   若要載入包含所有 Analysis Services PowerShell 功能的 SQLPS，請執行 Import-module 指令程式。 如果您無法匯入此模組，可以針對載入模組的目的，暫時將執行原則變更為不受限制。 如需詳細資訊，請參閱 [匯入 SQLPS 模組](../../2014/database-engine/import-the-sqlps-module.md)。  
  
    ```  
    Import-module "sqlps"  
    ```  
  
     或者，您也可以使用 `import-module "sqlps" -disablenamechecking` 來隱藏有關未核准之動詞名稱的警告。  
  
-   若要單獨載入工作專用的 Analysis Services 指令程式，而不載入 Analysis Services 提供者或 Invoke-ASCmd 指令程式，您可以用獨立作業的方式載入 SQLASCmdlets 模組。  
  
    ```  
    Import-module "sqlascmdlets"  
    ```  
  
###  <a name="bkmk_remote"></a> 啟用遠端管理  
 您必須先啟用遠端管理和檔案共用，然後才能使用 Analysis Services PowerShell 搭配遠端 Analysis Services 執行個體。 下列的錯誤表示防火牆組態問題：*RPC 伺服器無法使用。 (來自 HRESULT 的例外狀況：0x800706BA) 」。  
  
1.  確認本機和遠端電腦都有 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 版本的用戶端與伺服器工具。  
  
2.  在裝載 Analysis Services 執行個體的遠端伺服器上，於 Windows 防火牆中開啟 TCP 通訊埠 2383。 如果您將 Analysis Services 安裝成具名執行個體或者正在使用自訂通訊埠，此通訊埠編號將會不同。 如需詳細資訊，請參閱 [設定 Windows 防火牆以允許 Analysis Services 存取](instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)。  
  
3.  在遠端伺服器上，確認下列服務已經啟動：遠端程序呼叫 (RPC) 服務、 TCP/IP NetBIOS Helper 服務、 Windows Management Instrumentation (WMI) 服務、 Windows 遠端管理 (Ws-management) 服務。  
  
4.  在遠端伺服器上，啟動 [群組原則物件編輯器] 嵌入式管理單元 (gpedit.msc)。  
  
5.  依序開啟 [電腦設定]、[系統管理範本]、[網路]、[網路連線]、[Windows 防火牆] 和 [網域設定檔]。  
  
6.  按兩下**Windows 防火牆：允許輸入遠端系統管理例外狀況**，選取**Enabled**，然後按一下**確定**。  
  
7.  按兩下**Windows 防火牆：允許輸入的檔案及印表機共用例外狀況**，選取**Enabled**，然後按一下**確定**。  
  
8.  在具有用戶端工具的本機電腦，請使用下列 cmdlet 來確認遠端管理，以實際的伺服器名稱取代*遠端伺服器名稱*預留位置。 如果 Analysis Services 安裝成預設執行個體，請省略執行個體名稱。 您先前必須匯入 SQLPS 模組，才能讓此命令運作。  
  
    ```  
    PS SQLSERVER:\> cd sqlas  
    PS SQLSERVER:\sqlas> cd <remote-server-name\instance-name>  
    PS SQLSERVER:\sqlas\<remote-server-name\instance-name> dir  
    ```  
  
 在某些情況下，可能需要額外的設定。 您可能必須在遠端伺服器上輸入下列命令，然後才能從另一部電腦發出命令至遠端伺服器：  
  
```  
Enable-psremoting  
```  
  
  
###  <a name="bkmk_connect"></a> 連接到 Analysis Services 物件  
 Analysis Services PowerShell 提供者支援導覽 Analysis Services 物件階層，而且它會設定執行命令的內容。 此提供者是透過 SQLPS 模組提供之 SQLSERVER 根提供者的延伸模組。 載入 SQLPS 模組之後，您就可以導覽路徑。  
  
 您可以連接到本機或遠端執行個體，但是某些指令程式只能在本機執行個體上執行 (亦即 merge-partition)。 您可以針對設定為 HTTP 存取的 Analysis Services 伺服器使用原生連接或 HTTP 連接。 下圖顯示原生和 HTTP 連接的導覽路徑。 下圖顯示原生和 HTTP 連接的導覽路徑。  
  
 **Analysis Services 的原生連接**  
  
 ![原生連接到 Analysis Services](media/ssas-powershell-nativeconnection.gif "Analysis Services 的原生連接")  
  
 下列範例示範如何使用原生連接來導覽物件階層。 您可以從提供者發出 `dir` 來檢視執行個體資訊。 您可以使用 `cd` 來檢視該執行個體的物件。  
  
```  
PS SQLSERVER:> cd sqlas  
PS SQLSERVER\sqlas:> dir  
PS SQLSERVER\sqlas:> cd localhost\default  
PS SQLSERVER\sqlas\localhost\default:> dir  
```  
  
 您應該會看到下列集合：組件、 資料庫、 角色和追蹤。 如果繼續使用 `cd` 和 `dir`，您就可以檢視每個集合的內容。  
  
 **Analysis Services 的 HTTP 連接**  
  
 ![HTTP 連接到 Analysis Services](media/ssas-powershell-httpconnection.gif "Analysis Services 的 HTTP 連接")  
  
 HTTP 連接就很有用，如果您使用本主題中的指示的 HTTP 存取您伺服器設定：[設定 Internet Information Services &#40;IIS&#41; 8.0 上 Analysis Services 的 HTTP 存取](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
 假設伺服器 URL 的 http://localhost/olap/msmdpump.dll，連接可能會如下所示：  
  
```  
PS SQLSERVER\sqlas:> cd http_ds  
PS SQLSERVER\sqlas\http_ds:> $Url=Encode-SqlName "http://localhost/olap/msmdpump.dll"  
PS SQLSERVER\sqlas\http_ds:> cd $Url  
PS SQLSERVER\sqlas\http_ds\http%3A%2F%2Flocalhost%2olap%2msmdpump%2Edll:> dir  
```  
  
 您應該會看到下列集合：組件、 資料庫、 角色和追蹤。 如果您無法檢視這些集合的內容，請檢查 OLAP 虛擬目錄的驗證設定。 請確定匿名存取已停用。 如果您正在使用 Windows 驗證，請確定 Windows 使用者帳戶擁有 Analysis Services 執行個體的系統管理權限。  
  
###  <a name="bkmk_admin"></a> 管理服務  
 確認服務正在執行。 傳回 SQL Server 服務的狀態、名稱和顯示名稱，包括 Analysis Services (MSSQLServerOLAPService) 和 Database Engine。  
  
```  
Get-service mssql*  
```  
  
 傳回處理序的相關屬性，包括處理序識別碼、控制代碼計數和記憶體使用量：  
  
```  
Get-process msmdsrv  
```  
  
 當您從管理員命令介面發出下列指令程式時，就會重新啟動服務：  
  
```  
Restart-service mssqlserverolapservice  
```  
  
###  <a name="bkmk_help"></a> 取得 Analysis Services PowerShell 的說明  
 您可以使用下列任何指令程式來確認指令程式可用性，並且取得有關服務、處理序和物件的詳細資訊。  
  
1.  `Get-help` 會傳回 Analysis Services 指令程式的內建說明，包括範例：  
  
    ```  
    Get-help invoke-ascmd -examples  
    ```  
  
2.  `Get-command` 會傳回十一個 Analysis Services PowerShell 指令程式的清單：  
  
    ```  
    get-command -module SQLASCmdlets  
    ```  
  
3.  `Get-member` 會傳回服務或處理序的屬性或方法。  
  
    ```  
    Get-service mssqlserverolapservice | get-member -type Property  
    ```  
  
    ```  
    Get-service mssqlserverolapservice | get-member -type Method  
    ```  
  
    ```  
    Get-process msmdsrv | get-member -type Property  
    ```  
  
4.  `Get-member` 也可以搭配 SQLAS 提供者來指定伺服器執行個體，以便傳回物件的屬性或方法 (例如，伺服器物件的 AMO 方法)。  
  
    ```  
    PS SQLSERVER:\sqlas\localhost\default > $serverObj = New-Object Microsoft.AnalysisServices.Server  
    PS SQLSERVER:\sqlas\localhost\default > $serverObj = | get-member -type Method  
    ```  
  
5.  `Get-PSdrive` 會傳回目前已安裝的提供者清單。 如果您匯入了 SQLPS 模組，就會在清單中看見 `SQLServer` 提供者 (SQLAS 屬於 SQLServer 提供者的一部分，永遠不會個別出現在清單中)：  
  
    ```  
    Get-PSDrive  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [安裝 SQL Server PowerShell](../database-engine/install-windows/install-sql-server-powershell.md)   
 [管理表格式的模型使用 PowerShell （部落格）](https://go.microsoft.com/fwlink/?linkID=227685)   
 [設定 Internet Information Services &#40;IIS&#41; 8.0 上 Analysis Services 的 HTTP 存取](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
  
