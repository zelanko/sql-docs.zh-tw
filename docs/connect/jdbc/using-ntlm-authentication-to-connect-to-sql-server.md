---
title: 使用 NTLM 驗證連線到 SQL Server
description: 了解如何搭配 JDBC 驅動程式使用 NTLM 驗證來建立 SQL 資料庫連線。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: lilgreenbird
ms.author: v-susanh
manager: kenvh
ms.openlocfilehash: ed1e16aac4de3277906d00c2b1a0f4458418cc95
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081767"
---
# <a name="using-ntlm-authentication-to-connect-to-sql-server"></a>使用 NTLM 驗證連線到 SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

允許 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 應用程式使用 **authenticationScheme** 連接屬性來指定要使用 NTLM v2 驗證連線至資料庫。 

下列屬性也用於 NTLM 驗證：

- **domain = domainName** (選擇性)
- **user = userName**
- **password = password**
- **integratedSecurity = true**

除了 **domain** 之外，其他屬性是必要的，如果使用 **NTLM** authenticationScheme 屬性時缺少任一個屬性，驅動程式將會擲回錯誤。 

如需連接屬性的詳細資訊，請參閱[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。 如需 Microsoft NTLM 驗證通訊協定的詳細資訊，請參閱 [Microsoft NTLM](/windows/desktop/SecAuthN/microsoft-ntlm) \(英文\)。

## <a name="remarks"></a>備註

請參閱[網路安全性：LAN Manager 驗證等級](/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level) \(部分機器翻譯\)，以取得 SQL 伺服器設定 (控制 NTLM 驗證行為) 的描述。 

## <a name="logging"></a>記錄

新增了新的記錄器以支援 Kerberos 驗證：com.microsoft.sqlserver.jdbc.internals.NTLMAuthentication。 如需詳細資訊，請參閱[追蹤驅動程式作業](../../connect/jdbc/tracing-driver-operation.md)。

## <a name="datasource"></a>DataSource

使用資料來源建立連線時，可以使用 **setAuthenticationScheme**、**setDomain** 和 (選擇性) **setServerSpn**，以程式設計方式設定 NTLM 屬性。

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(1433); // change if necessary
ds.setIntegratedSecurity(true);
ds.setAuthenticationScheme("NTLM");
ds.setDomain("<domainName>");
ds.setUser("<userName>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setServerSpn("<serverSpn");

try (Connection c = ds.getConnection(); Statement s = c.createStatement();
        ResultSet rs = s.executeQuery("select auth_scheme from sys.dm_exec_connections where session_id=@@spid")) {
    while (rs.next()) {
        System.out.println("Authentication Scheme: " + rs.getString(1));
    }
}
```

## <a name="service-principal-names"></a>服務主體名稱

服務主要名稱 (SPN) 是用戶端用以唯一識別服務執行個體的名稱。

您可以使用 **serverSpn** 連線屬性指定 SPN，或直接讓驅動程式為您建置 (預設)。 此屬性的格式為："MSSQLSvc/fqdn:port\@REALM"，其中 fqdn 是完整網域名稱，port 是連接埠號碼，REALM 是以大寫字母表示的 SQL Server 領域。 這個屬性的領域部分是選擇性的，因為預設領域與伺服器的領域相同。

例如，您的 SPN 可能看起來如下："MSSQLSvc/some-server.zzz.corp.contoso.com:1433"

如需有關服務主要名稱 (SPN) 的詳細資訊，請參閱：

- [用戶端連接中的服務主要名稱 (SPN) 支援](../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)

> [!NOTE]  
> 只有 Microsoft JDBC Driver 4.2 以上 (含) 版本支援 serverSpn 連線屬性。

> 在 JDBC 驅動程式 6.2 版之前，您必須明確地設定 **serverSpn**。 從 6.2 版本開始，驅動程式預設將能夠建置 **serverSpn**，不過，您也可以明確地使用 **serverSpn**。

## <a name="security-risks"></a>安全性風險

NTLM 通訊協定是舊的驗證通訊協定，具有各種弱點，因此會造成安全性風險。 其是以相對較弱的密碼編譯配置為基礎，而且容易遭受各種攻擊。 其會以 Kerberos 取代，這是更安全且建議的做法。 NTLM 驗證只應用於安全信任的環境中，或在無法使用 Kerberos 時使用。

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 只支援 NTLM v2，其在原始 v1 通訊協定上有一些安全性增強功能。 也建議您啟用擴充保護，或使用 SSL 加密來提高安全性。 

如需如何啟用擴充保護的詳細資訊，請參閱：

- [使用擴充保護連接至 Database Engine](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)

如需使用 SSL 加密進行連線的詳細資訊，請參閱：

- [使用 SSL 加密連線](../../connect/jdbc/connecting-with-ssl-encryption.md)

> [!NOTE]
> 7\.4 版不支援**同時**啟用擴充保護和加密。

## <a name="see-also"></a>另請參閱

[使用 JDBC 驅動程式連線到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)