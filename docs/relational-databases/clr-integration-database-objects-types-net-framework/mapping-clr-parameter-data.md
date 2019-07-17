---
title: 對應 CLR 參數資料 |Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlBinary data type
- SqlInt16 data type
- SqlMoney data type
- SqlString data type
- SqlSingle data type
- data types [CLR integration]
- SqlInt64 data type
- SqlDateTime data type
- SqlXml data type
- SqlBoolean data type
- SqlDecimal data type
- SqlBytes data type
- mapping data types [CLR integration]
- SqlChars data type
- SqlInt32 data type
ms.assetid: 89b43ee9-b9ad-4281-a4bf-c7c8d116daa2
author: rothja
ms.author: jroth
ms.openlocfilehash: 530db4d31d3db4773713816f1b68404990997512
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081307"
---
# <a name="mapping-clr-parameter-data"></a>對應 CLR 參數資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  下表列出[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型、 common language runtime (CLR) 中的對應項[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中**System.Data.SqlTypes**命名空間，其原生 CLR 對等項目中[!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET framework。  
  
||||  
|-|-|-|  
|**SQL Server 資料類型**|類型 (在 System.Data.SqlTypes 或 Microsoft.SqlServer.Types 中)|**CLR 資料類型 (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64，可為 Null\<Int64 >**|  
|**binary**|**SqlBytes、 SqlBinary**|**Byte[]**|  
|**bit**|**SqlBoolean**|**布林值，可為 Null\<布林值 >**|  
|**char**|None|None|  
|**cursor**|None|None|  
|**date**|**SqlDateTime**|**日期時間，可為 Null\<日期時間 >**|  
|**datetime**|**SqlDateTime**|**日期時間，可為 Null\<日期時間 >**|  
|**datetime2**|None|**日期時間，可為 Null\<日期時間 >**|  
|**DATETIMEOFFSET**|**無**|**DateTimeOffset，可為 Null\<DateTimeOffset >**|  
|**decimal**|**SqlDecimal**|**Decimal，可為 Null\<十進位 >**|  
|**float**|**SqlDouble**|**Double，可為 Null\<雙 >**|  
|**地理位置**|**SqlGeography**<br /><br /> **SqlGeography**定義於 Microsoft.SqlServer.Types.dll 中，它會隨 SQL Server，並可以從下載[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][功能套件](https://www.microsoft.com/download/details.aspx?id=52676)。|None|  
|**幾何**|**SqlGeometry**<br /><br /> **SqlGeometry**定義於 Microsoft.SqlServer.Types.dll 中，它會隨 SQL Server，並可以從下載[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][功能套件](https://www.microsoft.com/download/details.aspx?id=52676)。|None|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId**定義於 Microsoft.SqlServer.Types.dll 中，它會隨 SQL Server，並可以從下載[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][功能套件](https://www.microsoft.com/download/details.aspx?id=52676)。|None|  
|**image**|None|None|  
|**int**|**SqlInt32**|**Int32，可為 Null\<Int32 >**|  
|**money**|**SqlMoney**|**Decimal，可為 Null\<十進位 >**|  
|**nchar**|**SqlChars SqlString**|**String，Char]**|  
|**ntext**|None|None|  
|**numeric**|**SqlDecimal**|**Decimal，可為 Null\<十進位 >**|  
|**nvarchar**|**SqlChars SqlString**<br /><br /> **SQLChars**是較佳的相符項目，如資料傳輸和存取，並**SQLString**是比較適合執行 String 作業。|**String，Char]**|  
|**nvarchar(1)、 nchar(1)**|**SqlChars SqlString**|**Char、 String，Char []，可為 Null\<char >**|  
|**real**|**SqlSingle** (各種**SqlSingle**，不過，大於**實際**)|**單一、 可為 Null\<單一 >**|  
|**rowversion**|None|**Byte[]**|  
|**smallint**|**SqlInt16**|**Int16，可為 Null\<Int16 >**|  
|**smallmoney**|**SqlMoney**|**Decimal，可為 Null\<十進位 >**|  
|**sql_variant**|None|**物件**|  
|**table**|None|None|  
|**text**|None|None|  
|**time**|None|**時間範圍，可為 Null\<TimeSpan >**|  
|**timestamp**|None|None|  
|**tinyint**|**SqlByte**|**位元組，可為 Null\<位元組 >**|  
|**uniqueidentifier**|**SqlGuid**|**Guid，可為 Null\<Guid >**|  
|**使用者定義的 type(UDT)**|None|繫結到相同組件或相依組件中之使用者定義型別的相同類別。|  
|**varbinary**|**SqlBytes、 SqlBinary**|**Byte[]**|  
|**varbinary(1)、 binary(1)**|**SqlBytes、 SqlBinary**|**byte、 Byte []、 Nullable\<位元組 >**|  
|**varchar**|None|None|  
|**xml**|**SqlXml**|None|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>利用 Out 參數自動轉換資料類型  
 CLR 方法可以傳回給呼叫的程式碼或程式資訊標記一個輸入的參數**放大**修飾詞 (Microsoft Visual C#) 或 **\<Out() > ByRef** (Microsoft Visual Basic)如果輸入的參數是中的 CLR 資料類型**System.Data.SqlTypes**命名空間，而且呼叫程式會指定它的對等[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型當做輸入參數，會自動進行類型轉換當 CLR 方法傳回的資料類型。  
  
 例如，下列 CLR 預存程序有輸入的參數的**SqlInt32**標示為的 CLR 資料類型**out** (C#) 或 **\<Out() > ByRef** (Visual Basic):  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ ... }  
```  
  
```vb  
\<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( \<Out()> ByRef value As SqlInt32)  
...  
End Sub  
```  
  
 建置與資料庫中建立組件之後，會在建立預存程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用下列 TRANSACT-SQL，指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型**int**做為輸出參數：  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 CLR 預存程序呼叫， **SqlInt32**資料類型會自動轉換成**int**資料型別，並傳回給呼叫端程式。  
  
 不過，並非所有 CLR 資料類型都可以透過 out 參數，自動轉換為其對等的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。 下表列出這些例外。  
  
|||  
|-|-|  
|**CLR 資料類型 (SQL Server)**|**SQL Server 資料類型**|  
|**十進位**|SMALLMONEY|  
|**SqlMoney**|SMALLMONEY|  
|**十進位**|money|  
|**DateTime**|smalldatetime|  
|**SQLDateTime**|smalldatetime|  
  
## <a name="change-history"></a>變更記錄  
  
|更新的內容|  
|---------------------|  
|新增**SqlGeography**， **SqlGeometry**，並**SqlHierarchyId**對應資料表中的類型。|  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 的 SQL Server 資料類型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
