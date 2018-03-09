---
title: "使用集合 |Microsoft 文件"
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
- SQL Server Management Objects, collections
- SMO [SQL Server], collections
- collections [SMO]
ms.assetid: 209eb175-2514-4de1-bc32-b2e6a469d945
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ac05072224f6b6cc4e84b2144d827b6059b226d2
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2018
---
# <a name="using-collections"></a>使用集合
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  集合是已經從相同物件類別建構，而且共用相同父物件的物件清單。 集合物件一定會包含具有 Collection 後置詞之物件類型的名稱。 例如，若要存取指定之資料表內的資料行，請使用 <xref:Microsoft.SqlServer.Management.Smo.ColumnCollection> 物件類型。 它會包含屬於相同 <xref:Microsoft.SqlServer.Management.Smo.Column> 物件的所有 <xref:Microsoft.SqlServer.Management.Smo.Table> 物件。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] **For...每個**陳述式或[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] **foreach**陳述式可用來逐一查看集合的每個成員。  
  
## <a name="examples"></a>範例  
如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊，請參閱[建立 Visual C# 35。在 Visual Studio.NET 中的 SMO 專案](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-basic"></a>在 Visual Basic 中使用集合來參考物件  
 這個程式碼範例示範如何使用設定資料行屬性<xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>， <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>，和<xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A>屬性。 這些屬性代表集合，當這些屬性搭配可指定物件名稱的參數使用時，就可用來識別特定物件。 名稱和結構描述所需的<xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>集合物件屬性。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Modify a property using the Databases, Tables, and Columns collections to reference a column.
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("ModifiedDate").Nullable = True
'Call the Alter method to make the change on the instance of SQL Server.
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("ModifiedDate").Alter()
```
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-c"></a>在 Visual C# 中使用集合來參考物件  
 這個程式碼範例示範如何使用設定資料行屬性<xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>， <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>，和<xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A>屬性。 這些屬性代表集合，當這些屬性搭配可指定物件名稱的參數使用時，就可用來識別特定物件。 名稱和結構描述所需的<xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>集合物件屬性。  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Modify a property using the Databases, Tables, and Columns collections to reference a column.   
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("LastName").Nullable = true;   
//Call the Alter method to make the change on the instance of SQL Server.   
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("LastName").Alter();   
}  
```  
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-basic"></a>在 Visual Basic 中逐一查看集合的成員  
 這個程式碼範例會逐一<xref:Microsoft.AnalysisServices.Server.Databases%2A>集合屬性，並顯示所有資料庫的執行個體的連接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
Dim count As Integer
Dim total As Integer
'Iterate through the databases and call the GetActiveDBConnectionCount method.
Dim db As Database
For Each db In srv.Databases
    count = srv.GetActiveDBConnectionCount(db.Name)
    total = total + count
    'Display the number of connections for each database.
    Console.WriteLine(count & " connections on " & db.Name)
Next
'Display the total number of connections on the instance of SQL Server.
Console.WriteLine("Total connections =" & total)
```
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-c"></a>在 Visual C# 中逐一查看集合的成員  
 這個程式碼範例會逐一<xref:Microsoft.AnalysisServices.Server.Databases%2A>集合屬性，並顯示所有資料庫的執行個體的連接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
```csharp  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
int count = 0;   
int total = 0;   
//Iterate through the databases and call the GetActiveDBConnectionCount method.   
Database db = default(Database);   
foreach ( db in srv.Databases) {   
  count = srv.GetActiveDBConnectionCount(db.Name);   
  total = total + count;   
  //Display the number of connections for each database.   
  Console.WriteLine(count + " connections on " + db.Name);   
}   
//Display the total number of connections on the instance of SQL Server.   
Console.WriteLine("Total connections =" + total);   
}   
```  
  
  
