---
title: "SQL Server Integration Services (SSIS) 向外延展 Master |Microsoft 文件"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1672c015186998065b5d6dc95897147aa11d14ec
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-ssis-scale-out-master"></a>Integration Services (SSIS) 相應放大主機
相應放大主機透過 SSISDB 目錄和相應放大主機服務，管理相應放大系統。 

SSISDB 目錄儲存相應放大背景工作、封裝和執行的所有資訊。 它提供介面，以啟用相應放大背景工作以及在相應放大中執行封裝。 如需詳細資訊，請參閱[逐步解說︰設定 Integration Services 相應放大](walkthrough-set-up-integration-services-scale-out.md)、[在 Integration Services 中執行套件](run-packages-in-integration-services-ssis-scale-out.md)。

相應放大主機服務是 Windows 服務，負責與相應放大背景工作通訊。 它會透過 HTTPS 與相應放大背景工作交換封裝執行的狀態，並在 SSISDB 中處理資料。 

## <a name="scale-out-related-sql-views-and-stored-procedures-in-ssisdb"></a>標尺出相關的 SQL 檢視和預存程序在 SSISDB 中

#### <a name="views"></a>Views:
[[catalog].[master_properties]](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md)、[[catalog].[worker_agents]](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md)。

#### <a name="stored-procedures"></a>預存程序：

- 針對相應放大背景工作管理︰  
 [[catalog].[disable_worker_agent]](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)、[[catalog].[enable_worker_agent]](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)。
- 針對在相應放大中執行封裝︰   
[[catalog].[create_execution]](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)、[[catalog].[add_execution_worker]](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)、[[catalog].[start_execution]](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)。   

## <a name="configure-sql-server-integration-services-scale-out-master-service"></a>設定 SQL Server Integration Services 相應放大主機服務
相應放大主機服務可以使用 \<磁碟機\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config 檔案設定。 更新組態檔後必須重新啟動服務。


組態  |Description  |[預設值]  
---------|---------|---------
PortNumber|用來與相應放大背景工作通訊的網路連接埠號碼。|8391         
SSLCertThumbprint|用來保護與相應放大背景工作通訊的 SSL 憑證指紋。|在相應放大主機安裝期間指定的 SSL 憑證指紋         
SqlServerName|名稱[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]包含 SSISDB 目錄。 例如 ServerName\\\\InstanceName。|與標尺出主要安裝的 SQL server 名稱。         
CleanupCompletedJobsIntervalInMs|已完成執行工作的清除間隔，以毫秒為單位。|43200000         
DealWithExpiredTasksIntervalInMs|過期執行工作的處理間隔，以毫秒為單位。|300000
MasterHeartbeatIntervalInMs|相應放大主機活動訊號的間隔，以毫秒為單位。 這會指定相應放大主機更新其在 SSISDB 目錄中線上狀態的間隔。|30000
SqlConnectionTimeoutInSecs|以秒為單位的 SQL 連接逾時連接到 SSISDB 時。|15        

## <a name="view-scale-out-master-service-log"></a>檢視相應放大主機服務記錄檔
標尺出主要服務記錄檔位於\<驅動程式\>: \Users\\*[帳戶]*\AppData\Local\SSIS\ScaleOut\Master 資料夾路徑。 

*[帳戶]*指的是執行標尺出主機服務的帳戶。 預設的帳戶是 SSISScaleOutMaster140。

