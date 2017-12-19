---
title: "處理 SQL Server Integration Services Scale Out 中的憑證 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e09fec1fcf9cf0221dad50d708adef773b297237
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="deal-with-certificates-in-sql-server-integration-services-scale-out"></a>處理 SQL Server Integration Services Scale Out 中的憑證

為了保護 Scale Out 主機和 Scale Out 背景工作之間的通訊安全，系統會在 Scale Out 中使用兩個憑證，亦即 Scale Out 主機憑證和 Scale Out 背景工作憑證。 

## <a name="scale-out-master-certificate"></a>Scale Out 主機憑證

在大部分情況下，系統會在 Scale Out 主機安裝期間設定 Scale Out 主機憑證。

在 [SQL Server 安裝精靈] 中的 [Integration Services Scale Out 設定 - 主機節點] 頁面上，您可以選擇建立新的自我簽署 SSL 憑證，或使用現有的 SSL 憑證。

![主機設定](media/master-config.PNG)

如果您對憑證沒有特殊需求，可以選擇建立新的自我簽署 SSL 憑證。 您可以進一步在憑證中指定 CN。 請確定 CN 中包含 Scale Out 背景工作稍後要使用的主端點主機名稱。 根據預設，主機節點會包含電腦名稱和 IP。 

如果您選擇使用現有的憑證，請按一下 [瀏覽] 從本機電腦的「根憑證存放區」選取 SSL 憑證。

### <a name="change-scale-out-master-certificate"></a>變更 Scale Out 主機憑證

您可能會因憑證到期或其他原因而需要變更 Scale Out 主機憑證。 遵循下面的步驟：

#### <a name="1-create-a-ssl-certificate"></a>1.建立 SSL 憑證。
使用下列命令，在主機節點上建立並安裝 SSL 憑證：
```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```
範例：
```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```

#### <a name="2-bind-the-certificate-to-master-port"></a>2.將憑證繫結至主機連線埠
使用下列命令，檢查原始的繫結：
```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```
範例：
```dos
netsh http show sslcert ipport=0.0.0.0:8391
```
使用下列命令，刪除原始的繫結並設定新的繫結：
```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={SSL Certificate Thumbprint} certstorename=Root appid={original appid}
```
範例：
```dos
netsh http delete sslcert ipport=0.0.0.0:8391
netsh http add sslcert ipport=0.0.0.0:8391 certhash=01d207b300ca662f479beb884efe6ce328f77d53 certstorename=Root appid={a1f96506-93e0-4c91-9171-05a2f6739e13}
```
#### <a name="3-update-scale-out-master-service-configuration-file"></a>3.更新 Scale Out 主機服務設定檔
更新主機節點上的 Scale Out 主機服務設定檔：\<磁碟機\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config。 將 **SSLCertThumbprint** 更新為新的 SSL 憑證指紋。

#### <a name="4-restart-scale-out-master-service"></a>4.重新啟動 Scale Out 主機服務

#### <a name="5-reconnect-scale-out-worker-to-scale-out-master"></a>5.將 Scale Out 背景工作重新連線至 Scale Out 主機
針對每個 Scale Out 背景工作，您可以刪除背景工作並使用 [Scale Out 管理員](integration-services-ssis-scale-out-manager.md)將其重新新增，或遵循以下步驟 5.1 至 5.3：

5.1 將用戶端 SSL 憑證安裝至背景工作節點上的本機電腦根存放區

5.2 更新 Scale Out 背景工作服務設定檔：更新背景工作節點上的 Scale Out 背景工作服務設定檔：\<磁碟機\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config。 將 **MasterHttpsCertThumbprint** 更新為新的 SSL 憑證指紋。

5.3 重新啟動 Scale Out 背景工作服務


## <a name="scale-out-worker-certificate"></a>Scale Out 背景工作憑證

系統會在 Scale Out 背景工作安裝期間自動產生 Scale Out 背景工作憑證。 

### <a name="change-scale-out-worker-certificate"></a>變更 Scale Out 背景工作憑證

如果您要變更 Scale Out 背景工作憑證，請遵循下列步驟。

#### <a name="1-create-a-certificate"></a>1.建立憑證
使用下列命令，建立並安裝憑證：
```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
範例：
```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
#### <a name="2-install-the-client-certificate-to-the-root-store-of-local-machine-on-worker-node"></a>2.將用戶端憑證安裝至背景工作節點上的本機電腦根存放區

#### <a name="3-give-service-access-to-the-certificate"></a>3.將服務存取權授與憑證
刪除舊的憑證，並使用下列命令，將 Scale Out 背景工作服務存取權授與新憑證：
```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```
範例：
```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```
#### <a name="4-update-scale-out-worker-configuration-file"></a>4.更新 Scale Out 背景工作設定檔
更新背景工作節點上的 Scale Out 背景工作服務設定檔：\<磁碟機\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config。 將 **WorkerHttpsCertThumbprint** 更新為新的憑證指紋。

#### <a name="5-install-the-client-certificate-to-the-root-store-of-local-machine-on-master-node"></a>5.將用戶端憑證安裝至主機節點上的本機電腦根存放區

#### <a name="6-restart-scale-out-worker-service"></a>6.重新啟動 Scale Out 背景工作服務
