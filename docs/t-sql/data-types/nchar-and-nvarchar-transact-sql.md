---
description: nchar 和 nvarchar (Transact-SQL)
title: nchar 和 nvarchar (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- nvarchar data type
- nchar data type
ms.assetid: 81ee5637-ee31-4c4d-96d0-56c26a742354
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6e4083a2e06ced4275af0938e222143fa255ff48
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "92037511"
---
# <a name="nchar-and-nvarchar-transact-sql"></a>nchar 和 nvarchar (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

固定大小 **nchar** 或變動大小 **nvarchar** 的字元資料類型。 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 開始，當使用支援[補充字元 (SC)](../../relational-databases/collations/collation-and-unicode-support.md#Supplementary_Characters) 的定序時，這些資料類型會存放完整範圍的 [Unicode](../../relational-databases/collations/collation-and-unicode-support.md#Unicode_Defn) 字元並使用 [UTF-16](https://www.wikipedia.org/wiki/UTF-16) 字元編碼。 若指定非 SC 定序，則這些資料類型只會存放 [UCS-2](https://www.wikipedia.org/wiki/Universal_Coded_Character_Set#Encoding_forms) 字元編碼所支援之字元資料的子集。

## <a name="arguments"></a>引數
**nchar** [ ( n ) ]  
固定大小字串資料。 *n* 會定義字串大小 (單位為位元組配對)，且必須是 1 到 4,000 之間的值。 儲存體大小是 *n* 個位元組的兩倍。 針對 [UCS-2](https://www.wikipedia.org/wiki/UTF-16#U+0000_to_U+D7FF_and_U+E000_to_U+FFFF) 編碼，儲存大小是 *n* 位元組的兩倍，而可存放的字元數目也是 *n*。 針對 UTF-16 編碼，儲存大小仍是 *n* 位元組的兩倍，但可存放的字元數目可能小於 *n*，因為補充字元使用兩個位元組配對 (亦稱為 [代理配對 (surrogate-pair)](https://www.wikipedia.org/wiki/UTF-16#U+010000_to_U+10FFFF))。 **nchar** 的 ISO 同義字為 **national char** 及 **national character**。
  
**nvarchar** [ ( n | **max** ) ]  
可變大小字串資料。 *n* 會定義字串大小 (單位為位元組配對)，且可以是 1 到 4,000 之間的值。 **max** 表示儲存大小上限是 2^30-1 個字元 (2 GB)。 儲存大小是 *n* 位元組的兩倍 + 2 位元組。 針對 [UCS-2](https://www.wikipedia.org/wiki/UTF-16#U+0000_to_U+D7FF_and_U+E000_to_U+FFFF) 編碼，儲存大小是 *n* 位元組的兩倍 + 2 位元組，而可存放的字元數目也是 *n*。 針對 UTF-16 編碼，儲存大小仍是 *n* 位元組的兩倍 + 2 位元組，但可存放的字元數目可能小於 *n*，因為補充字元使用兩個位元組配對 (亦稱為 [代理配對 (surrogate-pair)](https://www.wikipedia.org/wiki/UTF-16#U+010000_to_U+10FFFF))。 **nvarchar** 的 ISO 同義字為 **national char varying** 及 **national character varying**。
  
## <a name="remarks"></a>備註  
常見的誤解是假設 [NCHAR(*n*) 和 NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)，*n* 會定義字元數。 但是在 [NCHAR(*n*) 和 NVARCHAR(*n*)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md) 中，*n* 會定義字串長度 (以 **位元組配對** 為單位) (0-4,000)。 *n* 一律不會定義可儲存的字元數。 這類似於 [CHAR (*n*) 和 VARCHAR (*n*)](../../t-sql/data-types/char-and-varchar-transact-sql.md) 的定義。   
發生誤解的原因是，在使用 Unicode 範圍 0-65,535 中所定義的字元時，每個位元組配對可以儲存一個字元。 不過，在較高的 Unicode 範圍 (65,536-1,114,111) 中，一個字元可能會使用兩個位元組配對。 例如，在定義為 NCHAR(10) 的資料行中，[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 可以儲存 10 個字元，該字元會使用一個位元組配對 (Unicode 範圍 0-65,535)，但使用兩個位元組配對 (Unicode 範圍 65,536-1,114,111) 時，則會小於 10 個字元。 如需 Unicode 儲存和字元範圍的詳細資訊，請參閱 [UTF-8 和 UTF-16 之間的儲存差異](../../relational-databases/collations/collation-and-unicode-support.md#storage_differences)。     

當資料定義或變數宣告陳述式中沒有指定 *n* 時，預設長度為 1。 當 *n* 不是由 CAST 函式指定時，預設長度為 30。

若使用 **nchar** 或 **nvarchar**，建議您：
- 當資料行資料項目的大小一致時，請使用 **nchar**。  
- 當資料行資料項目的大小變化相當大時，請使用 **nvarchar**。  
- 當資料行資料項目的大小變化相當大，且字串長度可能超出 4,000 位元組配對時，請使用 **nvarchar(max)**。  
  
**sysname** 是系統提供的使用者定義資料類型，功能相當於 **nvarchar(128)**，但不可為 Null。 **sysname** 可用於參考資料庫物件名稱。
  
除非使用 COLLATE 子句指派特定定序；否則，使用 **nchar** 或 **nvarchar** 的物件會被指派資料庫的預設定序。
  
**nchar** 和 **nvarchar** 的 SET ANSI_PADDING 一律設為 ON。 SET ANSI_PADDING OFF 不適用於 **nchar** 或 **nvarchar** 資料類型。
  
在 Unicode 字元字串常數前面加上字母 N 以表示 UCS-2 或 UTF-16 輸入，視是否使用 SC 定序而定。 若沒有 N 前置詞，字串會被轉換為資料庫的預設字碼頁，這可能無法識別特定字元。 從 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 開始，當使用支援 UTF-8 的定序時，預設字碼頁能夠存放 UNICODE UTF-8 字元集。 
 
> [!NOTE]  
> 當使用字母 N 來前置字串常數時，若要轉換的常數未超過 nvarchar 字串資料類型的最大長度 (4,000)，則隱含轉換的結果便會是 UCS-2 或 UTF-16 字串。 否則，隱含轉換會導致大值 nvarcha(max)。
  
> [!WARNING]  
> 每個非 Null 的 **varchar(max)** 或 **nvarchar(max)** 資料行都需要額外 24 個位元組的固定配置，而不利於排序作業期間 8,060 個位元組的資料列限制。 這些額外的位元組可能會對資料表中的非 null **varchar(max)** 或 **nvarchar(max)** 資料行數目產生隱含限制。 建立資料表時 (高於最大資料列大小超過允許上限 8,060 位元組所引發的一般警告) 或插入資料時，不會提供任何特殊錯誤。 如此大型的資料列可能會在某些一般作業期間發生使用者非預期的錯誤 (例如錯誤 512)。  這些作業的其中兩個範例是叢集索引鍵更新或多種完整資料行集。
  
## <a name="converting-character-data"></a>轉換字元資料  
如需轉換字元資料的資訊，請參閱 [char 和 varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)。
  
## <a name="see-also"></a>另請參閱
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40;Transact-SQL&#41;](../statements/collations.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)    
[定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)     
[單位元組和多位元組字元集](/cpp/c-runtime-library/single-byte-and-multibyte-character-sets)  
