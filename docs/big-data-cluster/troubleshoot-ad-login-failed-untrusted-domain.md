---
title: AD 模式登入失敗 - 不受信任的網域
titleSuffix: SQL Server Big Data Cluster
description: 修正行為 - 當端點 DNS 項目設定為指向別名名稱的 CNAME 時，用戶端將無法進行驗證。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 05/01/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 669d8f050c3dd86d733c33741eb6fc846245aff2
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891038"
---
# <a name="symptom-ad-mode-login-fails---untrusted-domain-big-data-clusters"></a>徵兆：AD 模式登入失敗 - 不受信任的網域 (巨量資料叢集)

在 Active Directory 模式的 SQL Server 巨量資料叢集 (BDC) 中，連線嘗試可能會失敗，並傳回下列錯誤：

`Login failed. The login is from an untrusted domain and cannot be used with Integrated authentication.`

當將 DNS 項目設定為 CNAME，其指向將流量散發到 Kubernetes 節點的反向 Proxy 其別名名稱時，就會發生這種情況。

## <a name="root-cause"></a>根本原因

當端點 DNS 項目設定為 CNAME，其指向將流量散發到 Kubernetes 節點的反向 Proxy 其別名名稱時：

- Kerberos 驗證處理程序會尋找符合 CNAME 項目的服務主體名稱 (SPN)；而非在 Active Directory 中由 BDC 所註冊的真正 SPN
- 驗證失敗 

## <a name="confirm-root-cause"></a>確認根本原因

驗證失敗後，請檢查 Kerberos 票證的快取。 

若要檢查票證的快取，請使用 `klist` 命令。 

尋找其 SPN 與您已嘗試連線端點相符的票證。

預期的票證不存在。

在此範例中，主要端點 `bdc-sql` DNS 記錄是設定為名為 `ServerReverseProxy` 反向 Proxy 的 CNAME

```PowerShell
Resolve-DnsName bdc-sql
```

下列區段會顯示前一個命令的結果。

```
Name                           Type   TTL   Section    NameHost
----                           ----   ---   -------    --------
bdc-sql.mydomain.com           CNAME  3600  Answer     ReverseProxyServer.mydomain.com

Name       : ReverseProxyServer.mydomain.com
QueryType  : A
TTL        : 3600
Section    : Answer
IP4Address : 193.168.5.10
```

>[!NOTE]
>下列區段會參考 [`tshark`](https://www.wireshark.org/docs/man-pages/tshark.html)。 `tshark` 是安裝為 [Wireshark](https://www.wireshark.org/docs/) 網路追蹤公用程式一部分的命令列公用程式。

若要查看來自 Active Directory 所要求的 SPN，請使用 `tshark`。 下列命令會將網路追蹤擷取限制為 Kerberos 通訊協定的通訊，且只會顯示 `krb-error (30)` 訊息。 這些訊息應會包含失敗的 SPN 要求訊息。

```bash
tshark -Y "kerberos && kerberos.msg_type == 30" -T fields -e kerberos.error_code -e kerberos.SNameString
```

從不同的命令殼層嘗試連線到主要 Pod：

```bash
klist purge

sqlcmd -S bdc-sql.mydomain.com,31433 -E
```

請參閱下列範例輸出。

```bash
klist purge

Current LogonId is 0:0xf6b58
        Deleting all tickets:
        Ticket(s) purged!

sqlcmd -S bdc-sql.mydomain.com,31433 -E
sqlcmd: Error: Microsoft ODBC Driver 17 for SQL Server : Login failed. The login is from an untrusted domain and cannot be used with Integrated authentication.
```

檢查 `tshark` 輸出。 

```bash
Capturing on 'Ethernet 3'
25      krbtgt,RLAZURE.COM
7       MSSQLSvc,ReverseProxyServer.mydomain.com:31433
2 packets captured
```

請注意，用戶端要求的 `SPN MSSQLSvc,ReverseProxyServer.mydomain.com:31433` 不存在。 連線嘗試最後會失敗，並出現錯誤 7。 錯誤 7 表示 `KRB5KDC_ERR_S_PRINCIPAL_UNKNOWN Server not found in Kerberos database`。

在正確的組態中，用戶端會要求由 BDC 註冊的 SPN。 在此範例中，正確的 SPN 應為 `MSSQLSvc,bdc-sql.mydomain.com:31433`。

>[!NOTE]
>錯誤 25 表示 `KDC_ERR_PREAUTH_REQUIRED` - 需要額外的預先驗證。 您可放心忽略這項錯誤訊息。 系統會在初始 Kerberos AD 要求上傳回 `KDC_ERR_PREAUTH_REQUIRED`。 根據預設，Windows Kerberos 用戶端不會在第一個要求中包含預先驗證資訊。

若要查看由 BDC 針對主要端點所註冊的 SPN 清單，請執行 `setspn -L mssql-master`。 

請參閱下列範例輸出：

```bash
Registered ServicePrincipalNames for CN=mssql-master,OU=bdc,DC=mydomain,DC=com:
        MSSQLSvc/bdc-sqlread.mydomain.com:31436
        MSSQLSvc/-sqlread:31436
        MSSQLSvc/bdc-sqlread.mydomain.com
        MSSQLSvc/bdc-sqlread
        MSSQLSvc/bdc-sql.mydomain.com:31433
        MSSQLSvc/bdc-sql:31433
        MSSQLSvc/bdc-sql.mydomain.com
        MSSQLSvc/bdc-sql
        MSSQLSvc/master-p-svc.mydomain.com:1533
        MSSQLSvc/master-p-svc:1533
        MSSQLSvc/master-p-svc.mydomain.com:1433
        MSSQLSvc/master-p-svc:1433
        MSSQLSvc/master-p-svc.mydomain.com
        MSSQLSvc/master-p-svc
        MSSQLSvc/master-svc.mydomain.com:1533
        MSSQLSvc/master-svc:1533
        MSSQLSvc/master-svc.mydomain.com:1433
        MSSQLSvc/master-svc:1433
        MSSQLSvc/master-svc.mydomain.com
        MSSQLSvc/master-svc
```

在上方的結果中，不應註冊反向 Proxy 位址。

## <a name="resolve"></a>解決

本節會說明解決此問題的兩種方式。 進行適當的變更之後，請在用戶端中執行 `ipconfig -flushdns` 和 `klist purge`。 然後再次嘗試連線。

### <a name="option-1"></a>選項 1

移除 DNS 中每個 BDC 端點的 CNAME 記錄，如果有多個主要節點，則使用指向每個 Kubernetes 節點或每個 Kubernetes 主要節點的多個 `A` 記錄加以取代。

>[!TIP]
>以下所述的指令碼會使用 PowerShell。 如需詳細資訊，請參閱[在 Linux 上安裝 PowerShell](/powershell/scripting/install/installing-powershell-core-on-linux)。

您可使用下列 PowerShell 指令碼來更新 DNS 端點記錄。 在連線到相同網域的任何電腦上執行指令碼：

```powershell
#Specify the DNS server, example contoso.local
$Domain_DNS_name=mydomain.com'

#DNS records for bdc endpoints
$Controller_DNS_name = 'bdc-control'
$Managment_proxy_DNS_name= 'bdc-proxy'
$Master_Primary_DNS_name = 'bdc-sql'
$Master_Secondary_DNS_name = 'bdc-sqlread'
$Gateway_DNS_name = 'bdc-gateway'
$AppProxy_DNS_name = 'bdc-appproxy'

#Performing Endpoint DNS records Checks..

#Build array of endpoints 
$BdcEndpointsDns = New-Object System.Collections.ArrayList

[void]$BdcEndpointsDns.Add($Controller_DNS_name)
[void]$BdcEndpointsDns.Add($Managment_proxy_DNS_name)
[void]$BdcEndpointsDns.Add($Master_Primary_DNS_name)
[void]$BdcEndpointsDns.Add($Master_Secondary_DNS_name)
[void]$BdcEndpointsDns.Add($Gateway_DNS_name)
[void]$BdcEndpointsDns.Add($AppProxy_DNS_name)

#Build arrary for results 
$BdcEndpointsDns_Result = New-Object System.Collections.ArrayList

foreach ($DnsName in $BdcEndpointsDns) {
    try {
        $endpoint_DNS_record = Resolve-DnsName $DnsName -Type A -Server $Domain_DNS_IP_address -ErrorAction Stop 
        foreach ($ip in $endpoint_DNS_record.IPAddress) {
            [void]$BdcEndpointsDns_Result.Add("OK - $DnsName is an A record with an IP $ip")
        }
    }
    catch {
        [void]$BdcEndpointsDns_Result.Add("MisConfiguration - $DnsName is not an A record or does not exists")
    }  
}

#show the results 
$BdcEndpointsDns_Result
```

### <a name="option-2"></a>選項 2

或者，將 CNAME 修改為指向反向 Proxy 的 IP 位址，而不是反向 Proxy 的名稱，就可以解決此問題。

## <a name="confirm-resolution"></a>確認解決方式

使用上述其中一個選項解決此問題之後，請使用 Active Directory 連線到巨量資料叢集來確認修正。

## <a name="next-steps"></a>後續步驟

[確認網域控制站的反向 DNS 項目 (PTR 記錄)](active-directory-deploy.md#verify-reverse-dns-entry-for-domain-controller)。
