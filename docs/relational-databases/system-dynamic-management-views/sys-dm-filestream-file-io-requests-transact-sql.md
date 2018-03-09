---
title: "sys.dm_filestream_file_io_requests (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_filestream_file_io_requests
- dm_filestream_file_io_requests
- sys.dm_filestream_file_io_requests_TSQL
- dm_filestream_file_io_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_file_io_requests catalog view
ms.assetid: d41e39a5-14d5-4f3d-a2e3-a822b454c1ed
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 35d32705c8bce23a9cd46c5844fdc1a20c0cf7c3
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmfilestreamfileiorequests-transact-sql"></a>sys.dm_filestream_file_io_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  顯示命名空間擁有者 (NSO) 在給定時間處理之 I/O 要求的清單。  
  
|資料行|型別|Description|  
|------------|----------|-----------------|  
|**request_context_address**|**varbinary(8)**|顯示 NSO 記憶體區塊的內部位址，該記憶體區塊包含來自驅動程式的 I/O 要求。 不可為 Null。|  
|**current_spid**|**smallint**|顯示目前 SQL Server 連線的系統處理序識別碼 (SPID)。 不可為 Null。|  
|**request_type**|**nvarchar(60)**|顯示 I/O 要求封包 (IRP) 類型。 可能的要求類型是 REQ_PRE_CREATE、REQ_POST_CREATE、REQ_RESOLVE_VOLUME、REQ_GET_VOLUME_INFO、REQ_GET_LOGICAL_NAME、REQ_GET_PHYSICAL_NAME、REQ_PRE_CLEANUP、REQ_POST_CLEANUP、REQ_CLOSE、REQ_FSCTL、REQ_QUERY_INFO、REQ_SET_INFO、REQ_ENUM_DIRECTORY、REQ_QUERY_SECURITY 和 REQ_SET_SECURITY。 不可為 Null|  
|**request_state**|**nvarchar(60)**|顯示 I/O 要求在 NSO 中的狀態。 可能的值為 REQ_STATE_RECEIVED、REQ_STATE_INITIALIZED、REQ_STATE_ENQUEUED、REQ_STATE_PROCESSING、REQ_STATE_FORMATTING_RESPONSE、REQ_STATE_SENDING_RESPONSE、REQ_STATE_COMPLETING 和 REQ_STATE_COMPLETED。 不可為 Null。|  
|**request_id**|**int**|顯示驅動程式指派給此要求的唯一要求識別碼。 不可為 Null。|  
|**irp_id**|**int**|顯示唯一 IRP 識別碼。 這在識別與給定 IRP 相關的所有 I/O 要求時相當實用。 不可為 Null。|  
|**handle_id**|**int**|表示命名空間控制代碼識別碼。 這是 NSO 專用的識別碼，在執行個體中是唯一的。 不可為 Null。|  
|**client_thread_id**|**varbinary(8)**|顯示源自要求之用戶端應用程式的執行緒識別碼。<br /><br /> **\*\*警告\* \*** 這是用戶端應用程式在 SQL Server 的同一部機器上執行時才有意義。 當遠端電腦上，執行用戶端應用程式時**client_thread_id**顯示代表遠端用戶端的運作方式的特定系統處理序的執行緒識別碼。<br /><br /> 可為 Null。|  
|**client_process_id**|**varbinary(8)**|如果用戶端應用程式在與 SQL Server 相同的電腦上執行，顯示用戶端應用程式的處理序識別碼。 若是遠端用戶端，這會顯示代表用戶端應用程式運作的系統處理序識別碼。 可為 Null。|  
|**handle_context_address**|**varbinary(8)**|顯示與用戶端控制代碼相關聯之內部 NSO 結構的位址。 可為 Null。|  
|**filestream_transaction_id**|**varbinary(128)**|顯示與給定控制代碼相關聯之交易的識別碼，以及與此控制代碼相關聯的所有要求。 它是所傳回的值**get_filestream_transaction_context**函式。 可為 Null。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [Filestream 及 FileTable 動態管理檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)  
  
  
