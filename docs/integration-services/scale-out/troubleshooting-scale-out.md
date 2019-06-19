---
title: 針對 SQL Server Integration Services (SSIS) Scale Out 進行疑難排解 | Microsoft Docs
description: 本文描述如何針對 SSIS Scale Out 的常見問題進行疑難排解
ms.custom: performance
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
manager: craigg
ms.openlocfilehash: 8de649eb8f6311270c64969981e78315cee29450
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65718284"
---
# <a name="troubleshoot-scale-out"></a>針對 Scale Out 進行疑難排解

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



SSIS Scale Out 涉及 SSIS 目錄資料庫 `SSISDB`、Scale Out Master 服務與 Scale Out Worker 服務之間的通訊。 有時，這項通訊會因設定錯誤、沒有存取權限和其他原因而中斷。 本文可協助您針對 Scale Out 設定問題進行疑難排解。

若要調查您遇到的徵兆，請遵循下列步驟逐步執行，直到問題解決為止。

## <a name="scale-out-master-fails"></a>Scale Out Master 失敗

### <a name="symptoms"></a>徵狀 
-   Scale Out 主機無法連線至 SSISDB。 

-   主機屬性無法顯示在 Scale Out 管理員中。

-   在 `[catalog].[master_properties]` 檢視中，不會填入主要屬性。

### <a name="solution"></a>方案
1.  檢查是否已啟用 Scale Out。

    在 SSMS 中，於 [物件總管] 中的 [SSISDB]  上按一下滑鼠右鍵，然後選取 [已啟用 Scale Out 功能]  。

    ![已啟用 Scale Out](media/isenabled.PNG)

    如果屬性值為 False，請呼叫 `[catalog].[enable_scaleout]` 預存程序來啟用 Scale Out。

2.  檢查 Scale Out Master 設定檔中指定的 SQL Server 名稱是否正確，然後重新啟動 Scale Out Master 服務。

## <a name="scale-out-worker-fails"></a>Scale Out Worker 失敗

### <a name="symptoms"></a>徵狀 
-   Scale Out Worker 無法連線至 Scale Out Master。

-   Scale Out Worker 未於其新增在 Scale Out Manager 之後顯示。

-   Scale Out Worker 不會顯示在 `[catalog].[worker_agents]` 檢視中。

-   Scale Out Worker 服務正在執行，但 Scale Out Worker 離線。

### <a name="solution"></a>方案
請檢查 `\<drive\>:\Users\\*[account running worker service]*\AppData\Local\SSIS\Cluster\Agent` 下方之 Scale Out Worker 服務記錄中的錯誤訊息。

## <a name="no-endpoint-listening"></a>無端點接聽

### <a name="symptoms"></a>徵狀

*「System.ServiceModel.EndpointNotFoundException:沒有任何在 https://* [機器名稱]:[連接埠] */ClusterManagement/ 上進行接聽的端點可以接受該訊息。」*

### <a name="solution"></a>方案

1.  檢查 Scale Out Master 服務設定檔中指定的連接埠號碼是否正確，然後重新啟動 Scale Out Master 服務。 

2.  檢查 Scale Out Worker 服務設定中指定的主要端點是否正確，然後重新啟動 Scale Out Worker 服務。

3.  檢查是否已在 Scale Out Master 節點上開啟防火牆連接埠。

4.  解決 Scale Out Master 節點與 Scale Out Worker 節點之間的任何其他連線問題。

## <a name="could-not-establish-trust-relationship"></a>無法建立信任關係

### <a name="symptoms"></a>徵狀
*「System.ServiceModel.Security.SecurityNegotiationException:無法利用授權 '[機器名稱]:[連接埠]' 為 SSL/TLS 安全通道建立信任關係。」*

*「System.Net.WebException:基礎連線已關閉:無法為 SSL/TLS 安全通道建立信任關係。」*

*「System.Security.Authentication.AuthenticationException:根據驗證程序，遠端憑證無效。」*

### <a name="solution"></a>方案
1.  將 Scale Out Master 憑證安裝至 Scale Out Worker 節點上本機電腦的根憑證存放區 (如果尚未安裝憑證)，然後重新啟動 Scale Out Worker 服務。

2.  檢查主要端點中的主機名稱是否包含在 Scale Out Master 憑證的 CN 中。 如果沒有，請重設 Scale Out Worker 設定檔中的主要端點，然後重新啟動 Scale Out Worker 服務。 

    > [!NOTE]
    > 如果由於 DNS 設定而無法變更主要端點的主機名稱，您必須變更 Scale Out Master 憑證。 請參閱[管理 SSIS Scale Out 的憑證](deal-with-certificates-in-ssis-scale-out.md)。

3.  檢查 Scale Out Worker 設定中指定的主要指紋是否符合 Scale Out Master 憑證的指紋。 

## <a name="could-not-establish-secure-channel"></a>無法建立安全通道

### <a name="symptoms"></a>徵狀

*「System.ServiceModel.Security.SecurityNegotiationException:無法以授權 '[機器名稱]:[連接埠]' 建立 SSL/TLS 的安全通道。」*

*「System.Net.WebException:要求已中止:無法建立 SSL/TLS 安全通道。」*

### <a name="solution"></a>方案
執行下列命令，檢查執行 Scale Out Worker 服務的帳戶是否可以存取 Scale Out Worker 憑證：

```dos
winhttpcertcfg.exe -l -c LOCAL_MACHINE\MY -s {CN of the worker certificate}
```

如果帳戶沒有存取權，請執行下列命令來授與存取權，然後重新啟動「Scale Out 背景工作」服務。

```dos
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the worker certificate} -a {the account running Scale Out Worker service}
```

## <a name="http-request-forbidden"></a>HTTP 要求已禁止

### <a name="symptoms"></a>徵狀

*「System.ServiceModel.Security.MessageSecurityException:用戶端驗證配置 'Anonymous' 禁止 HTTP 要求。」*

*「System.Net.WebException:遠端伺服器傳回錯誤：(403) 禁止。」*

### <a name="solution"></a>方案
1.  將 Scale Out Worker 憑證安裝至 Scale Out Master 節點上本機電腦的根憑證存放區 (如果尚未安裝憑證)，然後重新啟動 Scale Out Worker 服務。

2.  清除「Scale Out 主機」 節點上本機電腦之根憑證存放區中的無用憑證。

3.  透過在 Scale Out Master 節點上新增下列登錄項目，將安全通道設定為不再於 TLS/SSL 交握過程中傳送可信任的根憑證授權單位清單。

    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL`

    值名稱：**SendTrustedIssuerList** 

    值類型：**REG_DWORD** 

    值資料：**0 (False)**

4.  如果無法如步驟 2 中所述清除所有非自我簽署憑證，請將下列登錄機碼值設定為 2。

    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL`

    值名稱：**ClientAuthTrustMode** 

    值類型：**REG_DWORD** 

    值資料：**2**

    > [!NOTE]
    > 如果您在根憑證存放區中有非自我簽署的憑證，用戶端憑證驗證將會失敗。 如需詳細資訊，請參閱[Internet Information Services (IIS) 8 可能會以 HTTP 403.7 或 403.16 錯誤來拒絕用戶端憑證要求](https://support.microsoft.com/help/2802568/internet-information-services-iis-8-may-reject-client-certificate-requ) (\英文\)。

## <a name="http-request-error"></a>HTTP 要求錯誤

### <a name="symptoms"></a>徵狀

 「System.ServiceModel.CommunicationException:對 https://[機器名稱]:[連接埠]/ClusterManagement/ 發出 HTTP 要求時發生錯誤。這可能是因為在 HTTPS 的情況下，伺服器憑證未使用 HTTP.SYS 正確設定。也可能是因為用戶端與伺服器之間的安全性繫結不相符所造成。」

### <a name="solution"></a>方案
1.  執行下列命令，檢查主要節點上 Scale Out Master 憑證是否正確地繫結至主要端點中的連接埠：

    ```dos
    netsh http show sslcert ipport=0.0.0.0:{Master port}
    ```

    檢查顯示的憑證雜湊是否與 Scale Out Master 憑證指紋相符。 如果繫結不正確，請執行下列命令重設繫結，然後重新啟動 Scale Out Worker 服務。

    ```dos
    netsh http delete sslcert ipport=0.0.0.0:{Master port}
    netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={Master certificate thumbprint} certstorename=Root  appid={random guid}
    ```

## <a name="cannot-open-certificate-store"></a>無法開啟憑證存放區

### <a name="symptoms"></a>徵狀
在 Scale Out Manager 中將 Scale Out Worker 連線至 Scale Out Master 時驗證失敗，並出現錯誤訊息：「無法在電腦上開啟憑證存放區」  。

### <a name="solution"></a>方案

1.  以系統管理員身分執行 Scale Out Manager。 如果您使用 SSMS 開啟 Scale Out Manager，則需要以系統管理員身分執行 SSMS。

2.  在電腦上啟動遠端登錄服務 (如果尚未執行)。

## <a name="execution-doesnt-start"></a>無法開始執行

### <a name="symptoms"></a>徵狀
不會啟動 Scale Out 中的執行。

### <a name="solution"></a>方案

在 `[catalog].[worker_agents]` 檢視中，檢查您選取要執行套件之電腦的狀態。 必須至少有一個背景工作在線上且已啟用。

## <a name="no-log"></a>無記錄

### <a name="symptoms"></a>徵狀 
套件執行成功，但未記錄任何訊息。

### <a name="solution"></a>方案

請檢查裝載 SSISDB 的 SQL Server 執行個體是否允許使用 SQL Server 驗證。

> [!NOTE]  
> 如果您已變更 Scale Out 記錄的帳戶，請參閱[變更 Scale Out 記錄的帳戶](change-logdb-account.md)，並確認記錄所使用的連接字串。

## <a name="error-messages-arent-helpful"></a>錯誤訊息不是很有幫助

### <a name="symptoms"></a>徵狀
套件執行報表中的錯誤訊息不足以進行疑難排解。

### <a name="solution"></a>方案
在 `WorkerSettings.config` 中設定的 `TasksRootFolder` 下方，可以找到其他執行記錄。 此資料夾預設為 `\<drive\>:\Users\\[account]\AppData\Local\SSIS\ScaleOut\Tasks`。 *[account]* 是執行 Scale Out Worker 服務的帳戶，預設值為 `SSISScaleOutWorker140`。

若要使用 [執行識別碼]  找出套件執行的記錄，請執行下列 Transact-SQL 命令來取得 [工作識別碼]  。 然後，尋找 `TasksRootFolder` 下包含 [工作識別碼]  的子資料夾名稱。

```sql
SELECT [TaskId]
FROM [SSISDB].[internal].[tasks] tasks, [SSISDB].[internal].[executions] executions 
WHERE executions.execution_id = *Your Execution Id* AND tasks.JobId = executions.job_id
```

> [!WARNING]
> 此查詢適用於進行疑難排解。 查詢中所參考的內部檢視未來會進行變更。 

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱下列有關安裝和設定 SSIS Scale Out 的文章：
-   [在單一電腦上開始使用 Integration Services (SSIS) Scale Out](get-started-with-ssis-scale-out-onebox.md)
-   [逐步解說：設定 Integration Services (SSIS) Scale Out](walkthrough-set-up-integration-services-scale-out.md)
