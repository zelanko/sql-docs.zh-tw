---
title: CLR Scalar 值函數 |微軟文件
description: 標量值函數返回單個值。 在 SQL Server CLR 整合中,可以在託管代碼中編寫標量值使用者定義的函數。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- SVF
- scalar-valued functions
ms.assetid: 20dcf802-c27d-4722-9cd3-206b1e77bee0
author: rothja
ms.author: jroth
ms.openlocfilehash: a44187fc41409d149501c4cda7e99817be034a12
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488415"
---
# <a name="clr-scalar-valued-functions"></a>CLR 純量值函式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  純量值函式 (SVF) 會傳回單一值，如字串、整數或位元值。 您可以使用任何 .NET Framework 程式設計語言在託管代碼中創建標量值使用者定義的函數。 這些函數可供 [!INCLUDE[tsql](../../includes/tsql-md.md)] 或其他 Managed 程式碼存取。 有關 CLR 整合的優點以及託管代碼[!INCLUDE[tsql](../../includes/tsql-md.md)]和之間的選擇,請參閱[CLR 整合概述](../../relational-databases/clr-integration/clr-integration-overview.md)。  
  
## <a name="requirements-for-clr-scalar-valued-functions"></a>CLR 純量值函式的需求  
 .NET Framework SVF 會在 .NET Framework 組件中實作為類別上的方法。 從 SVF 傳回的輸入參數和類型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以是 支援的任何標量資料類型,但**varchar、char、****char****行版本**,**文字****、ntext、****影像**,**時間戳**, 或**游標**除外。**table** SVF 必須確保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型與實作方法的傳回資料類型相符。 有關類型轉換的詳細資訊,請參閱[映射 CLR 參數資料](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。  
  
 在 .NET Framework 語言中實現 .NET 框架 SVF 時,可以指定**SqlFunction**自定義屬性以包含有關該函數的其他資訊。 **SqlFunction**屬性指示函數是否訪問或修改數據(如果是確定性數據),以及函數是否涉及浮點操作。  
  
 純量值使用者定義函數可能具有決定性，也可能不具決定性。 當以一組特定的輸入參數呼叫具有決定性的函數時，一律會傳回相同的結果。 當以一組特定的輸入參數呼叫不具決定性的函數時，它可能會傳回不同的結果。  
  
> [!NOTE]  
>  在提供相同輸入值和相同資料庫狀態時，如果某個函數不一定會產生相同輸出值，請勿將這個函數標示為具有決定性。 當某個函數不是真的具有決定性卻將它標示為具有決定性時，可能會導致索引檢視表和計算資料行損毀。 通過將 **「確定」** 屬性設置為 true,將函數標記為確定性。  
  
### <a name="table-valued-parameters"></a>資料表值參數  
 資料表值參數 (TVP) 是使用者定義資料表類型，會傳入到程序或函數中，提供有效的方式將資料的多個資料列傳遞到伺服器。 雖然 TVP 提供相似的功能給參數陣列，但是也提供更大的彈性和與 [!INCLUDE[tsql](../../includes/tsql-md.md)] 更緊密的整合。 它們也能夠協助您獲得更佳的效能。 TVP 也減少與伺服器之間的往返次數。 除了傳送多個要求到伺服器 (例如夾帶純量參數的清單)，資料能以 TVP 的形式傳送到伺服器。 使用者定義資料表類型無法以資料表值參數的形式傳遞到 Managed 預存程序或在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序中執行的函數，也無法從該預存程序或函數傳回。 有關 TVP 的詳細資訊,請參閱[使用表值參數&#40;資料庫引擎&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)。  
  
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
  
 第一行代碼引用**Microsoft.SqlServer.Server.Server**存取屬性和**系統.Data.SqlClient**以造訪ADO.NET命名空間。 ( 此命名空間包含**SqlClient**,.NET[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]框架資料提供者 。  
  
 接下來,該函數接收**SqlFunction**自定義屬性,該屬性位於**Microsoft.SqlServer.Server**命名空間中。 此自訂屬性會指出使用者定義函數 (UDF) 是否會使用同處理序提供者來讀取伺服器上的資料。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允許 UDF 更新、插入或刪除資料。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以讓不使用同處理序提供者之 UDF 的執行最佳化。 這是通過設置**數據訪問金德****數據訪問金指示的。** 在下一行中，目標方法為 public static (Visual Basic .NET 中則為 shared)。  
  
 **SqlContext**類位於**Microsoft.SqlServer.Server.Server**命名空間中,然後可以存取**SqlCommand**物件,該物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]與已設置的實例連接。 雖然此處未使用,但當前事務上下文也可通過**System.事務**應用程式程式設計介面 (API) 獲得。  
  
 函數體中的大多數代碼行應該看起來熟悉那些編寫了使用**System.Data.SqlClient**命名空間中找到類型的用戶端應用程式的開發人員。  
  
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
  
 通過初始化**SqlCommand**物件指定相應的命令文本。 前面的範例計算表**SalesOrderHeader**中的行數。 接下來,調用**cmd**物件的**ExecuteScalar**方法。 這將返回基於查詢的類型**int**的值。 最後，訂單計數會傳回到呼叫端。  
  
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
>  使用 **/clr:pure**編譯的可視C++資料庫物件不支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 上 執行。 例如，這類資料庫物件包括純量值函式。  
  
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
 [對應 CLR 參數資料](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)   
 [CLR 整合自訂屬性概述](https://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)   
 [使用者定義的函數](../../relational-databases/user-defined-functions/user-defined-functions.md)   
 [從 CLR 資料庫物件進行資料存取](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
