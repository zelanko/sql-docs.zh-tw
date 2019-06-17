---
title: sp_help_fulltext_columns_cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_columns_cursor
- sp_help_fulltext_columns_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_columns_cursor
ms.assetid: 26054e76-53b7-4004-8d48-92ba3435e9d7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6d158c0703190e78209c9a9550040f9bc667b371
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65983049"
---
# <a name="sphelpfulltextcolumnscursor-transact-sql"></a>sp_help_fulltext_columns_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  利用資料指標來傳回指定給全文檢索索引的資料行。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[sys.fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)目錄檢視。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_fulltext_columns_cursor [ @cursor_return = ] @cursor_variable OUTPUT   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @cursor_return = ] @cursor_variable OUTPUT` 這類型的輸出變數**游標**。 產生的資料指標是可捲動的唯讀動態資料指標。  
  
`[ @table_name = ] 'table_name'` 是全文檢索索引資訊要求的一或兩部分資料表名稱。 *table_name*已**nvarchar(517)** ，預設值是 NULL。 如果*table_name*省略，則每個全文檢索索引的資料表擷取全文檢索索引資料行資訊。  
  
`[ @column_name = ] 'column_name'` 是全文檢索索引中繼資料所需的資料行的名稱。 *column_name*已**sysname**預設值是 NULL。 如果*column_name*省略或是 NULL，傳回的每個全文檢索索引資料行的全文檢索資料行資訊*table_name*。 如果*table_name*也會省略，則為 NULL，每個全文檢索索引資料行的資料庫中的所有資料表傳回全文檢索索引資料行資訊。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|資料表擁有者。 這是建立資料表之資料庫使用者的名稱。|  
|**TABLE_ID**|**int**|資料表的識別碼。|  
|**TABLE_NAME**|**sysname**|資料表名稱。|  
|**FULLTEXT_COLUMN_NAME**|**sysname**|在全文檢索索引資料表中，指定給索引作業的資料行。|  
|**FULLTEXT_COLID**|**int**|全文檢索索引資料行的資料行識別碼。|  
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|在全文檢索索引資料表中，指定全文檢索索引資料行之文件類型的資料行。 全文檢索索引資料行時，才適用此值**varbinary （max)** 或是**映像**資料行。|  
|**FULLTEXT_BLOBTP_COLID**|**int**|文件類型資料行的資料行識別碼。 全文檢索索引資料行時，才適用此值**varbinary （max)** 或是**映像**資料行。|  
|**FULLTEXT_LANGUAGE**|**sysname**|資料行的全文檢索搜尋所用的語言。|  
  
## <a name="permissions"></a>Permissions  
 執行權限預設為隸屬**公開**角色。  
  
## <a name="examples"></a>範例  
 下列範例會傳回資料庫的所有資料表中，指定要編製全文檢索索引之資料行的相關資訊。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_columns_cursor @mycursor OUTPUT  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END;  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>另請參閱  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [sp_fulltext_column &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [sp_help_fulltext_columns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
