---
title: 使用 Azure Active Directory 驗證連線 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.technology:
- drivers
ms.topic: article
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ed4b2623b7a80358622b8153d316428b742ef31e
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="connecting-using-azure-active-directory-authentication"></a>使用 Azure Active Directory 驗證連線

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文章提供有關如何開發使用 SQL Server 的 Microsoft JDBC Driver 6.0 （或更高） 的 Azure Active Directory 驗證功能的 Java 應用程式的資訊。

您可以使用 Azure Active Directory (AAD) 驗證，連接到 Azure SQL Database v12 的機制使用 Azure Active Directory 中的身分識別。 使用 Azure Active Directory 驗證來集中管理身分識別的資料庫使用者，以及 SQL Server 驗證的替代方案。 JDBC 驅動程式可讓您連接到 Azure SQL DB JDBC 連接字串中指定您的 Azure Active Directory 認證。 如需如何設定 Azure Active Directory 驗證的詳細資訊，請造訪[連接到 SQL 資料庫使用 Azure Active Directory 驗證](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。 

已加入兩個新的連接屬性來支援 Azure Active Directory 驗證：
*   **驗證**： 此屬性用於指出要用於連接的 SQL 驗證方法。 可能的值為： **ActiveDirectoryIntegrated**， **ActiveDirectoryPassword**， **SqlPassword**，且預設**NotSpecified**.
    * 使用 ' authentication = ActiveDirectoryIntegrated' 連接到 SQL 資料庫使用整合式的 Windows 驗證。 若要使用這個驗證模式，您需要在內部部署 Active Directory Federation Services (ADFS) 與 Azure AD 雲端中建立同盟。 這是設定以及 Kerberos 票證，您可以存取 Azure SQL DB，而不提示輸入認證時登入加入網域的電腦。 
    * 使用 ' authentication = ActiveDirectoryPassword' 連接到 SQL 資料庫使用的 Azure AD 主體名稱和密碼。
    * 使用 ' authentication = SqlPassword' 連接到 SQL Server 使用的使用者名稱/使用者名稱和密碼的屬性。
    * 使用 ' authentication = NotSpecified'，或保留為預設值時不需要這些驗證方法的任何一個。

*   **accessToken**： 使用這個屬性來連接到 SQL 資料庫使用存取權杖。 accessToken 只能設定 getConnection() 方法的 Properties 參數使用 DriverManager 類別中。 它不能在連接 URL。  

如需詳細資訊，請參閱 [驗證] 屬性上[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)頁面。  


## <a name="client-setup-requirements"></a>用戶端安裝需求
請先確定用戶端電腦上已安裝下列元件：
* Java 7 或更新版本
*   Microsoft JDBC Driver 6.0 （或更新版本） for SQL Server
*   如果您使用存取權杖為基礎的驗證模式，您需要[azure-activedirectory-程式庫-如-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)執行的範例，在此文件及其相依項目。 如需詳細資訊，請參閱**連接使用存取權杖**> 一節。
*   如果您使用 ActiveDirectoryPassword 驗證模式，您需要[azure-activedirectory-程式庫-如-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其相依項目。 如需詳細資訊，請參閱**使用 ActiveDirectoryPassword 驗證模式連接**> 一節。
*   如果您使用 ActiveDirectoryIntegrated 模式時，您需要 azure-activedirectory-程式庫-如-java 和其相依性。 如需詳細資訊，請參閱**使用 ActiveDirectoryIntegrated 驗證模式連接**> 一節。
    
## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>連接使用 ActiveDirectoryIntegrated 驗證模式
 6.4 的版本，Microsoft JDBC 驅動程式會加入 ActiveDirectoryIntegrated 驗證使用 Kerberos 票證在多種平台 （Windows/Linux 和 Mac） 的支援。
請參閱[Windows、 Linux 和 Mac 上的 設定 Kerberos 票證](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac)如需詳細資訊。 或者，在 Windows 中，sqljdbc_auth.dll 也可用來 ActiveDirectoryIntegrated 驗證 JDBC 驅動程式。

> [!NOTE]
>  如果您使用較舊版本的驅動程式，請檢查這[連結](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)才能使用這個驗證模式的個別相依性。 

下列範例示範如何使用 ' authentication = ActiveDirectoryIntegrated' 模式。 在加入網域的電腦與 Azure Active Directory 同盟時，執行此範例。 自主的資料庫使用者，表示您的 Azure AD 主體，或其中一個群組，您屬於、 必須存在於資料庫中，必須具備 CONNECT 權限。 

再建置及執行此範例中，用戶端電腦 (所在，您想要執行此範例)，下載[azure-activedirectory-程式庫-如為 java 程式庫](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其相依項目，並將它們包含的 Java 建置路徑中

伺服器/資料庫名稱取代您的伺服器/資料庫名稱，在下列幾行之前執行此範例：

```
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

若要使用 ActiveDirectoryIntegrated 驗證模式範例：
```
import java.sql.Connection;
import java.sql.ResultSet;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class IntegratedExample {

    public static void main(String[] args) throws Exception {
        SQLServerDataSource ds = new SQLServerDataSource();

        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryIntegrated");
        ds.setHostNameInCertificate("*.database.windows.net");

        Connection connection = ds.getConnection();

        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
```
自動用戶端電腦上執行這個範例會使用 Kerberos 票證，因此需要無密碼。 如果建立連線之後，您應該會看到下列訊息：
```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>在 Windows、 Linux 和 Mac 上設定 Kerberos 票證

您需要設定將目前的使用者連結至 Windows 網域帳戶的 Kerberos 票證。 以下包含重要步驟的摘要。

#### <a name="windows"></a>視窗
JDK 隨附`kinit`可用來從 KDC （金鑰發佈中心） 取得 TGT，在網域加入同盟與 Azure Active Directory 的機器。

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>步驟 1： 票證授權票證擷取
- **在執行**: Windows
- **動作**:
  - 使用命令`kinit username@DOMAIN.COMPANY.COM`從 KDC 中取得的 TGT，然後它會提示您輸入網域密碼。
  - 使用`klist`若要查看可用的票證。 如果 kinit 成功，您應該會看到 krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM 票證。

> [!NOTE]
>  您可能需要指定`.ini`檔案搭配`-Djava.security.krb5.conf`KDC 找出應用程式。

#### <a name="linux-and-mac"></a>Linux 和 Mac

##### <a name="requirements"></a>需求
存取 Windows 網域的電腦才能查詢 Kerberos 網域控制站

##### <a name="step-1-find-kerberos-kdc"></a>步驟 1： 尋找 Kerberos KDC
- **在執行**: Windows 命令列
- **動作**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` （其中"DOMAIN.COMPANY.COM"對應至您的網域名稱）
- **範例輸出**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **若要擷取的資訊**DC 名稱，在此情況下 `co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>步驟 2： 設定 KDC krb5.conf 中
- **在執行**: Linux/Mac
- **動作**： 編輯 /etc/krb5.conf 在您選擇的編輯器中。 設定下列機碼
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  然後儲存 krb5.conf 檔案，然後結束

> [!NOTE]
>  網域必須是全部大寫。

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>步驟 3： 測試票證授權票證擷取
- **在執行**: Linux/Mac
- **動作**:
  - 使用命令`kinit username@DOMAIN.COMPANY.COM`從 KDC 中取得的 TGT，然後它會提示您輸入網域密碼。
  - 使用`klist`若要查看可用的票證。 如果 kinit 成功，您應該會看到 krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM 票證。

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>連接使用 ActiveDirectoryPassword 驗證模式
下列範例示範如何使用 ' authentication = ActiveDirectoryPassword' 模式。

再建置及執行範例：
1.  在用戶端電腦 (所在，您想要執行此範例)，下載[azure-activedirectory-程式庫-如為 java 程式庫](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其相依項目，並將它們包含的 Java 建置路徑中
2.  找出下列幾行程式碼，並取代您的伺服器/資料庫名稱的伺服器/資料庫名稱。
    ```
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  找出下列幾行程式碼和使用者名稱，取代為您想要做為連接的 Azure AD 使用者的名稱。
    ```
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

若要使用 ActiveDirectoryPassword 驗證模式範例：
```
import java.sql.Connection;
import java.sql.ResultSet;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class UserPasswordExample {
    
    public static void main(String[] args) throws Exception{
        SQLServerDataSource ds = new SQLServerDataSource();
        
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database
        ds.setUser("bob@cqclinic.onmicrosoft.com"); // Replace with your user name
        ds.setPassword("password"); // Replace with your password
        ds.setAuthentication("ActiveDirectoryPassword");
        ds.setHostNameInCertificate("*.database.windows.net");
        
        Connection connection = ds.getConnection();
        
        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
```
如果建立連線之後，您應該會看到下列訊息做為輸出：
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> 包含的使用者資料庫必須存在，表示指定之自主的資料庫使用者和 Azure AD 使用者或群組，指定 Azure AD 使用者屬於、 必須存在於資料庫中，而且必須具有 CONNECT 權限 （除了 Azure Active Directory伺服器管理員或群組）


## <a name="connecting-using-access-token"></a>連接使用存取權杖
應用程式/服務可以從 Azure Active Directory 擷取存取權杖，並使用該項資訊來連接到 SQL Azure 資料庫。 請注意該 accessToken 只能設定 getConnection() 方法的 Properties 參數使用 DriverManager 類別中。 它不能在連接字串。
 
下列範例包含簡單的 Java 應用程式連接到 Azure SQL Database 使用存取權杖型驗證。 再建置及執行範例，請執行下列步驟：
1.  Azure Active Directory 中建立應用程式帳戶，為您的服務。
    1. 登入 Azure 管理入口網站
    2. 按一下左側導覽中的 Azure Active Directory
    3. 按一下 「 應用程式註冊 」 索引標籤。
    4. 抽屜按一下 「 新的應用程式註冊 」。
    5. 輸入 mytokentest 作為應用程式的易記名稱，選取 「 Web 應用程式/應用程式開發介面 」。
    6. 我們不需要登入 URL。 只是提供的任何項目: 「http://mytokentest"。
    7. 按一下底部的 [建立]。
    9. 仍在 Azure 入口網站中，按一下您的應用程式的 [設定] 索引標籤，開啟 [屬性] 索引標籤。
    10. 找出 「 應用程式識別碼 」 （也稱為用戶端識別碼） 值，並將它複製擱置在一旁，您稍後設定您的應用程式 (例如，1846943b-ad04-4808-aa13-4702d908b5c1) 時。 請參閱下列快照集。
    11. 找出 「 應用程式識別碼 URL 」 值，並將它複製擱置在一旁，這是 STS 的 URL。
    12. 下一節 「 金鑰 」，建立一個機碼 [名稱] 欄位中填入、 選取金鑰的持續時間和儲存設定 （將保留空白的 [值] 欄位）。 [值] 欄位應該是在儲存之後，自動填入，複製產生的值。 這是用戶端密碼。

    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. 登入您 Azure SQL Server 使用者資料庫，做為 Azure Active Directory 系統管理員，以及使用 T-SQL 命令佈建應用程式主體之自主的資料庫使用者。 請參閱[連接到 SQL Database 或 SQL 資料倉儲使用 Azure Active Directory 驗證](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)如需有關如何建立 Azure Active Directory 系統管理員 」 和 「 自主的資料庫使用者。

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  在用戶端電腦 (所在，您想要執行此範例)，下載[azure-activedirectory-程式庫-如-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)媒體櫃和其相依性，並將它們包含的 Java 建置路徑中。 請注意，azure-activedirectory-程式庫-如-java 只需要執行此特定範例，因為它使用本文件庫 Api 從 Azure AD 擷取存取權杖。 如果您已經有一個存取權杖，您可以略過此步驟。 請注意，您也需要移除下列區段中擷取存取權杖的範例。

在下列範例中，請以您的值取代 STS 的 URL、 用戶端識別碼、 用戶端密碼、 伺服器和資料庫名稱。

```
import java.sql.Connection;
import java.sql.ResultSet;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

// The azure-activedirectory-library-for-java is needed to retrieve the access token from the AD. 
import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;
import com.microsoft.aad.adal4j.ClientCredential;


public class TokenBasedExample {

    public static void main(String[] args) throws Exception{

        // Retrieve the access token from the AD.
        String spn = "https://database.windows.net/";
        String stsurl = "https://microsoft.onmicrosoft.com/..."; // Replace with your STS URL.
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

        Connection connection = ds.getConnection();

        ResultSet rs = connection.createStatement().executeQuery("SELECT SUSER_SNAME()");
        if(rs.next()){
            System.out.println("You have successfully logged on as: " + rs.getString(1));
        }
    }
}
``` 

如果連接成功，您應該會看到下列訊息做為輸出：
```
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
