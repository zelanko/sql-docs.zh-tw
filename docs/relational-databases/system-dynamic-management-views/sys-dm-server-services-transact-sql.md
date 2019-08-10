---
title: _server_services (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 01/07/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_server_services
- sys.dm_server_services
- sys.dm_server_services_TSQL
- dm_server_services_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_server_services dynamic management view
ms.assetid: 3f0defd0-478d-4e7f-96be-8795c9de4e3f
author: stevestein
ms.author: sstein
ms.openlocfilehash: b1c44b269f68b39d633a18f366615fd41b582938
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892955"
---
# <a name="sysdm_server_services-transact-sql"></a>sys.dm_server_services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目前執行個體中 SQL Server、全文檢索與 SQL Server Agent 服務的詳細資訊。 使用此動態管理檢視可報告有關這些服務的狀態資訊。  
  
 
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|servicename|**nvarchar(256)**|、全文檢索[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]或 SQL Server Agent 服務的名稱。 不可為 null。|  
|startup_type|**int**|指出服務的啟動模式。 以下是可能的值和其對應的描述。<br /><br /> 0：其他<br />1：其他<br />2：Automatic<br />3：手動<br />4：已停用<br /><br /> 可為 Null。|  
|startup_type_desc|**nvarchar(256)**|說明服務的啟動模式。 以下是可能的值和其對應的描述。<br /><br /> 另一方面其他 (啟動啟動)<br />另一方面其他 (系統啟動)<br />自動：自動啟動<br />手動：需求啟動<br />已停用：已停用<br /><br /> 不可為 null。|  
|status|**int**|指出服務目前的狀態。 以下是可能的值和其對應的描述。<br /><br /> 1：Stopped<br />2：其他 (啟動擱置中)<br />3：其他 (停止暫止)<br />4：執行中<br />5：其他 (繼續暫止)<br />7其他 (暫停暫止)<br />utf-7已暫停<br /><br /> 可為 Null。|  
|status_desc|**nvarchar(256)**|說明服務目前的狀態。 以下是可能的值和其對應的描述。<br /><br /> 已經服務已停止。<br />其他 (啟動作業暫止):服務正在啟動中。<br />其他 (停止作業暫止):服務正在停止中。<br />運行服務正在執行中。<br />其他 (繼續作業暫止):服務處於擱置狀態。<br />其他 (暫停暫止):服務正在暫停的過程中。<br />而服務已暫停。<br /><br /> 不可為 null。|  
|process_id|**int**|服務的處理序識別碼。 不可為 null。|  
|last_startup_time|**datetimeoffset(7)**|服務上次啟動的日期和時間。 可為 Null。|  
|service_account|**nvarchar(256)**|已獲授權可控制服務的帳戶。 這個帳戶可以啟動或停止服務，或修改服務屬性。 不可為 null。|  
|filename|**nvarchar(256)**|服務可執行檔的路徑和檔案名稱。 不可為 null。|  
|is_clustered|**nvarchar(1)**|指出服務是否安裝為叢集伺服器的資源。 不可為 null。|  
|cluster_nodename|**nvarchar(256)**|安裝服務所在之叢集節點的名稱。 可為 Null。|
|instant_file_initialization_enabled|**nvarchar(1)**|指定是否為[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]服務啟用立即檔案初始化。<br /><br />Y = 已針對服務啟用立即檔案初始化。<br /><br />N = 已停用服務的立即檔案初始化。<br /><br /> 可為 Null。<br /><br /> **注意：** 不適用於其他服務, 例如 SQL Server Agent。<br /><br /> **適用於：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](從[!INCLUDE[sssql11](../../includes/sssql11-md.md)] SP4 和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 到[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])。|  

## <a name="security"></a>安全性  
  
### <a name="permissions"></a>Permissions  
 需要伺服器的 `VIEW SERVER STATE` 權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_server_registry &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-registry-transact-sql.md)  
  
