---
title: SQL Server Integration Services (SSIS) Scale Out Master | Microsoft Docs
description: 本文描述 SSIS Scale Out 的 Scale Out Master 元件
ms.custom: performance
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: e3e52a854224210ed4561dbce12877fbb4c0f6fb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68082117"
---
# <a name="integration-services-ssis-scale-out-master"></a>Integration Services (SSIS) 相應放大主機

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Scale Out Master 透過 SSISDB 目錄和 Scale Out Master 服務來管理 Scale Out 系統。 

SSISDB 目錄儲存 Scale Out Worker、套件和執行的所有資訊。 它提供介面，以啟用相應放大背景工作以及在相應放大中執行封裝。如需詳細資訊，請參閱[逐步解說：設定 Integration Services Scale Out](walkthrough-set-up-integration-services-scale-out.md) 和[在 Integration Services 中執行套件](run-packages-in-integration-services-ssis-scale-out.md)。

Scale Out Master 服務是一種 Windows 服務，負責與 Scale Out Worker 通訊。 它會透過 HTTPS 傳回 Scale Out Worker 上的套件執行狀態，並在 SSISDB 上處理資料。 

## <a name="scale-out-views-and-stored-procedures-in-ssisdb"></a>SSISDB 中的 Scale Out 檢視和預存程序

### <a name="views"></a>檢視

- [[catalog].[master_properties]](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md)
- [[catalog].[worker_agents]](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md)

### <a name="stored-procedures"></a>預存程序

- 針對管理 Scale Out Worker：
    - [[catalog].[disable_worker_agent]](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)
    - [[catalog].[enable_worker_agent]](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)

- 針對在 Scale Out 中執行套件︰
    - [[catalog].[create_execution]](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)
    - [[catalog].[add_execution_worker]](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)
    - [[catalog].[start_execution]](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)

## <a name="configure-the-scale-out-master-service"></a>設定 Scale Out Master 服務

您可以使用 `<drive>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config` 檔案來設定 Scale Out Master 服務。 更新設定檔之後，必須重新啟動服務。


|組態  |Description  |[預設值]  |
|---------|---------|---------|
|PortNumber|用來與相應放大背景工作通訊的網路連接埠號碼。|8391|
|SSLCertThumbprint|用來保護與相應放大背景工作通訊的 SSL 憑證指紋。|在相應放大主機安裝期間指定的 SSL 憑證指紋|
|SqlServerName|包含 SSISDB 目錄的 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 名稱。 例如，ServerName\\InstanceName。|使用 Scale Out Master 安裝的 SQL Server 名稱。|
|CleanupCompletedJobsIntervalInMs|已完成執行工作的清除間隔，以毫秒為單位。|43200000|
|DealWithExpiredTasksIntervalInMs|過期執行工作的處理間隔，以毫秒為單位。|300000|
|MasterHeartbeatIntervalInMs|相應放大主機活動訊號的間隔，以毫秒為單位。 此屬性指定 Scale Out Master 更新其在 SSISDB 目錄中線上狀態的間隔。|30000|
|SqlConnectionTimeoutInSecs|連線至 SSISDB 時的 SQL 連線逾時，以秒為單位。|15|
||||    

## <a name="view-the-scale-out-master-service-log"></a>檢視 Scale Out Master 服務記錄

Scale Out Master 服務記錄檔位在 `<drive>:\Users\[account]\AppData\Local\SSIS\ScaleOut\Master` 資料夾中。 

*[account]* 參數是執行 Scale Out Master 服務的帳戶。 此帳戶預設為 `SSISScaleOutMaster140`。

## <a name="next-steps"></a>後續步驟

[Integration Services (SSIS) Scale Out Worker](integration-services-ssis-scale-out-worker.md)
