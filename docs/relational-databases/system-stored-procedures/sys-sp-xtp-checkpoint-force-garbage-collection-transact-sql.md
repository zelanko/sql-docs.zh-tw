---
title: sys.databases sp_xtp_checkpoint_force_garbage_collection （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_checkpoint_force_garbage_collection_TSQL
- sys.sp_xtp_checkpoint_force_garbage_collection
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_checkpoint_force_garbage_collection
ms.assetid: 82b35b2b-edbd-44ac-9fc8-80695f2fd1df
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 45eb999d6101902ebf9d079235f56d28e343f8e9
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82814479"
---
# <a name="syssp_xtp_checkpoint_force_garbage_collection-transact-sql"></a>sys.sp_xtp_checkpoint_force_garbage_collection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  以記錄序號 (LSN) 標記合併作業中使用的來源檔案，之後不需要用到這些來源檔案時，可進行記憶體回收。 另外也會將相關 LSN 小於記錄截斷點的檔案移至檔案資料流記憶體回收。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
 
## <a name="syntax"></a>語法  
  
```  
sys.sp_xtp_checkpoint_force_garbage_collection [[ @dbname=database_name]  
```  
  
## <a name="arguments"></a>引數  
 *database_name*  
 執行記憶體回收所在的資料庫。 預設為目前資料庫。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 代表成功。 非零代表失敗。  
  
## <a name="result-set"></a>結果集  
 傳回的資料列包含下列資訊：  
  
|資料行|描述|  
|------------|-----------------|  
|num_collected_items|指出已移至檔案資料流記憶體回收的檔案數目。 這些檔案的記錄序號 (LSN) 小於記錄截斷點的 LSN。|  
|num_marked_for_collection_items|指出 LSN 已更新為記錄檔結束 LSN 的記錄檔 blockID 的資料檔案/差異檔案數目。|  
|last_collected_xact_seqno|傳回上一個對應的 LSN，至此之前的檔案都已移至檔案資料流記憶體回收。|  
  
## <a name="permissions"></a>權限  
 需要資料庫擁有者權限。  
  
## <a name="sample"></a>範例  
  
```  
exec [sys].[sp_xtp_checkpoint_force_garbage_collection] hkdb1  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的系統預存程式](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
