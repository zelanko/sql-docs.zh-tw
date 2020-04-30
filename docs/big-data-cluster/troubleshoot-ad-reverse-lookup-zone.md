---
title: AD 模式部署已停止 - 缺少 DC 的反向對應區域項目
titleSuffix: SQL Server Big Data Cluster
description: 以 AD 模式部署 BDC 停滯，因為缺少網域控制站 DNS 伺服器中網域控制站的反向對應區域項目。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 04/21/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4cac5fe891533d623a686a02641f63cb25d4b17f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82154153"
---
# <a name="ad-mode-deployment-stopped---missing-reverse-lookup-zone-entry-for-dc"></a>AD 模式部署已停止 - 缺少 DC 的反向對應區域項目

以 Active Directory (AD) 模式部署發生凍結。 請檢查徵兆，以了解原因是否是網域控制站 DNS 伺服器缺少反向對應區域項目。 

## <a name="symptom"></a>徵狀

您已開始以 AD 模式部署 BDC，但部署已停滯而未繼續進行。

下列範例顯示某個 Bash 殼層中的部署結果。

```
The privacy statement can be viewed at:
https://go.microsoft.com/fwlink/?LinkId=853010
 
The license terms for SQL Server Big Data Cluster can be viewed at:
Enterprise: https://go.microsoft.com/fwlink/?linkid=2104292
Standard: https://go.microsoft.com/fwlink/?linkid=2104294
Developer: https://go.microsoft.com/fwlink/?linkid=2104079
 
Cluster deployment documentation can be viewed at:
https://aka.ms/bdc-deploy
 
NOTE: Cluster creation can take a significant amount of time depending on
configuration, network speed, and the number of nodes in the cluster.
 
Starting cluster deployment.
Cluster controller endpoint is available at bdc-control.contoso.com:30080, 193.168.5.14:30080.
Waiting for control plane to be ready after 5 minutes.
Waiting for control plane to be ready after 10 minutes.
Waiting for control plane to be ready after 15 minutes.
Waiting for control plane to be ready after 20 minutes.
Waiting for control plane to be ready after 25 minutes.
```

檢查目前已部署的 Pod。

```bash
kubectl get pods -n mssql-cluster
```

下方結果指出只部署了屬於控制站的 Pod。 並不會建立用於計算、資料或儲存體的 Pod。

```
NAME              READY   STATUS    RESTARTS   AGE
control-rts5t     3/3     Running   0          18m
controldb-0       2/2     Running   0          18m
controlwd-csgst   1/1     Running   0          16m
dns-7kfnz         2/2     Running   0          16m
logsdb-0          1/1     Running   0          16m
logsui-2pc29      1/1     Running   0          16m
metricsdb-0       1/1     Running   0          16m
metricsdc-4rtm4   1/1     Running   0          16m
metricsdc-6lr2t   1/1     Running   0          16m
metricsdc-ftx9m   1/1     Running   0          16m
metricsdc-h59jb   1/1     Running   0          16m
metricsui-lvdpt   1/1     Running   0          16m
mgmtproxy-mkmxp   2/2     Running   0          16m
```

請檢查安全性支援容器記錄。 尋找 LDAP 錯誤。 

## <a name="check-security-support-container"></a>檢查安全性支援容器 

檢閱安全性支援容器記錄。

下列命令會在命名空間 `mssql-cluster` 的叢集中收集安全性支援記錄。

```bash
azdata bdc debug copy-logs -n mssql-cluster -c security-support
```

將記錄解壓縮，並找出 `\mssql-cluster\control-<identifier>\controller\control-rts5t-controller-stdout.log`。

> [!TIP]
> 收集記錄的方法有許多個。 您可以使用 Azure Data Studio 中的筆記本，而不使用 `azdata` 來複製記錄。
> 在 Azure Data Studio 中，連線到 Kubernetes 叢集，然後執行適當的疑難排解筆記本。 以下是筆記本的範例。
>
> - TSG027 - 觀察叢集部署
> - TSG061 - 取得 BDC 命名空間中 Pod 的所有容器記錄結尾
> - TSG001 - 執行 `azdata` copy-logs
>

## <a name="inspect-the-logs"></a>檢查記錄

找出記錄。 下列範例會指向控制站部署記錄。 

`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-YYYYMMDD-HHMMSS\<namespace>\control-<identifier>\controller\control-<identifier>-controller-stdout.log`"

```
YYYY-MM-DD HH:MM:SS.ms | ERROR | Failed to create AD user account 'cntrl-controller'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=cntrl-controller,OU=bdc, DC=CONTOSO, DC=com' to 'CONTOSO.COM': Server is unwilling to perform. 
YYYY-MM-DD HH:MM:SS.ms | ERROR | Failed to create AD user account 'ldap-user'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=ldap-user,OU=bdc, DC=CONTOSO, DC=com' to 'CONTOSO.COM': Server is unwilling to perform. 
YYYY-MM-DD HH:MM:SS.ms | ERROR | Failed to create AD user account 'nginx-mgmtproxy'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=nginx-mgmtproxy,OU=bdc, DC=CONTOSO, DC=com' to 'CONTOSO.COM': Server is unwilling to perform. 
```

## <a name="cause"></a>原因

缺少網域控制站 DNS 項目中網域控制站的反向對應區域項目。 

## <a name="resolution"></a>解決方案

執行下列 PowerShell 指令碼以確認是否已設定反向 DNS 項目 (PTR 記錄)。

```powershell
#Domain Controller FQDN 'DCserver01.contoso.local'
$Domain_controller_FQDN = 'DCserver01.contoso.local'

#Performing Domain Controller DNS record, reverse PTR Checks...
$DcControllerDnsPtr_Result = New-Object System.Collections.ArrayList
try {
    $Domain_controller_DNS_Record = Resolve-DnsName $Domain_controller_FQDN -Type A -Server $Domain_DNS_IP_address -ErrorAction Stop
    foreach ($ip in $Domain_controller_DNS_Record.IPAddress) {
        #resolving hostname by IP address to make sure we have reverse PTR record 
        if ((Resolve-DnsName $ip).NameHost -eq $Domain_controller_FQDN) {
            [void]$DcControllerDnsPtr_Result.add("OK - $Domain_controller_FQDN has an A record with an IP $ip, Reverse PTR record is in place") 
        }
        else {
            [void]$DcControllerDnsPtr_Result.add("Missing - $Domain_controller_FQDN has an A record with an IP $ip, But no reverse PTR record was found for the host")
        }
    }
}
catch {
    [void]$DcControllerDnsPtr_Result.add("Error - " + $_.exception.message)
}

#show the results 
$DcControllerDnsPtr_Result
```

## <a name="next-steps"></a>後續步驟

[確認網域控制站的反向 DNS 項目 (PTR 記錄)](deploy-active-directory.md#verify-reverse-dns-entry-for-domain-controller)。
