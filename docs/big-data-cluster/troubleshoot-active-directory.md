---
title: 對 Active Directory 模式部署進行疑難排解
titleSuffix: SQL Server Big Data Cluster
description: 對 Active Directory 網域中的 SQL Server 巨量資料叢集部署進行疑難排解。
author: rl-msft
ms.author: rafidl
ms.reviewer: mikeray
ms.date: 03/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d887eadd021641241516a1478c6ac13e0d0bdec
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "79191209"
---
# <a name="troubleshoot-sql-server-big-data-cluster-active-directory-mode-deployment"></a>對 SQL Server 巨量資料叢集 Active Directory 模式部署進行疑難排解

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文說明如何對 Active Directory 模式中的 SQL Server 巨量資料叢集部署進行疑難排解。

## <a name="check-deployment-progress"></a>檢查部署進度

部署可能需要數分鐘的時間。 如果叢集未在 15 分鐘後就緒，請檢查控制器記錄以取得詳細資料。

正在部署叢集時，請檢查 Pod。

```console
kubectl get pods -n mssql-cluster
```

確認傳回的 Pod 清單包含：

- `compute-`$
- `data-`
- `storage-`

如果未建立計算、資料和儲存體 Pod，請檢查記錄以找出原因。

## <a name="check-logs"></a>查看記錄

如果部署在未建立計算、資料或儲存體 Pod 的情況下結束，請檢查下列記錄以找出原因： 

- 檢查 `controller.log` (`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-20200219-093941\mssql-cluster\control-<suffix>\controller\controller\<date>\controller.log`)。 尋找下列項目︰

  `WARN | StatefulSet master is not ready with 0 ready pods and 3 unready pods `

- 檢查 `master-0` `provisioner.log` (`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-20200219-093941\mssql-cluster\master-0\mssql-server\provisioner\provisioner.log`)

  ```
  ERROR | Failed to create sql login for domain user [<domain>.<top-level-domain>\<domain-group>]
    Traceback (most recent call last):
      File "/opt/provisioner/bin/scripts/provisioningpool.py", line 214, in executeNonQueries
        connection.execute_non_query(command)
      File "src/_mssql.pyx", line 1033, in _mssql.MSSQLConnection.execute_non_query
      File "src/_mssql.pyx", line 1061, in _mssql.MSSQLConnection.execute_non_query
      File "src/_mssql.pyx", line 1634, in _mssql.check_and_raise
      File "src/_mssql.pyx", line 1683, in _mssql.maybe_raise_MSSQLDatabaseException
    _mssql.MSSQLDatabaseException: (15401, b"Windows NT user or group '<domain>.<top-level-domain>\\<domain-group>' not found. Check the name again.DB-Lib error message 20018, severity 16:\nGeneral SQL Server error: Check messages from the SQL Server\n")
  WARNING | [3/3] Provisioning exception occurred during provisioning step: ProvisioningMasterPool.
  WARNING | Failed to create sql login for domain user [<domain>.<top-level-domain>\<domain-group>]
  WARNING | Retrying.
  ```

  在上述範例中，因為網域群組的範圍是網域本機，所以部署無法為網域使用者建立登入。 請使用網域全域或網域通用範圍群組。 [在 Active Directory 模式中部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deploy-active-directory.md) 說明 AD 群組範圍需求。

## <a name="check-the-scope-of-domain-groups"></a>檢查網域群組的範圍。

檢查網域群組 (<`domain-group`>) 的範圍。 使用 [get-adgroup](/powershell/module/addsadministration/get-adgroup/)。

如果 `<domain-group>` 群組範圍為網域本機 (`DomainLocal`)，則部署會失敗。 

下列 PowerShell 指令碼會檢查名為 `bdcadmins` 和 `bdcusers` 的兩個 AD 群組範圍。 以群組的名稱取代這些名稱。 

```powershell
#Administrators and users AD groups
$Cluster_admins_group='bdcadmins'
$Cluster_users_group='bdcusers'

#Performing AD Group Checks...

#AD admin group Check
$ClusterAdminGroupScope_Result = New-Object System.Collections.ArrayList
try {
    $GroupScope = Get-ADgroup -Identity $Cluster_admins_group | Select-Object -ExpandProperty GroupScope
    
    if ($GroupScope -eq 'DomainLocal') {
        [void]$ClusterAdminGroupScope_Result.Add("Misconfiguration - $Cluster_admins_group Group scope is $GroupScope, this scope is not supported, Please change group scope to either Global or Univesal") 
    }
    else {
        [void]$ClusterAdminGroupScope_Result.Add("OK - $Cluster_admins_group Group scope is $GroupScope")
    }
}
catch {
    [void]$ClusterAdminGroupScope_Result.Add("Error - " + $_.exception.message)
}
#Ad users group check
$ClusterUsersGroupScope_Result = New-Object System.Collections.ArrayList
$GroupScope = ''
try {
    $GroupScope = Get-ADgroup -Identity $Cluster_users_group | Select-Object -ExpandProperty GroupScope
    
    if ($GroupScope -eq 'DomainLocal') {
        [void]$ClusterUsersGroupScope_Result.Add("Misconfiguration - $Cluster_users_group Group scope is $GroupScope, this scope is not supported, Please change group scope to either Global or Univesal")
    } 
    else 
    { [void]$ClusterUsersGroupScope_Result.Add("OK - $Cluster_users_group Group scope is $GroupScope") }
}
catch {
    [void]$ClusterUsersGroupScope_Result.Add("Error - " + $_.exception.message)
}

#Display the results
$ClusterUsersGroupScope_Result
```

## <a name="check-security-support-container"></a>檢查安全性支援容器 

檢閱安全性支援容器記錄。

下列命令會在命名空間 `mssql-cluster` 的叢集中收集安全性支援記錄。

```console
azdata bdc debug copy-logs -n mssql-cluster -c security-support
```

將記錄解壓縮，並找出 `\mssql-cluster\control-<identifier>\controller\control-rts5t-controller-stdout.log`。

在記錄中尋找下列項目：

```
ERROR    | Failed to create AD user account 'cntrl-controller'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=cntrl-controller,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform. 
ERROR | Failed to create AD user account 'ldap-user'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=ldap-user,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform. 
ERROR | Failed to create AD user account 'nginx-mgmtproxy'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=nginx-mgmtproxy,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform.
```

當網域控制站 DNS 伺服器遺漏反向 DNS 項目 (PTR 記錄) 時，則可能會發生這些項目。

## <a name="verify-reverse-lookup-ptr-record"></a>確認反向對應 (PTR 記錄)
    
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

[確認網域控制站的反向 DNS 項目 (PTR 記錄)](deploy-active-directory.md#verify-reverse-dns-entry-for-domain-controller)。