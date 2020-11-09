---
title: 對應 CLR 參數資料 |Microsoft Docs
description: 本文列出 Microsoft SQL Server 的資料類型、CLR for SQL Server 中的對應專案，以及 .NET Framework 中的原生 CLR 對等專案。
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
ms.openlocfilehash: 59cc4c80781f899701f872bd1e8cdd1eea823358
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384723"
---
# <a name="mapping-clr-parameter-data"></a>對應 CLR 參數資料
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  下表列出 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型、SqlTypes 命名空間中的 common language RUNTIME (CLR) 的資料類型， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以及其在 .NET Framework 中的原生 CLR 對應專案 **System.Data.SqlTypes** [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
||||  
|-|-|-|  
|**SQL Server 資料類型**|類型 (在 System.Data.SqlTypes 或 Microsoft.SqlServer.Types 中)|**CLR 資料類型 (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64、Nullable\<Int64>**|  
|**binary**|**SqlBytes、SqlBinary**|**Byte []**|  
|**bit**|**SqlBoolean**|**布林值（可為 Null）\<Boolean>**|  
|**char**|無|無|  
|**cursor**|無|無|  
|**date**|**SqlDateTime**|**DateTime、Nullable\<DateTime>**|  
|**datetime**|**SqlDateTime**|**DateTime、Nullable\<DateTime>**|  
|**datetime2**|無|**DateTime、Nullable\<DateTime>**|  
|**DATETIMEOFFSET**|**None**|**DateTimeOffset、可為 Null\<DateTimeOffset>**|  
|**decimal**|**SqlDecimal**|**Decimal、Nullable\<Decimal>**|  
|**float**|**SqlDouble**|**Double、Nullable\<Double>**|  
|**地理位置**|**SqlGeography**<br /><br /> **SqlGeography** 是在 Microsoft.SqlServer.Types.dll 中定義，這會隨 SQL Server 安裝，並且可從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能套件](https://www.microsoft.com/download/details.aspx?id=100430)下載。|無|  
|**幾何**|**SqlGeometry**<br /><br /> **SqlGeometry** 是在 Microsoft.SqlServer.Types.dll 中定義，這會隨 SQL Server 安裝，並且可從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能套件](https://www.microsoft.com/download/details.aspx?id=100430)下載。|無|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId** 是在 Microsoft.SqlServer.Types.dll 中定義，這會隨 SQL Server 安裝，並且可從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能套件](https://www.microsoft.com/download/details.aspx?id=100430)下載。|無|  
|**image**|無|無|  
|**int**|**SqlInt32**|**Int32、Nullable\<Int32>**|  
|**money**|**SqlMoney**|**Decimal、Nullable\<Decimal>**|  
|**nchar**|**SqlChars、SqlString**|**String, Char[]**|  
|**ntext**|無|無|  
|**numeric**|**SqlDecimal**|**Decimal、Nullable\<Decimal>**|  
|**nvarchar**|**SqlChars、SqlString**<br /><br /> **SQLChars** 是資料傳輸和存取的較佳相符，而 **SQLString** 則是更適合用來執行字串作業。|**String, Char[]**|  
|**Nvarchar (1) 、Nchar (1)**|**SqlChars、SqlString**|**Char、String、Char []、Nullable\<char>**|  
|**real**|不過， **SqlSingle** ( **SqlSingle** 的範圍，大於 **real** ) |**單一、可為 Null\<Single>**|  
|**rowversion**|無|**Byte []**|  
|**smallint**|**SqlInt16**|**Int16、Nullable\<Int16>**|  
|**smallmoney**|**SqlMoney**|**Decimal、Nullable\<Decimal>**|  
|**sql_variant**|無|**Object**|  
|**table**|無|無|  
|**text**|無|無|  
|**time**|無|**TimeSpan、Nullable\<TimeSpan>**|  
|**timestamp**|無|無|  
|**tinyint**|**SqlByte**|**Byte、Nullable\<Byte>**|  
|**uniqueidentifier**|**SqlGuid**|**Guid，可為 Null\<Guid>**|  
|**(UDT 的使用者定義型別)**|無|繫結到相同組件或相依組件中之使用者定義型別的相同類別。|  
|**varbinary**|**SqlBytes、SqlBinary**|**Byte []**|  
|**Varbinary (1) ，二進位 (1)**|**SqlBytes、SqlBinary**|**byte、Byte []、Nullable\<byte>**|  
|**varchar**|無|無|  
|**xml**|**SqlXml**|無|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>利用 Out 參數自動轉換資料類型  
 如果輸入參數是 SqlTypes 命名空間中的 CLR 資料類型，而呼叫程式指定其對等資料型別做為輸入參數，CLR 方法可以將輸入參數以 **out** )  (修飾詞的形式傳回給 **\<Out()> 呼叫程式碼或程式 (microsoft** Visual Basic) 如果輸入參數是 **System.Data.SqlTypes** 命名空間中的 CLR 資料型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 例如，下列 CLR 預存程式具有 **SqlInt32** CLR 資料類型的輸入參數，標記為 **Out** (c # ) 或 **\<Out()> ByRef** (Visual Basic) ：  
  
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
  
 在資料庫中建立並建立元件之後，就會使用下列 Transact-sql 在中建立預存程式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，這會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **整數** 的資料類型指定為輸出參數：  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 呼叫 CLR 預存程式時， **SqlInt32** 資料類型會自動轉換成 **int** 資料類型，並傳回給呼叫的程式。  
  
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
|將 **SqlGeography** 、 **SqlGeometry** 和 **SqlHierarchyId** 類型新增至對應資料表。|  
  
## <a name="see-also"></a>另請參閱  
 [.NET Framework 的 SQL Server 資料類型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
