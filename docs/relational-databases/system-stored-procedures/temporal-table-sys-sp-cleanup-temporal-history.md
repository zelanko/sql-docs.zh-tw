---
description: 'sys. sp_cleanup_temporal_history (Transact-sql) '
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
ms.openlocfilehash: 30e689666336bfc76c7ec5e5f5df363363801baf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473304"
---
# <a name="syssp_cleanup_temporal_history-transact-sql"></a>sys. sp_cleanup_temporal_history (Transact-sql) 

[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

從時態歷程記錄資料表中移除符合在單一交易內設定之 HISTORY_RETENTION 期間的所有資料列。

## <a name="syntax"></a>語法

```
sp_cleanup_temporal_history [@schema_name = ] schema_name, [@table_name = ] table_name [, [@row_count=] @row_count_var [OUTPUT]]
```

## <a name="arguments"></a>引數

*\@table_name*

叫用保留清除的時態表名稱。

*schema_name*

目前時態表所屬的架構名稱

*row_count_var* [輸出]

傳回已刪除資料列數的輸出參數。 如果歷程記錄資料表有叢集資料行存放區索引，此參數將會傳回一律為0。

## <a name="remarks"></a>備註

這個預存程式只能搭配指定了有限保留期限的時態表使用。
只有當您需要立即清除歷程記錄資料表中的所有過時資料列時，才使用這個預存程式。 您應該知道它對資料庫記錄檔和 i/o 子系統可能會有顯著的影響，因為它會刪除相同交易內所有合格的資料列。

一律建議依賴內部背景工作來進行清除，以移除一般工作負載和資料庫一般影響最低的過時資料列。

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
