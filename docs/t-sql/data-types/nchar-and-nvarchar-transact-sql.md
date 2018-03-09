---
title: "nchar 和 nvarchar (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- nvarchar data type
- nchar data type
ms.assetid: 81ee5637-ee31-4c4d-96d0-56c26a742354
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4c3f2e9ad1d63992be8f4e4a4c65d821fae73389
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="nchar-and-nvarchar-transact-sql"></a>nchar 和 nvarchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

字元資料類型都是固定長度， **nchar**，或是可變長度**nvarchar**，Unicode 資料，且使用 UNICODE ucs-2 字元集。
  
## <a name="arguments"></a>引數  
**nchar** [(n)]  
固定長度的 Unicode 字串資料。 *n*定義字串長度，而且必須是 1 到 4,000 的值。 儲存體大小是兩次 *n* 位元組。 當定序字碼頁使用雙位元組字元時，儲存體大小仍 *n* 位元組。 根據字串的儲存體大小 *n* 位元組可以為指定的值小於 *n* 。 ISO 同義字**nchar**是**國家 （地區) 的 char**和**國家字元集**...
  
**nvarchar** [(n |**max** )]  
長度可變的 Unicode 字串資料。 *n*定義字串長度，而且可以是 1 到 4,000 的值。 **最大**表示最大儲存體大小是 2 ^31-1 個字元 (2 GB)。 儲存體大小 (以位元組為單位) 是輸入資料之實際長度的兩倍 + 2 位元組。 ISO 同義字**nvarchar**是**國家 （地區) 的 char varying**和**不同的國家字元集**。
  
## <a name="remarks"></a>備註  
當 *n* 中未指定資料定義或變數宣告陳述式中，預設長度為 1。 當 *n* 未利用 CAST 函數，則預設長度為 30。
  
使用**nchar**當資料行資料項目的大小可能會移至類似。
  
使用**nvarchar**當資料行資料項目的大小可能會移至的變化。
  
**sysname**是系統提供的使用者定義資料類型，其作用相當於**nvarchar （128)**，不同之處在於它不是可為 null。 **sysname**用來參考資料庫物件名稱。
  
物件，使用**nchar**或**nvarchar**除非利用 COLLATE 子句指派特定定序會被指派資料庫的預設定序。
  
SET ANSI_PADDING 一律為 ON **nchar**和**nvarchar**。 SET ANSI_PADDING OFF 不適用於**nchar**或**nvarchar**資料型別。
  
前置詞的 Unicode 字元字串常數，以字母 n 表示。沒有 N 前置詞，字串會轉換成資料庫的預設字碼頁。 這個預設字碼頁可能無法辨識特定字元。
 
> [!NOTE]  
>  當以字母 N 字串常數前面加上，隱含轉換如果會導致 Unicode 字串常數轉換不會超過最大長度的 Unicode 字串資料類型 (4000)。 否則，隱含的轉換將會導致 Unicode 大數值 (max)。
  
> [!WARNING]  
>  每個非 null **varchar （max)**或**nvarchar （max)**資料行需要 24 個位元組的額外修正配置，而不利於排序作業期間 8,060 位元組的資料列限制。 這可以建立隱含限制的非 null 數**varchar （max)**或**nvarchar （max)**可以建立資料表中的資料行。 建立資料表時 (高於最大資料列大小超過允許上限 8060 位元組所引發的一般警告) 或插入資料時，不會提供任何特殊錯誤。 如此大型的資料列可能會在某些一般作業 (如叢集索引鍵更新) 期間造成錯誤 (如錯誤 512)，或讓使用者直到執行作業前都無法預期多種完整資料行集。  
  
## <a name="converting-character-data"></a>轉換字元資料  
有關轉換字元資料的詳細資訊，請參閱[char 和 varchar &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md).
  
## <a name="examples"></a>範例  
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyNCharColumn nchar(15)  
,MyNVarCharColumn nvarchar(20)
  
);  
  
GO  
INSERT INTO dbo.MyTable VALUES (N'Test data', N'More test data');  
GO  
SELECT MyNCharColumn, MyNVarCharColumn  
FROM dbo.MyTable;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyNCharColumn   MyNVarCharColumn  
--------------- --------------------  
Test data       More test data  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40;TRANSACT-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[像 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET ANSI_PADDING &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)
  
  
