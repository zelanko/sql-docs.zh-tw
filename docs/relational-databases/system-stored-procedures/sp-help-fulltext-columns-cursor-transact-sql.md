---
title: sp_help_fulltext_columns_cursor （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1ed545d31cd5f05fa8360d2cf73a88787f98df45
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85901469"
---
# <a name="sp_help_fulltext_columns_cursor-transact-sql"></a>sp_help_fulltext_columns_cursor (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  利用資料指標來傳回指定給全文檢索索引的資料行。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用[sys.databases fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)目錄檢視。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_fulltext_columns_cursor [ @cursor_return = ] @cursor_variable OUTPUT   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @cursor_return = ] @cursor_variable OUTPUT`這是**cursor**類型的輸出變數。 產生的資料指標是可捲動的唯讀動態資料指標。  
  
`[ @table_name = ] 'table_name'`這是要求全文檢索索引資訊的一或兩部分資料表名稱。 *table_name*是**Nvarchar （517）**，預設值是 Null。 如果省略*table_name* ，就會針對每個全文檢索索引資料表來抓取全文檢索索引資料行資訊。  
  
`[ @column_name = ] 'column_name'`這是所需之全文檢索索引中繼資料的資料行名稱。 *column_name*是**sysname** ，預設值是 Null。 如果省略*column_name*或為 Null，則會針對*table_name*的每個全文檢索索引資料行傳回全文檢索資料行資訊。 如果*table_name*也省略或為 Null，則會針對資料庫中所有資料表的每個全文檢索索引資料行傳回全文檢索索引資料行資訊。  
  
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
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|在全文檢索索引資料表中，指定全文檢索索引資料行之文件類型的資料行。 只有當全文檢索索引資料行是**Varbinary （max）** 或**image**資料行時，這個值才適用。|  
|**FULLTEXT_BLOBTP_COLID**|**int**|文件類型資料行的資料行識別碼。 只有當全文檢索索引資料行是**Varbinary （max）** 或**image**資料行時，這個值才適用。|  
|**FULLTEXT_LANGUAGE**|**sysname**|資料行的全文檢索搜尋所用的語言。|  
  
## <a name="permissions"></a>權限  
 執行許可權預設為**public**角色的成員。  
  
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
 [COLUMNPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [sp_fulltext_column &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [sp_help_fulltext_columns &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
