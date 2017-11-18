---
title: "使用 Azure Active Directory 驗證連線 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
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
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 83d5ad3bae131b58dd344c3f5f9bfc7f5d0c4f5a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-using-azure-active-directory-authentication"></a>使用 Azure Active Directory 驗證連線
本文章提供有關如何開發使用 SQL Server 的 Microsoft JDBC Driver 6.0 （或更高） 的 Azure Active Directory 驗證功能的 Java 應用程式的資訊。

從 Microsoft JDBC Driver 6.0 for SQL Server，您可以使用 Azure Active Direcoty (AAD) 驗證這是連接到 Azure SQL Database v12 的一種機制使用 Azure Active Directory 中的身分識別。 使用 Azure Active Directory 驗證來集中管理身分識別的資料庫使用者，以及 SQL Server 驗證的替代方案。 JDBC Driver 6.0 （或更新版本） 可讓您連接到 Azure SQL DB JDBC 連接字串中指定您的 Azure Active Directory 認證。 如需如何設定 Azure Active Directory 驗證的詳細資訊，請造訪[連接到 SQL 資料庫使用 Azure Active Directory 驗證](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。 

已加入兩個新的連接屬性來支援 Azure Active Directory 驗證：
*   **驗證**： 此屬性用於指出要用於連接的 SQL 驗證方法。 可能的值為： **ActiveDirectoryIntegrated**， **ActiveDirectoryPassword**， **SqlPassword**和預設**NotSpecified**.
    * 使用 ' authentication = ActiveDirectoryIntegrated' 連接到 SQL 資料庫使用整合式的 Windows 驗證。 若要使用這個驗證模式，您需要在內部部署 Active Directory Federation Services (ADFS) 與 Azure AD 雲端中建立同盟。 一旦安裝程式，您可以在不需輸入 ceredentials 當您登入加入網域的電腦存取 Azure SQL DB。 
    * 使用 ' authentication = ActiveDirectoryPassword' 連接到 SQL 資料庫使用的 Azure AD 主體名稱和密碼。
    * 使用 ' authentication = SqlPassword' 連接到 SQL Server 使用的使用者名稱/使用者名稱和密碼的屬性。
    * 使用 ' authentication = NotSpecified' 或保留為預設值，如果這些驗證方法都不需要。

*   **accessToken**： 使用這個屬性來連接到 SQL 資料庫使用存取權杖。 accessToken 只能設定 getConnection() 方法的 Properties 參數使用 DriverManager 類別中。 它不能在連接 URL。  

如需詳細資訊，請參閱 [驗證] 屬性上[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)頁面。  


## <a name="client-setup-requirements"></a>用戶端安裝需求
請先確定用戶端電腦上已安裝下列元件：
* Java 7 或更新版本
*   6.2 （或更新版本） 的 Microsoft JDBC Driver for SQL Server
*   如果您使用存取權杖型的驗證模式，您將需要[azure-activedirectory-程式庫-如-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)執行的範例，在此文件及其相依項目。 請參閱**連接使用存取權杖**> 一節以取得詳細資料。
*   如果您使用的 ActiveDirectoryPassword 驗證模式，您將需要[azure-activedirectory-程式庫-如-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其相依項目。 請參閱**使用 ActiveDirectoryPassword 驗證模式連接**> 一節以取得詳細資料。
*   如果您使用 ActiveDirectoryIntegrated 模式時，您必須安裝 Active Directory Authentication Library for SQL Server (ADALSQL。DLL) 和 sqljdbc_auth.dll。
    * ADALSQL。DLL 可讓應用程式對 Microsoft Azure SQL Database 使用 Azure Active Directory 進行驗證。 下載從 DLL [Microsoft SQL Server 的 Microsoft Active Directory 驗證程式庫](http://www.microsoft.com/en-us/download/details.aspx?id=48742)
    * 如 ADALSQL。DLL 兩個二進位版本 X86 和 X64 可供下載。 如果已安裝不正確的二進位版本，或如果 DLL 遺失時，驅動程式將會引發下列錯誤: 「 無法載入 adalsql.dll (Authentication =...)。 錯誤碼： 0x2。 」。 在這種情況下下載適合的 ADALSQL 版本。DLL。 
    * sqljdbc_auth.dll 是驅動程式套件中可用。 將 sqljdbc_auth.dll 檔複製到安裝 JDBC 驅動程式的電腦上的 Windows 系統路徑上的目錄。 或者，您也可以設定 java.libary.path 系統屬性來指定 sqljdbc_auth.dll 的目錄。 
    * 如果您是在 x64 處理器上執行 64 位元的 JVM，請使用 x64 資料夾中的 sqljdbc_auth.dll 檔案。 
    * 如果您執行的是 32 位元的 Java Virtual Machine (JVM)，即使作業系統為 x64 版，也請使用 x86 資料夾中的 sqljdbc_auth.dll 檔案。 
    * 例如，如果您使用 32 位元的 JVM，JDBC 驅動程式安裝在預設目錄，您可以指定 DLL 的位置啟動的 Java 應用程式時，請使用下列虛擬機器 (VM) 引數：  
        ```
        -Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86
        ```
    
## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>連接使用 ActiveDirectoryIntegrated 驗證模式
下列範例示範如何使用 ' authentication = ActiveDirectoryIntegrated' 模式。 在加入網域的電腦與 Azure Active Directory 同盟時，執行此範例。 自主的資料庫使用者，表示您的 Azure AD 主體，或其中一個群組，您屬於、 必須存在於資料庫中，必須具備 CONNECT 權限。 
    
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
加入至同盟與 Azure Active Directory 網域的電腦上執行此範例中會自動使用您的 Windows 認證，因此需要無密碼。 如果建立連線之後，您會看到下列訊息：
```
You have successfully logged on as: <your domain user name>
```

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
如果建立連線之後，您會看到下列訊息做為輸出：
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> 包含的使用者資料庫必須存在，表示指定之自主的資料庫使用者與 Azure AD 使用者或群組，指定 Azure AD 使用者屬於、 必須存在於資料庫中，而且必須具有 CONNECT 權限 （除了 Azure Active Directory伺服器管理員或群組）


## <a name="connecting-using-access-token"></a>連接使用存取權杖
應用程式/服務可以從 Azure Active Directory 擷取存取權杖，並使用該項資訊來連接到 SQL Azure 資料庫。 請注意該 accessToken 只能設定 getConnection() 方法的 Properties 參數使用 DriverManager 類別中。 它不能在連接字串。
 
下列範例包含簡單的 Java 應用程式連接到 Azure SQL Database 使用存取權杖型的驗證。 再建置及執行範例，請執行下列步驟：
1.  Azure Active Directory 中建立應用程式帳戶，為您的服務。
    1. 登入 Azure 管理入口網站
    2. 按一下左側導覽中的 Azure Active Directory
    3. 按一下您要註冊範例應用程式的目錄租用戶。 這必須是相同的目錄與您的資料庫 （裝載您資料庫的伺服器） 相關聯。
    4. 按一下 [應用程式] 索引標籤。
    5. 抽屜，按一下 [新增]。
    6. 按一下 [新增我的組織開發的應用程式]。
    7. 輸入 mytokentest 作為應用程式的易記名稱，選取 「 Web 應用程式和/或 Web API 」，然後再按下一步。
    8. 假設此應用程式協助程式/服務並不是 web 應用程式，它並沒有登入 URL 或應用程式識別碼 URI。 針對這兩個欄位中，輸入 http://mytokentest
    9. 雖然仍在 Azure 入口網站中，按一下 應用程式的 設定 索引標籤
    10. 尋找用戶端識別碼值，並將它複製擱置在一旁，您稍後 （也就設定您的應用程式時 a4bbfe26-dbaa-4fec-8ef5-223d229f647d)。 請參閱下列快照集。
    11. 下一節 「 金鑰 」，選取金鑰的持續時間、 儲存組態，並複製的索引鍵，供日後使用。 這是用戶端密碼。
    12. 底部，按一下 「 檢視在端點上 」，並複製下 「 OAUTH 2.0 授權端點 」 的 URL 以供稍後使用。 這是 STS 的 URL。


![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)


2. 登入您 Azure SQL Server 使用者資料庫，做為 Azure Active Directory 系統管理員，以及使用 T-SQL 命令佈建應用程式主體之自主的資料庫使用者。 請參閱[連接到 SQL Database 或 SQL 資料倉儲使用 Azure Active Directory 驗證](https://azure.microsoft.com/en-us/documentation/articles/sql-database-aad-authentication/)如需有關如何建立 Azure Active Directory 系統管理員 」 和 「 自主的資料庫使用者。

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  在用戶端電腦 (所在，您想要執行此範例)，下載[azure-activedirectory-程式庫-如-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)媒體櫃和其相依性，並將它們包含的 Java 建置路徑中。 請注意，azure-activedirectory-程式庫-如-java 只需要執行此特定範例，因為它使用本文件庫 Api 從 Azure AD 擷取存取權杖。 如果您已經有一個存取權杖，您可以略過此步驟。 請注意，您也必須移除下列區段中擷取存取權杖的範例。

在下列範例中，取代 STS 的 URL，用戶端識別碼、 用戶端密碼、 伺服器和資料庫名稱，以您的值。

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
        String stsurl = "https://login.microsoftonline.com/..."; // Replace with your STS URL.
        String clientId = "a4bbfe26-dbaa-4fec-8ef5-223d229f647d"; // Replace with your client ID.
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

如果連接成功，您會看到下列訊息做為輸出：
```
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 

