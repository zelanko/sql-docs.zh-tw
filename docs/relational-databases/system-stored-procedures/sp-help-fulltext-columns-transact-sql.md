---
title: 遇到 sp_help_fulltext_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_columns
- sp_help_fulltext_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_columns
ms.assetid: 92c8656b-f7fd-4904-9796-acc9ffed4106
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8009c9d2aa5f4b8f8be873633420bd1b088ece16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055087"
---
# <a name="sphelpfulltextcolumns-transact-sql"></a>sp_help_fulltext_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回指定給全文檢索索引的資料行。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[sys.fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)目錄檢視。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_fulltext_columns [ [ @table_name = ] 'table_name' ] ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @table_name = ] 'table\_name'` 是全文檢索索引資訊要求的一或兩部分資料表名稱。 *table_name*已**nvarchar(517)** ，預設值是 NULL。 如果*table_name*省略，則每個全文檢索索引的資料表擷取全文檢索索引資料行資訊。  
  
`[ @column_name = ] 'column\_name'` 是全文檢索索引中繼資料要求的資料行的名稱。 *column_name*已**sysname**，預設值是 NULL。 如果*column_name*省略或是 NULL，傳回的每個全文檢索索引資料行的全文檢索資料行資訊*table_name*。 如果*table_name*也會省略，則為 NULL，每個全文檢索索引資料行的資料庫中的所有資料表傳回全文檢索索引資料行資訊。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|資料表擁有者。 這是建立資料表之資料庫使用者的名稱。|  
|**TABLE_ID**|**int**|資料表的識別碼。|  
|**TABLE_NAME**|**sysname**|資料表的名稱。|  
|**FULLTEXT_COLUMN_NAME**|**sysname**|在全文檢索索引資料表中，指定給索引作業的資料行。|  
|**FULLTEXT_COLID**|**int**|全文檢索索引資料行的資料行識別碼。|  
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|在全文檢索索引資料表中，指定全文檢索索引資料行之文件類型的資料行。 全文檢索索引資料行時，才適用此值**varbinary （max)** 或是**映像**資料行。|  
|**FULLTEXT_BLOBTP_COLID**|**int**|文件類型資料行的資料行識別碼。 全文檢索索引資料行時，才適用此值**varbinary （max)** 或是**映像**資料行。|  
|**FULLTEXT_LANGUAGE**|**sysname**|資料行的全文檢索搜尋所用的語言。|  
  
## <a name="permissions"></a>Permissions  
 執行權限預設為隸屬**公開**角色。  
  
## <a name="examples"></a>範例  
 下列範例會傳回已指定給 `Document` 資料表中的全文檢索索引之資料行的相關資訊。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_columns 'Production.Document';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [sp_fulltext_column &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [sp_help_fulltext_columns_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
