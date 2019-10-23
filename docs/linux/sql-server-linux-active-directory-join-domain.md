---
title: 將 Linux 上的 SQL Server 加入 Active Directory
titleSuffix: SQL Server
description: ''
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.date: 04/01/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 90a2bcdac4fd1870adc4eeaa888b906857ef9854
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305284"
---
# <a name="join-sql-server-on-a-linux-host-to-an-active-directory-domain"></a>將 Linux 主機上的 SQL Server 加入 Active Directory 網域

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文提供如何將 SQL Server Linux 主機電腦加入 Active Directory (AD) 網域的一般指引。 您可使用下列兩種方法：使用內建的 SSSD 套件，或使用協力廠商 Active Directory 提供者。 協力廠商網域加入產品的範例包括 [PowerBroker Identity Services (PBIS)](https://www.beyondtrust.com/)、[One Identity](https://www.oneidentity.com/products/authentication-services/) 和 [Centrify](https://www.centrify.com/)。 本指南包含檢查 Active Directory 設定的步驟。 不過，它並未提供在使用協力廠商公用程式時如何將電腦加入網域的指示。

## <a name="prerequisites"></a>Prerequisites

設定 Active Directory 驗證之前，您必須先在網路上設定 Active Directory 網域控制站 (Windows)。 然後，將 Linux 主機上的 SQL Server 加入 Active Directory 網域。

> [!IMPORTANT]
> 本文所述的範例步驟僅供指引參考。 根據整體環境的設定方式而定，您環境中的實際步驟可能稍有不同。 如需環境的特定設定、自訂及任何必要的疑難排解，請連絡您的系統和網域管理員。

## <a name="check-the-connection-to-a-domain-controller"></a>檢查網域控制站的連線

請確認您可以使用網域的簡短和完整名稱來與網域控制站連線：

```bash
ping contoso
ping contoso.com
```

> [!TIP]
> 本教學課程分別使用 **contoso.com** 和 **CONTOSO.COM** 作為範例網域和領域名稱。 它也會使用 **DC1.CONTOSO.COM** 作為網域控制站的完整網域名稱範例。 您必須以自有值來取代這些名稱。

如果其中一項名稱檢查失敗，請更新您的網域搜尋清單。 下列各節分別提供適用於 Ubuntu、Red Hat Enterprise Linux (RHEL) 和 SUSE Linux Enterprise Server (SLES) 的指示。

### <a name="ubuntu"></a>Ubuntu

1. 編輯 **/etc/network/interfaces** 檔案，以讓您的 Active Directory 網域位於網域搜尋清單中：

   ```/etc/network/interfaces
   # The primary network interface
   auto eth0
   iface eth0 inet dhcp
   dns-nameservers **<AD domain controller IP address>**
   dns-search **<AD domain name>**
   ```

   > [!NOTE]
   > 網路介面 `eth0` 可能會因不同電腦而有所不同。 若要找出您使用的是哪一個，請執行 **ifconfig**。 然後，複製具有 IP 位址並已傳送和接收位元組的介面。

1. 編輯此檔案之後，請重新啟動網路服務：

   ```bash
   sudo ifdown eth0 && sudo ifup eth0
   ```

1. 接下來，檢查 **/etc/resolv.conf** 檔案是否包含類似下列範例的程式碼行：

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

### <a name="rhel"></a>RHEL

1. 編輯 **/etc/sysconfig/network-scripts/ifcfg-eth0** 檔案，以讓您的 Active Directory 網域位於網域搜尋清單中。 或者，視需要編輯其他介面設定檔：

   ```/etc/sysconfig/network-scripts/ifcfg-eth0
   PEERDNS=no
   DNS1=**<AD domain controller IP address>**
   DOMAIN="contoso.com com"
   ```

1. 編輯此檔案之後，請重新啟動網路服務：

   ```bash
   sudo systemctl restart network
   ```

1. 現在，檢查 **/etc/resolv.conf** 檔案是否包含類似下列範例的程式碼行：

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

1. 如果您仍然無法 Ping 網域控制站，請尋找網域控制站的完整網域名稱和 IP 位址。 範例網域名稱為 **DC1.CONTOSO.COM**。 將下列項目新增至 **/etc/hosts**：

   ```/etc/hosts
   **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
   ```

### <a name="sles"></a>SLES

1. 編輯 **/etc/sysconfig/network/config** 檔案，以讓您的 Active Directory 網域控制站 IP 用於 DNS 查詢，且您的 Active Directory 網域位於網域搜尋清單中：

   ```/etc/sysconfig/network/config
   NETCONFIG_DNS_STATIC_SEARCHLIST=""
   NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
   ```

1. 編輯此檔案之後，請重新啟動網路服務：

   ```bash
   sudo systemctl restart network
   ```

1. 接下來，檢查 **/etc/resolv.conf** 檔案是否包含類似下列範例的程式碼行：

   ```/etc/resolv.conf
   search contoso.com com
   nameserver **<AD domain controller IP address>**
   ```

## <a name="join-to-the-ad-domain"></a>加入 AD 網域

在驗證網域控制站的基本設定和連線能力之後，您可以使用下列兩個選項來聯結 SQL Server Linux 主機電腦與 Active Directory 網域控制站：

- [選項 1：使用 SSSD 套件](#option1)
- [選項 2：使用協力廠商 OpenLDAP 提供者的公用程式](#option2)

### <a id="option1"></a> 選項 1：使用 SSSD 套件來加入 AD 網域

此方法會使用 **realmd** 和 **sssd** 套件，將 SQL Server 主機加入 AD 網域。

> [!NOTE]
> 這是將 Linux 主機加入 AD 網域控制站的慣用方法。

使用下列步驟，將 SQL Server 主機加入 Active Directory 網域：

1. 使用 [realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join)，將您的主機電腦加入 AD 網域。 您必須先使用 Linux 發行版本的套件管理員，在 SQL Server 主機電腦上安裝 **realmd** 和 Kerberos 用戶端套件：

   **RHEL：**

   ```base
   sudo yum install realmd krb5-workstation
   ```

   **SUSE：**

   ```bash
   sudo zypper install realmd krb5-client
   ```

   **Ubuntu:**

   ```bash
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. 如果 Kerberos 用戶端套件安裝提示您提供領域名稱，請以大寫輸入您的網域名稱。

1. 在您確認 DNS 設定無誤之後，請執行下列命令來加入網域。 您必須使用具有足夠 AD 權限的 AD 帳戶進行驗證，才能將新的電腦加入網域。 此命令會在 AD 中建立新的電腦帳戶、建立 **/etc/krb5.keytab** 主機 Keytab 檔、在 **/etc/sssd/sssd.conf** 中設定網域，以及更新 **/etc/krb5.conf**。

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   ```

   您應該會看到 `Successfully enrolled machine in realm` 此訊息。

   下表列出一些您可能會收到的錯誤訊息，以及解決這些錯誤的建議：

   | 錯誤訊息 | 建議 |
   |---|---|
   | `Necessary packages are not installed` | 請先使用 Linux 發行版本的套件管理員安裝這些套件，然後再次執行 realm join 命令。 |
   | `Insufficient permissions to join the domain` | 請連絡網域系統管理員，確認您有足夠權限可將 Linux 電腦加入您的網域。 |
   | `KDC reply did not match expectations` | 您可能未針對使用者指定正確的領域名稱。 領域名稱會區分大小寫；通常是大寫，且可以使用 realm discover contoso.com 命令來識別。 |

   SQL Server 會使用 SSSD 和 NSS，將使用者帳戶和群組對應至安全性識別碼 (SID)。 您必須設定並執行 SSSD，SQL Server 才能成功建立 AD 登入。 **realmd** 通常會在加入網域的過程中自動執行此動作，但在某些情況下，您必須另外進行此作業。

   如需詳細資訊，請參閱如何[手動設定 SSSD](https://access.redhat.com/articles/3023951) 和[設定 NSS 以使用 SSSD](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options)。

1. 確認您現在可以透過網域收集使用者的相關資訊，並取得該使用者的 Kerberos 票證。 下列範例會針對上述目的，使用 **id**、[kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html) 和 [klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html) 命令。

   ```bash
   id user@contoso.com

   uid=1348601103(user@contoso.com) gid=1348600513(domain group@contoso.com) groups=1348600513(domain group@contoso.com)

   kinit user@CONTOSO.COM

   Password for user@CONTOSO.COM:

   klist
   Ticket cache: FILE:/tmp/krb5cc_1000
   Default principal: user@CONTOSO.COM
   ```

   > [!NOTE]
   > - 如果**識別碼使用者\@contoso.com** 傳回 `No such user`，請執行 `sudo systemctl status sssd` 命令以確定成功啟動 SSSD 服務。 如果服務正在執行，但您仍然看到此錯誤，請嘗試啟用 SSSD 的詳細資訊記錄。 如需詳細資訊，請參閱 Red Hat 文件的 [Troubleshooting SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting) (針對 SSSD 進行疑難排解)。
   >
   > - 如果 **kinit 使用者\@CONTOSO.COM** 傳回 `KDC reply did not match expectations while getting initial credentials`，請確認您已指定大寫的領域。

如需詳細資訊，請參閱 Red Hat 文件的 [Discovering and Joining Identity Domains](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html) (探索及加入識別身分網域)。

### <a id="option2"></a> 選項 2：使用協力廠商 OpenLDAP 提供者的公用程式

您可以使用協力廠商公用程式，例如 [PBIS](https://www.beyondtrust.com/)、[VAS](https://www.oneidentity.com/products/authentication-services/) 或 [Centrify](https://www.centrify.com/)。 本文未涵蓋每個個別公用程式的步驟。 您必須先使用其中一個公用程式，將 SQL Server 的 Linux 主機加入網域，再繼續進行。  

SQL Server 不會使用協力廠商整合器的程式碼或程式庫來進行任何 AD 相關查詢。 SQL Server 一律會直接在此安裝程式中使用 OpenLDAP 程式庫呼叫來查詢 AD。 系統只會使用協力廠商整合器來將 Linux 主機加入 AD 網域，而 SQL Server 與這些公用程式沒有任何直接的通訊。

> [!IMPORTANT]
> 如需使用 **mssql-conf** `network.disablesssd` 設定選項的建議，請參閱[在 Linux 上搭配使用 Active Directory 驗證與 SQL Server](sql-server-linux-active-directory-authentication.md#additionalconfig) 一文的＜其他設定選項＞  一節。

確認您已正確設定 **/etc/krb5.conf**。 大多數協力廠商 Active Directory 提供者都會自動完成此設定。 不過，請檢查 **/etc/krb5.conf** 的下列值，以防止任何後續問題：

```/etc/krb5.conf
[libdefaults]
default_realm = CONTOSO.COM

[realms]
CONTOSO.COM = {
}

[domain_realm]
contoso.com = CONTOSO.COM
.contoso.com = CONTOSO.COM
```

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>檢查反向 DNS 是否已正確設定

下列命令應該會傳回 SQL Server 執行主機的完整網域名稱 (FQDN)。 例如 **SqlHost.contoso.com**。

```bash
host **<IP address of SQL Server host>**
```

此命令的輸出應該類似 `**<reversed IP address>**.in-addr.arpa domain name pointer SqlHost.contoso.com`。 如果此命令未傳回您主機的 FQDN，或 FQDN 不正確，請將 Linux 上的 SQL Server 主機反向 DNS 項目新增至您的 DNS 伺服器。

## <a name="next-steps"></a>後續步驟

本文涵蓋的必要條件說明如何在使用 Active Directory 驗證的 Linux 主機電腦上設定 SQL Server。 若要完成設定 Linux 上的 SQL Server 以支援 Active Directory 帳戶，請遵循[在 Linux 上搭配使用 Active Directory 驗證與 SQL Server](sql-server-linux-active-directory-authentication.md)中的指示。
