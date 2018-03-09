---
title: "建立、 改變和移除觸發程序 |Microsoft 文件"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- triggers [SMO]
ms.assetid: 8ddbe23b-6e31-4f8e-8a70-17bd5072413e
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc1849a9bd38af6cbca6d9ebcbea6a571af8816c
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2018
---
# <a name="creating-altering-and-removing-triggers"></a>建立、改變和移除觸發程式
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]在 SMO 中，觸發程序都由使用<xref:Microsoft.SqlServer.Management.Smo.Trigger>物件。 [!INCLUDE[tsql](../../../includes/tsql-md.md)]時引發的觸發程序由設定執行的程式碼<xref:Microsoft.SqlServer.Management.Smo.Trigger.TextBody%2A>觸發程序物件的屬性。 觸發程序的類型是利用 <xref:Microsoft.SqlServer.Management.Smo.Trigger> 物件的其他屬性所設定，例如 <xref:Microsoft.SqlServer.Management.Smo.Trigger.Update%2A> 屬性。 這是布林值屬性，指定是否引發觸發程序所**更新**父資料表上的記錄。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Trigger> 物件代表傳統的資料操作語言 (DML) 觸發程式。 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 和更新版本也支援資料定義語言 (DDL) 觸發程序。 DDL 觸發程序是由 <xref:Microsoft.SqlServer.Management.Smo.DatabaseDdlTrigger> 物件和 <xref:Microsoft.SqlServer.Management.Smo.ServerDdlTrigger> 物件表示。  
  
## <a name="example"></a>範例  
如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊，請參閱[建立 Visual C# 35。在 Visual Studio.NET 中的 SMO 專案](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
 
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-basic"></a>在 Visual Basic 中建立、改變和移除觸發程序  
 此程式碼範例示範如何在 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 資料庫中名為 `Sales` 的現有資料表上，建立及插入更新觸發程序。 此觸發程序會在資料表更新或新記錄插入時傳送提醒訊息。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim mysrv As Server
mysrv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim mydb As Database
mydb = mysrv.Databases("AdventureWorks2012")
'Declare a Table object variable and reference the Customer table.
Dim mytab As Table
mytab = mydb.Tables("Customer", "Sales")
'Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.
Dim tr As Trigger
tr = New Trigger(mytab, "Sales")
'Set TextMode property to False, then set other properties to define the trigger.
tr.TextMode = False
tr.Insert = True
tr.Update = True
tr.InsertOrder = Agent.ActivationOrder.First
Dim stmt As String
stmt = " RAISERROR('Notify Customer Relations',16,10) "
tr.TextBody = stmt
tr.ImplementationType = ImplementationType.TransactSql
'Create the trigger on the instance of SQL Server.
tr.Create()
'Remove the trigger.
tr.Drop()
``` 
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-c"></a>在 Visual C# 中建立、改變和移除觸發程序  
 此程式碼範例示範如何在 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 資料庫中名為 `Sales` 的現有資料表上，建立及插入更新觸發程序。 此觸發程序會在資料表更新或新記錄插入時傳送提醒訊息。  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server mysrv;  
            mysrv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database mydb;  
            mydb = mysrv.Databases["AdventureWorks2012"];  
            //Declare a Table object variable and reference the Customer table.   
            Table mytab;  
            mytab = mydb.Tables["Customer", "Sales"];  
            //Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.   
            Trigger tr;  
            tr = new Trigger(mytab, "Sales");  
            //Set TextMode property to False, then set other properties to define the trigger.   
            tr.TextMode = false;  
            tr.Insert = true;  
            tr.Update = true;  
            tr.InsertOrder = ActivationOrder.First;  
            string stmt;  
            stmt = " RAISERROR('Notify Customer Relations',16,10) ";  
            tr.TextBody = stmt;  
            tr.ImplementationType = ImplementationType.TransactSql;  
            //Create the trigger on the instance of SQL Server.   
            tr.Create();  
            //Remove the trigger.   
            tr.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-trigger-in-powershell"></a>在 PowerShell 中建立、改變和移除觸發程序  
 此程式碼範例示範如何在 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 資料庫中名為 `Sales` 的現有資料表上，建立及插入更新觸發程序。 此觸發程序會在資料表更新或新記錄插入時傳送提醒訊息。  
  
```powershell  
# Set the path context to the local, default instance of SQL Server and to the  
#database tables in Adventureworks2012  
CD \sql\localhost\default\databases\AdventureWorks2012\Tables\  
  
#Get reference to the trigger's target table  
$mytab = get-item Sales.Customer  
  
# Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.  
$tr  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Trigger `  
-argumentlist $mytab, "Sales"  
  
# Set TextMode property to False, then set other properties to define the trigger.   
$tr.TextMode = $false  
$tr.Insert = $true  
$tr.Update = $true  
$tr.InsertOrder = [Microsoft.SqlServer.Management.SMO.Agent.ActivationOrder]::First  
$tr.TextBody = " RAISERROR('Notify Customer Relations',16,10) "  
$tr.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Create the trigger on the instance of SQL Server.   
$tr.Create()  
  
#Remove the trigger.   
$tr.Drop()  
```  
  
  
