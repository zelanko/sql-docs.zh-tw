---
title: 使用 NTLM 驗證連接到 SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2019
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
ms.openlocfilehash: 11fe35e1dc90e32cac460b61fe8a6078c817b0ca
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68894100"
---
# <a name="using-ntlm-authentication-to-connect-to-sql-server"></a>使用 NTLM 驗證連接到 SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

允許應用程式使用 authenticationScheme 連接屬性來表示它想要使用 NTLM v2 驗證連接到資料庫。  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 

下列屬性也會用於 NTLM 驗證:

- **網域 = domainName**選擇性
- **user = userName**
- **password = password**
- **integratedSecurity = true**

除了**網域**以外, 其他屬性是強制性的, 當使用**NTLM** authenticationScheme 屬性時, 驅動程式將會擲回錯誤 (如果有的話)。 

如需連接屬性的詳細資訊, 請參閱[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。 如需 Microsoft NTLM 驗證通訊協定的詳細資訊, 請參閱[MICROSOFT ntlm](https://docs.microsoft.com/windows/desktop/SecAuthN/microsoft-ntlm)。

## <a name="remarks"></a>Remarks

如需 SQL server 設定的描述, 以控制 NTLM 驗證的行為, 請參閱[網路安全性: LAN Manager 驗證層級](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level)。 

## <a name="logging"></a>記錄

新增了新的記錄器以支援 Kerberos 驗證：com.microsoft.sqlserver.jdbc.internals.NTLMAuthentication。 如需詳細資訊，請參閱[追蹤驅動程式作業](../../connect/jdbc/tracing-driver-operation.md)。

## <a name="datasource"></a>DataSource

使用資料來源建立連接時, 可以使用**setAuthenticationScheme**、 **setDomain**和 (選擇性) **setServerSpn**以程式設計方式設定 NTLM 屬性。

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

## <a name="service-principal-names"></a>服務主要名稱

服務主要名稱 (SPN) 是用戶端用以唯一識別服務執行個體的名稱。

您可以使用 **serverSpn** 連線屬性指定 SPN，或直接讓驅動程式為您建置 (預設)。 此屬性的格式為："MSSQLSvc/fqdn:port\@REALM"，其中 fqdn 是完整網域名稱，port 是連接埠號碼，REALM 是以大寫字母表示的 SQL Server 領域。 這個屬性的領域部分是選擇性的, 因為預設領域與伺服器的領域相同。

例如, 您的 SPN 可能如下所示: 「MSSQLSvc/some-伺服器. zzz .com: 1433」

如需有關服務主要名稱 (SPN) 的詳細資訊，請參閱：

- [用戶端連接中的服務主要名稱 (SPN) 支援](https://docs.microsoft.com/sql/relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections?view=sql-server-2017)

> [!NOTE]  
> 只有 Microsoft JDBC Driver 4.2 以上 (含) 版本支援 serverSpn 連線屬性。

> 在6.2 版的 JDBC driver 之前, 您必須明確地設定**serverSpn**。 從6.2 版本中, 根據預設, 驅動程式將能夠建立**serverSpn** , 雖然一個也可以明確使用**serverSpn** 。

## <a name="security-risks"></a>安全性風險

NTLM 通訊協定是一種舊的驗證通訊協定, 具有各種弱點, 這會造成安全性風險。 它是以相對較弱的密碼編譯配置為基礎, 而且容易遭受各種攻擊。 它會以 Kerberos 取代, 這是更安全且建議的做法。 NTLM 驗證只應用於安全信任的環境中, 或在無法使用 Kerberos 時使用。

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]僅支援 NTLM v2, 其在原始 v1 通訊協定上有一些安全性增強功能。 It'ss 也建議啟用擴充保護, 或使用 SSL 加密來提高安全性。 

如需有關如何啟用擴充保護和的詳細資訊, 請參閱:

- [使用擴充保護連接至 Database Engine](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)

如需使用 SSL 加密進行連接的詳細資訊, 請參閱:

- [使用 SSL 加密連接](../../connect/jdbc/connecting-with-ssl-encryption.md)

> [!NOTE]
> 在7.4 版本中, 不支援**同時**啟用擴充保護和加密。

## <a name="see-also"></a>另請參閱

[使用 JDBC Driver 連接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
