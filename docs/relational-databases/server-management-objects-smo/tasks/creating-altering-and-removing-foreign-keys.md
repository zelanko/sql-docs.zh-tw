---
title: 建立、改變和移除外部索引鍵
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- foreign keys [SMO]
ms.assetid: d43c8dca-bb6b-4a41-8a79-c96fd546fc91
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c37f43e82bdad11909695d5a2799b5065c7cb5b9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74095547"
---
# <a name="creating-altering-and-removing-foreign-keys"></a>建立、改變和移除外部索引鍵
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理物件 (SMO) 中，外部索引鍵是由 <xref:Microsoft.SqlServer.Management.Smo.ForeignKey> 物件表示。  
  
 若要在 SMO 中建立外部索引鍵，您必須在 <xref:Microsoft.SqlServer.Management.Smo.ForeignKey> 物件的建構函式中，指定會在其上定義外部索引鍵的資料表。 您必須從該資料表至少選取一個資料行做為外部索引鍵。 若要進行這項作業，請建立 <xref:Microsoft.SqlServer.Management.Smo.ForeignKeyColumn> 物件變數，並指定做為外部索引鍵之資料行的名稱。 然後，指定參考的資料表和參考的資料行。 使用<xref:Microsoft.SqlServer.Management.Smo.ForeignKeyColumnCollection.Add%2A>方法，即可將資料行加入至**Columns**物件屬性。  
  
 代表外鍵的資料行會列在<xref:Microsoft.SqlServer.Management.Smo.ForeignKey>物件的**columns**物件屬性中。 外部索引鍵所參考的主要金鑰是由 <xref:Microsoft.SqlServer.Management.Smo.ForeignKey.ReferencedKey%2A> 屬性表示，該屬性位於 <xref:Microsoft.SqlServer.Management.Smo.ForeignKey.ReferencedTable%2A> 屬性所指定的資料表。  
  
## <a name="example"></a>範例  
 如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊，請參閱[在 Visual Studio .net 中建立 Visual C&#35; SMO 專案](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-altering-and-removing-a-foreign-key-in-visual-basic"></a>在 Visual Basic 中建立、改變和移除外部索引鍵  
 此程式碼範例示範如何在某個資料表的一個或多個資料行以及另一個資料表的主要索引鍵資料行之間，建立外部索引鍵關聯性。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Declare a Table object variable and reference the Employee table.
Dim tbe As Table
tbe = db.Tables("Employee", "HumanResources")
'Declare another Table object variable and reference the EmployeeDepartmentHistory table.
Dim tbea As Table
tbea = db.Tables("EmployeeDepartmentHistory", "HumanResources")
'Define a Foreign Key object variable by supplying the EmployeeDepartmentHistory as the parent table and the foreign key name in the constructor.
Dim fk As ForeignKey
fk = New ForeignKey(tbea, "test_foreignkey")
'Add BusinessEntityID as the foreign key column.
Dim fkc As ForeignKeyColumn
fkc = New ForeignKeyColumn(fk, "BusinessEntityID", "BusinessEntityID")
fk.Columns.Add(fkc)
'Set the referenced table and schema.
fk.ReferencedTable = "Employee"
fk.ReferencedTableSchema = "HumanResources"
'Create the foreign key on the instance of SQL Server.
fk.Create()
```
  
## <a name="creating-altering-and-removing-a-foreign-key-in-visual-c"></a>在 Visual C# 中建立、改變和移除外部索引鍵  
 此程式碼範例示範如何在某個資料表的一個或多個資料行以及另一個資料表的主要索引鍵資料行之間，建立外部索引鍵關聯性。  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
            //Declare another Table object variable and reference the EmployeeDepartmentHistory table.   
            Table tbea;  
            tbea = db.Tables["EmployeeDepartmentHistory", "HumanResources"];  
            //Define a Foreign Key object variable by supplying the EmployeeDepartmentHistory as the parent table and the foreign key name in the constructor.   
            ForeignKey fk;  
            fk = new ForeignKey(tbea, "test_foreignkey");  
            //Add BusinessEntityID as the foreign key column.   
            ForeignKeyColumn fkc;  
            fkc = new ForeignKeyColumn(fk, "BusinessEntityID", "BusinessEntityID");  
            fk.Columns.Add(fkc);  
            //Set the referenced table and schema.   
            fk.ReferencedTable = "Employee";  
            fk.ReferencedTableSchema = "HumanResources";  
            //Create the foreign key on the instance of SQL Server.   
            fk.Create();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-foreign-key-in-powershell"></a>在 PowerShell 中建立、改變和移除外部索引鍵  
 此程式碼範例示範如何在某個資料表的一個或多個資料行以及另一個資料表的主要索引鍵資料行之間，建立外部索引鍵關聯性。  
  
```powershell  
# Set the path context to the local, default instance of SQL Server and to the  
#database tables in Adventureworks2012  
CD \sql\localhost\default\databases\AdventureWorks2012\Tables\  
  
#Get reference to the FK table  
$tbea = get-item HumanResources.EmployeeDepartmentHistory  
  
# Define a Foreign Key object variable by supplying the EmployeeDepartmentHistory  
# as the parent table and the foreign key name in the constructor.   
$fk = New-Object -TypeName Microsoft.SqlServer.Management.SMO.ForeignKey `  
-argumentlist $tbea, "test_foreignkey"  
  
#Add BusinessEntityID as the foreign key column.   
$fkc = New-Object -TypeName Microsoft.SqlServer.Management.SMO.ForeignKeyColumn `  
-argumentlist $fk, "BusinessEntityID", "BusinessEntityID"  
$fk.Columns.Add($fkc)  
  
#Set the referenced table and schema.   
$fk.ReferencedTable = "Employee"  
$fk.ReferencedTableSchema = "HumanResources"  
  
#Create the foreign key on the instance of SQL Server.   
$fk.Create()  
```  
  
## <a name="sample-foreign-keys-primary-keys-and-unique-constraint-columns"></a>範例：外部索引鍵、主索引鍵和唯一條件約束資料行  
 此範例示範：  
  
-   在現有物件上尋找外部索引鍵。  
  
-   如何建立主索引鍵。  
  
-   如何建立唯一條件約束資料行。  
  
 此範例的 C# 版本：  
  
```  
// compile with:   
// /r:Microsoft.SqlServer.Smo.dll   
// /r:microsoft.sqlserver.management.sdk.sfc.dll   
// /r:Microsoft.SqlServer.ConnectionInfo.dll  
// /r:Microsoft.SqlServer.SqlEnum.dll  
  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Sdk.Sfc;  
using Microsoft.SqlServer.Management.Common;  
using System;  
  
public class A {  
   public static void Main() {  
      Server svr = new Server();  
      Database db = new Database(svr, "TESTDB");  
      db.Create();  
  
      // PK Table  
      Table tab1 = new Table(db, "Table1");  
  
      // Define Columns and add them to the table  
      Column col1 = new Column(tab1, "Col1", DataType.Int);  
  
      col1.Nullable = false;  
      tab1.Columns.Add(col1);  
      Column col2 = new Column(tab1, "Col2", DataType.NVarChar(50));  
      tab1.Columns.Add(col2);  
      Column col3 = new Column(tab1, "Col3", DataType.DateTime);  
      tab1.Columns.Add(col3);  
  
      // Create the ftable  
      tab1.Create();  
  
      // Define Index object on the table by supplying the Table1 as the parent table and the primary key name in the constructor.  
      Index pk = new Index(tab1, "Table1_PK");  
      pk.IndexKeyType = IndexKeyType.DriPrimaryKey;  
  
      // Add Col1 as the Index Column  
      IndexedColumn idxCol1 = new IndexedColumn(pk, "Col1");  
      pk.IndexedColumns.Add(idxCol1);  
  
      // Create the Primary Key  
      pk.Create();  
  
      // Create Unique Index on the table  
      Index unique = new Index(tab1, "Table1_Unique");  
      unique.IndexKeyType = IndexKeyType.DriUniqueKey;  
  
      // Add Col1 as the Unique Index Column  
      IndexedColumn idxCol2 = new IndexedColumn(unique, "Col2");  
      unique.IndexedColumns.Add(idxCol2);  
  
      // Create the Unique Index  
      unique.Create();  
  
      // Create Table2                    
      Table tab2 = new Table(db, "Table2");  
      Column col21 = new Column(tab2, "Col21", DataType.NChar(20));  
      tab2.Columns.Add(col21);  
      Column col22 = new Column(tab2, "Col22", DataType.Int);  
      tab2.Columns.Add(col22);  
      tab2.Create();  
  
      // Define a Foreign Key object variable by supplying the Table2 as the parent table and the foreign key name in the constructor.   
      ForeignKey fk = new ForeignKey(tab2, "Table2_FK");  
  
      // Add Col22 as the foreign key column.   
      ForeignKeyColumn fkc = new ForeignKeyColumn(fk, "Col22", "Col1");  
      fk.Columns.Add(fkc);  
      fk.ReferencedTable = "Table1";  
  
      // Create the foreign key on the instance of SQL Server.   
      fk.Create();                    
  
      // Get list of Foreign Keys on Table2  
      foreach (ForeignKey f in tab2.ForeignKeys) {  
            Console.WriteLine(f.Name + " " + f.ReferencedTable + " " + f.ReferencedKey);  
      }  
  
      // Get list of Foreign Keys referencing table1  
      foreach (Table tab in db.Tables) {  
         if (tab == tab1)  
            continue;  
            foreach (ForeignKey f in tab.ForeignKeys) {  
               if (f.ReferencedTable.Equals(tab1.Name))  
                  Console.WriteLine(f.Name + " " + f.Parent.Name);  
            }  
      }  
   }  
}  
```  
  
 範例的 Visual Basic 版本：  
  
```  
' compile with:   
' /r:Microsoft.SqlServer.Smo.dll   
' /r:microsoft.sqlserver.management.sdk.sfc.dll   
' /r:Microsoft.SqlServer.ConnectionInfo.dll  
' /r:Microsoft.SqlServer.SqlEnum.dll  
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Sdk.Sfc  
Imports Microsoft.SqlServer.Management.Common  
  
Public Class A  
   Public Shared Sub Main()  
      Dim svr As New Server()  
      Dim db As New Database(svr, "TESTDB")  
      db.Create()  
  
      ' PK Table  
      Dim tab1 As New Table(db, "Table1")  
  
      ' Define Columns and add them to the table  
      Dim col1 As New Column(tab1, "Col1", DataType.Int)  
  
      col1.Nullable = False  
      tab1.Columns.Add(col1)  
      Dim col2 As New Column(tab1, "Col2", DataType.NVarChar(50))  
      tab1.Columns.Add(col2)  
      Dim col3 As New Column(tab1, "Col3", DataType.DateTime)  
      tab1.Columns.Add(col3)  
  
      ' Create the ftable  
      tab1.Create()  
  
      ' Define Index object on the table by supplying the Table1 as the parent table and the primary key name in the constructor.  
      Dim pk As New Index(tab1, "Table1_PK")  
      pk.IndexKeyType = IndexKeyType.DriPrimaryKey  
  
      ' Add Col1 as the Index Column  
      Dim idxCol1 As New IndexedColumn(pk, "Col1")  
      pk.IndexedColumns.Add(idxCol1)  
  
      ' Create the Primary Key  
      pk.Create()  
  
      ' Create Unique Index on the table  
      Dim unique As New Index(tab1, "Table1_Unique")  
      unique.IndexKeyType = IndexKeyType.DriUniqueKey  
  
      ' Add Col1 as the Unique Index Column  
      Dim idxCol2 As New IndexedColumn(unique, "Col2")  
      unique.IndexedColumns.Add(idxCol2)  
  
      ' Create the Unique Index  
      unique.Create()  
  
      ' Create Table2                    
      Dim tab2 As New Table(db, "Table2")  
      Dim col21 As New Column(tab2, "Col21", DataType.NChar(20))  
      tab2.Columns.Add(col21)  
      Dim col22 As New Column(tab2, "Col22", DataType.Int)  
      tab2.Columns.Add(col22)  
      tab2.Create()  
  
      ' Define a Foreign Key object variable by supplying the Table2 as the parent table and the foreign key name in the constructor.   
      Dim fk As New ForeignKey(tab2, "Table2_FK")  
  
      ' Add Col22 as the foreign key column.   
      Dim fkc As New ForeignKeyColumn(fk, "Col22", "Col1")  
      fk.Columns.Add(fkc)  
      fk.ReferencedTable = "Table1"  
  
      ' Create the foreign key on the instance of SQL Server.   
      fk.Create()  
  
      ' Get list of Foreign Keys on Table2  
      For Each f As ForeignKey In tab2.ForeignKeys  
         Console.WriteLine((f.Name + " " + f.ReferencedTable & " ") + f.ReferencedKey)  
      Next  
  
      ' Get list of Foreign Keys referencing table1  
      For Each tab As Table In db.Tables  
         If (tab.Name.Equals(tab1.Name)) Then  
            Continue For  
         End If  
         For Each f As ForeignKey In tab.ForeignKeys  
            If f.ReferencedTable.Equals(tab1.Name) Then  
               Console.WriteLine(f.Name + " " + f.Parent.Name)  
            End If  
         Next  
      Next  
   End Sub  
End Class  
```  
  
  
