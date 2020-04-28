---
title: sys. dm_database_copies （Azure SQL Database） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dm_database_copies_TSQL
- sys.dm_database_copies
- dm_database_copies
- sys.dm_database_copies_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_database_copies
- sys.dm_database_copies
ms.assetid: d03d4657-86d1-4496-97e6-cc3bc292e0b1
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 0654bd9d15591d994b05ab2c01d9912bc0c56117
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68005079"
---
# <a name="sysdm_database_copies-azure-sql-database"></a>sys.dm_database_copies (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  傳回資料庫複本的相關資訊。  
  
若要傳回異地複寫連結的相關資訊，請使用[geo_replication_links](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)或[sys.databases dm_geo_replication_link_status](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md) views （可在 SQL Database V12 中取得）。
  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|`sys.databases` 檢視中目前資料庫的識別碼。|  
|**start_date**|**datetimeoffset**|起始資料庫複製作業時，區域性 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 資料中心的 UTC 時間。|  
|**modify_date**|**datetimeoffset**|資料庫複製作業完成時，區域性 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 資料中心的 UTC 時間。 新的資料庫和主要資料庫於此時間在交易上是一致的。 完成資訊每隔1分鐘會更新一次。<br /><br />反映 percent_complete 欄位上次更新的 UTC 時間。|  
|**percent_complete**|**real**|已複製位元組的百分比。 值的範圍是從 0 到 100。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 可能會從某些錯誤中自動復原 (例如容錯移轉)，然後再重新啟動資料庫複製作業。 在此情況下，percent_complete 會從 0 重新開始。|  
|**error_code**|**int**|如果大於 0，則代碼表示複製期間發生了錯誤。 如果未發生錯誤，值會等於 0。|  
|**error_desc**|**Nvarchar （4096）**|複製期間發生之錯誤的描述。|  
|**error_severity**|**int**|如果資料庫複製失敗，則傳回 16。|  
|**error_state**|**int**|如果複製失敗，則傳回 1。|  
|**copy_guid**|**uniqueidentifier**|複製作業的唯一識別碼。|  
|**partner_server**|**sysname**|建立複本之 SQL Database 伺服器的名稱。|  
|**partner_database**|**sysname**|夥伴伺服器上的資料庫複本名稱。|  
|**replication_state**|**tinyint**|此資料庫的連續複製複寫狀態。 值為：<br /><br /> 0 = 暫止。 已排程建立資料庫複本，但必要的準備步驟尚未完成，或暫時遭到植入配額封鎖。<br /><br /> 1 = 植入。 要植入的複製資料庫尚未與源資料庫完全同步。 在此狀態下，您無法連接到複本。 若要取消進行中的植入操作，必須卸載複製資料庫。|  
|**replication_state_desc**|**nvarchar(256)**|replication_state 的描述有下列幾種：<br /><br /> PENDING<br /><br /> SEEDING<br />|  
|**maximum_lag**|**int**|保留的欄位。|  
|**is_continuous_copy**|**bit**|0 = 傳回0|  
|**is_target_role**|**bit**|0 = 源資料庫<br /><br /> 1 = 複製資料庫|  
|**is_interlink_connected**|bit|保留的欄位。|  
|**is_offline_secondary**|bit|保留的欄位。|  
  
## <a name="permissions"></a>權限  
 此視圖僅適用于**master**資料庫中的伺服器層級主體登入。  
  
## <a name="remarks"></a>備註  
 您可以在來源或目標[!INCLUDE[ssSDS](../../includes/sssds-md.md)]伺服器的**master**資料庫中，使用 [ **sys.databases] dm_database_copies**視圖。 當資料庫複製順利完成，且新的資料庫變成上線時，會自動移除**sys. dm_database_copies** view 中的資料列。  
  
  
