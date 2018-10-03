---
title: sys.sp_xtp_merge_checkpoint_files (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 9121485ddbe3f4fd72bf40b4518a7af8b196fa23
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47725406"
---
# <a name="sysspxtpmergecheckpointfiles-transact-sql"></a>sys.sp_xtp_merge_checkpoint_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  **sys.sp_xtp_merge_checkpoint_files**合併指定的交易範圍中的所有資料和差異檔案。  
  
 如需詳細資訊，請參閱 <<c0> [ 建立及管理記憶體最佳化物件的儲存體](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
||  
|-|  
|**附註**： 這個預存程序中已過時[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。 它不再需要也不能，啟動[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。|  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.sp_xtp_merge_checkpoint_files database_name, @transaction_lower_bound, @transaction_upper_bound  
[;]  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 要叫用合併之資料庫的名稱。 如果該資料庫沒有記憶體中的資料表，這個程序會傳回使用者錯誤。 如果資料庫處於離線狀態，則會傳回錯誤。  
  
 *lower_bound_Tid*  
 資料檔中所示的交易 (bigint) 下限[sys.dm_db_xtp_checkpoint_files &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md)開始檢查點檔案合併的對應。 如果是無效的 transactonId 值，則會產生錯誤。  
  
 *upper_bound_Tid*  
 資料檔中所示的交易 (bigint) 上限[sys.dm_db_xtp_checkpoint_files &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md)。 如果是無效的 transactonId 值，則會產生錯誤。  
  
## <a name="return-code-values"></a>傳回碼值  
 None  
  
## <a name="cursors-returned"></a>傳回的資料指標  
 None  
  
## <a name="permissions"></a>Permissions  
 需要系統管理員 (sysadmin) 固定伺服器角色和 db_owner 固定資料庫角色。  
  
## <a name="remarks"></a>備註  
 合併有效範圍內的所有資料和差異檔案以產生單一資料和差異檔案。 這個程序不接受合併原則。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
