---
title: 使用 SQL Server PowerShell 路徑 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: f31d8e2c-8d59-4fee-ac2a-324668e54262
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5ca7d915b940296e6de6689e666401b0c3534c9d
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782724"
---
# <a name="work-with-sql-server-powershell-paths"></a>使用 SQL Server PowerShell 路徑
  當您導覽至 [!INCLUDE[ssDE](../includes/ssde-md.md)] 提供者路徑中的節點之後，即可使用與該節點相關聯之 [!INCLUDE[ssDE](../includes/ssde-md.md)] 管理物件的方法與屬性，進行工作或取得資訊。  
  
1.  [開始之前](#BeforeYouBegin)  
  
2.  **To work on a path node:**  [Listing Methods and Properties](#ListPropMeth), [Using Methods and Properties](#UsePropMeth)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
 當您導覽至 [!INCLUDE[ssDE](../includes/ssde-md.md)] 提供者路徑中的節點之後，可以執行兩種動作：  
  
-   您可以執行在節點上運作的 Windows PowerShell Cmdlet，例如 **Rename-Item**。  
  
-   您可以從相關聯的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理物件模型 (如 SMO) 呼叫方法。 例如，如果您導覽至路徑中的資料庫節點，您可以使用 <xref:Microsoft.SqlServer.Management.Smo.Database> 類別的方法和屬性。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供者是用來管理 [!INCLUDE[ssDE](../includes/ssde-md.md)]執行個體中的物件， 而不是用來處理資料庫中的資料。 如果您導覽至資料表或檢視表，即無法使用此提供者選取、插入、更新或刪除資料。 使用 **Invoke-Sqlcmd** Cmdlet 可從 Windows PowerShell 環境中，查詢或變更資料表與檢視中的資料。 如需詳細資訊，請參閱 [Invoke-Sqlcmd Cmdlet](../database-engine/invoke-sqlcmd-cmdlet.md)。  
  
##  <a name="ListPropMeth"></a> 列出方法與屬性
  
 請使用 **Get-Member** Cmdlet，以檢視特定物件或物件類別適用的方法或屬性。  
  
### <a name="examples-listing-methods-and-properties"></a>範例：列出方法與屬性  
 此範例將 Windows PowerShell 變數設定為 SMO <xref:Microsoft.SqlServer.Management.Smo.Database> 類別，並列出方法和屬性：  
  
```powershell
$MyDBVar = New-Object Microsoft.SqlServer.Management.SMO.Database  
$MyDBVar | Get-Member -Type Methods  
$MyDBVar | Get-Member -Type Properties  
```  
  
 您也可以使用 **Get-Member** 列出與 Windows PowerShell 路徑之結束節點相關聯的方法與屬性。  
  
 此範例會導覽至 SQLSERVER: 路徑中的 Databases 節點，並列出集合屬性：  
  
```powershell
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases  
Get-Item . | Get-Member -Type Properties  
```  
  
 此範例會導覽至 SQLSERVER: 路徑中的 AdventureWorks2012 節點，並列出物件屬性：  
  
```powershell
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012  
Get-Item . | Get-Member -Type Properties  
```  
  
##  <a name="UsePropMeth"></a>使用 SMO 方法和屬性  
  
 若要從 [!INCLUDE[ssDE](../includes/ssde-md.md)] 提供者路徑對物件進行工作，可以使用 SMO 方法與屬性。  
  
### <a name="examples-using-methods-and-properties"></a>範例：使用方法與屬性  
 此範例會使用 SMO [結構描述] 屬性來取得 AdventureWorks2012中 Sales 結構描述內的資料表清單：  
  
```powershell
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Tables  
Get-ChildItem | Where {$_.Schema -eq "Sales"}  
```  
  
 這個範例會使用 SMO**腳本**方法來產生腳本，其中包含您在 AdventureWorks2012 中重新建立視圖時必須具備的 `CREATE VIEW` 語句：  
  
```powershell
Remove-Item C:\PowerShell\CreateViews.sql  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Views  
foreach ($Item in Get-ChildItem) { $Item.Script() | Out-File -Filepath C:\PowerShell\CreateViews.sql -append }  
```  
  
 此範例使用 SMO **Create** 方法建立資料庫，然後使用 **State** 屬性顯示此資料庫是否存在：  
  
```powershell
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases  
$MyDBVar = New-Object Microsoft.SqlServer.Management.SMO.Database  
$MyDBVar.Parent = (Get-Item ..)  
$MyDBVar.Name = "NewDB"  
$MyDBVar.Create()  
$MyDBVar.State  
```  
  
## <a name="see-also"></a>請參閱  
 [SQL Server PowerShell 提供者](sql-server-powershell-provider.md)   
 [導覽 SQL Server PowerShell 路徑](navigate-sql-server-powershell-paths.md)   
 [將 URN 轉換成 SQL Server 提供者路徑](../database-engine/convert-urns-to-sql-server-provider-paths.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
