---
title: 使用資料表和索引資料分割 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- partitions [SMO]
- storing data [SMO]
- partitioned tables [SQL Server], SMO
- partitioned indexes [SQL Server], SMO
ms.assetid: 0e682d7e-86c3-4d73-950d-aa692d46cb62
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 045a676405904a3dd679c972fada8aeb1df01ee6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47847406"
---
# <a name="using-table-and-index-partitioning"></a>使用資料表和索引資料分割
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  要儲存資料，請使用所提供的儲存演算法[Partitioned Tables and Indexes](../../../relational-databases/partitions/partitioned-tables-and-indexes.md)。 分割作業可讓大型資料表和索引更容易管理及擴充。  
  
## <a name="index-and-table-partitioning"></a>索引和資料表資料分割  
 此功能可以讓索引和資料表資料散佈到資料分割中的多個檔案群組。 資料分割函數會定義資料表的資料列或索引如何依據某些資料行 (稱為分割資料行) 的值對應到資料分割集。 資料分割配置則會將資料分割函數所指定的每個資料分割都對應到檔案群組。 如此您就可以開發出封存策略，讓資料表可以擴充到檔案群組，並進而擴充到實體裝置。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Database>物件包含的集合<xref:Microsoft.SqlServer.Management.Smo.PartitionFunction>物件，代表所實作的資料分割函數和集合<xref:Microsoft.SqlServer.Management.Smo.PartitionScheme>描述資料如何對應至檔案群組的物件。  
  
 每個 <xref:Microsoft.SqlServer.Management.Smo.Table> 和 <xref:Microsoft.SqlServer.Management.Smo.Index> 物件都會在 <xref:Microsoft.SqlServer.Management.Smo.PartitionScheme> 屬性中指定所使用的資料分割配置，並在 <xref:Microsoft.SqlServer.Management.Smo.PartitionSchemeParameterCollection> 中指定資料行。  
  
## <a name="example"></a>範例  
 在下列的程式碼範例中，您必須選取用於建立應用程式的程式設計環境、程式設計範本和程式設計語言。 如需詳細資訊，請參閱 <<c0> [ 建立 Visual C&#35; Visual Studio.NET 中的 SMO 專案](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。</c0>  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-visual-c"></a>在 Visual C# 中為資料表設定資料分割配置  
 在程式碼範例示範如何建立資料分割函數和資料分割配置`TransactionHistory`資料表中[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]範例資料庫。 這些資料分割會以日期區分，用意在於將舊記錄區隔到 `TransactionHistoryArchive` 資料表中。  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Define and create three new file groups on the database.   
FileGroup fg2;   
fg2 = new FileGroup(db, "Second");   
fg2.Create();   
FileGroup fg3;   
fg3 = new FileGroup(db, "Third");   
fg3.Create();   
FileGroup fg4;   
fg4 = new FileGroup(db, "Fourth");   
fg4.Create();   
//Define a partition function by supplying the parent database and name arguments in the constructor.   
PartitionFunction pf;   
pf = new PartitionFunction(db, "TransHistPF");   
//Add a partition function parameter that specifies the function uses a DateTime range type.   
PartitionFunctionParameter pfp;   
pfp = new PartitionFunctionParameter(pf, DataType.DateTime);   
pf.PartitionFunctionParameters.Add(pfp);   
//Specify the three dates that divide the data into four partitions.   
object[] val;   
val = new object[] {"1/1/2003", "1/1/2004", "1/1/2005"};   
pf.RangeValues = val;   
//Create the partition function.   
pf.Create();   
//Define a partition scheme by supplying the parent database and name arguments in the constructor.   
PartitionScheme ps;   
ps = new PartitionScheme(db, "TransHistPS");   
//Specify the partition function and the filegroups required by the partition scheme.   
ps.PartitionFunction = "TransHistPF";   
ps.FileGroups.Add("PRIMARY");   
ps.FileGroups.Add("second");   
ps.FileGroups.Add("Third");   
ps.FileGroups.Add("Fourth");   
//Create the partition scheme.   
ps.Create();   
}   
```  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-powershell"></a>在 PowerShell 中為資料表設定資料分割配置  
 在程式碼範例示範如何建立資料分割函數和資料分割配置`TransactionHistory`資料表中[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]範例資料庫。 這些資料分割會以日期區分，用意在於將舊記錄區隔到 `TransactionHistoryArchive` 資料表中。  
  
```powershell  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
$db = $srv.Databases["AdventureWorks"]  
#Create four filegroups  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "First"  
$fg2 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Second"  
$fg3 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Third"  
$fg4 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Fourth"  
  
#Define a partition function by supplying the parent database and name arguments in the constructor.  
$pf =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionFunction -argumentlist $db, "TransHistPF"  
$T = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$T  
$T.GetType()  
#Add a partition function parameter that specifies the function uses a DateTime range type.  
$pfp =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionFunctionParameter -argumentlist $pf, $T  
  
#Specify the three dates that divide the data into four partitions.   
#Create an array of type object to hold the partition data  
$val = "1/1/2003"."1/1/2004","1/1/2005"  
$pf.RangeValues = $val  
$pf  
#Create the partition function  
$pf.Create()  
  
#Create partition scheme  
$ps = New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionScheme -argumentlist $db, "TransHistPS"  
$ps.PartitionFunction = "TransHistPF"  
  
#add the filegroups to the scheme   
$ps.FileGroups.Add("PRIMARY")  
$ps.FileGroups.Add("Second")  
$ps.FileGroups.Add("Third")  
$ps.FileGroups.Add("Fourth")  
  
#Create it at the server  
$ps.Create()  
```  
  
## <a name="see-also"></a>另請參閱  
 [Partitioned Tables and Indexes](../../../relational-databases/partitions/partitioned-tables-and-indexes.md)  
  
  
