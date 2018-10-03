---
title: 使用 Linux 上的 SQL Server 中的第三方 Active Directory 提供者 |Microsoft Docs
description: 本教學課程提供與協力廠商提供者的 AD 驗證的設定步驟
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
ms.openlocfilehash: beb342156098ebb5516466ad7fd4a771cc5a0616
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787283"
---
# <a name="use-third-party-active-directory-providers-with-sql-server-on-linux"></a>使用 Linux 上的 SQL Server 中的第三方 Active Directory 提供者

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章說明如何設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Linux 主機上使用 AD 驗證時使用第三方 AD 提供者，例如[PowerBroker 身分識別服務 (PBI)](https://www.beyondtrust.com/)， [Vintela 驗證服務 (VAS)](https://www.oneidentity.com/products/authentication-services/)，並[Centrify](https://www.centrify.com/)。 本指南包含的步驟，以檢查您的 AD 組態，它不要說明如何將機器加入網域。 如需詳細指示，來聯結[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]主控件，使用領域和 SSSD 的網域，請參閱 <<c2> [ 與 Linux 上的 SQL Server 使用 Active Directory 驗證](sql-server-linux-active-directory-authentication.md)。

## <a name="prerequisites"></a>先決條件

設定 AD 驗證之前，您需要設定 AD 網域控制站 (Windows) 上您的網路和聯結您[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]AD 網域的 Linux 主機上。 您可以使用[PBI](https://www.beyondtrust.com/)， [VAS](https://www.oneidentity.com/products/authentication-services/)，或[Centrify](https://www.centrify.com/)。

> [!NOTE]
>
>本教學課程使用"contoso.com"和"CONTOSO.COM"做為範例的網域和領域的名稱分別。 它也會使用 「 DC1。CONTOSO.COM"做為範例的完整的網域名稱，網域控制站。 您應該將它們替換為您自己的值。

## <a name="check-connection-to-domain-controller"></a>請檢查網域控制站的連線

您可以連絡與網域的簡短和完整格式名稱的網域控制站檢查。

   ```bash
   ping contoso

   ping contoso.com
   ```

   如果任一種失敗時，更新您的網域搜尋清單。

   - **Ubuntu**:

     編輯`/etc/network/interfaces`檔案，讓您的 AD 網域是網域的 [搜尋] 清單中： 

     ```/etc/network/interfaces
     <...>
     # The primary network interface
     auto eth0
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

     現在請檢查您`/etc/resolv.conf`檔案包含一條線，如下列範例所示：  

     ```/etc/resolv.conf
     search contoso.com com  
     nameserver **<AD domain controller IP address>**
     ```

   - **RHEL**:

     編輯`/etc/sysconfig/network-scripts/ifcfg-eth0`檔案 （或其他檔案為適當的介面組態），因此您的 AD 網域是網域的 [搜尋] 清單中：

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

   如果您仍然無法 ping 網域控制站，尋找完整的網域名稱 (例如 DC1。CONTOSO.COM) 和網域控制站的 IP 位址，並新增下列項目 `/etc/hosts`

   ```/etc/hosts
   **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
   ```

   - **SLES**:

     編輯`/etc/sysconfig/network/config`檔案，以便您 AD 網域控制站 IP 將用於 DNS 查詢和您的 AD 網域是網域的 [搜尋] 清單中：

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

## <a name="check-reverse-dns-is-properly-configured"></a>檢查已正確設定反向 DNS

下列命令應該會傳回主應用程式 （例如執行 SQL Server 的完整的網域名稱「 SqlHost.contoso.com")。

   ```bash
   host **<IP address of SQL Server host>**
   # **<reversed IP address>**.in-addr.arpa domain name pointerSqlHost.contoso.com.
   ```

   如果這不會傳回您主機的 FQDN，或如果 FQDN 不正確，請將反向 DNS 項目您[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]到您的 DNS 伺服器的 Linux 主機上。

## <a name="check-your-krb5-configuration-is-correct"></a>請檢查您 KRB5 組態正確

請檢查您`/etc/krb5.conf`已正確設定。 對於大部分的協力廠商 AD 提供者，這會自動完成。 不過，檢查`/etc/krb5.conf`如下列的值，以避免未來發生任何問題：

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

在本文中，我們涵蓋了如何設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Linux 主機上使用 AD 驗證時使用第三方 AD 提供者。 若要完成設定[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]在 Linux 上支援 AD 帳戶，請遵循指示[與 Linux 上的 SQL Server 使用 Active Directory 驗證](sql-server-linux-active-directory-authentication.md)。

> [!div class="nextstepaction"]
> [使用 Linux 上的 SQL Server 的 Active Directory 驗證](sql-server-linux-active-directory-authentication.md)

> [!NOTE]
>
> 您可以略過的 「 AD 網域聯結的 SQL Server 主機 」 一節[在 Linux 上的 SQL server 使用 Active Directory 驗證](sql-server-linux-active-directory-authentication.md)如所完成，在本教學課程。
