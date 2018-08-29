---
title: 建立、 改變和移除預存程序 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [SMO]
ms.assetid: 2a072f9c-8f11-4364-ab71-3990735a8d66
caps.latest.revision: 47
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: abe3ddc59cef2f2af2a0490eef67127455b04ee8
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43066841"
---
# <a name="creating-altering-and-removing-stored-procedures"></a>建立、改變和移除預存程序
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]管理物件 (SMO) 預存程序由<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure>物件。  
  
 建立<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure>在 SMO 中的物件需要設定<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure.TextBody%2A>屬性設[!INCLUDE[tsql](../../../includes/tsql-md.md)]定義預存程序的指令碼。 參數需要\@前置詞，且必須建立使用的個別<xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter>物件以及加入至<xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter>的集合<xref:Microsoft.SqlServer.Management.Smo.StoredProcedure>物件。  
  
## <a name="example"></a>範例  
 如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊，請參閱 <<c0> [ 建立 Visual C&#35; Visual Studio.NET 中的 SMO 專案](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。</c0>  
  
## <a name="creating-altering-and-removing-a-stored-procedure-in-visual-basic"></a>在 Visual Basic 中建立、改變和移除預存程序  
 此程式碼範例示範如何建立預存程序[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]資料庫。 以下範例在給定員工識別碼時會傳回員工的姓。 預存程序需要一個輸入參數來指定員工識別碼，以及一個輸出參數來傳回員工的姓氏。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a StoredProcedure object variable by supplying the parent database and name arguments in the constructor.
Dim sp As StoredProcedure
sp = New StoredProcedure(db, "GetLastNameByEmployeeID")
'Set the TextMode property to false and then set the other object properties.
sp.TextMode = False
sp.AnsiNullsStatus = False
sp.QuotedIdentifierStatus = False
'Add two parameters.
Dim param As StoredProcedureParameter
param = New StoredProcedureParameter(sp, "@empval", DataType.Int)
sp.Parameters.Add(param)
Dim param2 As StoredProcedureParameter
param2 = New StoredProcedureParameter(sp, "@retval", DataType.NVarChar(50))
param2.IsOutputParameter = True
sp.Parameters.Add(param2)
'Set the TextBody property to define the stored procedure.
Dim stmt As String
stmt = " SELECT @retval = (SELECT LastName FROM Person.Person AS p JOIN HumanResources.Employee AS e ON p.BusinessEntityID = e.BusinessEntityID AND e.BusinessEntityID = @empval )"
sp.TextBody = stmt
'Create the stored procedure on the instance of SQL Server.
sp.Create()
'Modify a property and run the Alter method to make the change on the instance of SQL Server.   
sp.QuotedIdentifierStatus = True
sp.Alter()
'Remove the stored procedure.
sp.Drop()
``` 
  
## <a name="creating-altering-and-removing-a-stored-procedure-in-visual-c"></a>在 Visual C# 中建立、改變和移除預存程序  
 此程式碼範例示範如何建立預存程序[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]資料庫。 以下範例在給定員工識別碼 (`BusinessEntityID`) 時會傳回員工的姓氏。 預存程序需要一個輸入參數來指定員工識別碼，以及一個輸出參數來傳回員工的姓氏。  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a StoredProcedure object variable by supplying the parent database and name arguments in the constructor.   
            StoredProcedure sp;  
            sp = new StoredProcedure(db, "GetLastNameByBusinessEntityID");  
            //Set the TextMode property to false and then set the other object properties.   
            sp.TextMode = false;  
            sp.AnsiNullsStatus = false;  
            sp.QuotedIdentifierStatus = false;  
            //Add two parameters.   
            StoredProcedureParameter param;  
            param = new StoredProcedureParameter(sp, "@empval", DataType.Int);  
            sp.Parameters.Add(param);  
            StoredProcedureParameter param2;  
            param2 = new StoredProcedureParameter(sp, "@retval", DataType.NVarChar(50));  
            param2.IsOutputParameter = true;  
            sp.Parameters.Add(param2);  
            //Set the TextBody property to define the stored procedure.   
            string stmt;  
            stmt = " SELECT @retval = (SELECT LastName FROM Person.Person,HumanResources.Employee WHERE Person.Person.BusinessEntityID = HumanResources.Employee.BusinessentityID AND HumanResources.Employee.BusinessEntityID = @empval )";  
            sp.TextBody = stmt;  
            //Create the stored procedure on the instance of SQL Server.   
            sp.Create();  
            //Modify a property and run the Alter method to make the change on the instance of SQL Server.   
            sp.QuotedIdentifierStatus = true;  
            sp.Alter();  
            //Remove the stored procedure.   
            sp.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-stored-procedure-in-powershell"></a>在 PowerShell 中建立、改變和移除預存程序  
 此程式碼範例示範如何建立預存程序[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]資料庫。 以下範例在給定員工識別碼 (`BusinessEntityID`) 時會傳回員工的姓氏。 預存程序需要一個輸入參數來指定員工識別碼，以及一個輸出參數來傳回員工的姓氏。  
  
```powershell  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a StoredProcedure object variable by supplying the parent database and name arguments in the constructor.   
$sp  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.StoredProcedure `  
-argumentlist $db, "GetLastNameByBusinessEntityID"  
  
#Set the TextMode property to false and then set the other object properties.   
$sp.TextMode = $false  
$sp.AnsiNullsStatus = $false  
$sp.QuotedIdentifierStatus = $false  
  
# Add two parameters  
$type = [Microsoft.SqlServer.Management.SMO.Datatype]::Int  
$param  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.StoredProcedureParameter `  
-argumentlist $sp,"@empval",$type  
$sp.Parameters.Add($param)  
  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::NVarChar(50)  
$param2  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.StoredProcedureParameter `  
-argumentlist $sp,"@retval",$type  
$param2.IsOutputParameter = $true  
$sp.Parameters.Add($param2)  
  
#Set the TextBody property to define the stored procedure.   
$sp.TextBody =  " SELECT @retval = (SELECT LastName FROM Person.Person,HumanResources.Employee WHERE Person.Person.BusinessEntityID = HumanResources.Employee.BusinessentityID AND HumanResources.Employee.BusinessEntityID = @empval )"  
  
# Create the stored procedure on the instance of SQL Server.   
$sp.Create()  
  
# Modify a property and run the Alter method to make the change on the instance of SQL Server.   
$sp.QuotedIdentifierStatus = $true  
$sp.Alter()  
  
#Remove the stored procedure.   
$sp.Drop()  
```  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.SqlServer.Management.Smo.StoredProcedure>  
  
  
