---
description: 使用資料表和索引資料分割
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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9744fe42994499539d57f0e84fd73b2809208642
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464878"
---
# <a name="using-table-and-index-partitioning"></a>使用資料表和索引資料分割
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  資料可以使用 [Partitioned Tables and Indexes](../../../relational-databases/partitions/partitioned-tables-and-indexes.md)提供的儲存演算法來儲存。 分割作業可讓大型資料表和索引更容易管理及擴充。  
  
## <a name="index-and-table-partitioning"></a>索引和資料表資料分割  
 此功能可以讓索引和資料表資料散佈到資料分割中的多個檔案群組。 資料分割函數會定義資料表的資料列或索引如何依據某些資料行 (稱為分割資料行) 的值對應到資料分割集。 資料分割配置則會將資料分割函數所指定的每個資料分割都對應到檔案群組。 如此您就可以開發出封存策略，讓資料表可以擴充到檔案群組，並進而擴充到實體裝置。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Database> 物件包含表示所實作之資料分割函數的 <xref:Microsoft.SqlServer.Management.Smo.PartitionFunction> 物件集合，以及描述資料如何對應到檔案群組的 <xref:Microsoft.SqlServer.Management.Smo.PartitionScheme> 物件集合。  
  
 每個 <xref:Microsoft.SqlServer.Management.Smo.Table> 和 <xref:Microsoft.SqlServer.Management.Smo.Index> 物件都會在 <xref:Microsoft.SqlServer.Management.Smo.PartitionScheme> 屬性中指定所使用的資料分割配置，並在 <xref:Microsoft.SqlServer.Management.Smo.PartitionSchemeParameterCollection> 中指定資料行。  
  
## <a name="example"></a>範例  
 在下列的程式碼範例中，您必須選取用於建立應用程式的程式設計環境、程式設計範本和程式設計語言。 如需詳細資訊，請參閱 [Visual Studio .NET 中的建立 Visual C&#35; SMO 專案](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-visual-c"></a>在 Visual C# 中為資料表設定資料分割配置  
 此程式碼範例顯示如何為 `TransactionHistory` 範例資料庫中的 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 資料表建立資料分割函數和資料分割配置。 這些資料分割會以日期區分，用意在於將舊記錄區隔到 `TransactionHistoryArchive` 資料表中。  
  
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
 此程式碼範例顯示如何為 `TransactionHistory` 範例資料庫中的 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 資料表建立資料分割函數和資料分割配置。 這些資料分割會以日期區分，用意在於將舊記錄區隔到 `TransactionHistoryArchive` 資料表中。  
  
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
 [分割資料表與索引](../../../relational-databases/partitions/partitioned-tables-and-indexes.md)  
  
  
