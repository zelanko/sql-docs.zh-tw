---
title: sys.database_connection_stats (Azure SQL Database) |Microsoft 文件
ms.custom: ''
ms.date: 03/25/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.database_connection_stats
- database_connection_stats
- database_connection_stats_TSQL
- sys.database_connection_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_connection_stats
- database_connection_stats
ms.assetid: 5c8cece0-63b0-4dee-8db7-6b43d94027ec
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: a2d592be762189c76a1f02c062b398486101ccba
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdatabaseconnectionstats-azure-sql-database"></a>sys.database_connection_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  包含統計資料[!INCLUDE[ssSDS](../../includes/sssds-md.md)]資料庫**連線**事件，提供資料庫連接成功和失敗的概觀。 如需有關連接性事件的詳細資訊，請參閱中的事件類型[sys.event_log &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md)。  
  
|統計資料|型別|Description|  
|---------------|----------|-----------------|  
|**database_name**|**sysname**|資料庫的名稱。|  
|**start_time**|**datetime2**|彙總間隔開始的 UTC 日期和時間。 這個時間永遠是 5 分鐘的倍數。 例如：<br /><br /> '2011-09-28 16:00:00'<br />'2011-09-28 16:05:00'<br />'2011-09-28 16:10:00'|  
|**end_time**|**datetime2**|彙總間隔結束的 UTC 日期和時間。 **End_time**一律會多出剛好 5 分鐘比對應**start_time**相同的資料列中。|  
|**success_count**|**int**|成功連接的數目。|  
|**total_failure_count**|**int**|連接失敗的總數。 這是總和**connection_failure_count**， **terminated_connection_count**，和**throttled_connection_count**，但不包括死結事件。|  
|**connection_failure_count**|**int**|登入失敗的數目。|  
|**terminated_connection_count**|**int**|***只適用於[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]v11。***<br /><br /> 終止的連接數目。|  
|**throttled_connection_count**|**int**|***只適用於[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]v11。***<br /><br /> 節流的連接數目。|  
  
## <a name="remarks"></a>備註  
  
### <a name="event-aggregation"></a>事件彙總  
 這個檢視的事件資訊會在 5 分鐘間隔內收集和彙總。 計數資料行代表在給定時間間隔內，特定資料庫發生特殊連接性事件的次數。  
  
 例如，如果使用者在連接到 Database1 資料庫時，於 2012 年 2 月 5 日 11:00 到 11:05 (UTC) 之間失敗七次，這項資訊會在這個檢視的單一資料列中提供：  
  
|**database_name**|**start_time**|**end_time**|**success_count**|**total_failure_count**|**connection_failure_count**|**terminated_connection_count**|**throttled_connection_count**|  
|------------------------|---------------------|-------------------|------------------------|-------------------------------|------------------------------------|---------------------------------------|--------------------------------------|  
|`Database1`|`2012-02-05 11:00:00`|`2012-02-05 11:05:00`|`0`|`7`|`7`|`0`|`0`|  
  
### <a name="interval-starttime-and-endtime"></a>間隔的 start_time 和 end_time  
 在事件發生時，事件是否包含在彙總間隔*上*或*之後 * * * start_time** 和*之前 * * * end_time** 對於該間隔。 例如，正巧發生在 `2012-10-30 19:25:00.0000000` 的事件只會納入到以下所示的第二段間隔：  
  
```  
  
start_time                    end_time  
2012-10-30 19:20:00.0000000   2012-10-30 19:25:00.0000000  
2012-10-30 19:25:00.0000000   2012-10-30 19:30:00.0000000  
```  
  
### <a name="data-updates"></a>資料更新  
 這個檢視中的資料會累積一段時間。 通常資料會在彙總間隔開始的 1 小時內累積，但是最長可能需要 24 小時，所有資料才會出現在檢視中。 在這段期間，單一資料列內的資訊會定期更新。  
  
### <a name="data-retention"></a>資料保留  
 根據邏輯伺服器的資料庫數目以及每個資料庫所產生的唯一事件數目而定，這個檢視表中的資料最長會保留 30 天或以下。 若要保留這項資訊更長的時間，請將資料複製到另一個資料庫。 在您製作檢視的初始副本之後，檢視中的資料列可能會隨資料累積而更新。 為了讓資料副本保持最新狀態，請定期執行資料列的資料表掃描，查看現有資料列的事件計數是否增加，並且識別新資料列 (您可以使用開始和結束時間識別唯一資料列)，然後用這些變更來更新您的資料副本。  
  
### <a name="errors-not-included"></a>不包括錯誤  
 這個檢視可能不會包括所有連接和錯誤資訊：  
  
-   這個檢視不包括所有[!INCLUDE[ssSDS](../../includes/sssds-md.md)]資料庫可能發生的錯誤，只有在 事件類型的指定[sys.event_log &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md)。  
  
-   如果在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 資料中心內發生機器故障，則事件資料表中可能會遺漏邏輯伺服器的少量資料。  
  
-   如果已透過 DoSGuard 封鎖 IP 位址，則來自該 IP 位址的連接嘗試事件就無法收集，也不會出現在這個檢視中。  
  
## <a name="permissions"></a>Permissions  
 具有存取權限的使用者**主要**資料庫有唯讀存取此檢視。  
  
## <a name="example"></a>範例  
 下列範例顯示的查詢**sys.database_connection_stats**傳回中午到 2011 年 9 月 25 日中午到 9/28/2011 (UTC) 之間發生的資料庫連接摘要。 根據預設，查詢結果會依照**start_time** （遞增順序）。  
  
```  
SELECT *  
FROM sys.database_connection_stats   
WHERE start_time>='2011-09-25:12:00:00' and end_time<='2011-09-28 12:00:00';  
```  
  
## <a name="see-also"></a>另請參閱  
 [疑難排解 Windows Azure SQL Database](http://msdn.microsoft.com/library/windowsazure/ee730906.aspx)  
  
  
