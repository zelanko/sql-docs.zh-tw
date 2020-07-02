---
title: 對應 CLR 參數資料 |Microsoft Docs
description: 本文列出 Microsoft SQL Server 的資料類型、SQL Server 的 CLR 中的對等專案，以及 .NET Framework 中的原生 CLR 對應項。
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
ms.openlocfilehash: 911b56023ea78ec75e605a39a39b705724101dee
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85719934"
---
# <a name="mapping-clr-parameter-data"></a>對應 CLR 參數資料
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  下表列出 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型、在 SqlTypes 命名空間中的 common language RUNTIME （CLR）中的對等專案， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以及其在 .NET Framework 中的原生 CLR 對應項**System.Data.SqlTypes** [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
||||  
|-|-|-|  
|**SQL Server 資料類型**|類型 (在 System.Data.SqlTypes 或 Microsoft.SqlServer.Types 中)|**CLR 資料類型 (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64、Nullable\<Int64>**|  
|**binary**|**SqlBytes、SqlBinary**|**Byte[]**|  
|**bit**|**SqlBoolean**|**布林值，可為 Null\<Boolean>**|  
|**char**|None|None|  
|**cursor**|None|None|  
|**date**|**SqlDateTime**|**DateTime，Nullable\<DateTime>**|  
|**datetime**|**SqlDateTime**|**DateTime，Nullable\<DateTime>**|  
|**datetime2**|None|**DateTime，Nullable\<DateTime>**|  
|**DATETIMEOFFSET**|**None**|**DateTimeOffset，Nullable\<DateTimeOffset>**|  
|**decimal**|**SqlDecimal**|**十進位、可為 Null\<Decimal>**|  
|**float**|**SqlDouble**|**Double、Nullable\<Double>**|  
|**區域**|**SqlGeography**<br /><br /> **SqlGeography**會定義在 Microsoft.SqlServer.Types.dll 中，這會與 SQL Server 一起安裝，而且可以從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能套件](https://www.microsoft.com/download/details.aspx?id=52676)下載。|None|  
|**性質**|**SqlGeometry**<br /><br /> **SqlGeometry**會定義在 Microsoft.SqlServer.Types.dll 中，這會與 SQL Server 一起安裝，而且可以從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能套件](https://www.microsoft.com/download/details.aspx?id=52676)下載。|None|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId**會定義在 Microsoft.SqlServer.Types.dll 中，這會與 SQL Server 一起安裝，而且可以從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能套件](https://www.microsoft.com/download/details.aspx?id=52676)下載。|None|  
|**image**|None|None|  
|**int**|**SqlInt32**|**Int32，Nullable\<Int32>**|  
|**money**|**SqlMoney**|**十進位、可為 Null\<Decimal>**|  
|**nchar**|**SqlChars、SqlString**|**String, Char[]**|  
|**ntext**|None|None|  
|**numeric**|**SqlDecimal**|**十進位、可為 Null\<Decimal>**|  
|**nvarchar**|**SqlChars、SqlString**<br /><br /> **SQLChars**是較佳的資料傳輸和存取比對，而**SQLString**則是更符合執行字串作業的結果。|**String, Char[]**|  
|**Nvarchar （1）、Nchar （1）**|**SqlChars、SqlString**|**Char、String、Char []、Nullable\<char>**|  
|**real**|**SqlSingle** （不過， **SqlSingle**的範圍大於**real**）|**單一、可為 Null\<Single>**|  
|**rowversion**|None|**Byte[]**|  
|**smallint**|**SqlInt16**|**Int16，Nullable\<Int16>**|  
|**smallmoney**|**SqlMoney**|**十進位、可為 Null\<Decimal>**|  
|**sql_variant**|None|**Object**|  
|**table**|None|None|  
|**text**|None|None|  
|**time**|None|**TimeSpan、可為 Null\<TimeSpan>**|  
|**timestamp**|None|None|  
|**tinyint**|**SqlByte**|**Byte、Nullable\<Byte>**|  
|**uniqueidentifier**|**SqlGuid**|**Guid，可為 Null\<Guid>**|  
|**使用者定義型別（UDT）**|None|繫結到相同組件或相依組件中之使用者定義型別的相同類別。|  
|**varbinary**|**SqlBytes、SqlBinary**|**Byte[]**|  
|**Varbinary （1）、binary （1）**|**SqlBytes、SqlBinary**|**byte、Byte []、Nullable\<byte>**|  
|**varchar**|None|None|  
|**xml**|**SqlXml**|None|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>利用 Out 參數自動轉換資料類型  
 如果輸入參數是**SqlTypes**命名空間中的 CLR 資料類型，而且呼叫程式指定其對等的資料類型做為輸入參數，則 clr 方法可以將輸入參數以**out**修飾詞（microsoft Visual c #）或** \<Out()> ByRef** （microsoft Visual Basic）標記，藉以將資訊傳回給呼叫程式碼或程式： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 當 clr 方法傳回資料類型時，會自動發生類型轉換。  
  
 例如，下列 CLR 預存程式具有以**out** （c #）或** \<Out()> ByRef** （Visual Basic）標記之**SqlInt32** CLR 資料類型的輸入參數：  
  
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
  
 在資料庫中建立並建立元件之後，會在中使用下列 Transact-sql 來建立預存程式，其會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int**的資料類型指定為輸出參數：  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 呼叫 CLR 預存程式時， **SqlInt32**資料類型會自動轉換成**int**資料類型，並傳回給呼叫的進程。  
  
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
|已將**SqlGeography**、 **SqlGeometry**和**SqlHierarchyId**類型加入至對應資料表。|  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 的 SQL Server 資料類型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
