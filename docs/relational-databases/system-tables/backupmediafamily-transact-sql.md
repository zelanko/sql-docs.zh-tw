---
title: backupmediafamily （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupmediafamily
- backupmediafamily_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backupmediafamily system table
- backup media [SQL Server], backupmediafamily system table
ms.assetid: ee16de24-3d95-4b2e-a094-78df2514d18a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6ea3fd7937447ba3ed0f3ad89965301dead772cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68122876"
---
# <a name="backupmediafamily-transact-sql"></a>backupmediafamily (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每個媒體家族，各包含一個資料列。 如果媒體家族位於鏡像媒體集中，則在這個媒體集中，這個家族的每個鏡像都會各有一個個別的資料列。 此資料表會儲存在**msdb**資料庫中。  
    
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|用來識別這個家族為其成員之媒體集的唯一識別碼。 參考**backupmediaset （media_set_id）**|  
|**family_sequence_number**|**tinyint**|這個媒體家族在媒體集中的位置。|  
|**media_family_id**|**uniqueidentifier**|用來識別媒體家族的唯一識別碼。 可以是 NULL。|  
|**media_count**|**int**|媒體家族中的媒體數目。 可以是 NULL。|  
|**logical_device_name**|**nvarchar(128)**|這個備份裝置在 sys.databases 中的名稱**backup_devices. name**。 如果這是暫存的備份裝置（相對於存在於**sys. backup_devices**中的永久備份裝置），則**logical_device_name**的值為 Null。|  
|**physical_device_name**|**nvarchar(260)**|備份裝置的實體名稱。 可以是 NULL。 此欄位會在備份與還原程式之間共用。 它可能包含原始的備份目的地路徑或原始的還原來源路徑。 取決於資料庫的伺服器上的備份或還原是否先發生。 請注意，從相同備份檔案進行連續還原並不會更新路徑，而不論其在還原時的位置為何。 因此， **physical_device_name**欄位無法用來查看所使用的還原路徑。|  
|**device_type**|**tinyint**|備份裝置的類型：<br /><br /> 2 = 磁碟<br /><br /> 5 = 磁帶<br /><br /> 7 = 虛擬裝置<br /><br /> 9 = Azure 儲存體<br /><br /> 105 = 永久備份裝置。<br /><br /> 可以是 NULL。<br /><br /> 所有永久的裝置名稱和裝置號碼都可以在**sys.databases**中找到。 backup_devices。|  
|**physical_block_size**|**int**|用來寫入媒體家族的實體區塊大小。 可以是 NULL。|  
|**對稱**|**tinyint**|鏡像數目 (0-3)。|  
  
## <a name="remarks"></a>備註  
 RESTORE VERIFYONLY FROM *backup_device* with LOADHISTORY 會填入**backupmediaset**資料表的資料行，其中包含來自媒體集標頭的適當值。  
  
 若要減少此資料表以及其他備份和記錄資料表中的資料列數目，請執行[sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)預存程式。  
  
## <a name="see-also"></a>另請參閱  
 [備份和還原資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [系統資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
