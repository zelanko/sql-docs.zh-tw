---
description: 建立、改變和移除檢視
title: 建立、改變和移除檢視
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- views [SMO]
ms.assetid: 7d445c0e-77ef-4734-993b-e022de31df23
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b4c942adfbe2b9edf450d332450bf8a8a958a80e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475539"
---
# <a name="creating-altering-and-removing-views"></a>建立、改變和移除檢視
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]
  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理物件 (SMO) 中，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 檢視是由 <xref:Microsoft.SqlServer.Management.Smo.View> 物件表示。  
  
 <xref:Microsoft.SqlServer.Management.Smo.View.TextBody%2A> 物件的 <xref:Microsoft.SqlServer.Management.Smo.View> 屬性會定義檢視。 該屬性等於用於建立檢視的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] SELECT 陳述式。  
  
## <a name="example"></a>範例  
 如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊，請參閱 [Visual Studio .NET 中的建立 Visual C&#35; SMO 專案](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-altering-and-removing-a-view-in-visual-basic"></a>在 Visual Basic 中建立、改變和移除檢視  
 此程式碼範例示範如何使用內部聯結建立兩個資料表的檢視。 該檢視是利用文字模式建立，所以必須設定 <xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> 屬性。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a View object variable by supplying the parent database, view name and schema in the constructor.
Dim myview As View
myview = New View(db, "Test_View", "Sales")
'Set the TextHeader and TextBody property to define the view.
myview.TextHeader = "CREATE VIEW [Sales].[Test_View] AS"
myview.TextBody = "SELECT h.SalesOrderID, d.OrderQty FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID"
'Create the view on the instance of SQL Server.
myview.Create()
'Remove the view.
myview.Drop()
```
  
## <a name="creating-altering-and-removing-a-view-in-visual-c"></a>在 Visual C# 中建立、改變和移除檢視  
 此程式碼範例示範如何使用內部聯結建立兩個資料表的檢視。 該檢視是利用文字模式建立，所以必須設定 <xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> 屬性。  
  
```csharp  
{  
        //Connect to the local, default instance of SQL Server.   
        Server srv;   
        srv = new Server();   
        //Reference the AdventureWorks2012 database.   
        Database db;   
        db = srv.Databases["AdventureWorks2012"];   
        //Define a View object variable by supplying the parent database, view name and schema in the constructor.   
        View myview;   
        myview = new View(db, "Test_View", "Sales");   
        //Set the TextHeader and TextBody property to define the view.   
        myview.TextHeader = "CREATE VIEW [Sales].[Test_View] AS";   
        myview.TextBody = "SELECT h.SalesOrderID, d.OrderQty FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID";   
        //Create the view on the instance of SQL Server.   
        myview.Create();   
        //Remove the view.   
        myview.Drop();   
        }  
```  
  
## <a name="creating-altering-and-removing-a-view-in-powershell"></a>在 PowerShell 中建立、改變和移除檢視  
 此程式碼範例示範如何使用內部聯結建立兩個資料表的檢視。 該檢視是利用文字模式建立，所以必須設定 <xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> 屬性。  
  
```powershell   
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a View object variable by supplying the parent database, view name and schema in the constructor.   
$myview  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.View `  
-argumentlist $db, "Test_View", "Sales"  
  
# Set the TextHeader and TextBody property to define the view.   
$myview.TextHeader = "CREATE VIEW [Sales].[Test_View] AS"  
$myview.TextBody ="SELECT h.SalesOrderID, d.OrderQty FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID"  
  
# Create the view on the instance of SQL Server.   
$myview.Create()  
  
# Remove the view.   
$myview.Drop();  
```  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.SqlServer.Management.Smo.View>  
  
  
