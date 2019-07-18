---
title: 使用 Kerberos 整合驗證連線至 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 687802dc-042a-4363-89aa-741685d165b3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 89c87ecb551e3e75397bc431bdefc47fad18f8d2
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798601"
---
# <a name="using-kerberos-integrated-authentication-to-connect-to-sql-server"></a>使用 Kerberos 整合式驗證連接到 SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

從 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 開始，應用程式可使用 **authenticationScheme** 連線屬性來指定要使用類型 4 Kerberos 整合驗證連線至資料庫。 請參閱[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)如需有關連接屬性。 如需有關 Kerberos 的詳細資訊，請參閱 < [Microsoft Kerberos](https://go.microsoft.com/fwlink/?LinkID=100758)。

當您搭配 Java **Krb5LoginModule** 使用整合驗證時，可使用 [Class Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html) (類別 Krb5LoginModule) 設定模組。

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會為 IBM Java VM 設定下列屬性：

- **useDefaultCcache = true**
- **moduleBanner = false**

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 會為其他所有 Java VM 設定下列屬性：

- **useTicketCache = true**
- **doNotPrompt = true**

## <a name="remarks"></a>Remarks

之前[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]，應用程式可以指定整合式的驗證 （使用 Kerberos 或 NTLM，取決於所提供） 使用**integratedSecurity**連接屬性及參考**sqljdbc_auth.dll**中所述[Building the Connection URL](../../connect/jdbc/building-the-connection-url.md)。

從 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 開始，應用程式可使用 **authenticationScheme** 連線屬性來指定透過純 Java Kerberos 實作使用 Kerberos 整合驗證連線到資料庫：

- 如果您想要使用整合式的驗證**Krb5LoginModule**，您仍然必須指定**integratedSecurity = true**連接屬性。 您再也會指定**authenticationScheme = JavaKerberos**連接屬性。

- 若要繼續使用整合式的驗證搭配**sqljdbc_auth.dll**，只需指定**integratedSecurity = true**連接屬性 (並選擇性地**authenticationScheme =NativeAuthentication**)。

- 如果您指定**authenticationScheme = JavaKerberos**也未指定，但**integratedSecurity = true**，則驅動程式將會忽略**authenticationScheme**連接屬性，而且它會預期的連接字串中找到使用者名稱和密碼認證。

當使用資料來源建立連線時，您可以透過程式設計的方式，使用 **setAuthenticationScheme** 設定驗證配置，並 (選擇性) 使用 **setServerSpn** 為 Kerberos 連線設定 SPN。

已加入新的記錄器來支援 Kerberos 驗證：com.microsoft.sqlserver.jdbc.internals.KerbAuthentication。 如需詳細資訊，請參閱[追蹤驅動程式作業](../../connect/jdbc/tracing-driver-operation.md)。

以下指導方針可幫助您設定 Kerberos：

1. 設定**AllowTgtSessionKey**為 1 的 Windows 登錄中。 如需詳細資訊，請參閱 [Windows Server 2003 中的 Kerberos 通訊協定登錄項目與 KDC 設定金鑰](https://support.microsoft.com/kb/837361)。
2. 確定 Kerberos 組態 (UNIX 環境中的 krb5.conf) 指向您的環境所適用的正確領域和 KDC。
3. 使用 kinit 或登入網域來初始化 TGT 快取。
4. 當使用 **authenticationScheme=JavaKerberos** 的應用程式在 Windows Vista 或 Windows 7 作業系統上執行時，您應使用標準使用者帳戶。 但您若是在系統管理員帳戶下執行應用程式，該應用程式就必須以系統管理員的權限執行。

> [!NOTE]  
> 只有 Microsoft JDBC Driver 4.2 以上 (含) 版本支援 serverSpn 連線屬性。

## <a name="service-principal-names"></a>服務主要名稱

服務主要名稱 (SPN) 是用戶端用以唯一識別服務執行個體的名稱。

您可以使用 **serverSpn** 連線屬性指定 SPN，或直接讓驅動程式為您建置 (預設)。 此屬性的格式為："MSSQLSvc/fqdn:port\@REALM"，其中 fqdn 是完整網域名稱，port 是連接埠號碼，REALM 是以大寫字母表示的 SQL Server Kerberos 領域。 此選項的 REALM 部分並非必要，只在您 Kerberos 設定的預設領域與伺服器的領域相同，而且預設不會加入時才需要。 如果您想要支援跨領域驗證案例，且其中 Kerberos 設定中的預設領域和伺服器的領域不同，則您必須以 serverSpn 屬性設定 SPN。

例如，您的 SPN 可能看起來像:"MSSQLSvc/some-server.zzz.corp.contoso.com:1433\@ZZZZ。CORP.CONTOSO.COM"

如需有關服務主要名稱 (SPN) 的詳細資訊，請參閱：

- [如何在 SQL Server 中使用 Kerberos 驗證](https://support.microsoft.com/kb/319723)

- [搭配 SQL Server 使用 Kerberos](https://go.microsoft.com/fwlink/?LinkId=207814)

> [!NOTE]  
> 6\.2 版 JDBC 驅動程式的跨領域 Kerberos，正確地使用之前，您就必須明確設定**serverSpn**。
>
> 6\.2 從版開始，此驅動程式將能夠建置**serverSpn**根據預設，即使是使用跨領域 Kerberos。 雖然您可以使用**serverSpn**明確太。

## <a name="creating-a-login-module-configuration-file"></a>建立登入模組組態檔

您可以選擇指定 Kerberos 組態檔。 如果未指定組態檔，以下設定便有效：

Sun JVM  
 com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;

IBM JVM  
 com.ibm.security.auth.module.Krb5LoginModule required useDefaultCcache = true;

如果您決定建立登入模組組態檔，此檔案必須遵循以下格式：

```java
<name> {  
    <LoginModule> <flag> <LoginModule options>;  
    <optional_additional_LoginModules, flags_and_options>;  
};  
```

登入組態檔是由一個或多個項目組成，每一個項目都會指定哪一個基礎驗證技術應該用於特定應用程式。 例如，

```java
SQLJDBCDriver {  
   com.sun.security.auth.module.Krb5LoginModule required useTicketCache=true;  
};  
```

所以每一個登入模組組態檔項目都是由一個名稱以及緊接在後的一個或多個 LoginModule-specific 項目所組成，其中每一個 LoginModule-specific 項目都是以分號結尾，而且整組 LoginModule-specific 項目會括在大括號中。 每一個組態檔項目都是以分號結尾。

除了允許驅動程式使用登入模組組態檔中指定的設定來取得 Kerberos 認證以外，驅動程式也可以使用現有的認證。 當您的應用程式必須使用多份使用者認證建立連線時即可使用。

驅動程式會嘗試使用現有的認證 (如果可用的話)，然後再嘗試使用指定的登入模組進行登入。 因此，當使用 `Subject.doAs` 方法在特定內容下執行程式碼時，將會使用傳遞給 `Subject.doAs` 呼叫的認證來建立連線。

如需詳細資訊，請參閱 [JAAS 登入組態檔](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/LoginConfigFile.html)和 [Class Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html) (類別 Krb5LoginModule)。

從 Microsoft JDBC Driver 6.2 中，登入模組組態檔的名稱可以選擇性地傳遞使用連接屬性`jaasConfigurationName`，這可讓每個連線有它自己的登入設定。

## <a name="creating-a-kerberos-configuration-file"></a>建立 Kerberos 組態檔

如需 Kerberos 組態檔的詳細資訊，請參閱 [Kerberos 需求](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html)。

這是網域設定檔範例，其中 YYYY 與 ZZZZ 是網域名稱。

```ini
[libdefaults]  
default_realm = YYYY.CORP.CONTOSO.COM  
dns_lookup_realm = false  
dns_lookup_kdc = true  
ticket_lifetime = 24h  
forwardable = yes  

[domain_realm]  
.yyyy.corp.contoso.com = YYYY.CORP.CONTOSO.COM  
.zzzz.corp.contoso.com = ZZZZ.CORP.CONTOSO.COM  

[realms]  
        YYYY.CORP.CONTOSO.COM = {  
  kdc = krbtgt/YYYY.CORP. CONTOSO.COM @ YYYY.CORP. CONTOSO.COM  
  default_domain = YYYY.CORP. CONTOSO.COM  
}  

        ZZZZ.CORP. CONTOSO.COM = {  
  kdc = krbtgt/ZZZZ.CORP. CONTOSO.COM @ ZZZZ.CORP. CONTOSO.COM  
  default_domain = ZZZZ.CORP. CONTOSO.COM  
}  

```

## <a name="enabling-the-domain-configuration-file-and-the-login-module-configuration-file"></a>啟用網域組態檔和登入模組組態檔

您可以使用 Djava.security.krb5.conf 來啟用網域組態檔。 您可以讓使用登入模組組態檔 **-Djava.security.auth.login.config**。

例如，下列命令可用來啟動應用程式：

```bash
Java.exe -Djava.security.auth.login.config=SQLJDBCDriver.conf -Djava.security.krb5.conf=krb5.ini <APPLICATION_NAME>  

```

## <a name="verifying-that-sql-server-can-be-accessed-via-kerberos"></a>確認可以透過 Kerberos 存取 SQL Server

在 SQL Server Management Studio 中執行以下查詢：

```sql
select auth_scheme from sys.dm_exec_connections where session_id=\@\@spid
```

確定您擁有執行這個查詢的必要權限。

## <a name="constrained-delegation"></a>限制委派

從 Microsoft JDBC Driver 6.2，驅動程式支援 Kerberos 限制委派。 委派的認證可以傳遞為 org.ietf.jgss.GSSCredential 物件、 驅動程式會使用這些認證來建立連線。

```java
Properties driverProperties = new Properties();
GSSCredential impersonatedUserCredential = [userCredential]
driverProperties.setProperty("integratedSecurity", "true");
driverProperties.setProperty("authenticationScheme", "JavaKerberos");
driverProperties.put("gsscredential", impersonatedUserCredential);
Connection conn = DriverManager.getConnection(CONNECTION_URI, driverProperties);
```

## <a name="kerberos-connection-using-principal-names-and-password"></a>使用主體名稱和密碼的 Kerberos 連接

從 Microsoft JDBC Driver 6.2，驅動程式可以建立使用主體名稱和密碼連線傳遞的 Kerberos，連接字串中。

```java
jdbc:sqlserver://servername=server_name;integratedSecurity=true;authenticationScheme=JavaKerberos;userName=user@REALM;password=****
```

如果使用者屬於 default_realm krb5.conf 檔案中設定的使用者名稱屬性不需要領域。 當`userName`和`password`設定連同`integratedSecurity=true;`和`authenticationScheme=JavaKerberos;`屬性，連接會建立具有使用者名稱的值做為 Kerberos 主體沿著與提供的密碼。

## <a name="using-kerberos-authentication-from-unix-machines-on-the-same-domain"></a>在相同的網域上使用 Kerberos 驗證，從 Unix 電腦

本指南假設的運作中的 Kerberos 設定已經存在。 使用 Kerberos 驗證，若要確認上述是否為 true 的 Windows 電腦上執行下列程式碼。 的程式碼會列印到主控台中，如果成功的 「 驗證配置:: KERBEROS"。 沒有其他的執行階段旗標、 相依性或驅動程式設定所提供的項目之外。 若要確認成功連線的 Linux 上，可以執行同一個程式碼區塊。

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(1433); // change if necessary
ds.setIntegratedSecurity(true);
ds.setAuthenticationScheme("JavaKerberos");
ds.setDatabaseName("<database>");

try (Connection c = ds.getConnection(); Statement s = c.createStatement();
        ResultSet rs = s.executeQuery("select auth_scheme from sys.dm_exec_connections where session_id=@@spid")) {
    while (rs.next()) {
        System.out.println("Authentication Scheme: " + rs.getString(1));
    }
}
```

1. 網域加入的用戶端電腦與伺服器相同的網域。
2. （選擇性）設定的預設 Kerberos 票證的位置。 這最方便正確地設定`KRB5CCNAME`環境變數。
3. 取得 Kerberos 票證，以產生新的或將現有的預設 Kerberos 票證的位置中。 若要產生票證，只要使用終端機，並初始化透過票證`kinit USER@DOMAIN.AD`其中 「 使用者 」 與 「 網域。AD"分別為主體和網域。 例如：`kinit SQL_SERVER_USER03@MICROSOFT.COM`。 在預設的票證位置或中，將會產生票證`KRB5CCNAME`路徑如果設定。
4. 終端機中會提示您輸入密碼，請輸入密碼。
5. 驗證的認證，透過票證`klist`並確認認證是您想要用於驗證的項目。
6. 執行上述的範例程式碼，並確認 Kerberos 驗證成功。

## <a name="see-also"></a>另請參閱

[使用 JDBC Driver 連接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
