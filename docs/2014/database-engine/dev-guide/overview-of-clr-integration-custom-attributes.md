---
title: CLR 整合自訂屬性的概觀 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- custom attributes [CLR integration]
- attributes [CLR integration]
- common language runtime [SQL Server], attributes
- database objects [CLR integration], custom attributes
- building database objects [CLR integration], custom attributes
ms.assetid: ecf5c097-0972-48e2-a9c0-b695b7dd2820
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8df7881dd5f38935628cb6653d57763a8846e60f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62781103"
---
# <a name="overview-of-clr-integration-custom-attributes"></a>CLR 整合自訂屬性的概觀
  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的 Common Language Runtime (CLR) 允許使用描述性的關鍵字 (稱為屬性)。 這些屬性會針對許多元素 (如方法和類別) 提供其他資訊。 屬性會隨著物件的中繼資料儲存在組件中，而且可用來將程式碼描述給其他開發工具知道，或是影響 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內的執行階段行為。  
  
 當您向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 註冊 CLR 常式時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會衍生一組有關此常式的屬性。 這些常式屬性會決定該常式的功能，包括是否可以為此常式建立索引。 例如，將 `DataAccess` 屬性設定為 `DataAccessKind.Read` 可讓您從 CLR 函數內的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者資料表存取資料。 下列範例會示範簡單的情況下所在`DataAccess`屬性設定為從使用者資料表的資料存取方便**table1**。  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
  
public partial class UserDefinedFunctions  
{  
    [SqlFunction(DataAccess = DataAccessKind.Read)]  
    public static string func1()  
    {  
        // Open a connection and create a command  
        SqlConnection conn = new SqlConnection("context connection = true");  
        conn.Open();  
        SqlCommand cmd = conn.CreateCommand();  
        cmd.CommandText = "SELECT str_val FROM table1 WHERE int_val = 10";  
        // where table1 is a user table  
        // Execute this command   
        SqlDataReader rd = cmd.ExecuteReader();  
        // Set string ret_val to str_val returned from the query  
        string ret_val = rd.GetValue(0).ToString();  
        rd.Close();  
        return ret_val;  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Public partial Class UserDefinedFunctions  
    <SqlFunction(DataAccess = DataAccessKind.Read)> _   
    Public Shared Function func1() As String  
        ' Open a connection and create a command  
        Dim conn As SqlConnection = New SqlConnection("context connection = true")   
        conn.Open()  
        Dim cmd As SqlCommand =  conn.CreateCommand()   
        cmd.CommandText = "SELECT str_val FROM table1 WHERE int_val = 10"  
        ' where table1 is a user table  
        ' Execute this command   
        Dim rd As SqlDataReader =  cmd.ExecuteReader()   
        ' Set string ret_val to str_val returned from the query  
        Dim ret_val As String =  rd.GetValue(0).ToString()   
        rd.Close()  
        Return ret_val  
    End Function  
End Class  
```  
  
 如果是 [!INCLUDE[tsql](../../includes/tsql-md.md)] 常式，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會直接從常式定義衍生常式屬性。 如果是 CLR 常式，伺服器不會分析常式的主體來衍生這些屬性。 您可以改為將自訂屬性用於使用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 語言實作的類別和類別成員。  
  
 CLR 常式、使用者定義型別和彙總所需的自訂屬性會定義在 `Microsoft.SqlServer.Server` 命名空間內。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 常式的自訂屬性](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)  
  
  
