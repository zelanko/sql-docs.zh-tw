---
title: 實作全文檢索搜尋 |Microsoft Docs
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
helpviewer_keywords:
- full-text search [SMO]
ms.assetid: 9ce9ad9c-f671-4760-90b5-e0c8ca051473
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f666336ccc3040139042ba65351fe66ea97d90cc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37219008"
---
# <a name="implementing-full-text-search"></a>實作全文檢索搜尋
  全文檢索搜尋可用於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的每個執行個體，在 SMO 中是由 <xref:Microsoft.SqlServer.Management.Smo.Server.FullTextService%2A> 物件表示。 <xref:Microsoft.SqlServer.Management.Smo.FullTextService> 物件位於 `Server` 物件之下， 可用於管理 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 全文檢索搜尋服務的組態選項。 <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalogCollection> 物件屬於 <xref:Microsoft.SqlServer.Management.Smo.Database> 物件，且為 <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> 物件的集合 (這些物件表示針對資料庫所定義的全文檢索目錄)。 與一般索引不同的是，您只能為每個資料表定義一個全文檢索索引， 這是由 <xref:Microsoft.SqlServer.Management.Smo.FullTextIndexColumn> 物件中的 <xref:Microsoft.SqlServer.Management.Smo.Table> 物件表示。  
  
 若要建立全文檢索搜尋服務，您必須在資料庫上定義全文檢索目錄，並在資料庫的其中一個資料表上定義全文檢索搜尋索引。  
  
 首先，請呼叫 <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> 建構函式並指定目錄名稱，以在資料庫上建立全文檢索目錄。 接著再呼叫建構函式，並指定要在其上建立全文檢索索引的資料表，以建立全文檢索索引。 接下來可以使用 <xref:Microsoft.SqlServer.Management.Smo.FullTextIndexColumn> 物件並且提供資料表內資料行的名稱，以加入全文檢索索引的索引資料行。 然後再將 <xref:Microsoft.SqlServer.Management.Smo.FullTextIndex.CatalogName%2A> 屬性設定為已建立的目錄。 最後呼叫 <xref:Microsoft.SqlServer.Management.Smo.FullTextIndex.Create%2A> 方法，並在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體上建立全文檢索索引。  
  
## <a name="example"></a>範例  
 如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊，請參閱[Visual Studio.NET 中建立 Visual Basic SMO Project](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)或是[建立 Visual C&#35; Visual Studio.NET 中的 SMO 專案](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-a-full-text-search-service-in-visual-basic"></a>在 Visual Basic 中建立全文檢索搜尋服務  
 此程式碼範例會針對 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 範例資料庫中的 `ProductCategory` 資料表建立全文檢索搜尋目錄。 然後在 `ProductCategory` 資料表的 Name 資料行上建立全文檢索搜尋索引。 全文檢索搜尋索引需要資料行上已定義了唯一索引。  
  
```  
' compile with:   
' /r:Microsoft.SqlServer.SqlEnum.dll   
' /r:Microsoft.SqlServer.Smo.dll   
' /r:Microsoft.SqlServer.ConnectionInfo.dll   
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Sdk.Sfc  
Imports Microsoft.SqlServer.Management.Common  
  
Public Class A  
   Public Shared Sub Main()  
      ' Connect to the local, default instance of SQL Server.  
      Dim srv As Server = Nothing  
      srv = New Server()  
  
      ' Reference the AdventureWorks database.  
      Dim db As Database = Nothing  
      db = srv.Databases("AdventureWorks")  
  
      ' Reference the ProductCategory table.  
      Dim tb As Table = Nothing  
      tb = db.Tables("ProductCategory", "Production")  
  
      ' Define a FullTextCatalog object variable by specifying the parent database and name arguments in the constructor.  
      Dim ftc As FullTextCatalog = Nothing  
      ftc = New FullTextCatalog(db, "Test_Catalog")  
      ftc.IsDefault = True  
  
      ' Create the Full-Text Search catalog on the instance of SQL Server.  
      ftc.Create()  
  
      ' Define a FullTextIndex object varaible by supplying the parent table argument in the constructor.  
      Dim fti As FullTextIndex = Nothing  
      fti = New FullTextIndex(tb)  
  
      ' Define a FullTextIndexColumn object variable by supplying the parent index and column name arguements in the constructor.  
      Dim ftic As FullTextIndexColumn = Nothing  
      ftic = New FullTextIndexColumn(fti, "Name")  
  
      ' Add the indexed column to the index.  
      fti.IndexedColumns.Add(ftic)  
      fti.ChangeTracking = ChangeTracking.Automatic  
  
      ' Specify the unique index on the table that is required by the Full Text Search index.  
      fti.UniqueIndexName = "AK_ProductCategory_Name"  
  
      ' Specify the catalog associated with the index.  
      fti.CatalogName = "Test_Catalog"  
  
      ' Create the Full Text Search index on the instance of SQL Server.  
      fti.Create()  
   End Sub  
End Class  
```  
  
## <a name="creating-a-full-text-search-service-in-visual-c"></a>在 Visual C# 中建立全文檢索搜尋服務  
 此程式碼範例會針對 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 範例資料庫中的 `ProductCategory` 資料表建立全文檢索搜尋目錄。 然後在 `ProductCategory` 資料表的 Name 資料行上建立全文檢索搜尋索引。 全文檢索搜尋索引需要資料行上已定義了唯一索引。  
  
```  
// compile with:   
// /r:Microsoft.SqlServer.SqlEnum.dll   
// /r:Microsoft.SqlServer.Smo.dll   
// /r:Microsoft.SqlServer.ConnectionInfo.dll   
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Sdk.Sfc;  
using Microsoft.SqlServer.Management.Common;  
  
public class A {  
   public static void Main() {  
      // Connect to the local, default instance of SQL Server.  
      Server srv = default(Server);  
      srv = new Server();  
  
      // Reference the AdventureWorks database.  
      Database db = default(Database);  
      db = srv.Databases ["AdventureWorks"];  
  
      // Reference the ProductCategory table.  
      Table tb = default(Table);  
      tb = db.Tables["ProductCategory", "Production"];  
  
      // Define a FullTextCatalog object variable by specifying the parent database and name arguments in the constructor.  
      FullTextCatalog ftc = default(FullTextCatalog);  
      ftc = new FullTextCatalog(db, "Test_Catalog");  
      ftc.IsDefault = true;  
  
      // Create the Full-Text Search catalog on the instance of SQL Server.  
      ftc.Create();  
  
      // Define a FullTextIndex object varaible by supplying the parent table argument in the constructor.  
      FullTextIndex fti = default(FullTextIndex);  
      fti = new FullTextIndex(tb);  
  
      // Define a FullTextIndexColumn object variable by supplying the parent index and column name arguements in the constructor.  
      FullTextIndexColumn ftic = default(FullTextIndexColumn);  
      ftic = new FullTextIndexColumn(fti, "Name");  
  
      // Add the indexed column to the index.  
      fti.IndexedColumns.Add(ftic);  
      fti.ChangeTracking = ChangeTracking.Automatic;  
  
      // Specify the unique index on the table that is required by the Full Text Search index.  
      fti.UniqueIndexName = "AK_ProductCategory_Name";  
  
      // Specify the catalog associated with the index.  
      fti.CatalogName = "Test_Catalog";  
  
      // Create the Full Text Search index on the instance of SQL Server.  
      fti.Create();  
   }  
}  
```  
  
## <a name="creating-a-full-text-search-service-in-powershell"></a>在 PowerShell 中建立全文檢索搜尋服務  
 此程式碼範例會針對 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 範例資料庫中的 `ProductCategory` 資料表建立全文檢索搜尋目錄。 然後在 `ProductCategory` 資料表的 Name 資料行上建立全文檢索搜尋索引。 全文檢索搜尋索引需要資料行上已定義了唯一索引。  
  
```  
# Example of implementing a full text search on the default instance.  
# Set the path context to the local, default instance of SQL Server and database tables  
  
CD \sql\localhost\default\databases  
$db = get-item AdventureWorks2012  
  
CD AdventureWorks\tables  
  
#Get a reference to the table  
$tb = get-item Production.ProductCategory  
  
# Define a FullTextCatalog object variable by specifying the parent database and name arguments in the constructor.  
  
$ftc = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextCatalog -argumentlist $db, "Test_Catalog2"  
$ftc.IsDefault = $true  
  
# Create the Full Text Search catalog on the instance of SQL Server.  
$ftc.Create()  
  
# Define a FullTextIndex object variable by supplying the parent table argument in the constructor.  
$fti = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextIndex -argumentlist $tb  
  
#  Define a FullTextIndexColumn object variable by supplying the parent index   
#  and column name arguments in the constructor.  
  
$ftic = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextIndexColumn -argumentlist $fti, "Name"  
  
# Add the indexed column to the index.  
$fti.IndexedColumns.Add($ftic)  
  
# Set change tracking  
$fti.ChangeTracking = [Microsoft.SqlServer.Management.SMO.ChangeTracking]::Automatic  
  
# Specify the unique index on the table that is required by the Full Text Search index.  
$fti.UniqueIndexName = "AK_ProductCategory_Name"  
  
# Specify the catalog associated with the index.  
$fti.CatalogName = "Test_Catalog2"  
  
# Create the Full Text Search Index  
$fti.Create()  
```  
  
  
