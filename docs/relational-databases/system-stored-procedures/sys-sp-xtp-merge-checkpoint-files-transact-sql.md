---
title: sys.databases sp_xtp_merge_checkpoint_files （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_merge_checkpoint_files_TSQL
- sys.sp_xtp_merge_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_merge_checkpoint_files
ms.assetid: da04df2a-f7a1-41e7-a1ef-2d5d68919892
author: stevestein
ms.author: sstein
ms.openlocfilehash: 73638d41c7a24a37c068d365771b4d0469a174d5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041019"
---
# <a name="syssp_xtp_merge_checkpoint_files-transact-sql"></a>sys.sp_xtp_merge_checkpoint_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  **sp_xtp_merge_checkpoint_files**會合並指定之交易範圍中的所有資料和差異檔案。  
  
 如需詳細資訊，請參閱[建立和管理記憶體優化物件的儲存體](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
||  
|-|  
|**注意**：這個預存程式在中[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]已被取代。 已不再需要此檔案，且無法使用，啟動[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。|  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_xtp_merge_checkpoint_files database_name, @transaction_lower_bound, @transaction_upper_bound  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 要叫用合併之資料庫的名稱。 如果該資料庫沒有記憶體中的資料表，這個程序會傳回使用者錯誤。 如果資料庫處於離線狀態，則會傳回錯誤。  
  
 *lower_bound_Tid*  
 資料檔案之交易的（Bigint）下限，如[dm_db_xtp_checkpoint_files &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md)對應于合併的啟動檢查點檔案。 如果是無效的 transactonId 值，則會產生錯誤。  
  
 *upper_bound_Tid*  
 資料檔案之交易的（Bigint）上限（如[dm_db_xtp_checkpoint_files sys.databases &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md)中所示）。 如果是無效的 transactonId 值，則會產生錯誤。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="cursors-returned"></a>傳回的資料指標  
 None  
  
## <a name="permissions"></a>權限  
 需要系統管理員 (sysadmin) 固定伺服器角色和 db_owner 固定資料庫角色。  
  
## <a name="remarks"></a>備註  
 合併有效範圍內的所有資料和差異檔案以產生單一資料和差異檔案。 這個程序不接受合併原則。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
