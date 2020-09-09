---
description: sp_help_fulltext_columns (Transact-SQL)
title: sp_help_fulltext_columns (Transact-sql) |Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 029cd09cca1945a521d7a8a11c47ea8b7700b57e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535620"
---
# <a name="sp_help_fulltext_columns-transact-sql"></a>sp_help_fulltext_columns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回指定給全文檢索索引的資料行。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用 [sys. fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) 目錄 view。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_fulltext_columns [ [ @table_name = ] 'table_name' ] ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @table_name = ] 'table\_name'` 這是要求全文檢索索引資訊的一或兩部分資料表名稱。 *table_name* 是 **Nvarchar (517) **，預設值是 Null。 如果省略 *table_name* ，就會針對每個全文檢索索引資料表抓取全文檢索索引資料行資訊。  
  
`[ @column_name = ] 'column\_name'` 這是所要求之全文檢索索引中繼資料的資料行名稱。 *column_name* 是 **sysname**，預設值是 Null。 如果省略 *column_name* 或為 Null，就會針對 *table_name*的每個全文檢索索引資料行傳回全文檢索資料行資訊。 如果 *table_name* 也省略，或為 Null，就會針對資料庫中所有資料表的每個全文檢索索引資料行傳回全文檢索索引資料行資訊。  
  
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
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|在全文檢索索引資料表中，指定全文檢索索引資料行之文件類型的資料行。 只有當全文檢索索引資料行是 **Varbinary (max) ** 或 **image** 資料行時，這個值才適用。|  
|**FULLTEXT_BLOBTP_COLID**|**int**|文件類型資料行的資料行識別碼。 只有當全文檢索索引資料行是 **Varbinary (max) ** 或 **image** 資料行時，這個值才適用。|  
|**FULLTEXT_LANGUAGE**|**sysname**|資料行的全文檢索搜尋所用的語言。|  
  
## <a name="permissions"></a>權限  
 執行許可權預設為 **public** 角色的成員。  
  
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
 [sp_fulltext_column &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [sp_help_fulltext_columns_cursor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
