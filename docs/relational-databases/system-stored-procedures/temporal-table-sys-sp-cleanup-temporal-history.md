---
title: sys. sp_cleanup_temporal_history |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 6eff30b4-b261-4f1f-b93c-1f69d754298d
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: a9cd5efaf70a915b6a31dced0f79498a01dd7ef5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783597"
---
# <a name="syssp_cleanup_temporal_history-transact-sql"></a>sys.databases sp_cleanup_temporal_history （Transact-sql）

[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

從時態歷程記錄資料表中移除符合單一交易中所設定 HISTORY_RETENTION 期間的所有資料列。

## <a name="syntax"></a>語法

```
sp_cleanup_temporal_history [@schema_name = ] schema_name, [@table_name = ] table_name [, [@row_count=] @row_count_var [OUTPUT]]
```

## <a name="arguments"></a>引數

*\@table_name*

要叫用保留清除的時態表名稱。

*schema_name*

目前時態表所屬之架構的名稱

*row_count_var* [輸出]

傳回已刪除之資料列數的輸出參數。 如果歷程記錄資料表具有叢集資料行存放區索引，此參數會永遠傳回0。

## <a name="remarks"></a>備註

這個預存程式只能用於已指定有限保留週期的時態表。
只有當您需要立即清除歷程記錄資料表中的所有過時資料列時，才使用這個預存程式。 您應該知道，它可能會對資料庫記錄和 i/o 子系統產生顯著的影響，因為它會刪除相同交易內所有合格的資料列。

建議您一律依賴內部背景工作來進行清除作業，這會移除過時的資料列，而且通常會對一般工作負載和資料庫造成最小的影響。

## <a name="permissions"></a>權限

需要 db_owner 許可權。

## <a name="example"></a>範例

```sql
declare @rowcnt int
EXEC sys.sp_cleanup_temporal_history 'dbo', 'Department', @rowcnt output
select @rowcnt
```

## <a name="next-steps"></a>後續步驟

[時態表保留原則](https://docs.microsoft.com/azure/sql-database/sql-database-temporal-tables-retention-policy)
