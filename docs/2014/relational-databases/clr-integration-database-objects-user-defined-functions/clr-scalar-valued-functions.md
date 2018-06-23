---
title: CLR 純量值函式 |Microsoft 文件
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
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- SVF
- scalar-valued functions
ms.assetid: 20dcf802-c27d-4722-9cd3-206b1e77bee0
caps.latest.revision: 81
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 93c56555b0a11e2638f58019f6214c8c6971760c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146964"
---
# <a name="clr-scalar-valued-functions"></a>CLR 純量值函式
  純量值函式 (SVF) 傳回單一值，如字串、整數或位元值。您可以使用任何 .NET Framework 程式語言，以 Managed 程式碼建立純量值的使用者定義函數。 這些函數可供 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或其他 Managed 程式碼存取。 針對 CLR 整合和 managed 程式碼之間選擇的優勢的相關資訊和[!INCLUDE[tsql](../../includes/tsql-md.md)]，請參閱[CLR 整合的概觀](../clr-integration/clr-integration-overview.md)。  
  
## <a name="requirements-for-clr-scalar-valued-functions"></a>CLR 純量值函式的需求  
 .NET Framework SVF 會在 .NET Framework 組件中實作為類別上的方法。 輸入的參數和從 SVF 傳回的型別可以是任何純量資料類型所支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，除了`varchar`， `char`， `rowversion`， `text`， `ntext`， `image`， `timestamp`， `table`，或`cursor`。 SVF 必須確保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型與實作方法的傳回資料類型相符。 如需類型轉換的詳細資訊，請參閱[對應 CLR 參數資料](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。  
  
 當以 .NET Framework 語言實作 .NET Framework SVF 時，您可藉由指定 `SqlFunction` 自訂屬性，併入有關此函數的其他資訊。 `SqlFunction` 屬性會指出當函數具有決定性或涉及浮點運算時，是否可以存取或修改資料。  
  
 純量值使用者定義函數可能具有決定性，也可能不具決定性。 當以一組特定的輸入參數呼叫具有決定性的函數時，一律會傳回相同的結果。 當以一組特定的輸入參數呼叫不具決定性的函數時，它可能會傳回不同的結果。  
  
> [!NOTE]  
>  在提供相同輸入值和相同資料庫狀態時，如果某個函數不一定會產生相同輸出值，請勿將這個函數標示為具有決定性。 當某個函數不是真的具有決定性卻將它標示為具有決定性時，可能會導致索引檢視表和計算資料行損毀。 您可以將 `IsDeterministic` 屬性設定為 true，將函數標示為具有決定性。  
  
### <a name="table-valued-parameters"></a>資料表值參數  
 資料表值參數 (TVP) 是使用者定義資料表類型，會傳入到程序或函數中，提供有效的方式將資料的多個資料列傳遞到伺服器。 雖然 TVP 提供相似的功能給參數陣列，但是也提供更大的彈性和與 [!INCLUDE[tsql](../../includes/tsql-md.md)] 更緊密的整合。 它們也能夠協助您獲得更佳的效能。 TVP 也減少與伺服器之間的往返次數。 除了傳送多個要求到伺服器 (例如夾帶純量參數的清單)，資料能以 TVP 的形式傳送到伺服器。 使用者定義資料表類型無法以資料表值參數的形式傳遞到 Managed 預存程序或在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序中執行的函數，也無法從該預存程序或函數傳回。 如需有關 Tvp 的詳細資訊，請參閱[使用資料表值參數&#40;Database Engine&#41;](../tables/use-table-valued-parameters-database-engine.md)。  
  
## <a name="example-of-a-clr-scalar-valued-function"></a>CLR 純量值函式的範例  
 以下是可存取資料並傳回整數值的簡單 SVF：  
  
```csharp  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
  
public class T  
{  
    [SqlFunction(DataAccess = DataAccessKind.Read)]  
    public static int ReturnOrderCount()  
    {  
        using (SqlConnection conn   
            = new SqlConnection("context connection=true"))  
        {  
            conn.Open();  
            SqlCommand cmd = new SqlCommand(  
                "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
            return (int)cmd.ExecuteScalar();  
        }  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Public Class T  
    <SqlFunction(DataAccess:=DataAccessKind.Read)> _  
    Public Shared Function ReturnOrderCount() As Integer  
        Using conn As New SqlConnection("context connection=true")  
            conn.Open()  
            Dim cmd As New SqlCommand("SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
            Return CType(cmd.ExecuteScalar(), Integer)  
        End Using  
    End Function  
End Class  
```  
  
 第一行程式碼會參考 `Microsoft.SqlServer.Server` 來存取屬性，並參考 `System.Data.SqlClient` 來存取 ADO.NET 命名空間  (此命名空間包含 `SqlClient`，也就是 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])。  
  
 接下來，此函數會接收 `SqlFunction` 自訂屬性，該屬性可在 `Microsoft.SqlServer.Server` 命名空間中找到。 此自訂屬性會指出使用者定義函數 (UDF) 是否會使用同處理序提供者來讀取伺服器上的資料。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允許 UDF 更新、插入或刪除資料。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以讓不使用同處理序提供者之 UDF 的執行最佳化。 將 `DataAccessKind` 設定為 `DataAccessKind.None` 可表示這一點。 在下一行中，目標方法為 public static (Visual Basic .NET 中則為 shared)。  
  
 然後位於 `SqlContext` 命名空間的 `Microsoft.SqlServer.Server` 類別可以使用已經設定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的連接來存取 `SqlCommand` 物件。 也可透過 `System.Transactions` 應用程式開發介面 (API) 來使用目前的交易內容，不過這裡並不會使用。  
  
 如果開發人員已經撰寫會使用 `System.Data.SqlClient` 命名空間內之類型的用戶端應用程式，應該會覺得函數主體內的大多數程式碼行看起來很類似。  
  
 [C#]  
  
```  
using(SqlConnection conn = new SqlConnection("context connection=true"))   
{  
   conn.Open();  
   SqlCommand cmd = new SqlCommand(  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
   return (int) cmd.ExecuteScalar();  
}    
```  
  
 [Visual Basic]  
  
```  
Using conn As New SqlConnection("context connection=true")  
   conn.Open()  
   Dim cmd As New SqlCommand( _  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
   Return CType(cmd.ExecuteScalar(), Integer)  
End Using  
```  
  
 適當的命令文字是藉由初始化 `SqlCommand` 物件來指定。 上述範例會計算 `SalesOrderHeader` 資料表中的資料列數。 接下來會呼叫 `ExecuteScalar` 物件的 `cmd` 方法。 這樣會根據查詢傳回 `int` 類型的值。 最後，訂單計數會傳回到呼叫端。  
  
 如果將這段程式碼儲存在名為 FirstUdf.cs 的檔案中，它可以依照以下方式編譯成組件：  
  
 [C#]  
  
```  
csc.exe /t:library /out:FirstUdf.dll FirstUdf.cs   
```  
  
 [Visual Basic]  
  
```  
vbc.exe /t:library /out:FirstUdf.dll FirstUdf.vb  
```  
  
> [!NOTE]  
>  `/t:library` 表示應該產生程式庫，而不是可執行檔。 可執行檔無法在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中註冊。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，不支援以 `/clr:pure` 編譯之 Visual C++ 資料庫物件的執行。 例如，這類資料庫物件包括純量值函式。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢及註冊組件和 UDF 的範例引動過程為：  
  
```  
CREATE ASSEMBLY FirstUdf FROM 'FirstUdf.dll';  
GO  
  
CREATE FUNCTION CountSalesOrderHeader() RETURNS INT   
AS EXTERNAL NAME FirstUdf.T.ReturnOrderCount;   
GO  
  
SELECT dbo.CountSalesOrderHeader();  
GO  
  
```  
  
 請注意，[!INCLUDE[tsql](../../includes/tsql-md.md)] 中公開的函數名稱不必符合目標 public static 方法的名稱。  
  
## <a name="see-also"></a>另請參閱  
 [對應 CLR 參數資料](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)   
 [CLR 整合自訂屬性的概觀](../../database-engine/dev-guide/overview-of-clr-integration-custom-attributes.md)   
 [使用者定義函式](../user-defined-functions/user-defined-functions.md)   
 [從 CLR 資料庫物件進行資料存取](../clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  