---
title: 對應 CLR 參數資料 :微軟文件
description: 本文列出了 Microsoft SQL Server 資料類型、SQL Server 的 CLR 中的等效項以及 .NET 框架中的本機 CLR 等效項。
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
ms.openlocfilehash: 360a94229b107e9f24bb2a769157c75cdeb3c143
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488450"
---
# <a name="mapping-clr-parameter-data"></a>對應 CLR 參數資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  下表[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]列出了資料類型、在**System.Data.SqlType**命名空間[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中用於通用語言運行時 (CLR) 中的等效項及其本機 CLR 等效項。  
  
||||  
|-|-|-|  
|**SQL Server 資料類型**|類型 (在 System.Data.SqlTypes 或 Microsoft.SqlServer.Types 中)|**CLR 資料類型 (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64,\<空 無因64>**|  
|**binary**|**SqlBytes, SqlBinary**|**位元組***|  
|**bit**|**SqlBoolean**|**布林、\<可 空布爾>**|  
|**char**|None|None|  
|**cursor**|None|None|  
|**date**|**SqlDatetime**|**日期時間,空\<日期時間>**|  
|**datetime**|**SqlDatetime**|**日期時間,空\<日期時間>**|  
|**datetime2**|None|**日期時間,空\<日期時間>**|  
|**日期時間位移**|**None**|**日期時間偏移,空\<日期時間偏移>**|  
|**decimal**|**SqlDecimal**|**十進位,空\<小數>**|  
|**float**|**SqlDouble**|**雙、空\<雙>**|  
|**地理**|**SqlGeography**<br /><br /> **Sql地理在**Microsoft.SqlServer.Type.dll 中定義,它與 SQL Server[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]一起安裝, 可以從[功能包](https://www.microsoft.com/download/details.aspx?id=52676)下載。|None|  
|**幾何**|**SqlGeometry**<br /><br /> **SqlGeometry**在 Microsoft.SqlServer.Type.dll 中定義,它與 SQL Server 一起安裝[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)],可以從[功能包](https://www.microsoft.com/download/details.aspx?id=52676)下載。|None|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId**在 Microsoft.SqlServer.Type.dll 中定義,該伺服器與 SQL[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Server 一起 安裝,可以從[功能包](https://www.microsoft.com/download/details.aspx?id=52676)下載。|None|  
|**image**|None|None|  
|**int**|**SqlInt32**|**Int32,\<空 int32>**|  
|**money**|**SqlMoney**|**十進位,空\<小數>**|  
|**nchar**|**SqlChars, SqlString**|**字串,字元***|  
|**ntext**|None|None|  
|**numeric**|**SqlDecimal**|**十進位,空\<小數>**|  
|**nvarchar**|**SqlChars, SqlString**<br /><br /> **SQLChars**是數據傳輸和訪問的更好匹配 **,SQLString**更適合執行 String 操作。|**字串,字元***|  
|**恩瓦爾查爾(1),nchar(1)**|**SqlChars, SqlString**|**字元、字串、字元、可無字元\<>**|  
|**real**|**SqlSingle(** 但是**SqlSingle**的範圍大於**實際**)|**單、空\<單>**|  
|**rowversion**|None|**位元組***|  
|**smallint**|**SqlInt16**|**Int16,\<空 無因16>**|  
|**smallmoney**|**SqlMoney**|**十進位,空\<小數>**|  
|**sql_variant**|None|**Object**|  
|**table**|None|None|  
|**text**|None|None|  
|**time**|None|**時間跨度,空\<時間跨度>**|  
|**timestamp**|None|None|  
|**tinyint**|**SqlByte**|**位元組,\<空 位元組>**|  
|**uniqueidentifier**|**SqlGuid**|**吉德, 空\<可 貴>**|  
|**使用者定義型態 (UDT)**|None|繫結到相同組件或相依組件中之使用者定義型別的相同類別。|  
|**varbinary**|**SqlBytes, SqlBinary**|**位元組***|  
|**二進位(1),二進制(1)**|**SqlBytes, SqlBinary**|**位元組、位元組*、空\<位元組>**|  
|**varchar**|None|None|  
|**xml**|**SqlXml**|None|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>利用 Out 參數自動轉換資料類型  
 如果輸入參數在**系統中**為 CLR 數據類型,並且調用程式指定其等效數據類型為輸入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]參數,則使用**out**修改器(Microsoft Visual C#) 或**\<out()> ByRef()> ByRef())** 將資訊傳回調用代碼或程式,並且調用程式指定其等效數據類型為輸入參數,則當 CLR 方法返回數據類型時,將自動發生類型轉換。  
  
 例如,以下 CLR 儲存過程具有**SqlInt32** CLR 資料類型的輸入參數,該輸入參數標有**out** (C#) 或**\<out()> ByRef(** 可視基本):  
  
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
  
 在資料庫產生與建立程式集後,使用以下 Transact-SQL[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立儲存程序,該 SQL[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將**int**的資料型態指定 OUTPUT 參數:  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 呼叫 CLR 儲存過程時 **,SqlInt32**資料類型將自動轉換為**int**資料類型,並返回到呼叫程式。  
  
 不過，並非所有 CLR 資料類型都可以透過 out 參數，自動轉換為其對等的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。 下表列出這些例外。  
  
|||  
|-|-|  
|**CLR 資料類型 (SQL Server)**|**SQL Server 資料類型**|  
|**十進位**|SMALLMONEY|  
|**SqlMoney**|SMALLMONEY|  
|**Decimal**|money|  
|**Datetime**|smalldatetime|  
|**SQLDatetime**|smalldatetime|  
  
## <a name="change-history"></a>變更記錄  
  
|更新的內容|  
|---------------------|  
|在映射表中添加了**Sql地理學****、SqlGeometry**和**SqlHierarchyId**類型。|  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 的 SQL Server 資料類型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
