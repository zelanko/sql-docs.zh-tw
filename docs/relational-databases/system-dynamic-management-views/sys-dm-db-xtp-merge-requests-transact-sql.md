---
title: sys.dm_db_xtp_merge_requests (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: c1224e88-af74-4c99-ae32-d5d2c552a1f5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f522fde05ce951575d3e02b3cdc4d3336056bd4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026809"
---
# <a name="sysdmdbxtpmergerequests-transact-sql"></a>sys.dm_db_xtp_merge_requests (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

追蹤資料庫合併要求。 Merge 要求可能會產生 SQL server，或要求可能已有的使用者[sys.sp_xtp_merge_checkpoint_files & Amp;#40;transact-SQL&AMP;#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql.md)。

> [!NOTE]
> 這個動態管理檢視 (DMV)，Microsoft SQL Server 2014 之前的 sys.dm_db_xtp_merge_requests，存在。
> 但是，從 SQL Server 2016 開始此 DMV 就不再適用。

## <a name="columns-in-the-report"></a>在報表中的資料行

| 資料行名稱 | 資料類型 | 描述 |
| :-- | :-- | :-- |
| request_state | TINYINT | 合併要求的狀態：<br/>0 = Requested<br/>1 = Pending<br/>2 = 已安裝<br/>3 = Abandoned |
| request_state_desc | nvarchar(60) | 要求的目前狀態的意義：<br/><br/>要求-合併要求存在。<br/>暫止的合併會是正在處理。<br/>安裝-合併已完成。<br/>已放棄的合併無法完成，可能是因為儲存空間不足。 |
| destination_file_id | GUID | 用於合併來源檔案之目的地檔案的唯一識別碼。 |
| lower_bound_tsn | BIGINT | 目標合併檔案的最小時間戳記。 要合併之所有來源檔案的最低交易時間戳記。 |
| upper_bound_tsn | BIGINT | 目標合併檔案的最大時間戳記。 要合併之所有來源檔案的最高交易時間戳記。 |
| collection_tsn | BIGINT | 可收集目前資料列的時間戳記。<br/><br/>當 checkpoint_tsn 大於 collection_tsn 時，就會移除處於 Installed 狀態的資料列。<br/><br/>當 checkpoint_tsn 小於 collection_tsn 時，就會移除處於 Abandoned 狀態的資料列。 |
| checkpoint_tsn | BIGINT | 檢查點啟動的時間。<br/><br/>由時間戳記低於此數的交易所完成的所有刪除都會計算在新的資料檔案中。 剩餘的刪除則會移到目標差異檔案。 |
| sourcenumber_file_id | GUID | 最多 16 個內部檔案識別碼可唯一識別在合併的來源檔案。 |

## <a name="permissions"></a>Permissions

需要目前資料庫的 VIEW DATABASE STATE 權限。

## <a name="see-also"></a>另請參閱

[記憶體最佳化的資料表動態管理檢視 & Amp;#40;transact-SQL&AMP;#41](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)
