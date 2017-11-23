---
title: "資料類型同義字 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- data types [SQL Server], synonyms
- alternate names [SQL Server]
- synonyms [SQL Server], data types
ms.assetid: 390eef67-1a49-4185-a971-e07765be9717
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 07b4ada74ee54bf1c892e0938dd794e17ea4c0cb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="data-type-synonyms-transact-sql"></a>資料類型同義字 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包括資料類型同義字，是為了與 ISO 相容。 下表列出同義字和它們所對應的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料類型。
  
|同義字|SQL Server 系統資料類型|  
|---|---|
|**設定不同的二進位**|**varbinary**|  
|**char varying**|**varchar**|  
|**字元**|**char**|  
|**字元**|**char （1)**|  
|**字元 (**  *n*  **)**|**char(n)**|  
|**可變長度字元 (**  *n*  **)**|**varchar(n)**|  
|**Dec**|**decimal**|  
|**雙精度**|**float**|  
|**float**[**(***n***)**] 為 *n*  = 1-7|**real**|  
|**float**[**(***n***)**] 為 *n*  = 8-15|**float**|  
|**integer**|**int**|  
|**國家字元集 (**  *n*  **)**|**nchar （n)**|  
|**國家 （地區) 的 char (**  *n*  **)**|**nchar （n)**|  
|**不同的國家字元集 (**  *n*  **)**|**nvarchar （n)**|  
|**不同國家 （地區) 的 char (**  *n*  **)**|**nvarchar （n)**|  
|**國家 （地區） 的文字**|**ntext**|  
|**timestamp**|rowversion|  
  
資料類型同義字可用而不是對應的基底資料型別名稱中的資料定義語言 (DDL) 陳述式，如 CREATE TABLE、 CREATE PROCEDURE 或 DECLARE  *@variable* 。 不過，建立好物件之後，就看不見同義字了。 當建立物件時，會將同義字的相關基底資料類型指派給物件。 沒有在建立物件的陳述式中指定同義字的記錄。
  
從原始物件衍生而來的所有物件，如結果集資料行或運算式，都會被指派基底資料類型。 在原始物件及任何衍生物件上執行的所有後續中繼資料函數，都會報告基底資料類型，而不是同義字。 這個行為發生時的中繼資料作業，例如**sp_help**和其他系統預存程序、 資訊結構描述檢視中或報告資料表或結果集中的資料類型的各種資料存取 API 中繼資料作業資料行。
  
例如，您可以指定 `national character varying` 來建立一份資料表：
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, VarCharCol national character varying(10))  
```  
  
`VarCharCol`實際指派**nvarchar （10)**資料型別，而且所有後續中繼資料函式會將報告資料行做為**nvarchar （10)**資料行。 中繼資料函數絕不會將報告以**國家字元集 varying(10)**資料行。
  
## <a name="see-also"></a>另請參閱
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
