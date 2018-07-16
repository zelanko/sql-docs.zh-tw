---
title: 使用集合 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQL Server Management Objects, collections
- SMO [SQL Server], collections
- collections [SMO]
ms.assetid: 209eb175-2514-4de1-bc32-b2e6a469d945
caps.latest.revision: 47
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e3a56d7b6335734f8ddc90ea1a4438e6b6ae1763
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37179615"
---
# <a name="using-collections"></a>使用集合
  集合是已經從相同物件類別建構，而且共用相同父物件的物件清單。 集合物件一定會包含具有 Collection 後置詞之物件類型的名稱。 例如，若要存取指定之資料表內的資料行，請使用 <xref:Microsoft.SqlServer.Management.Smo.ColumnCollection> 物件類型。 它會包含屬於相同 <xref:Microsoft.SqlServer.Management.Smo.Column> 物件的所有 <xref:Microsoft.SqlServer.Management.Smo.Table> 物件。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] `For...Each`陳述式或[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] `foreach`陳述式可用來逐一查看集合的每個成員。  
  
## <a name="examples"></a>範例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-basic"></a>在 Visual Basic 中使用集合來參考物件  
 此程式碼範例示範如何使用設定資料行屬性<xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>， <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>，和<xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A>屬性。 這些屬性代表集合，當這些屬性搭配可指定物件名稱的參數使用時，就可用來識別特定物件。 名稱和結構描述所需的<xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>集合物件屬性。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCollections1](SMO How to#SMO_VBCollections1)]  -->  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-c"></a>在 Visual C# 中使用集合來參考物件  
 此程式碼範例示範如何使用設定資料行屬性<xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>， <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>，和<xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A>屬性。 這些屬性代表集合，當這些屬性搭配可指定物件名稱的參數使用時，就可用來識別特定物件。 名稱和結構描述所需的<xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A>集合物件屬性。  
  
```  
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
 此程式碼範例會逐一<xref:Microsoft.AnalysisServices.Server.Databases%2A>集合屬性，並顯示所有資料庫的執行個體的連接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCollections2](SMO How to#SMO_VBCollections2)]  -->  
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-c"></a>在 Visual C# 中逐一查看集合的成員  
 此程式碼範例會逐一<xref:Microsoft.AnalysisServices.Server.Databases%2A>集合屬性，並顯示所有資料庫的執行個體的連接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
```  
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
  
  
