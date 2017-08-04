---
title: "疑難排解 SQL Server Integration Services (SSIS) 向外的延展 |Microsoft 文件"
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
ms.openlocfilehash: 41bb853dd08591596f6f5baa918e174d0c26a6b5
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="troubleshooting-scale-out"></a>疑難排解 向外延展

SSIS 向外牽涉到 communtication 之間 SSISDB，標尺出主要服務和標尺出 Worker 服務。 有時候，通訊是因為設定錯誤，沒有存取權限以及其他原因而中斷。 這份文件可協助您向外延展組態進行疑難排解。

若要調查，您會遇到的徵兆，請遵循以下一個步驟，直到問題解決為止。

### <a name="symptoms"></a>**徵狀** 
標尺出主機無法連線到 SSISDB。 

主要內容無法顯示在標尺出管理員。

[SSISDB] 不會填入 master 的屬性。[目錄]。[master_properties]

### <a name="solution"></a>**方案**
步驟 1： 檢查是否啟用向外。

以滑鼠右鍵按一下**SSISDB** SSMS 並檢查 [物件總管] 中的節點**向外功能**。

![向外啟用](media\isenabled.PNG)

如果屬性值為 False，藉由呼叫預存程序 [SSISDB] 啟用向外。[目錄]。[enable_scaleout]。

步驟 2： 檢查標尺出主要組態檔中指定的 Sql Server 名稱是否正確，然後重新啟動標尺出主機服務。

### <a name="symptoms"></a>**徵狀** 
標尺出背景工作不能連接到標尺出 Master

標尺出背景工作不會顯示標尺出管理員中加入它之後

標尺出背景工作不會顯示在 [SSISDB]。[目錄]。[worker_agents]

標尺出 Worker 服務正在執行，標尺出背景工作處於離線狀態

### <a name="solutions"></a>**解決方案** 
請查看錯誤訊息，在標尺出背景工作服務記錄檔中的\<驅動程式\>: \Users\\*[執行背景工作的服務帳戶]*\AppData\Local\SSIS\Cluster\Agent。

**案例** 

System.ServiceModel.EndpointNotFoundException： 沒有端點時發生接聽 https://*[MachineName]: [Port]*/ClusterManagement/ 無法接受訊息。

步驟 1： 檢查標尺出主要服務組態檔中指定的連接埠號碼是否正確，然後重新啟動標尺出主機服務。 

步驟 2： 檢查是否正確指定標尺出背景工作的服務組態中的主要端點，並重新啟動標尺出 Worker 服務。

步驟 3： 檢查是否在標尺出主要節點上開啟防火牆連接埠。

步驟 4： 解決標尺出主要節點與標尺出背景工作節點之間的任何其他連線問題。

**案例**

System.ServiceModel.Security.SecurityNegotiationException： 無法建立 SSL/TLS 安全通道，與授權單位的信任關係 '*[電腦名稱]: [Port]*'。 ---> System.Net.WebException： 基礎連接已關閉： 無法建立 SSL/TLS 安全通道信任關係。 ---> System.Security.Authentication.AuthenticationException： 而言，驗證程序的遠端憑證無效。

步驟 1： 安裝標尺出主要憑證的標尺出背景工作節點上的本機電腦的根憑證存放區如果沒有尚未安裝並重新啟動標尺出 Worker 服務。

步驟 2： 檢查主要端點中的主機名稱，是否要包含在 Cn 的標尺出主要憑證。 如果沒有，重設標尺出背景工作組態檔中的主要端點，並重新啟動標尺出 Worker 服務。 

> [!Note]
> 如果無法變更主機名稱的 DNS 設定所造成的主要端點，您必須變更標尺出主要憑證。 請參閱[處理中 SSIS 向外憑證](deal-with-certificates-in-ssis-scale-out.md)。

步驟 3： 檢查主要在標尺出背景工作組態中指定的指紋是否符合的標尺出主要憑證指紋。 

**案例**

System.ServiceModel.Security.SecurityNegotiationException： 無法建立安全通道的 SSL/TLS 利用授權 '*[電腦名稱]: [Port]*'。 ---> System.Net.WebException： 此要求已中止： 無法建立 SSL/TLS 安全通道。

步驟 1： 檢查執行標尺出 Worker 服務的帳戶是否能夠存取標尺出背景工作憑證由下列命令。

```dos
winhttpcertcfg.exe -l -c LOCAL_MACHINE\MY -s {CN of the worker certificate}
```

如果帳戶沒有存取權，授與的以下命令，然後重新啟動標尺出 Worker 服務。

```dos
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the worker certificate} -a {the account running Scale Out Worker service}
```

**案例**

System.ServiceModel.Security.MessageSecurityException: HTTP 要求被禁止用戶端驗證配置 'Anonymous'。 ---> System.Net.WebException： 遠端伺服器傳回錯誤: (403) 禁止。

步驟 1： 安裝向外背景工作憑證的標尺出主要節點上的本機電腦的根憑證存放區如果不是尚未安裝並重新啟動標尺出 Worker 服務。

步驟 2： 清除無用標尺出主要節點上的本機電腦的根憑證存放區中的憑證。

步驟 3： 設定安全通道不會再傳送受信任的根憑證授權單位清單在 TLS/SSL 交握過程中，標尺出主要節點上新增登錄項目下方。

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

值名稱： SendTrustedIssuerList 

實值類型： REG_DWORD 

資料值： 0 (False)

**案例**

System.ServiceModel.CommunicationException： 時，發生錯誤發出 HTTP 要求為 https://*[電腦名稱]: [Port]*  /ClusterManagement /。 這可能是因為，伺服器憑證未正確設定使用 HTTP。在 HTTPS 的情況下 SYS。 這也無法用戶端與伺服器之間的安全性繫結不相符所造成。 

步驟 1： 檢查是否標尺出主要憑證繫結至主要端點中的連接埠正確地使用下列命令的主要節點上。 檢查是否顯示的憑證雜湊會與標尺出主要憑證指模比對。

```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```

如果繫結不正確，請使用下列命令將它重設，然後重新啟動標尺出 Worker 服務。

```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={Master certificate thumbprint} certstorename=Root appid={random guid}
```

### <a name="symptoms"></a>**徵狀**
無法啟動在向外執行。

### <a name="solution"></a>**方案**

請檢查您選取 [SSISDB] 中執行封裝的機器的狀態。[目錄]。[worker_agents]。 至少一個背景工作必須在線上而且已啟用。

### <a name="symptoms"></a>**徵狀** 
封裝執行成功，但不沒有記錄任何訊息。

### <a name="solution"></a>**方案**

請檢查 SQL Server 是否允許驗證 Sql server 主控 SSISDB。

> [!Note]  
> 如果您已變更的帳戶向外的記錄，請參閱[標尺出記錄變更的帳戶](change-logdb-account.md)並確認記錄所使用的連接字串。

### <a name="symptoms"></a>**徵狀**
封裝執行的報表中的錯誤訊息可能無法滿足疑難排解。

### <a name="solution"></a>**方案**
下 TasksRootFolder WorkerSettings.config 中設定可以找到更多的執行記錄。 根據預設，它是\<驅動程式\>: \Users\\*[帳戶]*\AppData\Local\SSIS\ScaleOut\Tasks。 *[帳戶]*是預設值 SSISScaleOutWorker140 執行標尺出 Worker 服務的帳戶。

若要找出與封裝執行的記錄檔*[執行 id]*，執行下列 T-SQL 命令來取得*[工作 id]*。 然後，尋找名為的子資料夾*[工作 id]*下 TasksRootFolder。<sup>1<sup>

```sql
SELECT [TaskId]
FROM [SSISDB].[internal].[tasks] tasks, [SSISDB].[internal].[executions] executions 
WHERE executions.execution_id = *Your Execution Id* AND tasks.JobId = executions.job_id
```
<sup>1</sup>此查詢是用於疑難排解用途僅和開啟時，標尺出工作者的診斷記錄/案例改進未來變更。 
