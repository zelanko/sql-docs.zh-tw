---
title: 使用檔案群組和檔案來儲存資料 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- filegroups [SMO]
- storing data [SMO]
- files [SMO]
- files [SMO], about files
- storage [SMO]
ms.assetid: 7e2327ce-e1a6-4904-83d1-0944b24a7b43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 270df8181fe42f48619736ba858dc0c16d9e30c7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "72781806"
---
# <a name="using-filegroups-and-files-to-store-data"></a>使用檔案群組和檔案來儲存資料
  資料檔案可用於儲存資料庫檔案。 資料檔案被分成檔案群組。  物件具有  屬性，這個屬性會參考  物件。 該集合中的每個 <xref:Microsoft.SqlServer.Management.Smo.FileGroup> 物件都具有 <xref:Microsoft.SqlServer.Management.Smo.FileGroup.Files%2A> 屬性。 這個屬性會參考 <xref:Microsoft.SqlServer.Management.Smo.DataFileCollection> 集合，其中包含資料庫所屬的所有資料檔。 檔案群組的主要功能是將用於儲存資料庫物件的檔案放入群組。 將一個資料庫物件散佈到數個檔案的其中一個理由就是改善效能，特別是如果檔案儲存在不同的磁碟機上。  
  
 每個自動建立的資料庫都具有名為 "Primary" 的檔案群組以及與資料庫同名的資料檔。 可以在集合中加入其他檔案和群組。  
  
## <a name="examples"></a>範例  
 在下列的程式碼範例中，您必須選取用於建立應用程式的程式設計環境、程式設計範本和程式設計語言。 如需詳細資訊，請參閱[在 Visual Studio .net 中建立 VISUAL BASIC SMO 專案](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)和[在 Visual Studio .Net 中建立 VISUAL C&#35; SMO 專案](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-basic"></a>在 Visual Basic 中將 FileGroups 和 DataFiles 加入至資料庫  
 主要檔案群組和資料檔會使用預設的屬性值自動建立。 程式碼範例會指定某些可以使用的某些屬性值； 否則，系統會使用預設屬性值。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBFileGroups1](SMO How to#SMO_VBFileGroups1)]  -->  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-c"></a>在 Visual C# 中將 FileGroups 和 DataFiles 加入至資料庫  
 主要檔案群組和資料檔會使用預設的屬性值自動建立。 程式碼範例會指定某些可以使用的某些屬性值； 否則，系統會使用預設屬性值。  
  
```csharp
{  
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a FileGroup object called SECONDARY on the database.   
            FileGroup fg1 = default(FileGroup);  
            fg1 = new FileGroup(db, "SECONDARY");  
            //Call the Create method to create the file group on the instance of SQL Server.   
            fg1.Create();  
            //Define a DataFile object on the file group and set the FileName property.   
            DataFile df1 = default(DataFile);  
            df1 = new DataFile(fg1, "datafile1");  
            df1.FileName = "c:\\Program Files\\Microsoft SQL Server\\MSSQL.1\\MSSQL\\Data\\datafile2.ndf";  
            //Call the Create method to create the data file on the instance of SQL Server.   
            df1.Create();  
        }  
```  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-powershell"></a>在 PowerShell 中將 FileGroups 和 DataFiles 加入至資料庫  
 主要檔案群組和資料檔會使用預設的屬性值自動建立。 程式碼範例會指定某些可以使用的某些屬性值； 否則，系統會使用預設屬性值。  
  
```powershell
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012.  
$db = get-item AdventureWorks2012  
  
#Create a new filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "SECONDARY"  
$fg1.Create()  
  
#Define a DataFile object on the file group and set the FileName property.   
$df1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.DataFile -argumentlist $fg1, "datafile1"  
  
#Make sure to have a directory created to hold the designated data file  
$df1.FileName = "c:\\TestData\\datafile2.ndf"  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$df1.Create()  
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-basic"></a>在 Visual Basic 中建立、改變和移除記錄檔  
 程式碼範例會建立 <xref:Microsoft.SqlServer.Management.Smo.LogFile> 物件、變更其中一個屬性，然後將它從資料庫移除。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBFileGroups3](SMO How to#SMO_VBFileGroups3)]  -->  
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-c"></a>在 Visual C# 中建立、改變和移除記錄檔  
 程式碼範例會建立 <xref:Microsoft.SqlServer.Management.Smo.LogFile> 物件、變更其中一個屬性，然後將它從資料庫移除。  
  
```csharp
//Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a LogFile object and set the database, name, and file name properties in the constructor.   
            LogFile lf1 = default(LogFile);  
            lf1 = new LogFile(db, "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf");  
            //Set the file growth to 6%.   
            lf1.GrowthType = FileGrowthType.Percent;  
            lf1.Growth = 6;  
            //Run the Create method to create the log file on the instance of SQL Server.   
            lf1.Create();  
            //Alter the growth percentage.
            lf1.Growth = 7;  
            lf1.Alter();  
            //Remove the log file.
            lf1.Drop();
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-powershell"></a>在 PowerShell 中建立、改變和移除記錄檔  
 程式碼範例會建立 <xref:Microsoft.SqlServer.Management.Smo.LogFile> 物件、變更其中一個屬性，然後將它從資料庫移除。  
  
```powershell
#Load the assembly containing the enums used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.SqlEnum")  
  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012  
$db = get-item AdventureWorks2012  
  
#Create a filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Secondary"  
  
#Call the Create method to create the file group on the instance of SQL Server.   
$fg1.Create()  
  
#Define a LogFile object on the file group and set the FileName property.   
$lf1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LogFile -argumentlist $db, "LogFile2"  
  
#Set a location for it - make sure the directory exists  
$lf1.FileName = "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf"  
  
#Set file growth to 6%  
$lf1.GrowthType = [Microsoft.SqlServer.Management.Smo.FileGrowthType]::Percent  
$lf1.Growth = 6.0  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$lf1.Create()  
  
#Alter a value and drop the log file  
$lf1.Growth = 7.0  
$lf1.Alter()  
$lf1.Drop()
```  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.SqlServer.Management.Smo.FileGroup>   
 [資料庫檔案與檔案群組](../../databases/database-files-and-filegroups.md)  
