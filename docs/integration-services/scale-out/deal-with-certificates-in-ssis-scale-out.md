---
title: "處理 Sql Server Integration Services 向外中的憑證 |Microsoft 文件"
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
ms.openlocfilehash: 2970b2b2cc7cf30c18a203ebbb92b5418bfc9be5
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="deal-with-certificates-in-sql-server-integration-services-scale-out"></a>處理 SQL Server Integration Services 向外中的憑證

若要保護標尺出主要和標尺出背景工作之間的通訊，兩個憑證會用於向外，也就是標尺出主要憑證和標尺出背景工作憑證。 

## <a name="scale-out-master-certificate"></a>標尺出主要憑證

在大部分情況下，在標尺出主要安裝期間設定標尺出主要憑證。

在**Integration Services 標尺出組態的主要節點**頁面上的 SQL Server 安裝精靈 中，您可以選擇建立新的自我簽署的 SSL 憑證，或使用現有的 SSL 憑證。

![主要組態](media/master-config.PNG)

如果憑證沒有特殊需求，您可以選擇建立新的自我簽署的 SSL 憑證。 您可以進一步指定在憑證中的 Cn。 請確定工作者使用的標尺出更新版本的主要端點的主機名稱包含在 Cn。 根據預設，電腦名稱和 ip 的主要節點會包含。 

如果您選擇使用現有的憑證，按一下 [瀏覽] 選取 SSL 憑證從**根**本機電腦憑證存放區。

### <a name="change-scale-out-master-certificate"></a>變更標尺出主要憑證

若要變更您的標尺出主要憑證因憑證到期或其他原因。 遵循下面的步驟：

#### <a name="1-create-a-ssl-certificate"></a>1.建立 SSL 憑證。
建立及安裝 SSL 憑證，在主要節點，使用下列命令：
```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```
範例：
```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```

#### <a name="2-bind-the-certificate-to-master-port"></a>2.將憑證繫結至主要連接埠
請檢查命令的原始繫結：
```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```
範例：
```dos
netsh http show sslcert ipport=0.0.0.0:8391
```
刪除原始的繫結，並設定新的繫結，並輸入下列命令：
```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={SSL Certificate Thumbprint} certstorename=Root appid={original appid}
```
範例：
```dos
netsh http delete sslcert ipport=0.0.0.0:8391
netsh http add sslcert ipport=0.0.0.0:8391 certhash=01d207b300ca662f479beb884efe6ce328f77d53 certstorename=Root appid={a1f96506-93e0-4c91-9171-05a2f6739e13}
```
#### <a name="3-update-scale-out-master-service-configuration-file"></a>3.更新標尺出主要服務組態檔
更新的標尺出主要服務組態檔，\<驅動程式\>: \Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config，在主要節點。 更新**SSLCertThumbprint**新的 SSL 憑證的指紋。

#### <a name="4-restart-scale-out-master-service"></a>4.重新啟動標尺出主要服務

#### <a name="5-reconnect-scale-out-worker-to-scale-out-master"></a>5.重新連線擴充到主要範圍外的背景工作
每個標尺出背景工作，請刪除背景工作並重新加入它與[標尺出管理員](integration-services-ssis-scale-out-manager.md)或遵循 5.1 至 5.3 以下步驟：

5.1 安裝用戶端 SSL 憑證的根存放區的背景工作節點上的本機電腦

5.2 出背景工作服務組態檔更新背景工作時的小數位數服務組態檔更新規模\<驅動程式\>: \Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config 背景工作節點上的。 更新**MasterHttpsCertThumbprint**新的 SSL 憑證的指紋。

5.3 Worker 服務出重新啟動的小數位數


## <a name="scale-out-worker-certificate"></a>標尺出背景工作憑證

標尺出背景工作憑證會在標尺出工作者的安裝期間自動產生的。 

### <a name="change-scale-out-worker-certificate"></a>變更標尺出背景工作憑證

在您想要變更小數位數出背景工作憑證的情況下，請遵循下列步驟。

#### <a name="1-create-a-certificate"></a>1.建立憑證
建立及安裝憑證使用下列命令：
```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
範例：
```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
#### <a name="2-install-the-client-certificate-to-the-root-store-of-local-machine-on-worker-node"></a>2.背景工作節點上的本機電腦的根存放區中安裝用戶端憑證

#### <a name="3-give-service-access-to-the-certificate"></a>3.提供服務的存取權給憑證
刪除舊的憑證，並且提供標尺出背景工作服務存取的憑證與命令的新憑證：
```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```
範例：
```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```
#### <a name="4-update-scale-out-worker-configuration-file"></a>4.更新標尺出工作者的組態檔
更新標尺出背景工作的服務組態檔，\<驅動程式\>: \Program Files\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config 背景工作節點上的。 更新**WorkerHttpsCertThumbprint**新憑證的指紋。

#### <a name="5-install-the-client-certificate-to-the-root-store-of-local-machine-on-master-node"></a>5.安裝用戶端憑證的根存放區在主機上的本機電腦節點

#### <a name="6-restart-scale-out-worker-service"></a>6.標尺出 Worker 服務重新啟動
