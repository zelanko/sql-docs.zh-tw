---
title: 使用 Azure Active Directory 驗證連線 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c87e7b85282c7ca237689296e08d2b7645240ed
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767136"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>使用 Azure Active Directory 驗證連線

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文章提供有關如何開發 Java 應用程式，以使用適用於 SQL Server 的 Microsoft JDBC Driver 6.0 （或更高版本） 的 Azure Active Directory 驗證功能的資訊。

您可以使用 Azure Active Directory (AAD) 驗證，也就是連線至 Azure SQL Database v12 的機制使用 Azure Active Directory 中的身分識別。 使用 Azure Active Directory 驗證集中管理資料庫使用者的身分識別，並作為 SQL Server 的替代驗證。 JDBC 驅動程式可讓您在 連線到 Azure SQL DB 的 JDBC 連接字串中指定您的 Azure Active Directory 認證。 如需如何設定 Azure Active Directory 驗證的詳細資訊，請造訪[連接到 SQL 資料庫使用 Azure Active Directory 驗證](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。 

已新增兩個新的連接屬性來支援 Azure Active Directory 驗證：
*   **驗證**： 使用這個屬性來指出要用於連線的 SQL 驗證方法。 可能的值為： **ActiveDirectoryIntegrated**， **ActiveDirectoryPassword**， **SqlPassword**，而預設**NotSpecified**.
    * 使用 ' authentication = ActiveDirectoryIntegrated' 連接到 SQL Database，使用整合式的 Windows 驗證。 若要使用此驗證模式中，您需要建立內部部署 Active Directory Federation Services (ADFS) 使用在雲端中的 AAD 同盟。 這設定完畢後以及 Kerberos 票證，您可以存取 Azure SQL DB 而不需要您登入加入網域的電腦時提示輸入認證。 
    * 使用 ' authentication = ActiveDirectoryPassword' 連接到 SQL Database，使用 Azure AD 主體名稱和密碼。
    * 使用 ' authentication = SqlPassword' 連接到 SQL Server 使用使用者名稱/使用者名稱和密碼的屬性。
    * 使用 ' 驗證 = NotSpecified' 或任何一種驗證方法需要時將它保留為預設值。

*   **accessToken**： 使用這個屬性來連接到 SQL database 使用存取權杖。 accessToken 只可以使用 DriverManager 類別中的 getconnection （） 方法的 Properties 參數來設定。 它不能在連接 URL 中。  

如需詳細資訊，請參閱 [驗證] 屬性上[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)頁面。  


## <a name="client-setup-requirements"></a>用戶端安裝需求
請先確定用戶端電腦上已安裝下列元件：
* Java 7 或更新版本
*   Microsoft JDBC Driver 6.0 （或更新版本） for SQL Server
*   如果您使用存取權杖為基礎的驗證模式，您需要[azure active directory-程式庫-針對-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)與其相依項目，若要執行這篇文章中的範例。 如需詳細資訊，請參閱 <<c0>  **使用存取權杖連線**一節。
*   如果您使用 ActiveDirectoryPassword 驗證模式，您需要[azure active directory-程式庫-針對-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)和其相依性。 如需詳細資訊，請參閱 <<c0>  **使用 ActiveDirectoryPassword 驗證模式連接**一節。
*   如果您使用 ActiveDirectoryIntegrated 模式，您需要 azure activedirectory-程式庫-針對-java 和其相依性。 如需詳細資訊，請參閱 <<c0>  **使用 ActiveDirectoryIntegrated 驗證模式連接**一節。
    
## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>使用 ActiveDirectoryIntegrated 驗證模式進行連接
 6.4 版中，Microsoft JDBC Driver 會加入支援 ActiveDirectoryIntegrated 驗證多個平台 （Windows/Linux 和 Mac） 上使用 Kerberos 票證。
如需詳細資訊，請參閱 <<c0> [ 在 Windows、 Linux 和 Mac 上的設定 Kerberos 票證](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac)如需詳細資訊。 或者，在 Windows，sqljdbc_auth.dll 也可用為 ActiveDirectoryIntegrated 驗證透過 JDBC 驅動程式。

> [!NOTE]
>  如果您使用較舊版本的驅動程式，請檢查這[連結](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)才能使用此驗證模式中的個別相依性。 

下列範例示範如何使用 ' authentication = ActiveDirectoryIntegrated' 模式。 在加入網域的電腦與 Azure Active Directory 同盟執行此範例。 代表您的 Azure AD 主體，或其中一個群組的自主的資料庫使用者，您屬於、 必須存在於資料庫中，而且必須具有 CONNECT 權限。 

再建置及執行此範例中，用戶端電腦上 (所在，您想要執行此範例)，下載[azure active directory-程式庫-針對-java 程式庫](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其相依性，並將它們包含在 Java 建置路徑

執行範例之前，以您的伺服器/資料庫名稱，在下列幾行取代伺服器/資料庫名稱：

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

若要使用 ActiveDirectoryIntegrated 驗證模式範例：
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADIntegrated {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryIntegrated");
        ds.setHostNameInCertificate("*.database.windows.net");

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();) {
            
            ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()");
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```
用戶端電腦上自動執行此範例會使用 Kerberos 票證，因此需要無密碼。 如果建立連線，您應該會看到下列訊息：
```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>在 Windows、 Linux 和 Mac 上設定 Kerberos 票證

您需要設定您目前的使用者連結到 Windows 網域帳戶的 Kerberos 票證。 主要步驟摘要如下所示。

#### <a name="windows"></a>Windows
JDK 隨附`kinit`，可用來取得 TGT 從金鑰發佈中心 (KDC) 網域加入同盟與 Azure Active Directory 的機器。

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>步驟 1： 票證授權票證擷取
- **在上執行**: Windows
- **動作**：
  - 使用命令`kinit username@DOMAIN.COMPANY.COM`從 KDC 取得 TGT，然後它會提示您輸入網域密碼。
  - 使用`klist`若要查看可用的票證。 如果 kinit 成功，您應該會看到從 krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM 票證。

> [!NOTE]
>  您可能需要指定`.ini`檔案中使用`-Djava.security.krb5.conf`找出 KDC 的應用程式。

#### <a name="linux-and-mac"></a>Linux 和 Mac

##### <a name="requirements"></a>需求
若要查詢您的 Kerberos 網域控制站的 Windows 網域的機器存取。

##### <a name="step-1-find-kerberos-kdc"></a>步驟 1： 尋找 Kerberos KDC
- **在上執行**: Windows 命令列
- **動作**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` （其中"DOMAIN.COMPANY.COM"對應至您的網域名稱）
- **範例輸出**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **若要擷取的資訊**DC 名稱，在此情況下 `co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>步驟 2： 設定 KDC 中 krb5.conf
- **在上執行**: Linux/Mac
- **動作**： 編輯您選擇的編輯器中 /etc/krb5.conf。 設定下列金鑰
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  然後將儲存 krb5.conf 檔案並結束

> [!NOTE]
>  網域必須是全部大寫字。

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>步驟 3： 測試票證授權票證擷取
- **在上執行**: Linux/Mac
- **動作**：
  - 使用命令`kinit username@DOMAIN.COMPANY.COM`從 KDC 取得 TGT，然後它會提示您輸入網域密碼。
  - 使用`klist`若要查看可用的票證。 如果 kinit 成功，您應該會看到從 krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM 票證。

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>使用 ActiveDirectoryPassword 驗證模式進行連接
下列範例示範如何使用 ' authentication = ActiveDirectoryPassword' 模式。

再建置及執行範例：
1.  用戶端電腦上 (所在，您想要執行此範例)，下載[azure active directory-程式庫-針對-java 程式庫](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其相依性，並將它們包含在 Java 建置路徑
2.  找出下列幾行程式碼，並取代您的伺服器/資料庫名稱中的伺服器/資料庫名稱。
    ```java
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  找出下列幾行程式碼和使用者名稱，取代為您想要為連線的 AAD 使用者的名稱。
    ```java
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

使用 ActiveDirectoryPassword 驗證模式的範例：
```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AADUserPassword {
    
    public static void main(String[] args) throws Exception{
        
        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database
        ds.setUser("bob@cqclinic.onmicrosoft.com"); // Replace with your user name
        ds.setPassword("password"); // Replace with your password
        ds.setAuthentication("ActiveDirectoryPassword");
        ds.setHostNameInCertificate("*.database.windows.net");
        
        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();) {
            
            ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()");
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```
如果建立連線之後，您應該會看到下列訊息做為輸出：
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> 包含的使用者資料庫必須存在與自主的資料庫使用者，表示指定之 Azure AD 使用者或群組，也就是指定的 Azure AD 使用者屬於、 必須存在於資料庫中，而且必須具有 CONNECT 權限 （除了 Azure Active Directory伺服器管理員或群組）

## <a name="connecting-using-access-token"></a>使用存取權杖進行連線
應用程式/服務可以從 Azure Active Directory 擷取存取權杖，並使用該連接到 SQL Azure 資料庫。

> [!NOTE] 
> **accessToken**只能設定使用 DriverManager 類別中的 getconnection （） 方法的屬性參數。 它不能在連接字串。

下列範例包含簡單的 Java 應用程式連接到 Azure SQL Database 使用存取權杖型驗證。 再建置及執行範例，請執行下列步驟：
1.  建立 Azure Active Directory 中的應用程式帳戶，為您的服務。
    1. 登入 Azure 入口網站。
    2. 在左側導覽中，按一下 [Azure Active Directory 上]。
    3. 按一下 [應用程式註冊] 索引標籤。
    4. 在下拉式清單中，按一下 「 新的應用程式註冊 」。
    5. 輸入 mytokentest 作為應用程式的易記名稱，選取 [Web 應用程式/API]。
    6. 我們不需要登入 URL。 只是提供的任何項目: “http://mytokentest" 。
    7. 按一下底部的 [建立]。
    9. 仍是在 Azure 入口網站中，按一下您的應用程式的 [設定] 索引標籤並開啟 [屬性] 索引標籤。
    10. 尋找 「 應用程式識別碼 」 （也稱為用戶端識別碼） 值，並將它複製擱置在一旁，您稍後需要此設定您的應用程式 (例如 1846943b-ad04-4808-aa13-4702d908b5c1) 時。 請參閱下列快照集。
    11. 在 [金鑰] 區段中，請填寫 [名稱] 欄位中，選取金鑰的持續時間，然後儲存設定 （將保留空白的 [值] 欄位） 中建立的金鑰。 在儲存之後，[值] 欄位應該會自動填滿，複製產生的值。 這是用戶端密碼。
    12. 按一下左側面板上的 [Azure Active Directory]。 在 [應用程式註冊] 下尋找 「 結束點 」 索引標籤。複製 [OATH 2.0 權杖端點] 下的 URL，這是您 STS 的 URL。
    
    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. 登入您 Azure SQL Server 使用者資料庫，只要為 Azure Active Directory 系統管理員使用 T-SQL 命令佈建應用程式主體的自主的資料庫使用者。 如需詳細資訊，請參閱 <<c0> [ 連線到 SQL Database 或 SQL 資料倉儲使用 Azure Active Directory 驗證](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)如需有關如何建立 Azure Active Directory 系統管理員 」 和 「 自主的資料庫使用者的詳細資訊。

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  用戶端電腦上 (所在，您想要執行此範例)，下載[azure active directory-程式庫-針對-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)程式庫和其相依性，並將它們包含在 Java 建置路徑。 請注意，azure active directory-程式庫-針對-java 時，才需要執行此特定範例。 範例會使用本文件庫中的 Api，來擷取 Azure AAD 的存取權杖。 如果您已經有存取權杖，您可以略過此步驟。 請注意，您也需要移除在範例中，擷取存取權杖的區段。

在下列範例中，請以您的值取代的 STS 的 URL、 用戶端識別碼、 用戶端祕密、 伺服器和資料庫名稱。

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

// The azure-activedirectory-library-for-java is needed to retrieve the access token from the AD.
import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;

public class AADTokenBased {

    public static void main(String[] args) throws Exception {

        // Retrieve the access token from the AD.
        String spn = "https://database.windows.net/";
        String stsurl = "https://login.microsoftonline.com/..."; // Replace with your STS URL.
        String clientId = "1846943b-ad04-4808-aa13-4702d908b5c1"; // Replace with your client ID.
        String clientSecret = "..."; // Replace with your client secret.

        AuthenticationContext context = new AuthenticationContext(stsurl, false, Executors.newFixedThreadPool(1));
        ClientCredential cred = new ClientCredential(clientId, clientSecret);

        Future<AuthenticationResult> future = context.acquireToken(spn, cred, null);
        String accessToken = future.get().getAccessToken();

        System.out.println("Access Token: " + accessToken);

        // Connect with the access token.
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name.
        ds.setDatabaseName("demo"); // Replace with your database name.
        ds.setAccessToken(accessToken);
        ds.setHostNameInCertificate("*.database.windows.net");

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();) {

            ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()");
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
``` 

如果連線成功，您應該會看到下列訊息做為輸出：
```java
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
