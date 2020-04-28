---
title: sp_help_fulltext_catalogs （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_catalogs_TSQL
- sp_help_fulltext_catalogs
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_catalogs
ms.assetid: 1b94f280-e095-423f-88bc-988c9349d44c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 33c32949d57784d1579a3641c1b65e36e97fbf29
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68055136"
---
# <a name="sp_help_fulltext_catalogs-transact-sql"></a>sp_help_fulltext_catalogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回指定全文檢索目錄之全文檢索索引資料表的識別碼、名稱、根目錄、狀態和數目。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]請改用[sys.databases fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)目錄檢視。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_fulltext_catalogs [ @fulltext_catalog_name = ] 'fulltext_catalog_name'  
```  
  
## <a name="arguments"></a>引數  
`[ @fulltext_catalog_name = ] 'fulltext_catalog_name'`這是全文檢索目錄的名稱。 *fulltext_catalog_name*是**sysname**。 如果省略這個參數或它的值是 NULL，就會傳回目前資料庫所關聯的所有全文檢索目錄的相關資訊。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 下表顯示以**ftcatid**排序的結果集。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**fulltext_catalog_id**|**smallint**|全文檢索目錄識別碼。|  
|**名稱**|**sysname**|全文檢索目錄的名稱。|  
|**路徑名**|**nvarchar(260)**|從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 開始，這個子句不會有任何作用。|  
|**狀態**|**int**|目錄的全文檢索索引擴展狀態：<br /><br /> 0 = 閒置<br /><br /> 1 = 完整擴展進行中<br /><br /> 2 = 已暫停<br /><br /> 3 = 調整執行速度<br /><br /> 4 = 復原中<br /><br /> 5 = 已關閉<br /><br /> 6 = 累加擴展進行中<br /><br /> 7 = 正在建立索引<br /><br /> 8 = 磁碟已滿， 已暫停<br /><br /> 9 = 變更追蹤<br /><br /> NULL = 使用者沒有全文檢索目錄的 VIEW 權限，或資料庫未啟用全文檢索，或未安裝全文檢索元件。|  
|**NUMBER_FULLTEXT_TABLES**|**int**|與目錄相關聯之全文檢索索引資料表的數目。|  
  
## <a name="permissions"></a>權限  
 執行許可權預設為**public**角色的成員。  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `Cat_Desc` 全文檢索目錄的相關資訊。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_catalogs 'Cat_Desc' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [FULLTEXTCATALOGPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_catalog &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql.md)   
 [sp_help_fulltext_catalogs_cursor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
