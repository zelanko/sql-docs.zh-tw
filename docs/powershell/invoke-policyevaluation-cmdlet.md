---
title: Invoke-PolicyEvaluation Cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, Invoke-PolicyEvaluation
- Policy-Based Management, PowerShell
- Invoke-PolicyEvaluation cmdlet
- Cmdlets [SQL Server], Invoke-PolicyEvaluation
- PowerShell [SQL Server], Invoke-PolicyEvaluation
ms.assetid: 3e6d4f5a-59b7-4203-b95a-f7e692c0f131
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f5adc3571b07e3613514525f286241add73af1a8
ms.lasthandoff: 04/11/2017

---
# <a name="invoke-policyevaluation-cmdlet"></a>Invoke-PolicyEvaluation 指令程式
  **Invoke-PolicyEvaluation** 是一項 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Cmdlet，它會報告 SQL Server 物件的目標集是否符合在一或多個原則式管理原則中所指定的條件。  
  
## <a name="using-invoke-policyevaluation"></a>使用 Invoke-PolicyEvaluation  
 **Invoke-PolicyEvaluation** 會針對稱為目標集的一組 SQL Server 物件評估一或多個原則。 目標物件集來自目標伺服器。 每個原則都會定義一些條件，而它們就是目標物件所允許的狀態。 例如， **可信任的資料庫** 原則表示 TRUSTWORTHY 資料庫屬性必須設定為 OFF。  
  
 **-AdHocPolicyEvaluationMode** 參數會指定採取的動作：  
  
 檢查  
 使用目前登入的認證來報告目標物件的符合狀態。 請勿重新設定任何物件。 這是預設值。  
  
 CheckSqlScriptAsProxy  
 使用 **##MS_PolicyTSQLExecutionLogin##** Proxy 登入的認證來報告目標物件的符合狀態。 請勿重新設定任何物件。  
  
 設定  
 使用目前登入的認證來報告目標物件的符合狀態。 請重新設定任何不符合原則的可設定且具決定性選項。  
  
## <a name="specifying-polices"></a>指定原則  
 指定原則的方式會取決於儲存原則的位置。 您可以使用兩種格式來儲存原則：  
  
-   原則可以是儲存在原則存放區中的物件，例如 Database Engine 的執行個體。 您可以使用 SQLSERVER:\SQLPolicy 資料夾來指定原則存放區中的原則位置。 您可以使用 Windows PowerShell 指令程式來根據屬性篩選輸入原則，例如使用 Where-Object 來依據原則類別目錄篩選，或使用 Get-Item 來依據原則名稱篩選。  
  
-   原則可以匯出成 XML 檔。 您可以使用檔案系統磁碟機 (例如 D:) 來指定 XML 檔的位置。 您可以使用 Where-Object 等 Windows PowerShell 指令程式來依據檔案屬性 (例如檔案名稱) 篩選原則。  
  
 如果原則儲存在原則存放區中，您就必須傳入一組指向要評估之原則的 PSObjects。 您通常可以透過將 Get-Item 等 Cmdlet 的輸出傳送至 **Invoke-PolicyEvaluation**完成此作業，而且不需要指定 **-Policy** 參數。 例如，如果您已將 Microsoft 最佳作法原則匯入 Database Engine 的執行個體中，這個命令就會評估 **資料庫狀態** 原則：  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
Get-Item "Database Status" | Invoke-PolicyEvaluation -TargetServerName "MYCOMPUTER"  
```  
  
 這則範例會示範如何使用 Where-Object 來根據 **PolicyCategory** 屬性篩選原則存放區中的多個原則。 **Invoke-PolicyEvaluation** 會取用 **Where-Object**傳送輸出的物件。  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
gci | Where-Object {$_.PolicyCategory -eq "Microsoft Best Practices: Maintenance"} | Invoke-PolicyEvaluation -TargetServer "MYCOMPUTER"  
```  
  
 如果原則儲存成 XML 檔，您就必須使用 **-Policy** 參數來提供每個原則的路徑和名稱。 如果您沒有在 **-Policy** 參數中指定路徑， **Invoke-PolicyEvaulation** 就會使用 **sqlps** 路徑的目前設定。 例如，這個命令會針對您登入的預設資料庫評估與 SQL Server 一起安裝的其中一個 Microsoft 最佳作法原則：  
  
```  
Invoke-PolicyEvaluation -Policy "C:\Program Files\Microsoft SQL Server\130\Tools\Policies\DatabaseEngine\1033\Database Status.xml" -TargetServerName "MYCOMPUTER"  
```  
  
 這個命令會進行相同的作業，但是它會使用目前的 **sqlps** 路徑來建立原則 XML 檔的位置：  
  
```  
sl "C:\Program Files\Microsoft SQL Server\130\Tools\Policies\DatabaseEngine\1033"  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName "MYCOMPUTER"  
```  
  
 此範例將示範如何使用 **Get-ChildItem** Cmdlet 擷取多個原則 XML 檔，然後將這些物件傳送至 **Invoke-PolicyEvaluation**中：  
  
```  
sl "C:\Program Files\Microsoft SQL Server\130\Tools\Policies\DatabaseEngine\1033"  
gci "Database Status.xml", "Trustworthy Database.xml" | Invoke-PolicyEvaluation -TargetServer "MYCOMPUTER"  
```  
  
## <a name="specifying-the-target-set"></a>指定目標集  
 您可以使用三種參數來指定目標物件集：  
  
-   **-TargetServerName** 會指定包含目標物件的 SQL Server 執行個體。 您可以在使用針對 <xref:System.Data.SqlClient.SqlConnection> 類別之 ConnectionString 屬性所定義格式的字串中指定此資訊。 您可以使用 <xref:System.Data.SqlClient.SqlConnectionStringBuilder> 類別來建立格式正確的連接字串。 您也可以建立 <xref:Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection> 物件，並將它傳遞給 **-TargetServer**。 如果您提供只有伺服器名稱的字串， **Invoke-PolicyEvaluation** 就會使用 Windows 驗證來連接至伺服器。  
  
-   **-TargetObjects** 會使用在目標集中代表 SQL Server 物件的物件或物件陣列。 例如，您可以建立 <xref:Microsoft.SqlServer.Management.Smo.Database> 類別物件的陣列，以傳遞到 **-TargetObjects**。  
  
-   **-TargetExpressions** 會使用字串，其中包含在目標集中指定物件的查詢運算式。 查詢運算式的格式為以 '/' 字元分隔的節點。 每個節點的格式為 ObjectType[Filter]。 物件類型是 SQL Server 管理物件 (SMO) 物件階層中的其中一個物件。 篩選是篩選位於該節點之物件的運算式。 如需詳細資訊，請參閱 [Query Expressions and Uniform Resource Names](../powershell/query-expressions-and-uniform-resource-names.md)。  
  
 請指定 **-TargetObjects** 或 **-TargetExpression**，但不能同時指定。  
  
 這則範例會使用 Sfc.SqlStoreConnection 物件來指定目標伺服器：  
  
```  
sl "C:\Program Files\Microsoft SQL Server\130\Tools\Policies\DatabaseEngine\1033"  
$conn = New-Object Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection("server='MYCOMPUTER';Trusted_Connection=True")  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName $conn  
```  
  
 此範例會使用 **-TargetExpression** 來識別要評估的特定資料庫：  
  
```  
sl "C:\Program Files\Microsoft SQL Server\130\Tools\Policies\DatabaseEngine\1033"  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName "MyComputer" -TargetExpression "Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']"  
```  
  
## <a name="evaluating-analysis-services-policies"></a>評估 Analysis Services 原則  
 若要為 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的執行個體評估原則，您必須在 PowerShell 中載入並註冊組件、使用 Analysis Services 連接物件建立變數，然後將此變數傳遞給 **-TargetObject** 參數。 此範例將示範如何評估 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的最佳作法介面區組態原則：  
  
```  
sl "C:\Program Files\Microsoft SQL Server\130\Tools\Policies\AnalysisServices\1033"  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.AnalysisServices")  
$SSASsvr = new-object Microsoft.AnalysisServices.Server  
$SSASsvr.Connect("Data Source=Localhost")  
Invoke-PolicyEvaluation -Policy "Surface Area Configuration for Analysis Services Features.xml" -TargetObject $SSASsvr  
```  
  
## <a name="evaluating-reporting-services-policies"></a>評估 Reporting Services 原則  
 若要評估 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 原則，您必須在 PowerShell 中載入並註冊組件、使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 連接物件建立變數，然後將此變數傳遞給 **-TargetObject** 參數。 此範例將示範如何評估 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]的最佳作法介面區組態原則：  
  
```  
sl "C:\Program Files\Microsoft SQL Server\130\Tools\Policies\ReportingServices\1033"  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Dmf.Adapters")  
$SSRSsvr = new-object Microsoft.SqlServer.Management.Adapters.RSContainer('MyComputer')  
Invoke-PolicyEvaluation -Policy "Surface Area Configuration for Reporting Services 2008 Features.xml" -TargetObject $SSRSsvr  
```  
  
## <a name="formatting-output"></a>格式化輸出  
 根據預設， **Invoke-PolicyEvaluation** 的輸出會在命令提示字元視窗中以使用者可讀取的格式顯示成精簡報表。 您可以使用 **-OutputXML** 參數，指定此 Cmdlet 要改為將詳細的報表產生成 XML 檔。 **Invoke-PolicyEvaluation** 會使用「系統模組化語言交換格式」(Systems Modeling Language Interchange Format, SML-IF) 結構描述，所以 SML-IF 讀取器可以讀取此檔案。  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
Invoke-PolicyEvaluation -Policy "Datbase Status" -TargetServer "MYCOMPUTER" -OutputXML > C:\MyReports\DatabaseStatusReport.xml  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用 Database Engine Cmdlet](../relational-databases/scripting/use-the-database-engine-cmdlets.md)   
  
  
