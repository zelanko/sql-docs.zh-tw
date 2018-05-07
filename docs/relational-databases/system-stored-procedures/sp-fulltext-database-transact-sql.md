---
title: sp_fulltext_database (TRANSACT-SQL) |Microsoft 文件
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
- sp_fulltext_database_TSQL
- sp_fulltext_database
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_database
ms.assetid: eeb1e151-eb00-484c-8fd1-5641e621ffc6
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8f4904de1142052a8286aabb4a69bf439871b84e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="spfulltextdatabase-transact-sql"></a>sp_fulltext_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  對於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新版本中的全文檢索目錄沒有任何影響，而且是為了回溯相容性才提供支援。 **sp_fulltext_database**不停用全文檢索引擎，對於給定的資料庫。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中所有使用者建立的資料庫一定會啟用全文檢索索引。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]使用[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]改為。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_fulltext_database [@action=] 'action'  
```  
  
## <a name="arguments"></a>引數  
 [  **@action=**] **'***動作***'**  
 這是要執行的動作。 **動作**是**varchar （20)**，而且可以是下列值之一。  
  
|Value|Description|  
|-----------|-----------------|  
|**enable**|支援這個項目的目的，只是為了與舊版相容。 對於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新版本中的全文檢索目錄沒有任何影響。|  
|**disable**|支援這個項目的目的，只是為了與舊版相容。 對於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新版本中的全文檢索目錄沒有任何影響。|  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>備註  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新版本中，全文檢索索引無法關閉。 停用全文檢索索引不會移除資料列從**sysfulltextcatalogs**並不表示已啟用的全文檢索的資料表，不再標示全文檢索索引。 所有全文檢索中繼資料定義都仍在系統資料表中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色和**db_owner**固定的資料庫角色可以執行**sp_fulltext_database**。  
  
## <a name="see-also"></a>另請參閱  
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [FULLTEXTSERVICEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
