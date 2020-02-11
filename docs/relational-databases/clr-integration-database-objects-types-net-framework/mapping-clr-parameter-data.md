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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081307"
---
# <a name="mapping-clr-parameter-data"></a>對應 CLR 參數資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  下[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表列出資料類型、在**SqlTypes**命名空間中的 common language runtime （CLR） [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的對等專案，以及其在[!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 中的原生 CLR 對應項。  
  
||||  
|-|-|-|  
|**SQL Server 資料類型**|類型 (在 System.Data.SqlTypes 或 Microsoft.SqlServer.Types 中)|**CLR 資料類型 (.NET Framework)**|  
|**Bigint**|**SqlInt64**|**Int64、可\<為 null 的 int64>**|  
|**binary**|**SqlBytes、SqlBinary**|**Byte []**|  
|**bit**|**SqlBoolean**|**布林值、\<可為 null 的布林值>**|  
|**char**|None|None|  
|**cursor**|None|None|  
|**date**|**SqlDateTime**|**DateTime、可\<為 null 的 datetime>**|  
|**datetime**|**SqlDateTime**|**DateTime、可\<為 null 的 datetime>**|  
|**datetime2**|None|**DateTime、可\<為 null 的 datetime>**|  
|**DATETIMEOFFSET**|**無**|**DateTimeOffset、可\<為 null 的 datetimeoffset>**|  
|**decimal**|**SqlDecimal**|**十進位、可\<為 null 的十進位>**|  
|**float**|**SqlDouble**|**Double、可\<為 null 的 double>**|  
|**地理位置**|**SqlGeography**<br /><br /> **SqlGeography**是定義在與 SQL Server 一起安裝，而且可以從[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能套件](https://www.microsoft.com/download/details.aspx?id=52676)下載的。|None|  
|**幾何**|**SqlGeometry**<br /><br /> **SqlGeometry**是定義在與 SQL Server 一起安裝，而且可以從[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能套件](https://www.microsoft.com/download/details.aspx?id=52676)下載的。|None|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId**是定義在與 SQL Server 一起安裝，而且可以從[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能套件](https://www.microsoft.com/download/details.aspx?id=52676)下載的。|None|  
|**image**|None|None|  
|**int**|**SqlInt32**|**Int32、可\<為 null 的 int32>**|  
|**money**|**SqlMoney**|**十進位、可\<為 null 的十進位>**|  
|**nchar**|**SqlChars、SqlString**|**String, Char[]**|  
|**ntext**|None|None|  
|**數值**|**SqlDecimal**|**十進位、可\<為 null 的十進位>**|  
|**nvarchar**|**SqlChars、SqlString**<br /><br /> **SQLChars**是較佳的資料傳輸和存取比對，而**SQLString**則是更符合執行字串作業的結果。|**String, Char[]**|  
|**Nvarchar （1）、Nchar （1）**|**SqlChars、SqlString**|**Char、String、Char []、可\<為 null 的 Char>**|  
|**即時**|**SqlSingle** （不過， **SqlSingle**的範圍大於**real**）|**單一、可\<為 null 的單一>**|  
|**rowversion**|None|**Byte []**|  
|**smallint**|**SqlInt16**|**Int16、可\<為 null 的 int16>**|  
|**SMALLMONEY**|**SqlMoney**|**十進位、可\<為 null 的十進位>**|  
|**sql_variant**|None|**Object**|  
|**目錄**|None|None|  
|**text**|None|None|  
|**time**|None|**TimeSpan、可\<為 null 的 timespan>**|  
|**timestamp**|None|None|  
|**tinyint**|**SqlByte**|**Byte、可\<為 null 的 byte>**|  
|**uniqueidentifier**|**SqlGuid**|**Guid、可\<為 null 的 guid>**|  
|**使用者定義型別（UDT）**|None|繫結到相同組件或相依組件中之使用者定義型別的相同類別。|  
|**varbinary**|**SqlBytes、SqlBinary**|**Byte []**|  
|**Varbinary （1）、binary （1）**|**SqlBytes、SqlBinary**|**byte、Byte []、可\<為 null 的 byte>**|  
|**varchar**|None|None|  
|**stl**|**SqlXml**|None|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>利用 Out 參數自動轉換資料類型  
 如果輸入參數是系統中的 CLR 資料類型，CLR 方法可以將輸入參數標記為**out**修飾詞（microsoft Visual c #）或** \<out （） > ByRef** （microsoft Visual Basic），藉以將資訊傳回給呼叫程式碼或程式 **。 SqlTypes**命名空間和呼叫程式會將其對[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]等的資料類型指定為輸入參數，當 CLR 方法傳回資料類型時，會自動發生類型轉換。  
  
 例如，下列 clr 預存程式有一個**SqlInt32** CLR 資料類型的輸入參數，其標記為**out** （c #）或** \<out （） > ByRef** （Visual Basic）：  
  
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
  
 在資料庫中建立並建立元件之後，會在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用下列 transact-sql 來建立預存程式，其會將[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int**的資料類型指定為輸出參數：  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 呼叫 CLR 預存程式時， **SqlInt32**資料類型會自動轉換成**int**資料類型，並傳回給呼叫的進程。  
  
 不過，並非所有 CLR 資料類型都可以透過 out 參數，自動轉換為其對等的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。 下表列出這些例外。  
  
|||  
|-|-|  
|**CLR 資料類型 (SQL Server)**|**SQL Server 資料類型**|  
|**十**|SMALLMONEY|  
|**SqlMoney**|SMALLMONEY|  
|**十**|money|  
|**從中**|smalldatetime|  
|**SQLDateTime**|smalldatetime|  
  
## <a name="change-history"></a>變更記錄  
  
|更新的內容|  
|---------------------|  
|已將**SqlGeography**、 **SqlGeometry**和**SqlHierarchyId**類型加入至對應資料表。|  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 的 SQL Server 資料類型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
