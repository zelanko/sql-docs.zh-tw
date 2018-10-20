---
title: 使用 Azure Data Studio 進行連接時，請使用 Active Directory 驗證 (Kerberos) |Microsoft Docs
description: 了解如何啟用適用於 Azure 資料 Studio 中使用 Active Directory 驗證的 Kerberos
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: meet-bhagdev
ms.author: meetb
manager: craigg
ms.openlocfilehash: 8bbd03d815594cfae850a94ae8067d37f0f5c744
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356319"
---
# <a name="connect-includename-sosincludesname-sos-shortmd-to-your-sql-server-using-windows-authentication---kerberos"></a>連接[!INCLUDE[name-sos](../includes/name-sos-short.md)]到 SQL Server 使用 Windows 驗證-Kerberos 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 連接到 SQL Server 使用 Kerberos 的支援。

若要在 macOS 或 Linux 上使用整合式驗證 （Windows 驗證），您必須設定**Kerberos 票證**您目前的使用者連結到 Windows 網域帳戶。 

## <a name="prerequisites"></a>必要條件

- 若要查詢您的 Kerberos 網域控制站的 Windows 網域的機器存取。
- SQL Server 應該設定成允許 Kerberos 驗證。 在 Unix 上執行用戶端驅動程式的情況下，對整合式的驗證，才支援使用 Kerberos。 可以找到更多有關將 Sql Server 設定為使用 Kerberos 進行驗證[此處](https://support.microsoft.com/en-us/help/319723/how-to-use-kerberos-authentication-in-sql-server)。 應該針對每個您嘗試連接到 Sql Server 執行個體註冊 Spn。 SQL Server Spn 格式的相關詳細資料列[這裡](https://technet.microsoft.com/library/ms191153%28v=sql.105%29.aspx#SPN%20Formats)


## <a name="checking-if-sql-server-has-kerberos-setup"></a>正在檢查 Sql Server 是否有 Kerberos 設定

登入主機電腦的 Sql Server。 從 「 Windows 命令提示字元中，使用`setspn -L %COMPUTERNAME%`列出主機的所有服務主體名稱。 您應該會看到開頭為 MSSQLSvc/HostName.Domain.com 這表示 Sql Server 已註冊 SPN，而且已準備好接受 Kerberos 驗證的項目。 
- 如果您沒有 Sql Server 中，主機的存取權，則從任何其他 Windows 作業系統加入相同的 Active Directory，您可以使用命令`setspn -L <SQLSERVER_NETBIOS>`< SQLSERVER_NETBIOS > 所在的 Sql server 主機的電腦名稱。


## <a name="get-the-kerberos-key-distribution-center"></a>取得 Kerberos 金鑰發佈中心

尋找 Kerberos KDC （金鑰發佈中心） 組態值。 已加入至您的 Active Directory 網域的 Windows 電腦上執行下列命令： 

開始`cmd.exe`並執行`nltest`。

```
nltest /dsgetdc:DOMAIN.COMPANY.COM (where “DOMAIN.COMPANY.COM” maps to your domain’s name)

Sample Output
DC: \\dc-33.domain.company.com
Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
...
The command completed successfully
```
複製 DC 名稱是必要的 KDC 組態中的值，這個案例的 dc 33.domain.company.com

## <a name="join-your-os-to-the-active-directory-domain-controller"></a>加入您的作業系統，Active Directory 網域控制站

### <a name="ubuntu"></a>Ubuntu
```bash
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

編輯`/etc/network/interfaces`檔案，以便 AD 網域控制站的 IP 位址列示為 dns large。 例如： 

```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
iface eth0 inet dhcp
dns-nameservers **<AD domain controller IP address>**
dns-search **<AD domain name>**
```

> [!NOTE]
> 不同的電腦可能會不同的網路介面 (eth0)。 若要找出您正在使用哪一個，請執行 ifconfig，複製有 IP 位址及傳輸及收到位元組的介面。

在編輯這個檔案之後, 重新啟動網路服務：

```bash
sudo ifdown eth0 && sudo ifup eth0
```

現在，請確認您`/etc/resolv.conf`檔案包含的列，如下所示：  

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

編輯`/etc/sysconfig/network-scripts/ifcfg-eth0`檔案 （或其他檔案為適當的介面設定），以便 AD 網域控制站的 IP 位址列示為 DNS 伺服器：

```/etc/sysconfig/network-scripts/ifcfg-eth0
<...>
PEERDNS=no
DNS1=**<AD domain controller IP address>**
```

在編輯這個檔案之後, 重新啟動網路服務：

```bash
sudo systemctl restart network
```

現在，請確認您`/etc/resolv.conf`檔案包含的列，如下所示：  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>macOS

- 依照 [這些步驟] 將您的 macOS 加入 Active Directory 網域控制站 (https://support.apple.com/kb/PH26282?viewlocale=en_US&locale=en_US)。



## <a name="configure-kdc-in-krb5conf"></a>在 krb5.conf 設定 KDC

編輯`/etc/krb5.conf`在您選擇的編輯器中。 設定下列金鑰

```bash
sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = DOMAIN.COMPANY.COM
 
[realms]
DOMAIN.COMPANY.COM = {
   kdc = dc-33.domain.company.com
}
```

然後將儲存 krb5.conf 檔案並結束

> [!NOTE]
> 網域必須是全部大寫


## <a name="test-the-ticket-granting-ticket-retrieval"></a>測試票證授權票證擷取

取得票證授權票證 (TGT)，從 KDC。

```bash
kinit username@DOMAIN.COMPANY.COM
```

檢視可用的票證使用 kinit。 如果 kinit 成功，您應該會看到一個票證。 

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-using-includename-sosincludesname-sos-shortmd"></a>使用連線 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

* 建立新的連線設定檔

* 選擇**Windows 驗證**作為驗證類型

* 完成連線設定檔，請按一下**Connect**

成功連線之後，您的伺服器，會出現在*伺服器*資訊看板。
