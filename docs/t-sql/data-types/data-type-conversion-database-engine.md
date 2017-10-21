---
title: "資料類型轉換 (Database Engine) |Microsoft 文件"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c0ed7f8e0e681de9f962e3eb963c0af315a0c25c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="data-type-conversion-database-engine"></a>資料類型轉換 (Database Engine)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

在下列情況中可以轉換資料類型：
-   將一個物件的資料移到另一個物件、與另一個物件的資料作比較，或與另一個物件的資料結合時，可能需要將資料從一個物件的資料類型轉換成其他物件的資料類型。  
-   當資料從[!INCLUDE[tsql](../../includes/tsql-md.md)]移動到程式變數結果資料行、 傳回碼或輸出參數時，資料必須從轉換[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]系統資料類型轉換成變數的資料類型。  
  
在應用程式變數與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 結果集資料行、傳回程式碼、參數或參數標記之間轉換時，所支援的資料類型轉換是由資料庫 API 定義。
  
## <a name="implicit-and-explicit-conversion"></a>隱含和明確轉換
資料類型可以隱含或明確地轉換。
  
使用者看不到隱含轉換。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動將資料從一種類型轉換成其他資料類型。 例如，當**smallint**相較於**int**、 **smallint**隱含地轉換成**int**在比較之前會繼續進行。
  
**Getdate （)**隱含地轉換成日期樣式 0。 **Y**隱含地轉換成日期樣式 21。
  
明確轉換使用 CAST 或 CONVERT 函數。
  
[CAST 和 CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md)函式從一種資料類型值 （本機變數、 資料行或另一個運算式） 轉換成另一個。 例如，下列 `CAST` 函數會將 `$157.27` 的數值轉換成 `'157.27'` 的字元字串：
  
```sql
CAST ( $157.27 AS VARCHAR(10) )  
```  
  
如果您希望 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼符合 ISO，請使用 CAST 來取代 CONVERT。 要善用 CONVERT 的樣式功能，可不使用 CAST 而改用 CONVERT。
  
下圖顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統提供之資料類型所能使用的所有明確與隱含資料類型轉換。 這些包括**xml**， **bigint**，和**sql_variant**。 沒有隱含轉換在指派從**sql_variant**資料型別，但是沒有隱含轉換成**sql_variant**。
  
![資料類型轉換表](../../t-sql/data-types/media/lrdatahd.png "資料類型轉換表")
  
## <a name="data-type-conversion-behaviors"></a>資料類型轉換行為
當您要將某 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件的資料類型轉換成其他資料類型時，有部分隱含與明確資料類型的轉換不受支援。 例如， **nchar**值無法轉換成**映像**值。 **Nchar**只可以轉換成**二進位**使用明確的轉換，隱含轉換成**二進位**不支援。 不過， **nchar**可以明確或隱含地轉換成**nvarchar**。
  
下列主題說明其對應資料類型所表現的轉換行為：
  
 - [binary 和 varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)  
 - [datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)  
 - [money 和 smallmoney &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
 - [位元 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/bit-transact-sql.md)  
 - [datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
 - [smalldatetime &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)  
 - [char 和 varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)  
 - [decimal 和 numeric &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)  
 - [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
 - [日期 &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)  
 - [float 和 real &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
 - [時間 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/time-transact-sql.md)  
 - [日期時間 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/datetime-transact-sql.md)  
 - [int、 bigint、 smallint 和 tinyint &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
 - [uniqueidentifier &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/uniqueidentifier-transact-sql.md)  
  
###  <a name="converting-data-types-by-using-ole-automation-stored-procedures"></a>使用 OLE Automation 預存程序轉換資料類型  
因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料類型，而 OLE Automation 使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 資料類型，所以 OLE Automation 預存程序必須轉換在兩者之間傳遞的資料。
  
下表說明從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 到 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 的資料類型轉換。
  
|SQL Server 資料類型|Visual Basic 資料類型|  
|--------------------------|----------------------------|  
|**char**， **varchar**，**文字**， **nvarchar**， **ntext**|**字串**|  
|**十進位**，**數值**|**字串**|  
|**bit**|**布林**|  
|**二進位**， **varbinary**，**映像**|一維**byte （)**陣列|  
|**int**|**長整數**|  
|**smallint**|**Integer**|  
|**tinyint**|**位元組**|  
|**float**|**Double**|  
|**real**|**Single**|  
|**money**、 **smallmoney**|**貨幣**|  
|**datetime**， **smalldatetime**|**日期**|  
|設成 NULL 的任何類型|**Variant**設為 Null|  
  
所有單一[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]值會轉換成單一[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]值除了**二進位**， **varbinary**，和**映像**值。 這些值會轉換成一維**byte （)**陣列中[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]。 這個陣列具有多種**位元組 (**0 到*長度*1**)**其中*長度*是中的位元組數目[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **二進位**， **varbinary**，或**映像**值。
  
這些轉換是從 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 資料類型到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。
  
|Visual Basic 資料類型|SQL Server 資料類型|  
|----------------------------|--------------------------|  
|**長**，**整數**，**位元組**，**布林**，**物件**|**int**|  
|**Double**，**單一**|**float**|  
|**貨幣**|**money**|  
|**日期**|**datetime**|  
|**字串**4000 個字元或更少|**varchar**/**nvarchar**|  
|**字串**超過 4000 個字元|**文字**/**ntext**|  
|一維**byte （)** 8000 個位元組或更少的陣列|**varbinary**|  
|一維**byte （)**超過 8000 個位元組的陣列|**image**|  
  
## <a name="see-also"></a>另請參閱
[OLE Automation 預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[COLLATE &#40;TRANSACT-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)
  
  

