---
title: "sp_help_fulltext_tables_cursor (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_tables_cursor
- sp_help_fulltext_tables_cursor_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help_fulltext_tables_cursor
ms.assetid: 155791eb-8832-4596-8487-7fc70dfba5b9
caps.latest.revision: "25"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef0fa0c119c293e085d68124ee44dee378fb99d1
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sphelpfulltexttablescursor-transact-sql"></a>sp_help_fulltext_tables_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  利用資料指標來傳回登錄了全文檢索索引的資料表清單。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]使用新**sys.fulltext_indexes**目錄檢視。 如需詳細資訊，請參閱[sys.fulltext_indexes &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md).  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))、 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。|  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_fulltext_tables_cursor [ @cursor_return = ] @cursor_variable OUTPUT   
     [ , [ @fulltext_catalog_name = ] 'fulltext_catalog_name' ]   
     [ , [ @table_name = ] 'table_name' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@cursor_return=** ]  *@cursor_variable* 輸出  
 這類型的輸出變數**游標**。 這個資料指標是可捲動的唯讀動態資料指標。  
  
 [  **@fulltext_catalog_name=** ] **'***fulltext_catalog_name***'**  
 這是全文檢索目錄的名稱。 *fulltext_catalog_name*是**sysname**，預設值是 NULL。 如果*fulltext_catalog_name*省略或為 NULL，就會傳回所有與資料庫相關聯的全文檢索索引的資料表。 如果*fulltext_catalog_name*指定，但*table_name*省略或為 NULL，擷取這個目錄相關聯的每個全文檢索索引資料表的全文檢索索引資訊。 如果兩個*fulltext_catalog_name*和*table_name*指定，會傳回一個資料列，如果*table_name*聯*fulltext_catalog_name*;否則，就會引發錯誤。  
  
 [  **@table_name=**] **'***table_name***'**  
 這是所要求之全文檢索中繼資料一或兩部分的資料表名稱。 *table_name*是**nvarchar （517)**，預設值是 NULL。 如果只有*table_name*指定時，只適用於列*table_name*傳回。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|資料表擁有者。 這是建立資料表之資料庫使用者的名稱。|  
|**TABLE_NAME**|**sysname**|資料表名稱。|  
|**FULLTEXT_KEY_INDEX_NAME**|**sysname**|在指定為唯一索引鍵資料行的資料行上賦予 UNIQUE 條件約束的索引。|  
|**FULLTEXT_KEY_COLID**|**int**|FULLTEXT_KEY_NAME 所識別之唯一索引的資料行識別碼。|  
|**FULLTEXT_INDEX_ACTIVE**|**int**|指定此資料表中標示為全文檢索索引的資料行是否適合查詢：<br /><br /> 0 = 非使用中<br /><br /> 1 = 使用中|  
|**FULLTEXT_CATALOG_NAME**|**sysname**|全文檢索索引資料所在的全文檢索目錄。|  
  
## <a name="permissions"></a>Permissions  
 預設執行權限的成員**公用**角色。  
  
## <a name="examples"></a>範例  
 下列範例會傳回與 `Cat_Desc` 全文檢索目錄相關聯之全文檢索索引資料表的名稱。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_tables_cursor @mycursor OUTPUT, 'Cat_Desc';  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END;  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>請參閱＜  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_fulltext_table &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)   
 [sp_help_fulltext_tables &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
