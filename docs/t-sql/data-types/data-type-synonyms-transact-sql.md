---
title: 資料類型同義字 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
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
ms.openlocfilehash: ebe6db6130b3d9f058c1c8c65572263348f3dd99
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "72689838"
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
|**character(** _n_ **)**|**char(n)**|  
|**character varying(** _n_ **)**|**varchar(n)**|  
|**Dec**|**decimal**|  
|**Double precision**|**float**|  
|**float**[ **(** _n_ **)** ] 適用於 _n_ = 1-7|**real**|  
|**float**[ **(** _n_ **)** ] 適用於 _n_ = 8-15|**float**|  
|**integer**|**int**|  
|**national character(** _n_ **)**|**nchar(n)**|  
|**national char(** _n_ **)**|**nchar(n)**|  
|**national character varying(** _n_ **)**|**nvarchar(n)**|  
|**national char varying(** _n_ **)**|**nvarchar(n)**|  
|**national text**|**ntext**|  
|**timestamp**|rowversion|  
  
資料類型同義字可用來取代資料定義語言 (DDL) 陳述式中對應的基底資料類型名稱。 這些陳述式包括 CREATE TABLE、CREATE PROCEDURE 和 DECLARE *\@variable*。 不過，建立好物件之後，就看不見同義字了。 當建立物件時，會將同義字的相關基底資料類型指派給物件。 沒有在建立物件的陳述式中指定同義字的記錄。
  
從原始物件衍生的物件 (例如結果集資料行或運算式) 都會被指派基底資料類型。 使用原始物件或任何衍生物件的所有中繼資料函數都將報告基底資料類型，而非同義字，包括：

* 中繼資料作業 (例如**sp_help** 和其他系統預存程序)，
* 資訊結構描述檢視，以及
* 資料存取 API 中繼資料作業，可用來報告資料類型的資料表或結果集資料行。
  
例如，您可以指定 `national character varying` 來建立一份資料表：
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, VarCharCol national character varying(10))  
```  
  
`VarCharCol` 會被指派 **nvarchar(10)** 資料類型，而所有後續的中繼資料函數都會將資料行報告成 **nvarchar(10)** 資料行。 中繼資料函式永遠不會將它們報告成 **national character varying(10)** 資料行。
  
## <a name="see-also"></a>另請參閱
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
