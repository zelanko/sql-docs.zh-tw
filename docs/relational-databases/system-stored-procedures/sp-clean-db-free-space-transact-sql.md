---
title: "sp_clean_db_free_space (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_clean_db_free_space_TSQL
- sp_clean_db_free_space
dev_langs:
- TSQL
helpviewer_keywords:
- sp_clean_db_free_space
- ghost records
ms.assetid: faa96f7e-be92-47b1-8bc5-4dbba5331655
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 28035865fa180e9b1e379a0fbb3843956e162ccf
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="spcleandbfreespace-transact-sql"></a>sp_clean_db_free_space (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  移除資料庫頁面上因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中資料修改例行工作所留下的剩餘資訊。 sp_clean_db_free_space 會清除資料庫的所有檔案中的所有頁面。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_clean_db_free_space   
[ @dbname ] = 'database_name'   
[ , [ @cleaning_delay = ] 'delay_in_seconds' ] [;]  
```  
  
## <a name="arguments"></a>引數  
 [ @dbname=] '*database_name*'  
 這是要清除的資料庫名稱。 *dbname*是**sysname**不能是 NULL。  
  
 [ @cleaning_delay=] '*delay_in_seconds*'  
 指定頁面清除之間的延遲間隔。 如此有助於減少對 I/O 系統的影響。 *delay_in_seconds*是**int**預設值是 0。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="remarks"></a>備註  
 資料表中的刪除作業或是造成資料列移動的更新作業可以立即釋放頁面上的空間，其方式是移除資料列的參考。 但是在某些情況下，此資料列可以當做準刪除記錄實際存留在資料頁上。 背景處理序會定期移除準刪除記錄。 這項剩餘資料不會傳回[!INCLUDE[ssDE](../../includes/ssde-md.md)]以回應查詢。 但是，在資料或備份檔案的實體安全性遇到風險的環境中，您可以使用 sp_clean_db_free_space 清除這些準刪除記錄。  
  
 執行 sp_clean_db_free_space 所需的時間長度取決於檔案的大小、可用的空間及磁碟的容量。 因為執行 sp_clean_db_free_space 會大幅影響 I/O 活動，所以我們建議您在日常作業的時間之外執行這項程序。  
  
 在執行 sp_clean_db_free_space 之前，我們建議您最好建立完整資料庫備份。  
  
 相關[sp_clean_db_file_free_space](../../relational-databases/system-stored-procedures/sp-clean-db-file-free-space-transact-sql.md)預存程序可以清除單一檔案。  
  
## <a name="permissions"></a>Permissions  
 需要 db_owner 資料庫角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會從 `AdventureWorks2012` 資料庫中清除所有剩餘的資訊。  
  
```  
USE master;  
GO  
EXEC sp_clean_db_free_space   
@dbname = N'AdventureWorks2012' ;  
```  
  
## <a name="see-also"></a>請參閱  
 [Database Engine 預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
