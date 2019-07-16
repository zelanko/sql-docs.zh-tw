---
title: 加入至 Active Directory 的 Linux 上的 SQL Server
titleSuffix: SQL Server
description: ''
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.date: 04/01/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: d5cd6356f4bc691518f11e1e6fb00add527cc595
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027337"
---
# <a name="join-sql-server-on-a-linux-host-to-an-active-directory-domain"></a>加入 Active Directory 網域的 Linux 主機上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章提供有關如何將 SQL Server Linux 主機電腦加入 Active Directory (AD) 網域的一般指引。 有兩種方法： 使用內建的 SSSD 封裝，或使用協力廠商 Active Directory 提供者。 第三方網域聯結產品的範例包括[PowerBroker 身分識別服務 (PBI)](https://www.beyondtrust.com/)，[一個身分識別](https://www.oneidentity.com/products/authentication-services/)，並[Centrify](https://www.centrify.com/)。 本指南包含要檢查您的 Active Directory 設定的步驟。 不過，它並不打算提供有關如何使用協力廠商公用程式時，將機器加入網域的指示。

## <a name="prerequisites"></a>必要條件

設定 Active Directory 驗證之前，您需要設定一個 Active Directory 網域控制站，Windows，您的網路。 然後，加入您的 SQL Server 的 Active Directory 網域的 Linux 主機上。

> [!IMPORTANT]
> 這篇文章中所述的範例步驟適用於只使用指導方針。 實際步驟可能會在您的環境，根據您的整體環境的設定方式稍有不同的。 請連絡您的系統和網域系統管理員為您的環境的特定組態、 自訂和任何必要的疑難排解。

## <a name="check-the-connection-to-a-domain-controller"></a>請檢查網域控制站的連線

您可以連絡與網域的簡短和完整格式名稱的網域控制站的檢查：

```bash
ping contoso
ping contoso.com
```

> [!TIP]
> 本教學課程會使用**contoso.com**並**CONTOSO.COM**做為範例網域和領域名稱，分別。 它也會使用**DC1。CONTOSO.COM**如範例完整的網域控制站的網域名稱。 您必須以您自己的值來取代這些名稱。

如果任一項名稱檢查失敗時，更新您的網域搜尋清單。 下列各節分別提供適用於 Ubuntu、 Red Hat Enterprise Linux (RHEL) 及 SUSE Linux Enterprise Server (SLES) 的指示。

### <a name="ubuntu"></a>Ubuntu

1. 編輯 **/etc/network/interfaces**檔案，以便您的 Active Directory 網域是網域的 [搜尋] 清單中：

   ```/etc/network/interfaces
   # The primary network interface
   auto eth0
   iface eth0 inet dhcp
   dns-nameservers **<AD domain controller IP address>**
   dns-search **<AD domain name>**
   ```

   > [!NOTE]
   > 網路介面， `eth0`，針對不同的機器可能會不同。 若要了解您使用哪一個，執行**ifconfig**。 然後複製所具有的 IP 位址和傳輸和接收的位元組的介面。

1. 在編輯這個檔案之後, 重新啟動網路服務：

   ```bash
   sudo ifdown eth0 && sudo ifup eth0
   ```

1. 接下來，請檢查您 **/etc/resolv.conf**檔案包含一行，如下列範例所示：

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

### <a name="rhel"></a>RHEL

1. 編輯 **/etc/sysconfig/network-scripts/ifcfg-eth0**檔案，以便您的 Active Directory 網域是網域的 [搜尋] 清單中。 或編輯另一個適當的介面組態檔：

   ```/etc/sysconfig/network-scripts/ifcfg-eth0
   PEERDNS=no
   DNS1=**<AD domain controller IP address>**
   DOMAIN="contoso.com com"
   ```

1. 在編輯這個檔案之後, 重新啟動網路服務：

   ```bash
   sudo systemctl restart network
   ```

1. 現在，請確認您 **/etc/resolv.conf**檔案包含一行，如下列範例所示：

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

1. 如果您仍然無法 ping 網域控制站，尋找網域控制站的 IP 位址與完整的網域名稱。 範例的網域名稱是**DC1。CONTOSO.COM**。 新增下列項目，以**eg /etc/ 主機**:

   ```/etc/hosts
   **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
   ```

### <a name="sles"></a>SLES

1. 編輯 **/etc/sysconfig/network/config**檔案，以便您的 Active Directory 網域控制站 IP 用於 DNS 查詢，而且您的 Active Directory 網域是網域的 [搜尋] 清單中：

   ```/etc/sysconfig/network/config
   NETCONFIG_DNS_STATIC_SEARCHLIST=""
   NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
   ```

1. 在編輯這個檔案之後, 重新啟動網路服務：

   ```bash
   sudo systemctl restart network
   ```

1. 接下來，請檢查您 **/etc/resolv.conf**檔案包含一行，如下列範例所示：

   ```/etc/resolv.conf
   search contoso.com com
   nameserver **<AD domain controller IP address>**
   ```

## <a name="join-to-the-ad-domain"></a>加入 AD 網域

在基本組態和網域控制站的連線通過驗證之後，有兩個聯結與 Active Directory 網域控制站的 SQL Server Linux 主機電腦的選項：

- [選項 1:使用 SSSD 封裝](#option1)
- [選項 2:使用第三方 openldap 提供者公用程式](#option2)

### <a id="option1"></a> 選項 1:若要加入 AD 網域使用 SSSD 封裝

這個方法會加入 AD 網域使用的 SQL Server 主機**realmd**並**sssd**封裝。

> [!NOTE]
> 這是加入 AD 網域控制站的 Linux 主機的慣用的方法。

若要加入至 Active Directory 網域的 SQL Server 主機使用下列步驟：

1. 使用[realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join)主機電腦加入 AD 網域。 您必須先安裝兩者**realmd**和 SQL Server 主機上使用您的 Linux 散發套件管理員的 Kerberos 用戶端套件：

   **RHEL:**

   ```base
   sudo yum install realmd krb5-workstation
   ```

   **SUSE:**

   ```bash
   sudo zypper install realmd krb5-client
   ```

   **Ubuntu:**

   ```bash
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

1. 如果 Kerberos 的用戶端封裝安裝將會提示您輸入領域名稱，請以大寫輸入您的網域名稱。

1. 確認已正確設定您的 DNS 之後，請執行下列命令來加入網域。 您必須使用具有足夠的權限，AD 以新的電腦加入網域中的 AD 帳戶進行驗證。 此命令會在 AD 中建立新的電腦帳戶，會建立 **/etc/krb5.keytab**裝載 keytab 檔案、 設定中的網域 **/etc/sssd/sssd.conf**，並更新 **/etc/krb5.conf**.

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   ```

   您應該會看到訊息， `Successfully enrolled machine in realm`。

   下表列出一些您可能會收到的錯誤訊息和解決問題的建議：

   | 錯誤訊息 | 建議 |
   |---|---|
   | `Necessary packages are not installed` | 安裝這些套件使用您的 Linux 散發套件管理員，才能再次執行領域的聯結命令。 |
   | `Insufficient permissions to join the domain` | 使用網域系統管理員檢查您有足夠的權限加入您的網域中的 Linux 機器。 |
   | `KDC reply did not match expectations` | 您可能未指定使用者的正確領域名稱。 領域名稱會區分大小寫，則通常是大寫，和可以識別與命令領域探索 contoso.com。 |

   SQL Server 會使用 SSSD 和 NSS 對應使用者帳戶和群組安全性識別元 (Sid)。 SSSD 必須設定並執行 SQL Server 已成功建立 AD 登入。 **realmd**平常這會自動在加入網域，但在某些情況下，您必須分別執行此動作。

   如需詳細資訊，請參閱如何[手動設定 SSSD](https://access.redhat.com/articles/3023951)，並[設定來使用 SSSD NSS](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options)。

1. 請確認您現在可以收集使用者資訊從網域，而且您可以取得 Kerberos 票證，以該使用者。 下列範例會使用**識別碼**， [kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)，並[klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html)這個命令。

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
   > - 如果**識別碼user@contoso.com** 會傳回`No such user`，請確定已成功啟動 SSSD 服務： 執行命令`sudo systemctl status sssd`。 如果服務正在執行，而且您仍然看到錯誤，請嘗試啟用 SSSD 的詳細資訊記錄。 如需詳細資訊，請參閱 Red Hat 文件[疑難排解 SSSD](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting)。
   >
   > - 如果**kinit user@CONTOSO.COM** 會傳回`KDC reply did not match expectations while getting initial credentials`，請確定您以大寫指定領域。

如需詳細資訊，請參閱 Red Hat 文件[發掘並加入身分識別網域](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html)。

### <a id="option2"></a> 選項 2:使用第三方 openldap 提供者公用程式

您可以使用協力廠商公用程式，例如[PBI](https://www.beyondtrust.com/)， [VAS](https://www.oneidentity.com/products/authentication-services/)，或[Centrify](https://www.centrify.com/)。 這篇文章並未涵蓋每個個別的公用程式的步驟。 您必須先使用其中一個公用程式來加入網域中的 SQL Server 的 Linux 主機，然後再繼續往前。  

SQL Server 不使用協力廠商整合器程式碼或程式庫的任何 AD 相關的查詢。 SQL Server alwayson 會查詢 AD 直接在此安裝程式中使用 openldap 程式庫呼叫。 第三方整合者只會用來將 Linux 主機加入 AD 網域和 SQL Server 並沒有任何直接的通訊，使用這些公用程式。

> [!IMPORTANT]
> 使用的建議，請參閱**mssql conf** `network.disablesssd`中的組態選項**其他組態選項**一節的發行項[使用作用中Linux 上的 SQL Server 的目錄驗證](sql-server-linux-active-directory-authentication.md#additionalconfig)。

確認您 **/etc/krb5.conf**已正確設定。 對於大部分的協力廠商 Active Directory 提供者，此設定會自動完成。 不過，檢查 **/etc/krb5.conf**如下列的值，以避免未來發生任何問題：

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

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>反向 DNS 已正確設定的核取

下列命令應該傳回完整的網域名稱 (FQDN) 的主控件執行 SQL Server。 例如， **SqlHost.contoso.com**。

```bash
host **<IP address of SQL Server host>**
```

此命令的輸出應該會類似`**<reversed IP address>**.in-addr.arpa domain name pointer SqlHost.contoso.com`。 如果此命令不會傳回您主機的 FQDN，或如果 FQDN 不正確，加入您的 SQL Server，您的 DNS 伺服器的 Linux 主機上反向的 DNS 項目。

## <a name="next-steps"></a>後續步驟

本文涵蓋如何使用 Active Directory 驗證 Linux 主機機器上設定 SQL Server 的必要條件。 若要完成設定 Active Directory 帳戶，才能在 Linux 上的 SQL Server，請遵循指示[在 Linux 上的 SQL server 使用 Active Directory 驗證](sql-server-linux-active-directory-authentication.md)。