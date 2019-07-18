---
title: 管理 SQL Server Integration Services Scale Out 的憑證 | Microsoft Docs
ms.description: This article describes how to manage certificates to secure communications between SSIS Scale Out Master and Scale Out Workers.
ms.date: 12/19/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.custom: performance
ms.topic: conceptual
author: haoqian
ms.author: haoqian
manager: craigg
ms.openlocfilehash: 12f67e7a17ba253ab49b1e61fe3de33a45e0cb55
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65718730"
---
# <a name="manage-certificates-for-sql-server-integration-services-scale-out"></a>管理 SQL Server Integration Services Scale Out 的憑證

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



為了保護 Scale Out Master 與 Scale Out Worker 之間的通訊，SSIS Scale Out 會使用兩個憑證：一個用於 Master，一個用於 Worker。 

## <a name="scale-out-master-certificate"></a>Scale Out 主機憑證

在大部分情況下，系統會在 Scale Out Master 安裝期間設定 Scale Out Master 憑證。

在 [SQL Server 安裝精靈] 的 [Integration Services 相應放大設定 - 主要節點]  頁面中，您可以選擇建立新的自我簽署 SSL 憑證，或使用現有的 SSL 憑證。

![主機設定](media/master-config.PNG)

**新憑證**。 如果您對憑證沒有特殊需求，可以選擇建立新的自我簽署 SSL 憑證。 您可以進一步在憑證中指定 CN。 請確定 CN 中包含 Scale Out Worker 稍後要使用的主要端點主機名稱。 預設會包含主要節點的電腦名稱和 IP 位址。 

**現有憑證**。 如果您選擇使用現有的憑證，請按一下 [瀏覽]  從本機電腦的**根**憑證存放區中選取 SSL 憑證。

### <a name="change-the-scale-out-master-certificate"></a>變更 Scale Out Master 憑證

您可能會因憑證到期或其他原因而需要變更 Scale Out Master 憑證。 若要變更 Scale Out Master 憑證，請執行下列動作：

#### <a name="1-create-an-ssl-certificate"></a>1.建立 SSL 憑證。
使用下列命令，在主要節點上建立並安裝新的 SSL 憑證：

```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine -a sha1
```
例如：

```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine -a sha1
```

#### <a name="2-bind-the-certificate-to-the-master-port"></a>2.將憑證繫結至主要連線埠
使用下列命令，檢查原始繫結：

```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```

例如：

```dos
netsh http show sslcert ipport=0.0.0.0:8391
```

使用下列命令，刪除原始的繫結並設定新的繫結：

```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={SSL Certificate Thumbprint} certstorename=Root appid={original appid}
```

例如：

```dos
netsh http delete sslcert ipport=0.0.0.0:8391
netsh http add sslcert ipport=0.0.0.0:8391 certhash=01d207b300ca662f479beb884efe6ce328f77d53 certstorename=Root appid={a1f96506-93e0-4c91-9171-05a2f6739e13}
```

#### <a name="3-update-the-scale-out-master-service-configuration-file"></a>3.更新 Scale Out Master 服務設定檔
更新主要節點上的 Scale Out Master 服務設定檔 `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config`。 將 **SSLCertThumbprint** 更新為新的 SSL 憑證指紋。

#### <a name="4-restart-the-scale-out-master-service"></a>4.重新啟動 Scale Out Master 服務

#### <a name="5-reconnect-scale-out-workers-to-scale-out-master"></a>5.將 Scale Out Worker 重新連線至 Scale Out Master
針對每個 Scale Out Worker，刪除 Worker，然後使用 [Scale Out Manager](integration-services-ssis-scale-out-manager.md) 將其重新新增，或執行下列動作：

A.  將用戶端 SSL 憑證安裝至背景工作節點上本機電腦的根存放區。

B.  更新 Scale Out Worker 服務設定檔。

更新背景工作節點上的 Scale Out Worker 服務設定檔 `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config`。 將 **MasterHttpsCertThumbprint** 更新為新的 SSL 憑證指紋。

c.  重新啟動 Scale Out Worker 服務。

## <a name="scale-out-worker-certificate"></a>Scale Out 背景工作憑證

系統會在 Scale Out 背景工作安裝期間自動產生 Scale Out 背景工作憑證。 

### <a name="change-the-scale-out-worker-certificate"></a>變更 Scale Out Worker 憑證

如果您要變更 Scale Out Worker 憑證，請執行下列動作：

#### <a name="1-create-a-certificate"></a>1.建立憑證
使用下列命令，建立並安裝憑證：

```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```

例如：

```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```

#### <a name="2-install-the-client-certificate-to-the-root-store-of-the-local-computer-on-the-worker-node"></a>2.將用戶端憑證安裝至背景工作節點上本機電腦的根存放區

#### <a name="3-grant-service-access-to-the-certificate"></a>3.將服務存取權授與憑證
刪除舊的憑證，並使用下列命令，將 Scale Out Worker 服務存取權授與新憑證：

```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```

例如：

```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```

#### <a name="4-update-the-scale-out-worker-service-configuration-file"></a>4.更新 Scale Out Worker 服務設定檔
更新背景工作節點上的 Scale Out Worker 服務設定檔 `\<drive\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config`。 將 **WorkerHttpsCertThumbprint** 更新為新的憑證指紋。

#### <a name="5-install-the-client-certificate-to-the-root-store-of-the-local-computer-on-the-master-node"></a>5.將用戶端憑證安裝至主要節點上本機電腦的根存放區

#### <a name="6-restart-the-scale-out-worker-service"></a>6.重新啟動 Scale Out Worker 服務

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱下列文章：
-   [Integration Services (SSIS) Scale Out Master](integration-services-ssis-scale-out-master.md)
-   [Integration Services (SSIS) Scale Out Worker](integration-services-ssis-scale-out-worker.md)
