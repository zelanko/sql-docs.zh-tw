---
title: 使用 Linux 上的 SQL Server 中的第三方 Active Directory 提供者 |Microsoft Docs
description: 本教學課程提供與協力廠商提供者的 Active Directory 驗證的設定步驟
author: dylan-MSFT
ms.date: 07/25/2018
ms.author: dygray
manager: mikehab
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
helpviewer_keywords:
- Linux, AD authentication
ms.openlocfilehash: 0ffe146de3a842f9c273b4dbba2a9fe4d9ff7ff5
ms.sourcegitcommit: 41979c9d511b3eeb45134d30ccb0dbc6bba70f1a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/01/2018
ms.locfileid: "50757993"
---
# <a name="use-third-party-active-directory-providers-with-sql-server-on-linux"></a>使用 Linux 上的 SQL Server 中的第三方 Active Directory 提供者

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章說明如何設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Linux 主機上使用 Active Directory 驗證時使用協力廠商 Active Directory 提供者。 範例包括[PowerBroker 身分識別服務 (PBI)](https://www.beyondtrust.com/)，[一個身分識別](https://www.oneidentity.com/products/authentication-services/)，並[Centrify](https://www.centrify.com/)。 本指南包含要檢查您的 Active Directory 設定的步驟。 它已不打算指示如何將機器加入網域。 如需詳細指示，來聯結[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]藉由使用 realmd 和 SSSD 裝載網域，請參閱 <<c2> [ 與 Linux 上的 SQL Server 使用 Active Directory 驗證](sql-server-linux-active-directory-authentication.md)。

## <a name="prerequisites"></a>先決條件

設定 Active Directory 驗證之前，您需要設定一個 Active Directory 網域控制站，Windows，您的網路。 然後加入您[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Active Directory 網域的 Linux 主機上。 您可以使用[PBI](https://www.beyondtrust.com/)， [VAS](https://www.oneidentity.com/products/authentication-services/)，或[Centrify](https://www.centrify.com/)。

> [!NOTE]
>
>本教學課程會使用**`contoso.com`** 並**`CONTOSO.COM`** 做為範例網域和領域名稱，分別。 它也會使用**`DC1.CONTOSO.COM`** 如範例完整的網域控制站的網域名稱。 您應該使用您自己的值來取代這些名稱。

## <a name="check-the-connection-to-a-domain-controller"></a>請檢查網域控制站的連線

您可以連絡與網域的簡短和完整格式名稱的網域控制站的檢查：

```bash
ping contoso

ping contoso.com
```

如果任一項名稱檢查失敗時，更新您的網域搜尋清單：

- **Ubuntu**

  編輯`/etc/network/interfaces`檔案，以便您的 Active Directory 網域是網域的 [搜尋] 清單中： 

  ```/etc/network/interfaces
  <...>
  # The primary network interface
  auto eth0
  iface eth0 inet dhcp
  dns-nameservers **<AD domain controller IP address>**
  dns-search **<AD domain name>**
  ```

  > [!NOTE]  
  > 網路介面**eth0**，針對不同的機器可能會不同。 若要了解您使用哪一個，執行**ifconfig**。 然後複製所具有的 IP 位址和傳輸和接收的位元組的介面。

  在編輯這個檔案之後, 重新啟動網路服務：

  ```bash
  sudo ifdown eth0 && sudo ifup eth0
  ```

  現在請檢查您`/etc/resolv.conf`檔案包含一條線，如下列範例所示：  

  ```/etc/resolv.conf
  search contoso.com com  
  nameserver **<AD domain controller IP address>**
  ```

- **RHEL**

  編輯`/etc/sysconfig/network-scripts/ifcfg-eth0`檔案，以便您的 Active Directory 網域是網域的 [搜尋] 清單中。 或編輯另一個適當的介面組態檔：

  ```/etc/sysconfig/network-scripts/ifcfg-eth0
  <...>
  PEERDNS=no
  DNS1=**<AD domain controller IP address>**
  DOMAIN="contoso.com com"
  ```

  在編輯這個檔案之後, 重新啟動網路服務：

  ```bash
  sudo systemctl restart network
  ```

  現在請檢查您`/etc/resolv.conf`檔案包含一條線，如下列範例所示：  

  ```/etc/resolv.conf
  search contoso.com com  
  nameserver **<AD domain controller IP address>**
  ```

  如果您仍然無法 ping 網域控制站，尋找網域控制站的 IP 位址與完整的網域名稱。 範例的網域名稱是`DC1.CONTOSO.COM`。 新增下列項目以`/etc/hosts`:

  ```/etc/hosts
  **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
  ```

- **SLES**

  編輯`/etc/sysconfig/network/config`檔案，以便您的 Active Directory 網域控制站 IP 用於 DNS 查詢，而且您的 Active Directory 網域是網域的 [搜尋] 清單中：

  ```/etc/sysconfig/network/config
  <...>
  NETCONFIG_DNS_STATIC_SEARCHLIST=""
  NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
  ```

  在編輯這個檔案之後, 重新啟動網路服務：

  ```bash
  sudo systemctl restart network
  ```

  現在請檢查您`/etc/resolv.conf`檔案包含一條線，如下列範例所示：

  ```/etc/resolv.conf
  search contoso.com com
  nameserver **<AD domain controller IP address>**
  ```

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>反向 DNS 已正確設定的核取

下列命令應該會傳回執行 SQL Server 的主機的完整的網域名稱。 例如， **`SqlHost.contoso.com`**。

```bash
host **<IP address of SQL Server host>**
# **<reversed IP address>**.in-addr.arpa domain name pointerSqlHost.contoso.com.
```

如果此命令不會傳回您主機的 FQDN，或如果 FQDN 不正確，請為您新增的反向 DNS 項目[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到您的 DNS 伺服器的 Linux 主機上。

## <a name="check-that-your-krb5-configuration-is-correct"></a>請檢查您 KRB5 組態正確

請檢查您`/etc/krb5.conf`已正確設定。 對於大部分的協力廠商 Active Directory 提供者，此設定會自動完成。 不過，檢查`/etc/krb5.conf`如下列的值，以避免未來發生任何問題：

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

## <a name="next-steps"></a>後續步驟

這篇文章說明如何設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Linux 主機上使用 Active Directory 驗證時使用協力廠商 Active Directory 提供者。 若要完成設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Linux 上支援 Active Directory 帳戶，請遵循指示[與 Linux 上的 SQL Server 使用 Active Directory 驗證](sql-server-linux-active-directory-authentication.md)。

> [!div class="nextstepaction"]
> [使用 Linux 上的 SQL Server 的 Active Directory 驗證](sql-server-linux-active-directory-authentication.md)

> [!NOTE]
>
> 您可以略過**Active Directory 網域加入 SQL Server 主機**一節中[與 Linux 上的 SQL Server 使用 Active Directory 驗證](sql-server-linux-active-directory-authentication.md)如您剛才所完成，在本教學課程。
