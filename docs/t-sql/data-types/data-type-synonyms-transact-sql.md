---
title: 資料類型同義字 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], synonyms
- alternate names [SQL Server]
- synonyms [SQL Server], data types
ms.assetid: 390eef67-1a49-4185-a971-e07765be9717
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 482177b87fb4d62cbebb64361e0b26ed9a681c1f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47816556"
---
# <a name="data-type-synonyms-transact-sql"></a>資料類型同義字 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包括資料類型同義字，是為了與 ISO 相容。 下表列出同義字和它們所對應的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型。
  
|同義字|SQL Server 系統資料類型|  
|---|---|
|**Binary varying**|**varbinary**|  
|**char varying**|**varchar**|  
|**character**|**char**|  
|**character**|**char(1)**|  
|**character(** *n* **)**|**char(n)**|  
|**character varying(** *n* **)**|**varchar(n)**|  
|**Dec**|**decimal**|  
|**Double precision**|**float**|  
|**float**[**(***n***)**] for *n* = 1-7|**real**|  
|**float**[**(***n***)**] for *n* = 8-15|**float**|  
|**integer**|**int**|  
|**national character(** *n* **)**|**nchar(n)**|  
|**national char(** *n* **)**|**nchar(n)**|  
|**national character varying(** *n* **)**|**nvarchar(n)**|  
|**national char varying(** *n* **)**|**nvarchar(n)**|  
|**national text**|**ntext**|  
|**timestamp**|rowversion|  
  
資料類型同義字可用來取代資料定義語言 (DDL) 陳述式中對應的基底資料型別名稱，如 CREATE TABLE、CREATE PROCEDURE 或 DECLARE *@variable*。 不過，建立好物件之後，就看不見同義字了。 當建立物件時，會將同義字的相關基底資料類型指派給物件。 沒有在建立物件的陳述式中指定同義字的記錄。
  
從原始物件衍生而來的所有物件，如結果集資料行或運算式，都會被指派基底資料類型。 在原始物件及任何衍生物件上執行的所有後續中繼資料函數，都會報告基底資料類型，而不是同義字。 這個行為是隨著中繼資料作業而發生的，如 **sp_help** 和其他系統預存程序、資訊結構描述檢視，或各種報告資料表或結果集資料行之資料類型的資料存取 API 中繼資料作業。
  
例如，您可以指定 `national character varying` 來建立一份資料表：
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, VarCharCol national character varying(10))  
```  
  
`VarCharCol` 實際上會被指派一個 **nvarchar(10)** 資料類型，所有後續中繼資料函式都會將資料行報告成一個 **nvarchar(10)** 資料行。 中繼資料函式永遠不會將它們報告成 **national character varying(10)** 資料行。
  
## <a name="see-also"></a>另請參閱
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
