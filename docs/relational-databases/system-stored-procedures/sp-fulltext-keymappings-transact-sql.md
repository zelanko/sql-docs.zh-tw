---
title: sp_fulltext_keymappings (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_fulltext_keymappings_TSQL
- sp_fulltext_keymappings
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], key column
- sp_fulltext_keymappings
- full-text indexes [SQL Server], troubleshooting
ms.assetid: 2818fa42-072d-4664-a2f7-7ec363b51d81
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb89beba1349b6548604764d12458d4b4fcd45b1
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43104274"
---
# <a name="spfulltextkeymappings-transact-sql"></a>sp_fulltext_keymappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  傳回文件識別碼 (DocId) 和全文檢索索引鍵值之間的對應。 DocId 資料行包含值**bigint**對應至特定全文檢索索引鍵值全文檢索索引資料表中的整數。 滿足搜尋條件的 DocId 值會從全文檢索引擎傳送至 Database Engine，在此處會將這些值對應到正在查詢之基底資料表中的全文檢索索引鍵值。 全文檢索索引鍵資料行是資料表單一資料行上需要的唯一索引。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_fulltext_keymappings { table_id | table_id, docid | table_id, NULL, key }  
```  
  
#### <a name="parameters"></a>參數  
 *table_id*  
 這是全文檢索索引資料表的物件識別碼。 如果指定了無效*table_id*，則會傳回錯誤。 如需取得資料表的物件識別碼資訊，請參閱 < [OBJECT_ID &#40;TRANSACT-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)。  
  
 *docid*  
 這是對應至索引鍵值的內部文件識別碼 (DocId)。 無效的 *docid* 值不會傳回任何結果。  
  
 *索引鍵*  
 這是來自指定資料表的全文檢索索引鍵值。 無效的 *key* 值不會傳回任何結果。 全文檢索索引鍵值的相關資訊，請參閱[管理全文檢索索引](http://msdn.microsoft.com/library/28ff17dc-172b-4ac4-853f-990b5dc02fd1)。  
  
> [!IMPORTANT]  
>  如需有關使用一個、兩個或三個參數的詳細資訊，請參閱本主題稍後的「備註」。  
  
## <a name="return-code-values"></a>傳回碼值  
 無。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|DocId|**bigint**|這是對應至索引鍵值的內部文件識別碼 (DocId) 資料行。|  
|索引鍵|*|這是來自指定資料表的全文檢索索引鍵值。<br /><br /> 如果對應資料表中沒有任何的全文檢索索引鍵，就會傳回空白的資料列集。|  
  
 <sup>*</sup> 索引鍵的資料類型是相同基底資料表中全文檢索索引鍵資料行的資料類型。  
  
## <a name="permissions"></a>Permissions  
 這個函數是公用的，而且不需要任何特殊權限。  
  
## <a name="remarks"></a>備註  
 下表說明使用一個、兩個或三個參數的效果。  
  
|此參數清單|具有此結果|  
|--------------------------|----------------------|  
|*table_id*|只與叫用時*table_id*參數，sp_fulltext_keymappings 會傳回所有的全文檢索索引鍵 (Key) 值從指定的基底資料表，以及對應至每個索引鍵相關聯的 DocId。 這包含暫止刪除的索引鍵。<br /><br /> 這個函數對於多項問題的疑難排解很有用。 當選取的全文檢索索引鍵並非整數資料類型時，此函數特別適合用來查看全文檢索索引內容。 這項作業涉及聯結的結果的 sp_fulltext_keymappings **sys.dm_fts_index_keywords_by_document**。 如需詳細資訊，請參閱 < [sys.dm_fts_index_keywords_by_document &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)。<br /><br /> 不過，一般而言，建議您在可能的情況下，使用指定特定全文檢索索引鍵或 DocId 的參數來執行 sp_fulltext_keymappings。 以這種方式作業的效率，要比傳回整個索引鍵對應高得多，特別是在處理大型資料表時，因為在這種情況下，傳回整個索引鍵對應的效能成本可能相當高。|  
|*table_id*， *docid*|如果只有*table_id*並*docid*都有指定， *docid*必須為 nonNULL 且指定的資料表中指定的有效 DocId。 此函數非常適合用來隔離基底資料表的自訂全文檢索索引鍵 (對應至特定全文檢索索引的 DocId)。|  
|*table_id*(NULL)*金鑰*|如果有三個參數，第二個參數必須是 NULL，並*金鑰*必須為 nonNULL 且指定有效的全文檢索關鍵值從指定的資料表。 此函數非常適合用來隔離對應至基底資料表的特定自訂全文檢索索引鍵的 DocId。|  
  
 若有下列任何情況就會傳回錯誤：  
  
-   指定了無效*table_id*。  
  
-   資料表未建立全文檢索索引。  
  
-   可能是 nonNULL 的參數發現 NULL 值。  
  
## <a name="examples"></a>範例  
  
> [!NOTE]  
>  本節的範例中使用`Production.ProductReview`資料表的[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]範例資料庫。 您可以藉由執行針對提供的範例來建立這個索引`ProductReview`資料表中[CREATE FULLTEXT INDEX &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)。  
  
### <a name="a-obtaining-all-the-key-and-docid-values"></a>A. 取得所有索引鍵和 DocId 值  
 下列範例會使用[DECLARE](../../t-sql/language-elements/declare-local-variable-transact-sql.md)陳述式來建立區域變數`@table_id`，並將指定的識別碼`ProductReview`做為其值的資料表。 此範例會執行**sp_fulltext_keymappings**指定`@table_id`如*table_id*參數。  
  
> [!NOTE]  
>  使用**sp_fulltext_keymappings**只有*table_id*參數是適用於小型資料表。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @table_id int = OBJECT_ID(N'Production.ProductReview');  
EXEC sp_fulltext_keymappings @table_id;  
GO  
  
```  
  
 這則範例會從資料表中傳回所有 DocId 和全文檢索索引鍵，如下所示：  
  
||||  
|-|-|-|  
||`docid`|`key`|  
|`1`|`1`|`1`|  
|`2`|`2`|`2`|  
|`3`|`3`|`3`|  
|`4`|`4`|`4`|  
  
### <a name="b-obtaining-the-docid-value-for-a-specific-key-value"></a>B. 取得特定索引鍵值的 DocId 值  
 下列範例會使用 DECLARE 陳述式來建立區域變數 `@table_id`，以及指派 `ProductReview` 資料表的識別碼當做其值。 此範例會執行**sp_fulltext_keymappings**指定`@table_id`如*table_id*參數，則為 NULL *docid*參數，以及 4 個*金鑰*參數。  
  
> [!NOTE]  
>  使用**sp_fulltext_keymappings**只有*table_id*參數適用於小型資料表。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @table_id int = OBJECT_ID(N'Production.ProductReview');  
EXEC sp_fulltext_keymappings @table_id, NULL, 4;  
GO  
  
```  
  
 這則範例會傳回下列結果。  
  
||||  
|-|-|-|  
||`docid`|`key`|  
|`4`|`4`|`4`|  
  
## <a name="see-also"></a>另請參閱  
 [全文檢索搜尋和語意搜尋預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
