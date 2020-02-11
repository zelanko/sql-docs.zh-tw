---
title: 建立、改變和移除使用者定義函數 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- user-defined functions [SMO]
ms.assetid: 0ebebd3b-0775-41c2-989d-aa4cf81af12a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: edde17b3339a6a78f81ddf92da95afb2f8ba851c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "72782353"
---
# <a name="creating-altering-and-removing-user-defined-functions"></a>建立、改變和移除使用者定義函數
  物件<xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction>所提供的功能，可讓使用者以程式設計方式管理[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的使用者定義函數。 使用者定義函數支援輸入和輸出參數，也支援資料表資料行的直接參考。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 需要先在資料庫內註冊組件，然後才能在預存程序、使用者定義函數、觸發程序和使用者定義資料類型中使用組件。 SMO 以 <xref:Microsoft.SqlServer.Management.Smo.SqlAssembly> 物件支援此功能。  
  
 
  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> 物件會以 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.AssemblyName%2A>、<xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.ClassName%2A> 和 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.MethodName%2A> 屬性參考 .NET 組件。  
  
 當 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> 物件參考 .NET 組件時，您必須藉由建立 <xref:Microsoft.SqlServer.Management.Smo.SqlAssembly> 物件並將其加入至 <xref:Microsoft.SqlServer.Management.Smo.SqlAssemblyCollection> 物件 (後者屬於 <xref:Microsoft.SqlServer.Management.Smo.Database> 物件) 來註冊該組件。  
  
## <a name="example"></a>範例  
 如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊，請參閱[在 Visual Studio .net 中建立 VISUAL BASIC SMO 專案](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)或[在 Visual Studio .Net 中建立 VISUAL C&#35; SMO 專案](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-basic"></a>在 Visual Basic 中建立純量使用者定義函數  
 這個程式碼範例示範如何在 <xref:System.DateTime> 中，建立及移除具有輸入 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 物件參數和整數傳回類型的純量使用者定義函數。 使用者定義函數會建立在 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 資料庫上。 此範例會建立使用者定義函數 ISOweek，該函數取用日期引數並計算 ISO 週數。 為了讓這個函數能夠正確計算，必須先將資料庫 DATEFIRST 選項設定為 1，才能呼叫該函數。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBUserDefFuncs1](SMO How to#SMO_VBUserDefFuncs1)]  -->  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-c"></a>在 Visual C# 中建立純量使用者定義函數  
 這個程式碼範例示範如何在 <xref:System.DateTime> 中，建立及移除具有輸入 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] 物件參數和整數傳回類型的純量使用者定義函數。 使用者定義函數會建立在 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 資料庫上。 本範例會建立使用者定義函數。 `ISOweek`. 這個函數採用日期引數並計算 ISO 週數。 為了讓這個函數能夠正確計算，必須先將資料庫 `DATEFIRST` 選項設定為 `1` ，才能呼叫該函數。  
  
```csharp
{  
            //Connect to the local, default instance of SQL Server.   
           Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
           Database db = srv.Databases["AdventureWorks2012"];  
  
            //Define a UserDefinedFunction object variable by supplying the parent database and the name arguments in the constructor.   
            UserDefinedFunction udf = new UserDefinedFunction(db, "IsOWeek");  
  
            //Set the TextMode property to false and then set the other properties.   
            udf.TextMode = false;  
            udf.DataType = DataType.Int;  
            udf.ExecutionContext = ExecutionContext.Caller;  
            udf.FunctionType = UserDefinedFunctionType.Scalar;  
            udf.ImplementationType = ImplementationType.TransactSql;  
  
            //Add a parameter.   
  
     UserDefinedFunctionParameter par = new UserDefinedFunctionParameter(udf, "@DATE", DataType.DateTime);  
            udf.Parameters.Add(par);  
  
            //Set the TextBody property to define the user-defined function.   
            udf.TextBody = "BEGIN DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;";  
  
            //Create the user-defined function on the instance of SQL Server.   
            udf.Create();  
  
            //Remove the user-defined function.   
            udf.Drop();  
        }  
```  
  
## <a name="creating-a-scalar-user-defined-function-in-powershell"></a>在 PowerShell 中建立純量使用者定義函數  
 這個程式碼範例示範如何在 <xref:System.DateTime> 中，建立及移除具有輸入 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] 物件參數和整數傳回類型的純量使用者定義函數。 使用者定義函數會建立在 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 資料庫上。 本範例會建立使用者定義函數。 `ISOweek`. 這個函數採用日期引數並計算 ISO 週數。 為了讓這個函數能夠正確計算，必須先將資料庫 `DATEFIRST` 選項設定為 `1` ，才能呼叫該函數。  
  
```powershell
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = Get-Item Adventureworks2012  
  
# Define a user defined function object variable by supplying the parent database and name arguments in the constructor.
$udf  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunction -argumentlist $db, "IsOWeek"  
  
# Set the TextMode property to false and then set the other properties.
$udf.TextMode = $false  
$udf.DataType = [Microsoft.SqlServer.Management.SMO.DataType]::Int
$udf.ExecutionContext = [Microsoft.SqlServer.Management.SMO.ExecutionContext]::Caller  
$udf.FunctionType = [Microsoft.SqlServer.Management.SMO.UserDefinedFunctionType]::Scalar  
$udf.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Define a Parameter object variable by supplying the parent function, name and type arguments in the constructor.  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$par  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunctionParameter -argumentlist $udf, "@DATE",$type  
  
# Add the parameter to the function  
$udf.Parameters.Add($par)  
  
#Set the TextBody property to define the user-defined function.
$udf.TextBody = "BEGIN DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;"  
  
# Create the user-defined function on the instance of SQL Server.
$udf.Create()  
  
# Remove the user-defined function.
$udf.Drop()  
```  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction>  
