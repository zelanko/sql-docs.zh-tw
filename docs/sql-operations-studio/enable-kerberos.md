---
title: SQL Operations Studio (preview) 中的連接時，使用 Active Directory 驗證 (Kerberos) |Microsoft 文件
description: 了解如何啟用 Kerberos，若要使用 Active Directory 驗證的 SQL Operations Studio (preview)
ms.custom: tools|sos
ms.date: 11/17/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: meet-bhagdev
ms.author: meetb
manager: craigg
ms.openlocfilehash: 46726247dc8540e67611173f6692ce092bb5be33
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="connect-includename-sosincludesname-sos-shortmd-to-your-sql-server-using-windows-authentication---kerberos"></a>連接[!INCLUDE[name-sos](../includes/name-sos-short.md)]到 SQL Server 使用 Windows 驗證的 Kerberos 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 連接到 SQL Server 使用 Kerberos 的支援。

若要在 macOS 或 Lunix 上使用整合式驗證 （Windows 驗證），您必須設定**Kerberos 票證**將目前的使用者連結至 Windows 網域帳戶。 

## <a name="prerequisites"></a>必要條件

- Windows 網域的電腦才能查詢 Kerberos 網域控制站的存取。
- SQL Server 應該設定為允許 Kerberos 驗證。 在 Unix 上執行的用戶端驅動程式，支援整合式的驗證是只使用 Kerberos。 可以找到上設定 Sql Server 使用 Kerberos 進行驗證的詳細資訊[這裡](https://support.microsoft.com/en-us/help/319723/how-to-use-kerberos-authentication-in-sql-server)。 應該針對每個您嘗試連接到 Sql Server 執行個體註冊 Spn。 SQL Server Spn 格式的相關詳細資料列[這裡](https://technet.microsoft.com/en-us/library/ms191153%28v=sql.105%29.aspx#SPN%20Formats)


## <a name="checking-if-sql-server-has-kerberos-setup"></a>正在檢查 Sql Server 是否有 Kerberos 設定

主機電腦的 Sql Server 登入。 從 「 Windows 命令提示字元中，使用`setspn -L %COMPUTERNAME%`列出主機的所有服務主體名稱。 您應該會看到開頭 MSSQLSvc/HostName.Domain.com 這表示 Sql Server 已註冊 SPN，而且已準備好接受 Kerberos 驗證的項目。 
- 如果您沒有存取主應用程式的 Sql Server，然後從任何其他 Windows 作業系統加入相同 Active Directory，您可以使用命令`setspn -L <SQLSERVER_NETBIOS>`< SQLSERVER_NETBIOS > 所在的 Sql Server 主機的電腦名稱。


## <a name="get-the-kerberos-key-distribution-center"></a>取得 Kerberos 金鑰發佈中心

尋找 Kerberos KDC （金鑰發佈中心） 組態值。 已加入 Active Directory 網域的 Windows 電腦上執行下列命令： 

啟動`cmd.exe`並執行`nltest`。

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

編輯`/etc/network/interfaces`檔案，所以您的 AD 網域控制站的 IP 位址會列示為 dns nameserver。 例如： 

```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
iface eth0 inet dhcp
dns-nameservers **<AD domain controller IP address>**
dns-search **<AD domain name>**
```

> [!NOTE]
> 網路介面 (eth0) 可能會與不同的機器不同。 若要找出您要使用哪一項，執行 ifconfig 並複製有 IP 位址，以及傳輸和接收位元組的介面。

編輯這個檔案之後, 重新啟動網路服務：

```bash
sudo ifdown eth0 && sudo ifup eth0
```

現在請檢查您`/etc/resolv.conf`檔案包含類似下列一行：  

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

編輯`/etc/sysconfig/network-scripts/ifcfg-eth0`檔案 （或其他介面設定檔案依適當情況），讓您的 AD 網域控制站的 IP 位址會列示為 DNS 伺服器：

```/etc/sysconfig/network-scripts/ifcfg-eth0
<...>
PEERDNS=no
DNS1=**<AD domain controller IP address>**
```

編輯這個檔案之後, 重新啟動網路服務：

```bash
sudo systemctl restart network
```

現在請檢查您`/etc/resolv.conf`檔案包含類似下列一行：  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>macOS

- [遵循下列步驟] 時，將您 macOS 聯結至 Active Directory 網域控制站 (https://support.apple.com/kb/PH26282?viewlocale=en_US&locale=en_US)。



## <a name="configure-kdc-in-krb5conf"></a>在 krb5.conf 設定 KDC

編輯`/etc/krb5.conf`在您選擇的編輯器中。 設定下列機碼

```bash
sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = DOMAIN.COMPANY.COM
 
[realms]
DOMAIN.COMPANY.COM = {
   kdc = dc-33.domain.company.com
}
```

然後儲存 krb5.conf 檔案，然後結束

> [!NOTE]
> 網域必須全部大寫


## <a name="test-the-ticket-granting-ticket-retrieval"></a>測試票證授權票證擷取

取得票證授權票證 (TGT) 從 KDC。

```bash
kinit username@DOMAIN.COMPANY.COM
```

檢視可使用 kinit 的票證。 如果 kinit 成功，您應該會看到票證。 

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-using-includename-sosincludesname-sos-shortmd"></a>使用連線 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

* 建立新的連線設定檔

* 選擇**Windows 驗證**做為驗證類型

* 完成 連線設定檔中，按一下**連接**

已成功連接之後，您的伺服器，會出現在*伺服器*[資訊看板]。
