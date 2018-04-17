---
title: sys.dm_io_backup_tapes (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_io_backup_tapes
- dm_io_backup_tapes_TSQL
- sys.dm_io_backup_tapes_TSQL
- dm_io_backup_tapes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_backup_tapes dynamic management view
ms.assetid: 2e27489e-cf69-4a89-9036-77723ac3de66
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ac436bf8cecfd0f1c255e769dcfcd9b7420cc84
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmiobackuptapes-transact-sql"></a>sys.dm_io_backup_tapes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回磁帶裝置的清單和掛載要求的狀態，作為備份。   
 
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**physical_device_name**|**nvarchar(520)**|可以從中取出備份的實際實體裝置名稱。 不可為 Null。|  
|**logical_device_name**|**nvarchar(256)**|使用者指定的磁碟機的名稱 (從**sys.backup_devices**)。 如果沒有使用者指定名稱可用，便是 NULL。 可為 Null。|  
|**status**|**int**|磁帶的狀態：<br /><br /> 1 = 已開啟，可供使用<br /><br /> 2 = 掛載暫止<br /><br /> 3 = 使用中<br /><br /> 4 = 載入中<br /><br /> **注意：**載入磁帶時 (**狀態 = 4**)，尚未讀取媒體標籤。 這類複製媒體標籤值的資料行**media_sequence_number**，顯示預期的值，它們在磁帶上的實際值可能不同。 已讀取標籤之後，**狀態**變為**3** （使用中），以及媒體標籤資料行會反映所載入的實際磁帶。<br /><br /> 不可為 Null。|  
|**status_desc**|**nvarchar(520)**|磁帶狀態的描述：<br /><br /> AVAILABLE <br /><br /> MOUNT PENDING <br /><br /> IN USE <br /><br /> LOADING MEDIA<br /><br /> 不可為 Null。|  
|**mount_request_time**|**datetime**|要求掛載的時間。 如果沒有掛接已暫止，則為 NULL (**狀態 ！ = 2**)。 可為 Null。|  
|**mount_expiration_time**|**datetime**|掛載要求將到期 (逾時) 的時間。 如果沒有掛接已暫止，則為 NULL (**狀態 ！ = 2**)。 可為 Null。|  
|**database_name**|**nvarchar(256)**|將備份至這個裝置中的資料庫。 可為 Null。|  
|**spid**|**int**|工作階段識別碼。 這用來識別磁帶的使用者。 可為 Null。|  
|**command**|**int**|執行備份的命令。 可為 Null。|  
|**command_desc**|**nvarchar(120)**|命令的描述。 可為 Null。|  
|**media_family_id**|**int**|媒體家族的索引 (1...*n*)， *n*是媒體集中的媒體家族數目。 可為 Null。|  
|**media_set_name**|**nvarchar(256)**|媒體集的名稱 (如果有的話)，依照建立媒體集時，MEDIANAME 選項中的指定。 可為 Null。|  
|**media_set_guid**|**uniqueidentifier**|用來唯一識別媒體集的識別碼。 可為 Null。|  
|**media_sequence_number**|**int**|媒體家族內的磁碟區的索引 (1...*n*)。 可為 Null。|  
|**tape_operation**|**int**|正在執行的磁帶作業：<br /><br /> 1 = 讀取<br /><br /> 2 = 格式化<br /><br /> 3 = 初始化<br /><br /> 4 = 附加<br /><br /> 可為 Null。|  
|**tape_operation_desc**|**nvarchar(120)**|要執行的磁帶作業：<br /><br /> READ<br /><br /> FORMAT<br /><br /> INIT<br /><br /> APPEND <br /><br /> 可為 Null。|  
|**mount_request_type**|**int**|掛載要求的類型：<br /><br /> 1 = 特定磁帶。 所識別的磁帶**media_\*** 是必要的欄位。<br /><br /> 2 = 下一個媒體家族。 要求下一個尚未還原的媒體家族。 當還原的來源裝置比媒體家族少時，便使用這個項目。<br /><br /> 3 = 接續磁帶。 將延伸媒體家族，並要求接續磁帶。<br /><br /> 可為 Null。|  
|**mount_request_type_desc**|**nvarchar(120)**|掛載要求的類型：<br /><br /> SPECIFIC TAPE <br /><br /> NEXT MEDIA FAMILY <br /><br /> CONTINUATION VOLUME <br /><br /> 可為 Null。|  
  
## <a name="permissions"></a>Permissions  
 使用者必須有這部伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [我 O 相關動態管理檢視和函數&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

