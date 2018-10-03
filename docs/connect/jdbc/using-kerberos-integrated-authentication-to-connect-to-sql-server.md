---
title: 使用 Kerberos 整合驗證連線至 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 687802dc-042a-4363-89aa-741685d165b3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e4f058b1ae9f35df86b1e326c520bd4ebb588c4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798896"
---
# <a name="using-kerberos-integrated-authentication-to-connect-to-sql-server"></a>使用 Kerberos 整合式驗證連接到 SQL Server

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

從 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 開始，應用程式可使用 **authenticationScheme** 連線屬性來指定要使用類型 4 Kerberos 整合驗證連線至資料庫。 請參閱[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)如需有關連接屬性。 如需有關 Kerberos 的詳細資訊，請參閱 < [Microsoft Kerberos](http://go.microsoft.com/fwlink/?LinkID=100758)。

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

當您使用資料來源建立連線時，可以使用 setAuthenticationScheme 設定驗證配置，以及使用 **setServerSpn** 選擇性設定 Kerberos 連線的 SPN。

已加入新的記錄器來支援 Kerberos 驗證：com.microsoft.sqlserver.jdbc.internals.KerbAuthentication。 如需詳細資訊，請參閱[追蹤驅動程式作業](../../connect/jdbc/tracing-driver-operation.md)。

以下指導方針可幫助您設定 Kerberos：

1. 設定**AllowTgtSessionKey**為 1 的 Windows 登錄中。 如需詳細資訊，請參閱 [Windows Server 2003 中的 Kerberos 通訊協定登錄項目與 KDC 設定金鑰](http://support.microsoft.com/kb/837361)。
2. 確定 Kerberos 組態 (UNIX 環境中的 krb5.conf) 指向您的環境所適用的正確領域和 KDC。
3. 使用 kinit 或登入網域來初始化 TGT 快取。
4. 當使用 **authenticationScheme=JavaKerberos** 的應用程式在 Windows Vista 或 Windows 7 作業系統上執行時，您應使用標準使用者帳戶。 但是，如果您在系統管理員帳戶之下執行應用程式，則必須以系統管理員權限執行此應用程式。

> [!NOTE]  
> 只有 Microsoft JDBC Driver 4.2 以上 (含) 版本支援 serverSpn 連線屬性。

## <a name="service-principal-names"></a>服務主要名稱

服務主要名稱 (SPN) 是用戶端用以唯一識別服務執行個體的名稱。

您可以使用 **serverSpn** 連線屬性指定 SPN，或直接讓驅動程式為您建置 (預設)。 此屬性的格式為：“MSSQLSvc/fqdn:port\@REALM”，其中 fqdn 是完整網域名稱，port 是連接埠號碼，REALM 則是以大寫字母表示的 SQL Server Kerberos 領域。 如果您的 Kerberos 設定預設領域和該伺服器的領域相同，且預設值未將其包含在內，則這個屬性的領域部分是選擇性的。 如果您想要支援跨領域驗證案例，且其中 Kerberos 設定中的預設領域和伺服器的領域不同，則您必須以 serverSpn 屬性設定 SPN。

例如，您的 SPN 可能看起來像:"MSSQLSvc/some-server.zzz.corp.contoso.com:1433\@ZZZZ。CORP.CONTOSO.COM"

如需有關服務主要名稱 (SPN) 的詳細資訊，請參閱：

- [如何在 SQL Server 中使用 Kerberos 驗證](http://support.microsoft.com/kb/319723)

- [搭配 SQL Server 使用 Kerberos](http://go.microsoft.com/fwlink/?LinkId=207814)

> [!NOTE]  
> 6.2 版 JDBC 驅動程式的跨領域 Kerberos，正確地使用之前，您就必須明確設定**serverSpn**。
>
> 6.2 從版開始，此驅動程式將能夠建置**serverSpn**根據預設，即使是使用跨領域 Kerberos。 雖然您可以使用**serverSpn**明確太。

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

除了允許驅動程式使用登入模組組態檔中指定的設定來取得 Kerberos 認證以外，驅動程式也可以使用現有的認證。 當您的應用程式需要使用一個以上的使用者認證來建立連接時，這樣的處理方式會很實用。

驅動程式會嘗試使用現有的認證 (如果可用的話)，然後再嘗試使用指定的登入模組進行登入。 因此，當使用 Subject.doAs 方法在特定內容之下執行程式碼時，將會使用傳遞給 Subject.doAs 呼叫的認證來建立連接。

如需詳細資訊，請參閱 [JAAS 登入組態檔](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/LoginConfigFile.html)和 [Class Krb5LoginModule](https://docs.oracle.com/javase/8/docs/jre/api/security/jaas/spec/com/sun/security/auth/module/Krb5LoginModule.html) (類別 Krb5LoginModule)。

從 Microsoft JDBC Driver 6.2 中，登入模組組態檔的名稱可選擇性地使用傳遞連線屬性 jaasConfigurationName，這樣就能有它自己的登入設定的每個連線。

## <a name="creating-a-kerberos-configuration-file"></a>建立 Kerberos 組態檔

如需 Kerberos 組態檔的詳細資訊，請參閱 [Kerberos 需求](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jgss/tutorials/KerberosReq.html)。

這是網域組態檔範例，其中 YYYY 和 ZZZZ 是您網站的網域名稱。

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

例如，當您啟動應用程式時，您可以使用這個命令列：

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

## <a name="see-also"></a>另請參閱

[使用 JDBC Driver 連接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
