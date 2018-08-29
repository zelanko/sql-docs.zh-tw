---
title: sp_help_fulltext_catalogs_cursor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_catalogs_cursor
- sp_help_fulltext_catalogs_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_catalogs_cursor
ms.assetid: d44478d1-0cc4-415e-9d1a-6dccb64674fa
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e17b0cbf0676b76678dbf25a6e11094e9f4cf8eb
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43069230"
---
# <a name="sphelpfulltextcatalogscursor-transact-sql"></a>sp_help_fulltext_catalogs_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  利用資料指標來傳回指定全文檢索目錄之全文檢索索引資料表的識別碼、名稱、根目錄、狀態和數目。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)目錄檢視。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_fulltext_catalogs_cursor [ @cursor_return= ] @cursor_variable OUTPUT ,   
     [ @fulltext_catalog_name = ] 'fulltext_catalog_name'   
```  
  
## <a name="arguments"></a>引數  
 [  **@cursor_return=**] *@cursor_variable* **輸出**  
 這類型的輸出變數**游標**。 這個資料指標是可捲動的唯讀動態資料指標。  
  
 [ **@fulltext_catalog_name=**] **'***fulltext_catalog_name***'**  
 這是全文檢索目錄的名稱。 *fulltext_catalog_name*已**sysname**。 如果這個參數省略或是 NULL，就會傳回與目前資料庫相關聯之所有全文檢索目錄的相關資訊。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**fulltext_catalog_id**|**smallint**|全文檢索目錄識別碼。|  
|**名稱**|**sysname**|全文檢索目錄的名稱。|  
|**PATH**|**nvarchar(260)**|從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 開始，這個子句不會有任何作用。|  
|**狀態**|**int**|目錄的全文檢索索引擴展狀態：<br /><br /> 0 = 閒置<br /><br /> 1 = 完整擴展進行中<br /><br /> 2 = 已暫停<br /><br /> 3 = 調整執行速度<br /><br /> 4 = 復原中<br /><br /> 5 = 已關閉<br /><br /> 6 = 累加擴展進行中<br /><br /> 7 = 正在建立索引<br /><br /> 8 = 磁碟已滿， 已暫停<br /><br /> 9 = 變更追蹤|  
|**NUMBER_FULLTEXT_TABLES**|**int**|與目錄相關聯之全文檢索索引資料表的數目。|  
  
## <a name="permissions"></a>Permissions  
 執行權限預設為**公開**角色。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `Cat_Desc` 全文檢索目錄的相關資訊。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_catalogs_cursor @mycursor OUTPUT, 'Cat_Desc';  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>另請參閱  
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_catalog &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
