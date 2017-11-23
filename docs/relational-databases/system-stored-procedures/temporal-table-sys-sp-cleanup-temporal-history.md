---
title: "sys.sp_cleanup_temporal_history |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: 
ms.prod_service: sql-database
ms.service: sql-database
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6eff30b4-b261-4f1f-b93c-1f69d754298d
caps.latest.revision: "4"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed631f41e1ce49bfa431645b5f439925190198c7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="temporal-table---sysspcleanuptemporalhistory"></a>時態表-sys.sp_cleanup_temporal_history
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

移除符合設定的 HISTORY_RETENTION 期間內，在單一交易中的時態歷程記錄資料表中的所有資料列。
  
## <a name="syntax"></a>語法  
```  
sp_cleanup_temporal_history [@schema_name = ] schema_name, [@table_name = ] table_name [, [@row_count=] @row_count_var [OUTPUT]]
```  
  
## <a name="arguments"></a>引數  

*@table_name*

清除叫用哪一個保留的時態表的名稱。

*schema_name*

哪些目前時態表所屬的結構描述名稱

*row_count_var* [輸出]

輸出參數傳回的已刪除的資料列數目。 如果記錄資料表有叢集資料行存放區索引，這個參數會傳回永遠為 0。
  
## <a name="remarks"></a>備註
這個預存程序可以只用於時態表，具有有限的保留期限指定。
只有當您需要立即清除過時的所有資料列的歷程記錄資料表，請使用此預存程序。 您應該知道它可以身分，它會刪除所有合格的資料列，在相同交易內有重大影響的資料庫記錄檔和 I/O 子系統上。 

一律建議依賴清除的內部的背景工作移除過時的正常工作負載和一般的資料庫上的影響最小的資料列。

## <a name="permissions"></a>Permissions  
 需要 db_owner 權限。  

## <a name="example"></a>範例

```
declare @rowcnt int
EXEC sys.sp_cleanup_temporal_history 'dbo', 'Department', @rowcnt output
select @rowcnt
```

## <a name="see-also"></a>另請參閱

[時態表保留原則](https://docs.microsoft.com/azure/sql-database/sql-database-temporal-tables-retention-policy)
