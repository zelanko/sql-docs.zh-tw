---
title: 資料類型轉換 (資料庫引擎) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- converting data types [SQL Server]
- CONVERT function
- data types [SQL Server], converting
- implicit data type conversions
- explicit data type conversions [SQL Server]
- converting data types [SQL Server], about converting data types
ms.assetid: ffacf45e-a488-48d0-9bb0-dcc7fd365299
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 656f76bfb0b015742824b02e8d7f2f09c8bfe098
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008105"
---
# <a name="data-type-conversion-database-engine"></a>資料類型轉換 (資料庫引擎)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

在下列情況中可以轉換資料類型：
-   將一個物件的資料移到另一個物件、與另一個物件的資料作比較，或與另一個物件的資料結合時，可能需要將資料從一個物件的資料類型轉換成其他物件的資料類型。  
-   當 [!INCLUDE[tsql](../../includes/tsql-md.md)] 結果資料行、傳回碼或輸出參數的資料移至程式變數時，該資料必須從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型，轉換成變數的資料類型。  
  
在應用程式變數與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 結果集資料行、傳回程式碼、參數或參數標記之間轉換時，所支援的資料類型轉換是由資料庫 API 定義。
  
## <a name="implicit-and-explicit-conversion"></a>隱含及明確轉換
資料類型可以隱含或明確地轉換。
  
使用者看不到隱含轉換。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動將資料從一種類型轉換成其他資料類型。 例如，如果將 **smallint** 與 **int**做比較，會先將 **smallint** 隱含轉換成 **int**再繼續比較。
  
**GETDATE()** 會隱含轉換成日期樣式 0。 **SYSDATETIME()** 會隱含轉換成日期樣式 21。
  
明確轉換使用 CAST 或 CONVERT 函數。
  
[CAST 和 CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) 函數會將數值 (本機變數、資料行或其他運算式) 轉換成另一個資料類型。 例如，下列 `CAST` 函數會將 `$157.27` 的數值轉換成 `'157.27'` 的字元字串：
  
```sql
CAST ( $157.27 AS VARCHAR(10) )  
```  
  
如果您希望 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼符合 ISO，請使用 CAST 來取代 CONVERT。 要善用 CONVERT 的樣式功能，可不使用 CAST 而改用 CONVERT。
  
下圖顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統提供之資料類型所能使用的所有明確與隱含資料類型轉換。 這些包括 **xml**、**bigint** 和 **sql_variant**。 從 **sql_variant** 資料類型進行指派時，不可使用隱含轉換，但可以隱含轉換成 **sql_variant**。
  
![資料類型轉換資料表](../../t-sql/data-types/media/lrdatahd.png "資料類型轉換資料表")

雖然上圖顯示了 SQL Server 中允許的所有明確及隱含轉換，但是它並未指出轉換的結果資料類型。 當 SQL Server 執行明確轉換時，陳述式本身便會判斷結果的資料類型。 針對隱含轉換，指派陳述式 (例如設定變數值或將值插入資料行) 會產生變數宣告或資料行定義所定義的資料類型。 針對比較運算子或其他運算式，結果資料類型會取決於資料類型優先順序的規則。

例如，下列指令碼會定義 `varchar` 類型的變數、將 `int` 類型的值指派給變數，然後使用字串選取變數的串連。

```sql
DECLARE @string varchar(10);
SET @string = 1;
SELECT @string + ' is a string.'
```

`int` 值 `1` 會轉換成 `varchar`，因此 `SELECT` 陳述式會傳回 `1 is a string.` 值。

下列範例會顯示相似的指令碼，但是會改用 `int` 變數：

```sql
DECLARE @notastring int;
SET @notastring = '1';
SELECT @notastring + ' is not a string.'
```

在此情況下，`SELECT` 陳述式會擲回下列錯誤：

`Msg 245, Level 16, State 1, Line 3`
`Conversion failed when converting the varchar value ' is not a string.' to data type int.`

為了評估運算式 `@notastring + ' is not a string.'`，SQL Server 會遵循資料類型優先順序規則，在計算運算式的結果前完成隱含轉換。 因為 `int` 具有比 `varchar` 更高的優先順序，所以 SQL Server 會嘗試將字串轉換成整數，但由於此字串無法轉換成整數，因此會失敗。 若運算式提供可進行轉換的字串，則陳述式會成功，如下列範例所示：

```sql
DECLARE @notastring int;
SET @notastring = '1';
SELECT @notastring + '1'
```

在此情況下，字串 `1` 便可轉換成整數值 `1`，因此此 `SELECT` 陳述式即會傳回 `2` 的值。 請注意，在提供的資料類型為整數時，`+` 運算子會變成加法，而非串連。

## <a name="data-type-conversion-behaviors"></a>資料類型轉換行為

當您要將某 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件的資料類型轉換成其他資料類型時，有部分隱含與明確資料類型的轉換不受支援。 例如，**nchar** 值無法轉換成 **image** 值。 您只可使用明確轉換將 **nchar** 轉換成 **binary**；系統並不支援隱含轉換成 **binary**。 但 **nchar** 可以明確或隱含轉換成 **nvarchar**。
  
下列主題說明其對應資料類型所表現的轉換行為：
  
 - [binary 和 varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)  
 - [datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)  
 - [money 和 smallmoney &#40;Transact-SQL&#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
 - [bit &#40;Transact-SQL&#41;](../../t-sql/data-types/bit-transact-sql.md)  
 - [datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
 - [smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)  
 - [char 和 varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)  
 - [decimal 和 numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)  
 - [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
 - [日期 &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)  
 - [float 和 real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
 - [time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)  
 - [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)  
 - [int、bigint、smallint 和 tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
 - [uniqueidentifier &#40;Transact-SQL&#41;](../../t-sql/data-types/uniqueidentifier-transact-sql.md)  
  
###  <a name="converting-data-types-by-using-ole-automation-stored-procedures"></a>使用 OLE Automation 預存程序轉換資料類型  
因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料類型，而 OLE Automation 使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 資料類型，所以 OLE Automation 預存程序必須轉換在兩者之間傳遞的資料。
  
下表說明從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 到 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 的資料類型轉換。
  
|SQL Server 資料類型|Visual Basic 資料類型|  
|--------------------------|----------------------------|  
|**char**、**varchar**、**text**、**nvarchar**、**ntext**|**String**|  
|**decimal**、**numeric**|**String**|  
|**bit**|**布林值**|  
|**binary**、**varbinary**、**image**|一維 **Byte()** 陣列|  
|**int**|**Long**|  
|**smallint**|**整數**|  
|**tinyint**|**位元組**|  
|**float**|**Double**|  
|**real**|**Single**|  
|**money**、 **smallmoney**|**貨幣**|  
|**datetime**、**smalldatetime**|**日期**|  
|設成 NULL 的任何類型|**Variant** 設為 Null|  
  
所有單一的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 值皆會轉換成單一的 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 值，但不包括 **binary**、**varbinary** 及 **image** 值。 這些值會在 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 中轉換成一維的 **Byte()** 陣列。 此陣列的範圍為 **Byte(** 0 到 _length_ 1 **)** ，其中 *length* 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **binary**、**varbinary** 或 **image** 值中的位元組數目。
  
這些轉換是從 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 資料類型到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。
  
|Visual Basic 資料類型|SQL Server 資料類型|  
|----------------------------|--------------------------|  
|**Long**、**Integer**、**Byte**、**Boolean**、**Object**|**int**|  
|**Double**、**Single**|**float**|  
|**貨幣**|**money**|  
|**日期**|**datetime**|  
|字元數不超過 4000 個的 **String**|**varchar**/**nvarchar**|  
|多於 4000 個字元的 **String**|**text**/**ntext**|  
|位元組數不超過 8000 的一維 **Byte()** 陣列|**varbinary**|  
|位元組數超過 8000 的一維 **Byte()** 陣列|**image**|  
  
## <a name="see-also"></a>另請參閱
[OLE Automation 預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[COLLATE &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)
  
  
