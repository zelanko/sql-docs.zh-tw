---
title: 使用 Windows 驗證連線您的 SQL Server (Kerberos)
description: 了解如何啟用 Kerberos，以針對 Azure Data Studio 使用 Active Directory 驗證
ms.prod: azure-data-studio
ms.technology: ''
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.topic: conceptual
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: c2e6b303217d420d439d510fc3fc24886657684b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774666"
---
# <a name="connect-azure-data-studio-to-your-sql-server-using-windows-authentication---kerberos"></a>使用 Windows 驗證將 Azure Data Studio 連線到您的 SQL Server - Kerberos

Azure Data Studio 支援使用 Kerberos 連線到 SQL Server。

為了在 macOS 或 Linux 上使用整合式驗證 (Windows 驗證)，您必須設定 **Kerberos 票證**，將目前的使用者連結至 Windows 網域帳戶。

## <a name="prerequisites"></a>必要條件

- 存取已加入網域的 Windows 電腦，以查詢您的 Kerberos 網域控制站。
- SQL Server 應設定為允許 Kerberos 驗證。 針對在 UNIX 上執行的用戶端驅動程式，只有使用 Kerberos 才支援整合式驗證。 如需詳細資訊，請參閱[使用 Kerberos 整合式驗證連線到 SQL Server](../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。 針對您嘗試連線的每個 SQL Servr 執行個體，應該會註冊一個 SPN。 如需詳細資訊，請參閱[註冊服務主體名稱](https://technet.microsoft.com/library/ms191153%28v=sql.105%29.aspx#SPN%20Formats)。


## <a name="checking-if-sql-server-has-kerberos-setup"></a>檢查 SQL Server 是否已設定 Kerberos

登入 SQL Server 的主機電腦。 從 Windows 命令提示字元，使用 `setspn -L %COMPUTERNAME%` 來列出主機的所有服務主體名稱。 您應該會看到以 MSSQLSvc/HostName.Domain.com 開頭的項目，這表示 SQL Server 已註冊 SPN，並已準備好接受 Kerberos 驗證。 
- 如果您無法存取 SQL Server 的主機，則從任何其他已加入相同 Active Directory 的 Windows OS 中，您可以使用 `setspn -L <SQLSERVER_NETBIOS>` 命令，其中 <SQLSERVER_NETBIOS> 是 SQL Server 主機的電腦名稱。


## <a name="get-the-kerberos-key-distribution-center"></a>取得 Kerberos 金鑰發佈中心

尋找 Kerberos KDC (金鑰發佈中心) 設定值。 在加入 Active Directory 網域的 Windows 電腦上執行下列命令： 

啟動 `cmd.exe` 並執行 `nltest`。

```
nltest /dsgetdc:DOMAIN.COMPANY.COM (where "DOMAIN.COMPANY.COM" maps to your domain's name)

Sample Output
DC: \\dc-33.domain.company.com
Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
...
The command completed successfully
```
複製 DC 名稱，這是必要的 KDC 設定值，在此案例中為 dc-33.domain.company.com

## <a name="join-your-os-to-the-active-directory-domain-controller"></a>將您的 OS 加入 Active Directory 網域控制站

### <a name="ubuntu"></a>Ubuntu
```bash
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

編輯 `/etc/network/interfaces` 檔案，讓您的 AD 網域控制站 IP 位址列為 dns-nameserver。 例如： 

```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
iface eth0 inet dhcp
dns-nameservers **<AD domain controller IP address>**
dns-search **<AD domain name>**
```

> [!NOTE]
> 網路介面 (eth0) 可能會因不同電腦而有所不同。 若要找出您使用的是哪一個，請執行 ifconfig，並複製具有 IP 位址且已傳送和接收位元組的介面。

編輯此檔案之後，請重新啟動網路服務：

```bash
sudo ifdown eth0 && sudo ifup eth0
```

現在，檢查 `/etc/resolv.conf` 檔案是否包含如下所示的程式碼行：  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
```
   
### <a name="redhat-enterprise-linux"></a>RedHat Enterprise Linux
```bash
sudo yum install realmd krb5-workstation
```

編輯 `/etc/sysconfig/network-scripts/ifcfg-eth0` 檔案 (或視需要編輯其他介面設定檔)，以便將您的 AD 網域控制站 IP 位址列為 DNS 伺服器：

```/etc/sysconfig/network-scripts/ifcfg-eth0
<...>
PEERDNS=no
DNS1=**<AD domain controller IP address>**
```

編輯此檔案之後，請重新啟動網路服務：

```bash
sudo systemctl restart network
```

現在，檢查 `/etc/resolv.conf` 檔案是否包含如下所示的程式碼行：  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>macOS

- 遵循下列步驟，將您的 macOS 加入 Active Directory 網域控制站：



## <a name="configure-kdc-in-krb5conf"></a>在 krb5.conf 中設定 KDC

以您所選擇的編輯器編輯 `/etc/krb5.conf`。 設定下列金鑰

```bash
sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = DOMAIN.COMPANY.COM
 
[realms]
DOMAIN.COMPANY.COM = {
   kdc = dc-33.domain.company.com
}
```

然後，儲存 krb5.conf 檔案並結束

> [!NOTE]
> 網域必須全部為大寫


## <a name="test-the-ticket-granting-ticket-retrieval"></a>測試票證授權票證的擷取

從 KDC 取得票證授權票證 (TGT)。

```bash
kinit username@DOMAIN.COMPANY.COM
```

使用 klist 來檢視可用的票證。 如果 kinit 成功，您應該會看到票證。 

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-using-azure-data-studio"></a>使用 Azure Data Studio 連線

* 建立新的連線設定檔

* 選擇 [Windows 驗證] 作為驗證類型

* 完成連線設定檔，按一下 [連線]

成功連線之後，您的伺服器就會顯示在 [伺服器] 資料看板中。
