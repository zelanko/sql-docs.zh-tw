---
title: "針對 SQL Server Integration Services (SSIS) Scale Out 進行疑難排解 | Microsoft Docs"
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
ms.openlocfilehash: 56d61bc6ba76514ba2291243002a7423ec8e265c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="troubleshooting-scale-out"></a>針對 Scale Out 進行疑難排解

SSIS Scale Out 涉及 SSISDB、Scale Out 主機服務和 Scale Out 背景工作服務之間的通訊。 有時候，通訊會因為設定錯誤、沒有存取權限及其他原因而中斷。 這份文件可協助您針對 Scale Out 設定進行疑難排解。

若要調查您遇到的徵兆，請遵循下列步驟逐步執行，直到問題解決為止。

### <a name="symptoms"></a>**徵兆** 
Scale Out 主機無法連線至 SSISDB。 

主機屬性無法顯示在 Scale Out 管理員中。

[SSISDB].[catalog].[master_properties] 中未填入主機屬性

### <a name="solution"></a>**方案**
步驟 1：檢查是否已啟用 Scale Out。

以滑鼠右鍵按一下 SSMS [物件總管] 中的 [SSISDB] 節點，並確認 **Scale Out 功能已啟用**。

![已啟用 Scale Out](media\isenabled.PNG)

如果屬性值為 False，請藉由呼叫預存程序 [SSISDB].[catalog].[enable_scaleout] 來啟用 Scale Out。

步驟 2：檢查 Scale Out 主機設定檔中指定的 SQL Server 名稱是否正確，然後重新啟動 Scale Out 主機服務。

### <a name="symptoms"></a>**徵兆** 
Scale Out 背景工作無法連線至 Scale Out 主機

Scale Out 背景工作未於其在 Scale Out 管理員中新增之後顯示

Scale Out 背景工作未顯示在 [SSISDB].[catalog].[worker_agents] 中

Scale Out 背景工作服務正在執行，而 Scale Out 背景工作處於離線狀態

### <a name="solutions"></a>**方案** 
請查看 Scale Out 背景工作服務記錄檔中的錯誤訊息，該檔案位於 \<驅動程式\>:\Users\\[執行背景工作服務的帳戶]\AppData\Local\SSIS\Cluster\Agent。

**案例** 

System.ServiceModel.EndpointNotFoundException: 沒有任何在 https://[電腦名稱]:[連接埠]/ClusterManagement/ 上進行接聽的端點可以接受該訊息。

步驟 1：檢查 Scale Out 主機服務設定檔中指定的連接埠號碼是否正確，然後重新啟動 Scale Out 主機服務。 

步驟 2：檢查 Scale Out 背景工作服務設定中指定的主機端點是否正確，然後重新啟動 Scale Out 背景工作服務。

步驟 3：檢查是否已在 Scale Out 主機節點上開啟防火牆連接埠。

步驟 4：解決 Scale Out 主機節點與 Scale Out 背景工作節點之間的任何其他連線問題。

**案例**

System.ServiceModel.Security.SecurityNegotiationException: 無法利用授權 '[電腦名稱]:[連接埠]' 為 SSL/TLS 安全通道建立信任關係。 ---> System.Net.WebException: 基礎連線已關閉: 無法為 SSL/TLS 安全通道建立信任關係。 ---> System.Security.Authentication.AuthenticationException: 根據驗證程序，遠端憑證是無效的。

步驟 1：將 Scale Out 主機憑證安裝到 Scale Out 背景工作節點上本機電腦的根憑證存放區 (如果尚未安裝的話)，然後重新啟動 Scale Out 背景工作服務。

步驟 2：檢查主要端點中的主機名稱是否包含在 Scale Out 主機憑證的 CN 中。 如果沒有，請重設 Scale Out 背景工作設定檔中的主要端點，然後重新啟動 Scale Out 背景工作服務。 

> [!Note]
> 如果由於 DNS 設定而無法變更主要端點的主機名稱，您必須變更 Scale Out 主機憑證。 請參閱[處理 SSIS Scale Out 中的憑證](deal-with-certificates-in-ssis-scale-out.md)。

步驟 3：檢查 Scale Out 背景工作設定中指定的主要指紋是否符合 Scale Out 主機憑證的指紋。 

**案例**

System.ServiceModel.Security.SecurityNegotiationException: 無法利用授權 '[電腦名稱]:[連接埠]' 為 SSL/TLS 建立安全通道。 ---> System.Net.WebException: 要求已中止: 無法建立 SSL/TLS 的安全通道。

步驟 1：透過下列命令，檢查執行 Scale Out 背景工作服務的帳戶是否具有 Scale Out 背景工作憑證的存取權。

```dos
winhttpcertcfg.exe -l -c LOCAL_MACHINE\MY -s {CN of the worker certificate}
```

如果帳戶沒有存取權，請透過下列命令授與權限，然後重新啟動 Scale Out 背景工作服務。

```dos
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the worker certificate} -a {the account running Scale Out Worker service}
```

**案例**

System.ServiceModel.Security.MessageSecurityException: HTTP 要求被用戶端驗證配置 'Anonymous' 禁止。 ---> System.Net.WebException: 遠端伺服器傳回一個錯誤: (403) 禁止。

步驟 1：將 Scale Out 背景工作憑證安裝到 Scale Out 主機節點上本機電腦的根憑證存放區 (如果尚未安裝的話)，然後重新啟動 Scale Out 背景工作服務。

步驟 2：清除 Scale Out 主機節點上本機電腦之根憑證存放區中的無用憑證。

步驟 3：透過在 Scale Out 主機節點上新增下列登錄項目，將安全通道設定為不再於 TLS/SSL 交握過程中傳送可信任的根憑證授權單位清單。

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

值名稱：SendTrustedIssuerList 

值類型：REG_DWORD 

資料值：0 (False)

**案例**

System.ServiceModel.CommunicationException: 對 https://[電腦名稱]:[連接埠]/ClusterManagement/ 發出 HTTP 要求時發生錯誤。 這可能是因為在 HTTPS 的情況下，伺服器憑證未使用 HTTP.SYS 正確設定。 也可能是因為用戶端與伺服器之間的安全性繫結不相符所造成。 

步驟 1：使用下列命令，在主機節點上檢查 Scale Out 主機憑證是否正確繫結至主要端點上的連接埠。 檢查顯示的憑證雜湊是否與 Scale Out 主機憑證指紋相符。

```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```

如果繫結不正確，請使用下列命令將其重設，然後重新啟動 Scale Out 背景工作服務。

```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={Master certificate thumbprint} certstorename=Root appid={random guid}
```

### <a name="symptoms"></a>**徵兆**
在 Scale Out 管理員中將 Scale Out 背景工作連線至 Scale Out 主機時驗證失敗，並出現錯誤訊息：「無法在電腦上開啟憑證存放區」。

### <a name="solution"></a>**方案**

步驟 1：以系統管理員身分執行 Scale Out 管理員。 如果使用 SSMS 來開啟，則需要以系統管理員身分執行 SSMS。

步驟 2：在電腦上啟動遠端登錄服務 (如果未執行的話)。

### <a name="symptoms"></a>**徵兆**
不會啟動 Scale Out 中的執行。

### <a name="solution"></a>**方案**

請檢查 [SSISDB].[catalog].[worker_agents] 中您選取來執行套件的電腦之狀態。 必須至少有一個背景工作在線上且已啟用。

### <a name="symptoms"></a>**徵兆** 
套件執行成功，但沒有記錄任何訊息。

### <a name="solution"></a>**方案**

請檢查裝載 SSISDB 的 SQL Server 是否允許使用 SQL Server 驗證。

> [!Note]  
> 如果您已變更 Scale Out 記錄的帳戶，請參閱[變更 Scale Out 記錄的帳戶](change-logdb-account.md)，並確認記錄所使用的連接字串。

### <a name="symptoms"></a>**徵兆**
套件執行報表中的錯誤訊息可能不足以進行疑難排解。

### <a name="solution"></a>**方案**
在 WorkerSettings.config 中設定的 TasksRootFolder 下可以找到其他執行記錄檔。它預設是 \<驅動程式\>:\Users\\[帳戶]\AppData\Local\SSIS\ScaleOut\Tasks。 [帳戶] 是執行 Scale Out 背景工作服務的帳戶，預設值為 SSISScaleOutWorker140。

若要使用 [執行識別碼] 找出套件執行的記錄檔，請執行下列 T-SQL 命令來取得 [工作識別碼]。 然後，在 TasksRootFolder 下尋找名為 [工作識別碼] 的子資料夾。<sup>1<sup>

```sql
SELECT [TaskId]
FROM [SSISDB].[internal].[tasks] tasks, [SSISDB].[internal].[executions] executions 
WHERE executions.execution_id = *Your Execution Id* AND tasks.JobId = executions.job_id
```
<sup>1</sup> 此查詢僅適用於疑難排解用途，未來 Scale Out 背景工作的記錄/診斷狀況獲得改善後即可進行變更。 
