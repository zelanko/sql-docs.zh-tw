---
title: "sys.dm_db_xtp_merge_requests (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 02/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c1224e88-af74-4c99-ae32-d5d2c552a1f5
caps.latest.revision: "2"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b068552f48544b8dc3a7f11dd8981008cb080bad
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmdbxtpmergerequests-transact-sql"></a>sys.dm_db_xtp_merge_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]


追蹤資料庫合併要求。 合併要求可能是由 SQL Server 產生或要求無法可能已由使用者以[sys.sp_xtp_merge_checkpoint_files (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql.md)。

> [!NOTE]
> 這個動態管理檢視 (DMV)，Microsoft SQL Server 2014 之前的 sys.dm_db_xtp_merge_requests，存在。
> 
> 但是從 SQL Server 2016 開始此 DMV 不再適用。

## <a name="columns-in-the-report"></a>在報表中的資料行

| 資料行名稱 | 資料類型 | Description |
| :-- | :-- | :-- |
| request_state | tinyint | 合併要求的狀態：<br/>0 = Requested<br/>1 = Pending<br/>2 = 安裝<br/>3 = Abandoned |
| request_state_desc | nvarchar(60) | 要求的目前狀態的意義：<br/><br/>要求的合併要求存在。<br/>暫止的合併會為所處理。<br/>安裝-合併已完成。<br/>已放棄的合併無法完成，可能是因為儲存空間不足。 |
| destination_file_id | GUID | 用於合併來源檔案之目的地檔案的唯一識別碼。 |
| lower_bound_tsn | bigint | 目標合併檔案的最小時間戳記。 要合併之所有來源檔案的最低交易時間戳記。 |
| upper_bound_tsn | bigint | 目標合併檔案的最大時間戳記。 要合併之所有來源檔案的最高交易時間戳記。 |
| collection_tsn | bigint | 可收集目前資料列的時間戳記。<br/><br/>當 checkpoint_tsn 大於 collection_tsn 時，就會移除處於 Installed 狀態的資料列。<br/><br/>當 checkpoint_tsn 小於 collection_tsn 時，就會移除處於 Abandoned 狀態的資料列。 |
| checkpoint_tsn | bigint | 檢查點啟動的時間。<br/><br/>由時間戳記低於此數的交易所完成的所有刪除都會計算在新的資料檔案中。 剩餘的刪除則會移到目標差異檔案。 |
| sourcenumber_file_id | GUID | 可在合併中唯一識別來源檔案的內部檔案識別碼，最多 16 個。 |

## <a name="permissions"></a>Permissions

需要目前資料庫的 VIEW DATABASE STATE 權限。

## <a name="see-also"></a>另請參閱

[記憶體最佳化的資料表動態管理檢視 (TRANSACT-SQL)](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)


