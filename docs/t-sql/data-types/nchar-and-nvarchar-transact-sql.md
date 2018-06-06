---
title: nchar 和 nvarchar (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- nvarchar data type
- nchar data type
ms.assetid: 81ee5637-ee31-4c4d-96d0-56c26a742354
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f8918d985423174f09e1d796a406cc979dfc61f6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="nchar-and-nvarchar-transact-sql"></a>nchar 和 nvarchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

字元資料類型，它們是固定長度 (**nchar**) 或可變長度 (**nvarchar**) 的 Unicode 資料，且使用 UNICODE UCS-2 字元集。
  
## <a name="arguments"></a>引數  
**nchar** [ ( n ) ]  
固定長度的 Unicode 字串資料。 *n* 可定義字串長度，而且必須是 1 到 4,000 之間的值。 儲存體大小是 *n* 個位元組的兩倍。 當定序字碼頁使用雙位元組字元時，儲存體大小仍是 *n* 個位元組。 根據字串，*n* 個位元組的儲存體大小可能小於針對 *n* 所指定的值。 **nchar** 的 ISO 同義字為 **national char** 及 **national character**。
  
**nvarchar** [ ( n | **max** ) ]  
長度可變的 Unicode 字串資料。 *n* 定義字串長度，可以是 1 到 4,000 之間的值。 **max** 表示儲存體大小上限是 2^30-1 個字元。  以位元組為單位的最大儲存體大小是 2 GB。 儲存體實際大小是輸入字元數的兩倍 + 2 個位元組 (以位元組為單位)。 **nvarchar** 的 ISO 同義字為 **national char varying** 及 **national character varying**。
  
## <a name="remarks"></a>Remarks  
當資料定義或變數宣告陳述式中沒有指定 *n* 時，預設長度為 1。 當 *n* 不是由 CAST 函式指定時，預設長度為 30。
  
當資料行資料項目的大小可能相似時，請使用 **nchar**。
  
當資料行資料項目的大小可能非常不同時，請使用 **nvarchar**。
  
**sysname** 是系統提供的使用者定義資料類型，功能相當於 **nvarchar(128)**，但不可為 Null。 **sysname** 可用於參考資料庫物件名稱。
  
除非使用 COLLATE 子句指派特定定序；否則，使用 **nchar** 或 **nvarchar** 的物件會被指派資料庫的預設定序。
  
**nchar** 和 **nvarchar** 的 SET ANSI_PADDING 一律設為 ON。 SET ANSI_PADDING OFF 不適用於 **nchar** 或 **nvarchar** 資料類型。
  
請使用字母 N 來前置 Unicode 字元字串常數。若沒有 N 前置，字串會轉換成資料庫的預設字碼頁。 這個預設字碼頁可能無法辨識特定字元。
 
> [!NOTE]  
>  當使用字母 N 來前置字串常數時，若要轉換的常數未超過 Unicode 字串資料類型的最大長度 (4,000)，則隱含轉換的結果便會是 Unicode 字串。 否則，隱含轉換會導致 Unicode 大值 (max)。
  
> [!WARNING]  
>  每個非 null 的 **varchar(max)** 或 **nvarchar(max)** 資料行都需要額外 24 個位元組的固定配置，而不利於排序作業期間 8,060 個位元組的資料列限制。 這些額外的位元組可能會對資料表中的非 null **varchar(max)** 或 **nvarchar(max)** 資料行數目產生隱含限制。 建立資料表時 (高於最大資料列大小超過允許上限 8060 位元組所引發的一般警告) 或插入資料時，不會提供任何特殊錯誤。 如此大型的資料列可能會在某些一般作業期間發生使用者非預期的錯誤 (例如錯誤 512)。  這些作業的其中兩個範例是叢集索引鍵更新或多種完整資料行集。
  
## <a name="converting-character-data"></a>轉換字元資料  
如需轉換字元資料的資訊，請參閱 [char 和 varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)。
  
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
[COLLATE &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)
  
  
