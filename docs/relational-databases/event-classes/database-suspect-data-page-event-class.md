---
title: Database Suspect Data Page 事件類別 | Microsoft 文件
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], database mirroring
- suspect_pages system table
- database mirroring [SQL Server], event notifications
- Database Suspect Data Page event class
ms.assetid: 098e1443-a8a0-425c-9311-0a479b1370ed
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 10caa7bd8270cdc73d1d5f9addd2b0ef55b89073
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68009546"
---
# <a name="database-suspect-data-page-event-class"></a>Database Suspect Data Page 事件類別
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Database Suspect Data Page** 事件類別指出何時要將頁面加入 [msdb](../../relational-databases/system-tables/suspect-pages-transact-sql.md) 中的 [suspect_pages](../../relational-databases/databases/msdb-database.md)資料表。 請在監視可疑頁面出現的追蹤中包含此事件類別。  
  
> [!NOTE]  
>  這個事件會以非同步的方式發出，與將對應的資料列插入到 **suspect_pages** 資料表無關。 因此，接聽此事件的作業可能無法立即找到對應的 **suspect_pages** 項目。  
  
 當追蹤中包含 **Database Suspect Data Page** 事件類別時，負荷會相對的低。 如果可疑頁面數目增加，則負擔可能會比較大，例如，當磁碟機遇到問題時。  
  
## <a name="database-suspect-data-page-event-class-data-columns"></a>Database Suspect Data Page 事件類別資料行  
  
|資料行名稱|資料類型|描述|資料行識別碼|可篩選|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**DatabaseID**|**int**|已經引發可疑頁面事件之資料庫的識別碼。 這和 **suspect_pages** 資料表的 **database_id** 資料行相同。|3|是|  
|**EventClass**|**int**|事件的類型是 213。|27|否|  
|**EventSequence**|**int**|批次中的事件類別順序。|51|否|  
|**SPID**|**int**|遇到可疑頁面之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作的識別碼。|12|是|  
|**StartTime**|**datetime**|事件發生的時間。|14|是|  
|**Exchange Spill**|**int**|包含可疑頁面之資料庫檔案的識別碼。 這和 **suspect_pages** 資料表的 **file_id** 資料行相同。|22|是|  
|**ObjectID2**|**int**|檔案內可疑頁面的識別碼。 這和 **suspect_pages** 資料表的 **page_id** 資料行相同。|56|是|  
|**錯誤**|**int**|發生的錯誤類型。 這個值與 **suspect_pages** 資料表中頁面的 **event_type** 值相同。|31|是|  
  
## <a name="see-also"></a>另請參閱  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [管理 suspect_pages 資料表 &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
