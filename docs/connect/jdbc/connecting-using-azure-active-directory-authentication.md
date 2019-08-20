---
title: 使用 Azure Active Directory 驗證連線 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9c9d97be-de1d-412f-901d-5d9860c3df8c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b596936010fcdce4eb5c0701c5f0c6631cd9687e
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028126"
---
# <a name="connecting-using-azure-active-directory-authentication"></a>使用 Azure Active Directory 驗證連線

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文提供如何開發 JAVA 應用程式, 以使用 Microsoft JDBC Driver for SQL Server 的 Azure Active Directory 驗證功能的相關資訊。

您可以使用 Azure Active Directory (AAD) 驗證, 這是使用 Azure Active Directory 中的身分識別連接到 Azure SQL Database v12 的機制。 使用 Azure Active Directory 驗證集中管理資料庫使用者的身分識別，並作為 SQL Server 的替代驗證。 JDBC 驅動程式可讓您在 JDBC 連接字串中指定您的 Azure Active Directory 認證, 以連接到 Azure SQL DB。 如需如何設定 Azure Active Directory 驗證的相關資訊, 請造訪[使用 Azure Active Directory authentication 連線到 SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。 

在適用于 SQL Server 的 Microsoft JDBC 驅動程式中, 支援 Azure Active Directory 驗證的連接屬性為:
*   **驗證**: 使用這個屬性來指出要用於連接的 SQL 驗證方法。 可能的值為： 
    * **ActiveDirectoryMSI**
        * 支援自驅動程式版本**7.2**之後`authentication=ActiveDirectoryMSI` , 可以用來從已啟用「身分識別」支援的 Azure 資源內部連接到 Azure SQL Database/資料倉儲。 此外, 您也可以在 Connection/DataSource 屬性和此驗證模式中指定**msiClientId** , 這必須包含要用來取得**accessToken**以建立的的受控服務識別的用戶端識別碼。連接。
    * **ActiveDirectoryIntegrated**
        * 支援自驅動程式版本**6.0**之後`authentication=ActiveDirectoryIntegrated` , 可以用來連接到使用整合式驗證的 Azure SQL Database/資料倉儲。 若要使用此驗證模式, 您必須將內部部署 Active Directory 同盟服務 (ADFS) 與雲端中的 Azure Active Directory 建立同盟。 設定完成後, 您可以將原生程式庫 ' sqljdbc_auth ' 新增至 Windows OS 上的應用程式類別路徑, 或設定 Kerberos 票證以進行跨平臺驗證支援, 藉以進行連線。 當您登入已加入網域的電腦時, 您將能夠存取 Azure SQL DB/DW, 而不會提示您輸入認證。
    * **ActiveDirectoryPassword**
        * 支援自驅動程式版本**6.0**之後`authentication=ActiveDirectoryPassword` , 可以用來連接到使用 Azure AD 主要名稱和密碼的 Azure SQL Database/資料倉儲。
    * **SqlPassword**
        * 使用`authentication=SqlPassword`來連接到使用使用者名稱/使用者和密碼屬性的 SQL Server。
    * **NotSpecified**
        * 當`authentication=NotSpecified`不需要這些驗證方法時, 請使用或將其保留為預設值。

*   **accessToken**: 使用此連接屬性, 以使用存取權杖來連接到 SQL Database。 accessToken 只能使用 DriverManager 類別中 getConnection () 方法的 Properties 參數來設定。 它不能用在連接 URL 中。  

如需詳細資訊, 請參閱[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)頁面上的驗證屬性。  


## <a name="client-setup-requirements"></a>用戶端安裝需求
針對**ActiveDirectoryMSI** authentication, 下列元件必須安裝在用戶端電腦上:
* JAVA 8 或更新版本
* 適用于 SQL Server 的 Microsoft JDBC Driver 7.2 (或更新版本)
* 用戶端環境必須是 Azure 資源, 而且必須啟用「身分識別」功能支援。
* 自主資料庫使用者, 代表您的 Azure 資源系統指派的受控識別或使用者指派的受控識別, 或您的 MSI 所屬的其中一個群組, 必須存在於目標資料庫中, 而且必須具有 CONNECT 許可權。

針對其他驗證模式, 您必須在用戶端電腦上安裝下列元件:
* JAVA 7 或更新版本
* 適用于 SQL Server 的 Microsoft JDBC Driver 6.0 (或更新版本)
* 如果您使用的是以存取權杖為基礎的驗證模式, 您需要[azure-activedirectory-library for java](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其相依性, 才能執行本文中的範例。 如需詳細資訊, 請參閱**使用存取權杖連接**一節。
* 如果您使用**ActiveDirectoryPassword**驗證模式, 則需要[有適用于 java 的 azure-activedirectory 程式庫](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其相依性。 如需詳細資訊, 請參閱**使用 ActiveDirectoryPassword 驗證模式連接**一節。
* 如果您使用**ActiveDirectoryIntegrated**模式, 則需要有適用于 java 的 azure-activedirectory 程式庫及其相依性。 如需詳細資訊, 請參閱**使用 ActiveDirectoryIntegrated 驗證模式連接**一節。

## <a name="connecting-using-activedirectorymsi-authentication-mode"></a>使用 ActiveDirectoryMSI 驗證模式連接
下列範例示範如何使用 `authentication=ActiveDirectoryMSI` 模式。 從 Azure 資源、e、g a Azure 虛擬機器、App Service 或與 Azure Active Directory 同盟的函數應用程式中執行此範例。

在執行此範例之前, 請在下列幾行中將伺服器/資料庫名稱取代為您的伺服器/資料庫名稱:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
//Optional
ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used
```

使用 ActiveDirectoryMSI 驗證模式的範例:

```java
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class AAD_MSI {
    public static void main(String[] args) throws Exception {

        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setServerName("aad-managed-demo.database.windows.net"); // Replace with your server name
        ds.setDatabaseName("demo"); // Replace with your database name
        ds.setAuthentication("ActiveDirectoryMSI");
        // Optional
        ds.setMsiClientId("94de34e9-8e8c-470a-96df-08110924b814"); // Replace with Client ID of User-Assigned MSI to be used

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

在 Azure 虛擬機器上執行此範例, 會從_系統指派的受控識別_或_使用者指派的受控識別_(若已指定**msiClientId** ) 提取存取權杖, 並使用提取的存取權建立連線權杖. 如果已建立連接, 您應該會看到下列訊息:

```bash
You have successfully logged on as: <your MSI username>
```

## <a name="connecting-using-activedirectoryintegrated-authentication-mode"></a>使用 ActiveDirectoryIntegrated 驗證模式連接
使用6.4 版, Microsoft JDBC Driver 新增了在多個平臺 (Windows、Linux 和 macOS) 上使用 Kerberos 票證的 ActiveDirectoryIntegrated Authentication 支援。
如需詳細資訊, 請參閱[在 Windows、Linux 和 Mac 上設定 Kerberos 票證](https://docs.microsoft.com/sql/connect/jdbc/connecting-using-azure-active-directory-authentication#set-kerberos-ticket-on-windows-linux-and-mac), 以取得更多詳細資料。 或者, 在 Windows 上, sqljdbc_auth 也可以用來搭配 JDBC 驅動程式進行 ActiveDirectoryIntegrated 驗證。

> [!NOTE]
>  如果您使用的是較舊版本的驅動程式, 請檢查此[連結](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md), 以取得使用此驗證模式所需的個別相依性。 

下列範例示範如何使用 `authentication=ActiveDirectoryIntegrated` 模式。 請在已加入網域的電腦上執行此範例, 其與 Azure Active Directory 同盟。 代表您的 Azure AD 主體的自主資料庫使用者, 或是您所屬的其中一個群組, 必須存在於資料庫中, 而且必須具有 CONNECT 許可權。 

在建立並執行範例之前, 請在用戶端電腦 (您想要執行範例) 上下載[azure-activedirectory 程式庫-java 程式庫](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其相依性, 並將它們包含在 java 組建路徑中

在執行此範例之前, 請在下列幾行中將伺服器/資料庫名稱取代為您的伺服器/資料庫名稱:

```java
ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
ds.setDatabaseName("demo"); // replace with your database name
```

使用 ActiveDirectoryIntegrated 驗證模式的範例:
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

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```

在用戶端電腦上執行此範例時, 會自動使用您的 Kerberos 票證, 而且不需要任何密碼。 如果已建立連接, 您應該會看到下列訊息:

```
You have successfully logged on as: <your domain user name>
```

### <a name="set-kerberos-ticket-on-windows-linux-and-mac"></a>在 Windows、Linux 和 Mac 上設定 Kerberos 票證

您必須設定 Kerberos 票證, 將目前的使用者連結至 Windows 網域帳戶。 以下包含主要步驟的摘要。

#### <a name="windows"></a>Windows
JDK 隨附`kinit`, 可讓您在已加入網域的電腦上, 從金鑰發佈中心 (KDC) 取得 TGT, 此機器與 Azure Active Directory 同盟。

##### <a name="step-1-ticket-granting-ticket-retrieval"></a>步驟 1: 票證授與票證抓取
- **執行于**: Windows
- **動作**：
  - 使用命令`kinit username@DOMAIN.COMPANY.COM`從 KDC 取得 TGT, 然後它會提示您輸入您的網域密碼。
  - 使用`klist`來查看可用的票證。 如果 kinit 成功, 您應該會看到 krbtgt/DOMAIN. COMPANY .COM @ DOMAIN.COMPANY.COM 中的票證。

> [!NOTE]
>  您可能需要為您的`.ini`應用程式`-Djava.security.krb5.conf`指定一個檔案, 以找出 KDC。

#### <a name="linux-and-mac"></a>Linux 和 Mac

##### <a name="requirements"></a>需求
存取已加入網域的 Windows 電腦，以查詢您的 Kerberos 網域控制站。

##### <a name="step-1-find-kerberos-kdc"></a>步驟 1: 尋找 Kerberos KDC
- **執行于**: Windows 命令列
- **Action**: `nltest /dsgetdc:DOMAIN.COMPANY.COM` (其中 "DOMAIN.COMPANY.COM" 會對應至您的網功能變數名稱稱)
- **範例輸出**
  ```
  DC: \\co1-red-dc-33.domain.company.com
  Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
  ...
  The command completed successfully
  ```
- **要解壓縮的資訊**DC 名稱, 在此案例中為`co1-red-dc-33.domain.company.com`

##### <a name="step-2-configuring-kdc-in-krb5conf"></a>步驟 2: 在 krb5 中設定 KDC
- **執行于**: Linux/Mac
- **動作**: 在您選擇的編輯器中編輯/etc/krb5.conf。 設定下列金鑰
  ```
  [libdefaults]
    default_realm = DOMAIN.COMPANY.COM
   
  [realms]
  DOMAIN.COMPANY.COM = {
     kdc = co1-red-dc-28.domain.company.com
  }
  ```
  然後，儲存 krb5.conf 檔案並結束

> [!NOTE]
>  網域必須全部為大寫。

##### <a name="step-3-testing-the-ticket-granting-ticket-retrieval"></a>步驟 3：測試票證授權票證的擷取
- **執行于**: Linux/Mac
- **動作**：
  - 使用命令`kinit username@DOMAIN.COMPANY.COM`從 KDC 取得 TGT, 然後它會提示您輸入您的網域密碼。
  - 使用`klist`來查看可用的票證。 如果 kinit 成功, 您應該會看到 krbtgt/DOMAIN. COMPANY .COM @ DOMAIN.COMPANY.COM 中的票證。

## <a name="connecting-using-activedirectorypassword-authentication-mode"></a>使用 ActiveDirectoryPassword 驗證模式連接
下列範例示範如何使用 `authentication=ActiveDirectoryPassword` 模式。

建立並執行範例之前:
1.  在用戶端電腦 (您想要執行此範例) 上, 下載[azure-activedirectory 程式庫-java 程式庫](https://github.com/AzureAD/azure-activedirectory-library-for-java)及其相依性, 並將它們包含在 java 組建路徑中
2.  找出下列幾行程式碼, 並將伺服器/資料庫名稱取代為您的伺服器/資料庫名稱。
    ```java
    ds.setServerName("aad-managed-demo.database.windows.net"); // replace 'aad-managed-demo' with your server name
    ds.setDatabaseName("demo"); // replace with your database name
    ```
3.  找出下列幾行程式碼, 並以您想要連接的 AAD 使用者名稱取代 user name。
    ```java
    ds.setUser("bob@cqclinic.onmicrosoft.com"); // replace with your user name
    ds.setPassword("password");     // replace with your password
    ```

使用 ActiveDirectoryPassword 驗證模式的範例:
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
        
        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
```
如果已建立連接, 您應該會看到下列訊息作為輸出:
```
You have successfully logged on as: <your user name>
```

> [!NOTE]  
> 包含的使用者資料庫必須存在, 而且自主資料庫使用者 (代表指定的 Azure AD 使用者或其中一個群組、指定的 Azure AD 使用者所屬) 必須存在於資料庫中, 而且必須具有 CONNECT 許可權 (但不包括 Azure Active Directory伺服器管理員或群組)

## <a name="connecting-using-access-token"></a>使用存取權杖連接
應用程式/服務可以從 Azure Active Directory 抓取存取權杖, 並使用它連接到 Azure SQL Database/資料倉儲。

> [!NOTE] 
> **accessToken**只能使用 DriverManager 類別中 getConnection () 方法的 Properties 參數來設定。 不能在連接字串中使用它。

下列範例包含簡單的 JAVA 應用程式, 可使用存取權杖型驗證連接到 Azure SQL Database/資料倉儲。 在建立並執行範例之前, 請執行下列步驟:
1.  在 Azure Active Directory 中, 為您的服務建立應用程式帳戶。
    1. 登入 Azure 入口網站。
    2. 按一下左側導覽中的 [Azure Active Directory]。
    3. 按一下 [應用程式註冊] 索引標籤。
    4. 在抽屜中, 按一下 [新增應用程式註冊]。
    5. 輸入 mytokentest 作為應用程式的易記名稱, 然後選取 [Web 應用程式/API]。
    6. 我們不需要登入 URL。 只是提供的任何項目: “https://mytokentest" 。
    7. 按一下底部的 [建立]。
    9. 仍然在 Azure 入口網站中, 按一下應用程式的 [設定] 索引標籤, 然後開啟 [屬性] 索引標籤。
    10. 尋找「應用程式識別碼」 (也稱為用戶端識別碼) 值, 並將它複製到稍後, 在設定應用程式時需要用到 (例如, 1846943b-ad04-4808-aa13-4702d908b5c1)。 請參閱下列快照集。
    11. 在 [金鑰] 區段底下, 填入 [名稱] 欄位, 選取金鑰的持續時間, 然後儲存設定 (將 [值] 欄位保留空白) 以建立金鑰。 儲存之後, [值] 欄位應該會自動填入, 並複製產生的值。 這是用戶端密碼。
    12. 按一下左側面板上的 [Azure Active Directory]。 在 [應用程式註冊] 下, 尋找 [結束點] 索引標籤。複製「OATH 2.0 權杖端點」底下的 URL, 這是您的 STS URL。
    
    ![JDBC_AAD_Token](../../connect/jdbc/media/jdbc_aad_token.png)  
2. 以 Azure Active Directory 管理員身分登入 Azure SQL Server 的使用者資料庫, 並使用 T-sql 命令為您的應用程式主體布建自主資料庫使用者。 如需詳細資訊, 請參閱[使用 Azure Active Directory 驗證連接到 SQL Database 或 SQL 資料倉儲](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/), 以取得如何建立 Azure Active Directory 系統管理員和自主資料庫使用者的詳細資訊。

    ```
    CREATE USER [mytokentest] FROM EXTERNAL PROVIDER
    ```

3.  在用戶端電腦 (您想要執行此範例) 上, 下載[azure-activedirectory 程式庫-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)程式庫及其相依性, 並將它們包含在 java 組建路徑中。 請注意, 只有在執行此特定範例時, 才需要 azure-activedirectory 程式庫-java。 此範例會使用此程式庫中的 Api, 從 Azure AAD 抓取存取權杖。 如果您已經有存取權杖, 可以略過此步驟。 請注意, 您也必須移除範例中抓取存取權杖的區段。

在下列範例中, 將 STS URL、用戶端識別碼、用戶端密碼、伺服器和資料庫名稱取代為您的值。

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

        try (Connection connection = ds.getConnection(); 
                Statement stmt = connection.createStatement();
                ResultSet rs = stmt.executeQuery("SELECT SUSER_SNAME()")) {
            if (rs.next()) {
                System.out.println("You have successfully logged on as: " + rs.getString(1));
            }
        }
    }
}
``` 

如果連線成功, 您應該會看到下列訊息作為輸出:

```bash
Access Token: <your access token>
You have successfully logged on as: <your client ID>    
``` 
