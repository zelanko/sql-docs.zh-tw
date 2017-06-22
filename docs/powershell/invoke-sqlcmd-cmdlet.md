---
title: Invoke-Sqlcmd Cmdlet | Microsoft Docs
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PowerShell [SQL Server], Invoke-Sqlcmd
- Cmdlets [SQL Server], Invoke-Sqlcmd
- Invoke-Sqlcmd cmdlet
- sqlcmd utility, PowerShell
ms.assetid: 0c74d21b-84a5-4fa4-be51-90f0f7230044
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 679625527f4f29d086b50e2291af4cff14b74d3e
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="invoke-sqlcmd-cmdlet"></a>Invoke-Sqlcmd 指令程式
  **Invoke-Sqlcmd** 是一種執行指令碼的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Cmdlet，該指令碼「包含」了[!INCLUDE[tsql](../includes/tsql-md.md)] sqlcmd **公用程式所支援之語言 (** 及 XQuery) 與命令的陳述式。  
  
## <a name="using-invoke-sqlcmd"></a>使用 Invoke-Sqlcmd  
 **Invoke-Sqlcmd** Cmdlet 可讓您在 Windows PowerShell 環境中執行 **sqlcmd** 指令碼檔案。 **sqlcmd** 可以執行的大多數作業，也可利用 **Invoke-Sqlcmd**進行。  
  
 這是呼叫 Invoke-Sqlcmd 執行簡單查詢的範例，類似於指定 **sqlcmd** 且使用 **-Q** 和 **-S** 選項：  
  
```  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance"  
```  
  
 這是呼叫 **Invoke-Sqlcmd**的範例，其會指定輸入檔案並將輸出傳送至檔案，類似於指定 **sqlcmd** 且使用 **-i** 和 **-o** 選項：  
  
```  
Invoke-Sqlcmd -InputFile "C:\MyFolder\TestSQLCmd.sql" | Out-File -filePath "C:\MyFolder\TestSQLCmd.rpt"  
```  
  
 這是使用 Windows PowerShell 陣列將多個 **sqlcmd** 指令碼變數傳遞至 **Invoke-Sqlcmd**的範例。 用於識別 SELECT 陳述式中 **sqlcmd** 指令碼變數的 "$" 字元，已經使用 PowerShell 反勾號 "`" 逸出字元逸出：  
  
```  
$MyArray = "MyVar1 = 'String1'", "MyVar2 = 'String2'"  
Invoke-Sqlcmd -Query "SELECT `$(MyVar1) AS Var1, `$(MyVar2) AS Var2;" -Variable $MyArray  
```  
  
 這是使用適用於 Windows PowerShell 的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者巡覽至 [!INCLUDE[ssDE](../includes/ssde-md.md)]執行個體，然後使用 Windows PowerShell **Get-Item** Cmdlet 擷取此執行個體的 SMO Server 物件並將其傳遞給 **Invoke-Sqlcmd**的範例：  
  
```  
Set-Location SQLSERVER:\SQL\MyComputer\MyInstance  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance (Get-Item .)  
```  
  
 -Query 參數是位置性參數而且不需要加以命名。 如果傳遞給 **Invoke-Sqlcmd**的第一個字串未命名，就會將其視為 -Query 參數。  
  
```  
Invoke-Sqlcmd "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance"  
```  
  
## <a name="path-context-in-invoke-sqlcmd"></a>Invoke-Sqlcmd 中的路徑內容  
 如果您沒有使用 -Database 參數，Invoke-Sqlcmd 的資料庫內容就會由呼叫此指令程式時作用中的路徑所設定。  
  
|路徑|資料庫內容|  
|----------|----------------------|  
|以磁碟機而非 SQLSERVER: 為開頭|本機電腦上預設執行個體中登入識別碼的預設資料庫。|  
|SQLSERVER:\SQL|本機電腦上預設執行個體中登入識別碼的預設資料庫。|  
|SQLSERVER:\SQL\ComputerName|指定之電腦上預設執行個體中登入識別碼的預設資料庫。|  
|SQLSERVER:\SQL\ComputerName\InstanceName|指定之電腦上指定執行個體中登入識別碼的預設資料庫。|  
|SQLSERVER:\SQL\ComputerName\InstanceName\Databases|指定之電腦上指定執行個體中登入識別碼的預設資料庫。|  
|SQLSERVER:\SQL\ComputerName\InstanceName\Databases\DatabaseName|指定之電腦上指定執行個體中指定的資料庫。 這也適用於較長的路徑，例如指定資料庫內部之 Tables 和 Columns 節點的路徑。|  
  
 例如，假設在本機電腦的預設執行個體中，Windows 帳戶的預設資料庫是 master。 然後，下列命令就會傳回 master：  
  
```  
Set-Location SQLSERVER:\SQL  
Invoke-Sqlcmd "SELECT DB_NAME() AS DatabaseName;"  
```  
  
 下列命令則傳回 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]：  
  
```  
Set-Location SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Person.Person  
Invoke-Sqlcmd "SELECT DB_NAME() AS DatabaseName;"  
```  
  
 當 Invoke-Sqlcmd 使用路徑資料庫內容時，它會提供警告。 您可以使用 -SuppressProviderContextWarning 參數來關閉警告訊息。 您可以使用 -IgnoreProviderContext 參數來告知 Invoke-Sqlcmd 一律使用預設資料庫進行登入。  
  
## <a name="comparing-invoke-sqlcmd-and-the-sqlcmd-utility"></a>比較 Invoke-Sqlcmd 和 sqlcmd 公用程式  
 **Invoke-Sqlcmd** 可用於執行可使用 **sqlcmd** 公用程式執行的許多指令碼。 但是， **Invoke-Sqlcmd** 執行所在的 Windows PowerShell 環境，與 **sqlcmd** 執行所在的命令提示字元環境不同。 **Invoke-Sqlcmd** 的行為已經過修改，可在 Windows PowerShell 環境中工作。  
  
 並非所有的 **sqlcmd** 命令都實作於 **Invoke-Sqlcmd**中。 未實作的命令包含以下項目： **:!!**、 **:connect**、 **:error**、 **:out**、 **:ed**、 **:list**、 **:listvar**、 **:reset**、 **:perftrace**和 **:serverlist**。  
  
 **Invoke-Sqlcmd** 不會初始化 **sqlcmd** 環境或指令碼變數，例如 SQLCMDDBNAME 或 SQLCMDWORKSTATION。  
  
 **Invoke-Sqlcmd** 不會顯示訊息 (例如 PRINT 陳述式的輸出)，除非您指定 Windows PowerShell **-Verbose** 一般參數。 例如：  
  
```  
Invoke-Sqlcmd -Query "PRINT N'abc';" -Verbose  
```  
  
 PowerShell 環境不需要所有的 **sqlcmd** 參數。 例如，Windows PowerShell 會從 Cmdlet 格式化所有輸出，所以 **Invoke-Sqlcmd** 中不會實作指定格式化選項的 **sqlcmd**參數。 下表顯示 **Invoke-Sqlcmd** 參數與 **sqlcmd** 選項之間的關聯性：  
  
|描述|sqlcmd 選項|Invoke-Sqlcmd 參數|  
|-----------------|-------------------|------------------------------|  
|伺服器和執行個體名稱。|-S|-ServerInstance|  
|要使用的初始資料庫。|-d|-Database|  
|執行指定的查詢並結束。|-Q|-Query|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證登入識別碼。|-U|-Username|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證密碼。|-P|-Password|  
|變數定義。|-v|-Variable|  
|查詢逾時間隔。|-t|-QueryTimeout|  
|發生錯誤時停止執行|-b|-AbortOnError|  
|專用管理員連接。|-A|-DedicatedAdministratorConnection|  
|停用互動式命令、啟動指令碼和環境變數。|-X|-DisableCommands|  
|停用變數替代。|-X|-DisableVariables|  
|報表的最小嚴重性層級。|-v|-SeverityLevel|  
|報表的最小錯誤層級。|-m|-ErrorLevel|  
|登入逾時間隔。|-l|-ConnectionTimeout|  
|主機名稱。|-H|-HostName|  
|變更密碼並結束。|-Z|-NewPassword|  
|含有查詢的輸入檔|-i|-InputFile|  
|字元輸出的最大長度。|-w|-MaxCharLength|  
|二進位輸出的最大長度。|-w|-MaxBinaryLength|  
|使用 SSL 加密進行連接|無參數|-EncryptConnection|  
|顯示錯誤|無參數|-OutputSqlErrors|  
|輸出訊息至 stderr。|-r|無參數|  
|使用用戶端的地區設定|-r|無參數|  
|執行指定的查詢並維持執行中狀態。|-Q|無參數|  
|用於輸出資料的字碼頁。|-f|無參數|  
|變更密碼並維持執行中狀態|-Z|無參數|  
|封包大小|-A|無參數|  
|資料行分隔符號|-S|無參數|  
|控制項輸出標頭|-H|無參數|  
|指定控制字元|-k|無參數|  
|固定長度的顯示寬度|-Y|無參數|  
|變動長度的顯示寬度|-Y|無參數|  
|回應輸入。|-e|無參數|  
|啟用引號識別碼|-i|無參數|  
|移除尾端空白|-w|無參數|  
|列出執行個體|-l|無參數|  
|將輸出格式化為 Unicode|-U|無參數|  
|列印統計資料|-P|無參數|  
|命令結束|-c|無參數|  
|使用 Windows 驗證進行連接|-e|無參數|  
  
## <a name="see-also"></a>另請參閱  
 [使用 Database Engine Cmdlet](../relational-databases/scripting/use-the-database-engine-cmdlets.md)   
 [sqlcmd 公用程式](../tools/sqlcmd-utility.md)   
 [使用 sqlcmd 公用程式](../relational-databases/scripting/sqlcmd-use-the-utility.md)  
  
  

