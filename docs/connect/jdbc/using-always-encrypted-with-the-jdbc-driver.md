---
title: "JDBC 驅動程式搭配使用一律加密 |Microsoft 文件"
ms.custom: 
ms.date: 3/14/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5a32f8269bb6787087b54d161c50cf6f06488482
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2018
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>JDBC 驅動程式搭配使用永遠加密
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

此頁面提供有關如何開發使用的 Java 應用程式資訊[永遠加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md)和 Microsoft JDBC Driver 6.0 （或更新版本） for SQL Server。

一律加密可讓用戶端加密機密資料，並永遠不會顯示資料或 SQL Server 或 Azure SQL Database 的加密金鑰。 永遠加密驅動程式，例如 Microsoft JDBC Driver 6.0 （或更高） 啟用適用於 SQL Server，達成此行為，透過無障礙地加密與解密用戶端應用程式中的機密資料。 驅動程式會自動判斷哪一個查詢參數對應到永遠加密的資料庫資料行，而且會加密這些參數的值，它將它們傳送至 SQL Server 或 Azure SQL Database 之前。 同樣地，驅動程式會以清晰簡明的方式，將擷取自查詢結果的加密資料庫資料行資料進行解密。 如需詳細資訊，請參閱[一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)和[一律加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。

## <a name="prerequisites"></a>필수 구성 요소
- 請確定 Microsoft JDBC Driver 6.0 （或更新版本） 的開發電腦上安裝 SQL Server。 
- 下載並安裝 Java 密碼編譯延伸模組 (JCE) 無限制的強度管轄權原則檔。  請務必閱讀 zip 檔案的安裝指示和相關的詳細資料可能的匯出/匯入問題中包含的讀我檔案。  

    - 如果使用 mssql-jdbc-X.X.X.jre7.jar 或 sqljdbc41.jar，可以從下載原則檔[下載 Java 密碼編譯延伸模組 (JCE) 無限制的強度管轄權原則檔 7](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)

    - 如果使用 mssql-jdbc-X.X.X.jre8.jar 或 sqljdbc42.jar，可以從下載原則檔[下載 Java 密碼編譯延伸模組 (JCE) 無限制的強度管轄權原則檔 8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

    - 如果使用 mssql jdbc X.X.X.jre9.jar，沒有原則檔必須先下載。 在 Java 中 9 管轄權原則會預設為無限制的強度的加密。

## <a name="working-with-column-master-key-stores"></a>使用資料行主要金鑰存放區
若要加密或解密資料加密的資料行，SQL Server 會維護資料行加密金鑰。 資料行加密金鑰會儲存在資料庫中繼資料中的加密形式。 每個資料行加密金鑰有對應的資料行主要金鑰是用來加密資料行加密金鑰。 資料庫中繼資料不包含資料行主要金鑰。 這些索引鍵僅會保留用戶端。 不過資料庫中繼資料並包含資料行主要金鑰儲存在用戶端的相對位置的相關資訊。 例如，資料庫中繼資料可能說出的金鑰存放區中保留資料行主要金鑰是 Windows 憑證存放區，以及用來加密和解密的特定憑證的 Windows 憑證存放區中的特定路徑。 如果用戶端可存取該憑證，Windows 憑證存放區中，它可以取得憑證。 憑證可用來解密資料行加密金鑰。 確定加密金鑰會用來解密或加密使用該資料行加密金鑰的加密資料行的資料。

Microsoft JDBC Driver for SQL Server 與金鑰存放區，使用資料行主要金鑰存放區提供者，也就是執行個體的類別衍生自通訊**SQLServerColumnEncryptionKeyStoreProvider**。

### <a name="using-built-in-column-master-key-store-providers"></a>使用內建資料行主要金鑰存放區提供者
Microsoft JDBC Driver for SQL Server 隨附於下列內建的資料行主要金鑰存放區提供者。 這些提供者的某些預先註冊特定的提供者名稱 （用來查閱提供者），且部分需要額外的認證或明確註冊。

| 類別 | Description | 提供者 (查閱) 名稱 |預先註冊嗎？|
|:---|:---|:---|:---|
|**SQLServerColumnEncryptionAzureKeyVaultProvider**| Azure 金鑰保存庫金鑰存放區提供者。| AZURE_KEY_VAULT|否|
|**SQLServerColumnEncryptionCertificateStoreProvider**| Windows 憑證存放區提供者。|MSSQL_CERTIFICATE_STORE|是
|**SQLServerColumnEncryptionJavaKeyStoreProvider**| Java 金鑰存放區提供者|MSSQL_JAVA_KEYSTORE|是|

對於預先註冊的金鑰存放區提供者中，您不需要變更任何應用程式程式碼以使用這些提供者，但請注意下列項目：

- 您 （或您的 DBA） 需要確認設定的資料行主要金鑰中繼資料中的提供者名稱正確，且資料行主要金鑰路徑符合適用於給定的提供者的金鑰路徑格式。 建議您設定使用工具，例如 SQL Server Management Studio，會在發出 CREATE COLUMN MASTER KEY (TRANSACT-SQL) 陳述式時，自動產生有效的提供者名稱和金鑰路徑的索引鍵。
- 確定您的應用程式可以存取金鑰存放區中的索引鍵。 這項工作可能會授與您的應用程式存取金鑰和/或金鑰存放區根據金鑰存放區，或執行其他的金鑰存放區特有的組態步驟。 例如，使用 SQLServerColumnEncryptionJavaKeyStoreProvider，您需要提供的位置和連線內容中的金鑰存放區的密碼。 

所有這些金鑰存放區提供者所述的以下各節中的更多詳細資料。 您只需要實作一個使用永遠加密的金鑰存放區提供者。

### <a name="using-azure-key-vault-provider"></a>使用 Azure 金鑰保存庫提供者
Azure 金鑰保存庫是一個方便的選項來儲存和管理永遠加密的資料行主要金鑰 （特別是如果您的應用程式裝載於 Azure 時）。 Microsoft JDBC Driver for SQL Server 包含內建提供者，SQLServerColumnEncryptionAzureKeyVaultProvider，具有索引鍵儲存在 Azure 金鑰保存庫中的應用程式。 此提供者的名稱是 AZURE_KEY_VAULT。 若要使用 Azure 金鑰保存庫的存放區提供者，應用程式開發人員必須在 Azure 金鑰保存庫中建立保存庫和金鑰和 Azure Active Directory 中建立的應用程式註冊。 已註冊的應用程式必須授與取得，解密，加密、 解除包裝的金鑰、 包裝金鑰，以及確認權限定義為使用 with Always Encrypted 建立金鑰保存庫的存取原則中。 如需有關如何設定金鑰保存庫，以及建立資料行主要金鑰的詳細資訊，請參閱[逐步解說 – Azure 金鑰保存庫](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)和[Azure 金鑰保存庫中建立資料行主要金鑰](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault)。

這個頁面上，如果您已經建立 Azure 金鑰保存庫的範例以基礎的資料行主要金鑰和資料行加密金鑰，使用 SQL Server Management Studio，來重新建立它們的 T-SQL 指令碼看起來類似於這個範例有它自己的特定**KEY_路徑**和**ENCRYPTED_VALUE**:

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',
    KEY_PATH = N'https://<MyKeyValutName>.vault.azure.net:443/keys/Always-Encrypted-Auto1/c61f01860f37302457fa512bb7e7f4e8'
)

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x01BA000001680074507400700073003A002F002F006400610076006...
)
```

若要使用 Azure 金鑰保存庫，用戶端應用程式需要 SQLServerColumnEncryptionAzureKeyVaultProvider 具現化，並向驅動程式。

初始化 SQLServerColumnEncryptionAzureKeyVaultProvider 的範例如下：  

```
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**clientID**是 Azure Active Directory 執行個體中的應用程式註冊的應用程式識別碼。 **clientKey**下該應用程式提供 API 存取 Azure 金鑰保存庫註冊金鑰密碼。

應用程式建立 SQLServerColumnEncryptionAzureKeyVaultProvider 的執行個體之後，應用程式必須向使用 sqlserverconnection.registercolumnencryptionkeystoreproviders （） 方法的驅動程式的執行個體。 強烈建議使用預設查詢名稱 AZURE_KEY_VAULT，可以藉由呼叫 SQLServerColumnEncryptionAzureKeyVaultProvider.getName() API 取得註冊執行個體。 使用預設名稱，可讓您佈建及管理永遠加密金鑰 （工具使用預設名稱來產生資料行主要金鑰的中繼資料物件） 使用 SQL Server Management Studio 或 PowerShell 之類的工具。 下列範例會示範 Azure 金鑰保存庫提供者進行登錄。 如需有關 sqlserverconnection.registercolumnencryptionkeystoreproviders （） 方法的詳細資訊，請參閱[一律加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。

```
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
>  如果您使用 Azure 金鑰保存庫金鑰存放區提供者時，JDBC 驅動程式的 Azure 金鑰保存庫實作具有相依性 （從 GitHub) 必須與您的應用程式包含這些程式庫：
>
>  [azure-sdk-for-java](https://github.com/Azure/azure-sdk-for-java)
>
>  [azure-activedirectory-library-for-java libraries](https://github.com/AzureAD/azure-activedirectory-library-for-java)
>
> 如需如何 Maven 專案中包含這些相依性的範例，請參閱[下載 ADAL4J 和保存的相依性使用 Apache Maven](https://github.com/Microsoft/mssql-jdbc/wiki/Download-ADAL4J-And-AKV-Dependencies-with-Apache-Maven)

### <a name="using-windows-certificate-store-provider"></a>使用 Windows 憑證存放區提供者
SQLServerColumnEncryptionCertificateStoreProvider 可以用來將資料行主要金鑰儲存在 Windows 憑證存放區。 使用 [SQL Server Management Studio (SSMS) 永遠加密精靈] 或其他支援的工具來建立資料行主要金鑰和資料行加密金鑰定義資料庫中。 相同的精靈可以用來產生自我簽署的憑證可用來當做資料行主要金鑰的永遠加密的資料在 Windows 憑證存放區。 如需有關資料行主要金鑰和資料行加密金鑰的 T-SQL 語法的詳細資訊，請參閱[CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)和[CREATE COLUMN 如此 KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md)分別。

SQLServerColumnEncryptionCertificateStoreProvider 名稱是 MSSQL_CERTIFICATE_STORE，而且可以進行查詢 getName() 應用程式開發介面的提供者物件。 它會自動註冊的驅動程式，並可以順暢地使用，而不需要任何應用程式變更。

在此頁面上，如果您已經建立 Windows 憑證存放區範例以基礎的資料行主要金鑰和資料行加密金鑰，使用 SQL Server Management Studio，來重新建立它們的 T-SQL 指令碼可能類似於此範例使用自己的特定**KEY_PATH**和**ENCRYPTED_VALUE**:

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',
    KEY_PATH = N'CurrentUser/My/A2A91F59C461B559E4D962DA9D2BC6131B32CB91'
)

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E0074007500730065007200...
)
```

> [!IMPORTANT]
> 驅動程式支援所有平台上使用這份文件中的其他金鑰存放區提供者時，JDBC 驅動程式的 SQLServerColumnEncryptionCertificateStoreProvider 實作位於只有 Windows 作業系統。 它具有相依性所提供的驅動程式套件中的 sqljdbc_auth.dll 時。 若要使用此提供者，將 sqljdbc_auth.dll 檔案複製到安裝 JDBC 驅動程式的電腦上的 Windows 系統路徑的目錄。 或者，您也可以設定 java.libary.path 系統屬性來指定 sqljdbc_auth.dll 的目錄。 如果您執行的是 32 位元的 Java Virtual Machine (JVM)，即使作業系統為 x64 版，也請使用 x86 資料夾中的 sqljdbc_auth.dll 檔案。 如果您是在 x64 處理器上執行 64 位元的 JVM，請使用 x64 資料夾中的 sqljdbc_auth.dll 檔案。 例如，如果您使用 32 位元的 JVM，JDBC 驅動程式安裝在預設目錄，您可以指定 DLL 的位置啟動的 Java 應用程式時，請使用下列虛擬機器 (VM) 引數： `-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### <a name="using-java-key-store-provider"></a>使用 Java 金鑰存放區提供者
JDBC 驅動程式隨附內建金鑰存放區提供者實作 Java 金鑰存放區。 如果**keyStoreAuthentication**連接字串屬性出現在連接字串和其設定為"JavaKeyStorePassword"，驅動程式會自動具現化，並註冊 Java 金鑰存放區提供者。 Java 金鑰存放區提供者的名稱是 MSSQL_JAVA_KEYSTORE。 此名稱也可以使用 SQLServerColumnEncryptionJavaKeyStoreProvider.getName() API 來查詢。 

有三個連接字串屬性可讓用戶端應用程式，可指定驅動程式必須向 Java 金鑰存放區的認證。 驅動程式初始化提供者，根據連接字串中這三個屬性的值。

**keyStoreAuthentication:**識別要使用的 Java 金鑰存放區。 Microsoft JDBC driver 6.0 和更新版本的 SQL Server，您可以驗證這個屬性只能透過 Java 金鑰存放區。 Java 金鑰存放區中，這個屬性的值必須是`JavaKeyStorePassword`。

**keyStoreLocation:**儲存資料行主要金鑰的 Java 金鑰存放區檔案的路徑。 路徑中包含的金鑰存放區檔案名稱。

**keyStoreSecret:**密碼/密碼用於 keystore 和索引鍵。 使用 Java 金鑰存放區，金鑰存放區和金鑰的密碼必須相同。

提供這些認證連接字串中的範例如下：

```
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

您也可以取得或設定使用 SQLServerDataSource 物件的這些設定。 如需詳細資訊，請參閱[一律加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。

JDBC 驅動程式會自動具現化 SQLServerColumnEncryptionJavaKeyStoreProvider 時這些認證會在連接屬性。

### <a name="creating-a-column-master-key-for-the-java-key-store"></a>建立 Java 金鑰存放區資料行主要金鑰
SQLServerColumnEncryptionJavaKeyStoreProvider 可以搭配 JKS 或 PKCS12 金鑰存放區型別。 若要建立或匯入要與此提供者所使用的金鑰會使用 Java [keytool](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html)公用程式。 索引鍵必須有自己的金鑰存放區為相同的密碼。 如何建立公開金鑰和其相關聯的私密金鑰使用 keytool 公用程式的範例如下：

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

此命令會建立公開金鑰，並將它包裝在自我簽署憑證，會儲存在金鑰存放區 'keystore.jks' 以及其相關聯的私密金鑰的 X.509。 別名 'AlwaysEncryptedKey' 識別的金鑰存放區中此項目。

以下是相同的使用 PKCS12 存放區類型的範例：

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

如果金鑰存放區是型別 PKCS12，keytool 公用程式不會提示輸入金鑰的密碼和金鑰的密碼必須提供-keypass 選項，因為 SQLServerColumnEncryptionJavaKeyStoreProvider 需要金鑰存放區和索引鍵具有相同密碼。

您也可以從 Windows 憑證存放區，以.pfx 格式匯出憑證，並使用可搭配 SQLServerColumnEncryptionJavaKeyStoreProvider。 匯出的憑證也可匯入 Java 金鑰存放區為 JKS 金鑰存放區型別。

建立之後的 keytool 項目，建立資料行主要金鑰中繼資料在資料庫中，需要金鑰存放區提供者名稱和金鑰的路徑。 如需有關如何建立資料行主要金鑰中繼資料的詳細資訊，請參閱[CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)。 SQLServerColumnEncryptionJavaKeyStoreProvider，機碼路徑是索引鍵的別名，SQLServerColumnEncryptionJavaKeyStoreProvider 的名稱是 'MSSQL_JAVA_KEYSTORE'。 您也可以查詢此使用 getName() SQLServerColumnEncryptionJavaKeyStoreProvider 類別的公用 API 的名稱。 

建立資料行主要金鑰的 T-SQL 的語法是：

```
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
)
```

資料行主要金鑰定義 'AlwaysEncryptedKey' 上面所建立，將會是：

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```

> [!NOTE]
> 內建的 SQL Server management Studio 功能無法建立 Java 金鑰存放區的資料行主要金鑰定義。 必須以程式設計方式使用 T-SQL 命令。

### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>建立 Java 金鑰存放區資料行加密金鑰
SQL Server Management Studio 或任何其他工具，都無法用來建立資料行使用 Java 金鑰存放區中的資料行主要金鑰的加密金鑰。 用戶端應用程式必須建立以程式設計方式使用 SQLServerColumnEncryptionJavaKeyStoreProvider 類別資料行加密金鑰。 如需詳細資訊，請參閱[用於資料行主要金鑰存放區提供者以程式設計方式佈建金鑰](#using-column-master-key-store-providers-for-programmatic-key-provisioning)。

### <a name="implementing-a-custom-column-master-key-store-provider"></a>實作自訂資料行主要金鑰存放區提供者
如果您想要在現有的提供者不支援的金鑰存放區儲存資料行主要金鑰，您可以實作自訂提供者擴充 SQLServerColumnEncryptionKeyStoreProvider 類別，以及註冊使用的提供者Sqlserverconnection.registercolumnencryptionkeystoreproviders （） 方法。

```
public class MyCustomKeyStore extends SQLServerColumnEncryptionKeyStoreProvider{  
    private String name = "MY_CUSTOM_KEYSTORE";

    public void setName(String name)
    {
        this.name = name;
    }

    public String getName()
    {
        return name;
    }

    public byte[] encryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)
    {
        // Logic for encrypting the column encryption key
    }

    public byte[] decryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)
    {
        // Logic for decrypting the column encryption key
    }
}
```

註冊提供者：

```
SQLServerColumnEncryptionKeyStoreProvider storeProvider = new MyCustomKeyStore();
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(storeProvider.getName(), storeProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

## <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>使用資料行主要金鑰存放區提供者以程式設計方式佈建金鑰
當存取加密資料行時，Microsoft JDBC Driver for SQL Server 會明確地尋找並呼叫正確的資料行主要金鑰存放區提供者來解密資料行加密金鑰。 一般來說，一般應用程式程式碼不會直接呼叫資料行主要金鑰存放區提供者。 不過，您可以具現化並呼叫提供者以程式設計方式來佈建和管理永遠加密金鑰。 在完成此步驟中產生加密的資料行加密金鑰，例如作為部分資料行主要金鑰輪替，解密資料行加密金鑰。 如需詳細資訊，請參閱 [永遠加密的金鑰管理概觀](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。

如果您使用自訂金鑰存放區提供者時，可能必須使用實作您自己的金鑰管理工具。 在使用儲存在 Windows 憑證存放區或 Azure 金鑰保存庫中的金鑰時，您可以使用現有的工具，例如 SQL Server Management Studio 或 PowerShell，來管理和佈建金鑰。 當使用 Java 金鑰存放區中的金鑰時，您需要以程式設計方式佈建金鑰。 下列範例說明使用 SQLServerColumnEncryptionJavaKeyStoreProvider 類別來加密金鑰儲存在 Java 金鑰存放區索引鍵。

```
import java.sql.*;
import javax.xml.bind.DatatypeConverter;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programmatically for the Java Key Store.
 */
public class AlwaysEncrypted
{
    // Alias of the key stored in the keystore.
    private static String keyAlias = "<proide key alias>";

    // Name by which the column master key will be known in the database.
    private static String columnMasterKeyName = "MyCMK";

    // Name by which the column encryption key will be known in the database.
    private static String columnEncryptionKey = "MyCEK";

    // The location of the keystore.
    private static String keyStoreLocation = "C:\\Dev\\Always Encrypted\\keystore.jks";

    // The password of the keystore and the key.
    private static char[] keyStoreSecret = "********".toCharArray();

    /**
     * Name of the encryption algorithm used to encrypt the value of
     * the column encryption key. The algorithm for the system providers must be RSA_OAEP.
     */
    private static String algorithm = "RSA_OAEP";

    public static void main(String[] args)
    {
        String connectionString = GetConnectionString();
        try
        {
            // Note: if you are not using try-with-resources statements (as here),
            // you must remember to call close() on any Connection, Statement,
            // ResultSet objects that you create.

            // Open a connection to the database.
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))
            {
                // Instantiate the Java Key Store provider.
                SQLServerColumnEncryptionKeyStoreProvider storeProvider =
                        new SQLServerColumnEncryptionJavaKeyStoreProvider(
                                keyStoreLocation,
                                keyStoreSecret);

                byte [] encryptedCEK=getEncryptedCEK(storeProvider);

                /**
                 * Create column encryption key
                 * For more details on the syntax, see:
                 * https://docs.microsoft.com/sql/t-sql/statements/create-column-encryption-key-transact-sql
                 * Encrypted column encryption key first needs to be converted into varbinary_literal from bytes, 
                 * for which DatatypeConverter.printHexBinary is used
                 */
                String createCEKSQL = "CREATE COLUMN ENCRYPTION KEY "
                        + columnEncryptionKey
                        + " WITH VALUES ( "
                        + " COLUMN_MASTER_KEY = "
                        + columnMasterKeyName
                        + " , ALGORITHM =  '"
                        + algorithm
                        + "' , ENCRYPTED_VALUE =  0x"
                        + DatatypeConverter.printHexBinary(encryptedCEK)
                        + " ) ";

                try (Statement cekStatement = sourceConnection.createStatement())
                {
                    cekStatement.executeUpdate(createCEKSQL);
                    System.out.println("Column encryption key created with name : " + columnEncryptionKey);
                }
            }
        }
        catch (Exception e)
        {
            // Handle any errors that may have occurred.
            e.printStackTrace();
        }
    }

    // To avoid storing the sourceConnection String in your code,
    // you can retrieve it from a configuration file.
    private static String GetConnectionString()
    {
        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +
                "databaseName=ae2;user=sa;password=********;";

        return connectionUrl;
    }

    private static byte[] getEncryptedCEK(SQLServerColumnEncryptionKeyStoreProvider storeProvider) throws SQLServerException
    {
        /**
         * Following arguments needed by SQLServerColumnEncryptionJavaKeyStoreProvider
         * 1) keyStoreLocation :
         *      Path where keystore is located, including the keystore file name.
         * 2) keyStoreSecret :
         *      Password of the keystore and the key.
         */
        String plainTextKey = "You need to give your plain text";

        // plainTextKey has to be 32 bytes with current algorithm supported
        byte[] plainCEK = plainTextKey.getBytes();

        // This will give us encrypted column encryption key in bytes
        byte[] encryptedCEK = storeProvider.encryptColumnEncryptionKey(
                keyAlias,
                algorithm,
                plainCEK);

        return encryptedCEK;
    }
}
```

## <a name="enabling-always-encrypted-for-application-queries"></a>為應用程式查詢啟用 [永遠加密]
若要啟用加密參數及解密的目標加密資料行的查詢結果的最簡單方式是藉由設定的值**columnEncryptionSetting**連接字串關鍵字設**已啟用**.

下列連接字串是 JDBC 驅動程式中啟用 永遠加密的範例：

```
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);
```

下列程式碼是使用 SQLServerDataSource 物件的對等範例：

```
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("localhost");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");
SQLServerConnection con = (SQLServerConnection) ds.getConnection();
```

個別查詢也可以啟用 [永遠加密]。 如需詳細資訊，請參閱[控制永遠加密的效能影響](#controlling-the-performance-impact-of-always-encrypted)。 啟用 永遠加密不足，無法加密或解密成功。 您還需要確定︰
- 應用程式要有 [檢視任何資料行的主要金鑰定義] 和 [檢視任何資料行的加密金鑰定義] 資料庫權限，才能存取資料庫中永遠加密金鑰的相關中繼資料。 如需詳細資訊，請參閱[中一律加密 (Database Engine) 的權限](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)。
- 應用程式可以存取資料行主要金鑰所保護的資料行加密金鑰，加密查詢的資料庫資料行。 若要使用的 Java 金鑰存放區提供者，您需要提供額外的認證，連接字串中。 如需詳細資訊，請參閱[使用 Java 金鑰存放區提供者](#using-java-key-store-provider)。

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>設定如何將 java.sql.Time 值傳送至伺服器
**SendTimeAsDatetime**連接屬性用來設定如何將 java.sql.Time 值傳送至伺服器。 設為 false 時，時間值傳送為 SQL Server 的時間類型。 何時設為 true 的值傳送為 datetime 類型的時間。 如果時間資料行已加密， **sendTimeAsDatetime**屬性必須為 false，因為加密資料行不支援時間轉換成日期時間。 也請注意，這個屬性會預設為 true，所以必須使用加密的時間資料行時將它設定為 false。 否則，此驅動程式將會擲回例外狀況。 SQLServerConnection 類別從驅動程式 6.0 版開始，有兩種方法，以程式設計方式設定這個屬性的值：
 
* public void setSendTimeAsDatetime (sendTimeAsDateTimeValue 布林值)
* public boolean getSendTimeAsDatetime()

如需有關這個屬性的詳細資訊，請參閱[如何設定 java.sql.Time 值傳送給伺服器](configuring-how-java-sql-time-values-are-sent-to-the-server.md)。

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>設定字串值如何傳送至伺服器
**SendStringParametersAsUnicode**連接屬性用來設定如何將字串值傳送至 SQL Server。 如果設為 true，字串參數傳送到伺服器以 Unicode 格式。 如果設為 false，字串參數會以非 Unicode 格式，例如 ASCII 或 MBCS，而非 Unicode 傳送。 這個屬性的預設值為 true。 當啟用 永遠加密，加密 char/varchar/varchar(max) 資料行、 值**sendStringParametersAsUnicode**必須設為 true （或保留為預設值）。 如果這個屬性設定為 false 時，驅動程式會擲回例外狀況時，將加密的 char/varchar/varchar(max) 資料行的資料插入。 如需有關這個屬性的詳細資訊，請參閱[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>擷取和修改加密資料行中的資料
一旦您啟用 永遠加密的應用程式查詢，您可以使用標準的 JDBC Api 來擷取或修改加密的資料庫資料行中的資料。 如果您的應用程式具有必要的資料庫權限，而且可以存取資料行主要金鑰，驅動程式會加密目標加密資料行，以及解密擷取自加密資料行之資料的任何查詢參數。

如未啟用 [永遠加密]，使用目標加密資料行參數的查詢就會失敗。 只要查詢沒有以加密的資料行為目標的無參數查詢仍然可以從加密資料行擷取資料。 不過，驅動程式不會嘗試解密擷取自加密資料行的任何值，而且應用程式將會收到二進位的加密的資料 （以位元組陣列）。

下表摘要說明根據是否啟用 永遠加密或不查詢的行為：

|查詢特性 | [永遠加密] 已啟用，且應用程式可以存取金鑰和金鑰中繼資料|[永遠加密] 已啟用，但應用程式不能存取金鑰或金鑰中繼資料 | [永遠加密] 已停用|
|:---|:---|:---|:---|
| 有以加密資料行為目標之參數的查詢。 | 以清晰簡明的方式加密參數值。 | 錯誤 | 錯誤|
| 查詢擷取自加密資料行的資料，不含加密的資料行為目標的參數。| 以清晰簡明的方式解密來自加密資料行的結果。 應用程式接收加密的資料行設定之 SQL Server 類型對應的 JDBC 資料類型的純文字值。 | 錯誤 | 不解密來自加密資料行的結果。 應用程式收到位元組陣列 (byte[]) 形態的加密值。

### <a name="inserting-and-retrieving-encrypted-data-examples"></a>插入及擷取加密的資料範例 
以下範例將說明擷取和修改加密資料行中的資料。 這些範例假設目標資料表具有下列結構描述和加密的 SSN 和 BirthDate 資料行。 如果您已設定名為資料行主要金鑰 」 MyCMK"和資料行加密金鑰名為"MyCEK 」 （如在先前的金鑰存放區提供者章節所述），您可以建立使用這個指令碼的資料表：

```
CREATE TABLE [dbo].[Patients]([PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

每個 Java 程式碼範例中，您必須將金鑰存放區專屬的程式碼中所述的位置。

如果您使用 Azure 金鑰保存庫金鑰存放區提供者：

```
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
```

如果您使用 Windows 憑證存放區的金鑰存放區提供者：

```
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
```

如果您使用 Java 金鑰存放區的金鑰存放區提供者：

```
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### <a name="inserting-data-example"></a>插入資料範例
本例會將資料列插入病患資料表。 請注意下列事項：
- 範例程式碼中沒有任何需要加密的特定項目。 Microsoft JDBC Driver for SQL Server 會自動偵測，並會加密目標加密資料行的參數。 此行為可以讓加密應用程式。
- 插入至資料庫資料行，包括加密的資料行的值會當做參數使用 SQLServerPreparedStatement 傳遞。 雖然使用參數是選擇性的值傳送至非加密的資料行 （不過，強烈建議因有利於防止 SQL 資料隱碼） 時，它是所需目標加密資料行的值。 如果傳遞做為內嵌在查詢陳述式中的常值插入加密的資料行的值，則查詢會失敗，因為驅動程式會無法判斷目標加密資料行中的值，而且不會加密值。 結果，伺服器會因與加密資料行不相容而拒絕它們。
- 列印程式的所有值都會以純文字形式 Microsoft JDBC Driver for SQL Server 會以透明的方式解密擷取自加密資料行的資料。
- 如果您查詢，使用 WHERE 子句，在 WHERE 子句必須用來使驅動程式可以以透明的方式加密它傳送至資料庫之前，做為參數傳遞的值。 在下列範例中，SSN 做為參數傳遞，但 [姓氏] 會為常值如 LastName 不會加密。
- SSN 資料行為目標的參數使用的 setter 方法是 setString()，對應到 char/varchar SQL Server 資料類型。 如果這個參數，所使用的 setter 方法為 setNString()，對應至 nchar/nvarchar，則查詢會失敗，因為永遠加密 不支援加密的 nchar/nvarchar 值轉換成加密的 char/varchar 值。

```
try
{
    <Insert keystore-specific code here>

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String insertRecord="INSERT INTO [dbo].[Patients] VALUES (?, ?, ?, ?)";
        try (PreparedStatement insertStatement = sourceConnection.prepareStatement(insertRecord))
        {
            insertStatement.setString(1, "795-73-9838");
            insertStatement.setString(2, "Catherine");
            insertStatement.setString(3, "Abel");
            insertStatement.setDate(4, Date.valueOf("1996-09-10"));
            insertStatement.executeUpdate();
            System.out.println("1 record inserted.\n");
        }
    }
}
catch (Exception e)
{
    e.printStackTrace();
}
```

### <a name="retrieving-plaintext-data-example"></a>擷取純文字資料範例
下列範例會示範根據加密的值以及從加密資料行擷取純文字資料的篩選資料。 請注意下列事項：
- 在 WHERE 子句來篩選 SSN 資料行必須用於使 Microsoft JDBC Driver for SQL Server 可以明確地加密它傳送至資料庫之前，做為參數傳遞的值。
- 列印程式的所有值都會以純文字形式 Microsoft JDBC Driver for SQL Server 會以透明的方式解密從 SSN 和 BirthDate 資料行擷取的資料。

> [!NOTE]
> 如果使用決定性加密進行加密的資料行，查詢就可以在其上執行相等比較。 如需詳細資訊，請參閱[永遠加密 (Database Engine) 中的選取具確定性或隨機化加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)。

```
try
{
    <Insert keystore-specific code here>

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = ?;";
    
        try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))
        {
            selectStatement.setString(1, "795-73-9838");
            ResultSet rs = selectStatement.executeQuery();
            while(rs.next())
            {
                System.out.println("SSN: " +rs.getString("SSN") +
                    ", FirstName: " + rs.getString("FirstName") +
                    ", LastName:"+ rs.getString("LastName")+
                    ", Date of Birth: " + rs.getString("BirthDate"));
            }
        }
    }
}
catch (Exception e)  
{  
    e.printStackTrace();  
}
```
  
### <a name="retrieving-encrypted-data-example"></a>擷取加密的資料範例
如未啟用 [永遠加密]，只要查詢沒有以加密資料行為目標的參數，查詢就仍然可以從加密資料行擷取資料。

下列範例說明從加密資料行擷取二進位的加密的資料。 請注意下列事項：
- 連接字串中未啟用永遠加密，所以查詢會傳回加密的 SSN 和 BirthDate 值作為位元組陣列 （程式會將值轉換為字串）。
- 從加密資料行擷取資料但停用 [永遠加密] 的查詢可以有參數，只要沒有任何參數以加密資料行為目標。 下列查詢依 LastName 篩選的未加密的資料庫中。 如果依 SSN 或 BirthDate 篩選查詢，查詢會失敗。

```
try
{
    String connectionString  = "jdbc:sqlserver://localhost:1433;" + "databaseName=Clinic;user=sa;password=******";

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;";

        try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))
        {
            selectStatement.setString(1, "Abel");
            ResultSet rs = selectStatement.executeQuery();
            while (rs.next())
            {
                System.out.println("SSN: " + rs.getString("SSN") +
                    ", FirstName: " + rs.getString("FirstName") +
                    ", LastName:"+ rs.getString("LastName") +
                    ", Date of Birth: " + rs.getString("BirthDate"));
            }
        }
    }
}
catch (Exception e)
{
    e.printStackTrace();
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>避免常見的加密資料行查詢問題
本章節描述常見的錯誤類別，當查詢加密資料行從 Java 應用程式和如何加以避免的一些指導方針。

### <a name="unsupported-data-type-conversion-errors"></a>不支援的資料類型轉換錯誤
[永遠加密] 支援極少數的加密資料類型轉換。 請參閱[一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)支援的類型轉換詳細清單。 以下是您可以如何避免資料類型轉換錯誤。 請確認：

- 傳遞參數值的目標加密資料行時，您可以使用適當的 setter 方法。 請確定參數的 SQL Server 資料型別正是目標資料行的類型相同，或資料行的目標型別參數的 SQL Server 資料類型的轉換支援。 API 方法已加入為 SQLServerPreparedStatement、 SQLServerCallableStatement 和 SQLServerResultSet 類別傳遞參數對應到特定的 SQL Server 資料類型。 例如，如果資料行不會加密可用 setTimestamp() 方法來將參數傳遞至 datetime2 或 datetime 資料行。 但是，資料行加密時必須使用表示在資料庫中資料行的類型的確切方法。 例如，將值傳遞至加密的 datetime2 資料行，並將值傳遞到加密的日期時間資料行使用 setDateTime() 使用 setTimestamp()。 請參閱[一律加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)的新應用程式開發介面的完整清單。
- 以小數和數值 SQL Server 資料類型資料行為目標之參數的有效位數和小數位數，和為目標資料行設定的有效位數和小數位數相同。 API 方法已加入為 SQLServerPreparedStatement、 SQLServerCallableStatement 和 SQLServerResultSet 類別接受有效位數和小數位數，以及代表 decimal 和 numeric 資料類型的參數/資料行的資料值。 請參閱[一律加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)的新/多載的應用程式開發介面的完整清單。  
- 小數秒數有效位數/小數位數 datetime2、 datetimeoffset 或時間 SQL Server 資料類型資料行為目標的參數不是大於小數秒數有效位數/小數位數的目標資料行中修改的目標資料行值的查詢. API 方法已加入為 SQLServerPreparedStatement、 SQLServerCallableStatement 和 SQLServerResultSet 類別接受小數秒有效位數/小數位數以及代表這些資料型別參數的資料值。 如需新/多載的應用程式開發介面的完整清單，請參閱[一律加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。   

### <a name="errors-due-to-incorrect-connection-properties"></a>因為不正確的連接屬性的錯誤
本章節描述如何設定以使用一律加密資料的連接設定。 加密的資料類型支援有限的轉換，因為**sendTimeAsDatetime**和**sendStringParametersAsUnicode**連接設定使用加密的資料行時，需要適當的組態設定。 請確認： 
- [sendTimeAsDatetime](setting-the-connection-properties.md)連接設定為 false，將資料插入加密時間資料行時。 如需詳細資訊，請參閱[設定 java.sql.Time 值如何傳送至伺服器](configuring-how-java-sql-time-values-are-sent-to-the-server.md)。
- [sendStringParametersAsUnicode](setting-the-connection-properties.md)連接設定設定為 true （或保留為預設值） 時將資料插入加密的 char/varchar/varchar(max) 資料行。

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>因為傳送純文字，而不是傳送加密值所造成的錯誤。
任何以加密資料行為目標的值都需要在應用程式內加密。 嘗試插入/修改或篩選加密的資料行上以純文字值會產生類似以下錯誤：

```
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

若要避免這類錯誤，請確定︰
- 永遠加密 已啟用的應用程式 （連接字串，或以特定的查詢） 的加密的資料行為目標的查詢。
- 您使用備妥的陳述式和參數來傳送資料的目標加密資料行。 下列範例會顯示錯誤篩選常值/常數對加密資料行 (SSN)，而不是做為參數傳遞內常值的查詢。 此查詢將會失敗：

```
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## <a name="force-encryption-on-input-parameters"></a>輸入參數上強制加密
使用永遠加密時，[強制加密] 功能會強制加密參數。 如果使用強制加密，而且 SQL Server 通知驅動程式參數不需要加密，使用參數的查詢將會失敗。 此屬性會針對受到安全性攻擊危害的 SQL Server 提供額外的保護，此類 SQL Server 會將不正確的加密中繼資料提供給用戶端，而可能導致資料洩露。 設定 * 方法在 SQLServerPreparedStatement 和 SQLServerCallableStatement 類別和更新\*SQLServerResultSet 類別的方法多載接受布林值的引數來指定 [強制加密] 設定。 如果這個引數的值為 false，驅動程式將不會強制加密參數。 強制加密 」 設定為 true，查詢參數才會傳送目的地資料行已加密，並啟用 永遠加密的連接時或在陳述式。 使用這個屬性可讓一層額外的安全性，確保，驅動程式不會不小心傳送資料到 SQL Server 以純文字時預期要加密。

[強制加密] 設定使用 SQLServerPreparedStatement 和 SQLServerCallableStatement 方法多載資訊，請參閱[一律加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>控制永遠加密的效能影響
因為永遠加密 」 是用戶端加密技術，大部分的效能負擔是在用戶端，不是在資料庫觀察到。 除了加密和解密作業成本，其他的用戶端上的效能額外負荷來源如下：
- 額外反覆存取資料庫以擷取查詢參數的中繼資料。
- 呼叫資料行主要金鑰存放區以存取資料行主要金鑰。

本章節描述 Microsoft JDBC 驅動程式中的內建效能最佳化，適用於 SQL Server 和如何控制上述兩個因素對效能的影響。

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>控制反覆存取以擷取查詢參數的中繼資料
如果連接啟用一律加密時，預設驅動程式會呼叫[sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)每個參數化查詢，將查詢陳述式 （不含任何參數值） 傳遞至 SQL Server。 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)會分析查詢陳述式，以了解如果任何參數需要加密，而且如果是，針對每一個它傳回加密相關的資訊，讓驅動程式來加密參數值。 此行為可確保高層級的透明度，用戶端應用程式。 只要應用程式會使用參數來傳遞目標驅動程式的加密資料行的值，應用程式 （及應用程式開發人員） 並不需要知道哪些查詢存取加密資料行。

### <a name="setting-always-encrypted-at-the-query-level"></a>在查詢層級設定 [永遠加密]
若要控制擷取參數化查詢的加密中繼資料的效能影響，您可以啟用 永遠加密的個別查詢，而不是設定進行連接。 僅適用於您知道有以加密的資料行為目標之參數的查詢，如此一來可以確保 sys.sp_describe_parameter_encryption 會叫用。 不過請注意，這麼做會降低加密的透明度： 如果您變更資料庫資料行的加密屬性，您可能需要變更您的應用程式，以配合結構描述變更的程式碼。

若要控制個別查詢的永遠加密行為，您必須設定個別的陳述式物件，藉由傳遞列舉 SQLServerStatementColumnEncryptionSetting，指定將如何傳送和接收時讀取和寫入資料針對該特定陳述式的加密資料行。 以下是一些實用的方針：
- 如果用戶端應用程式透過資料庫連接傳送的大多數查詢存取加密資料行，請使用下列方針：
    - 設定**columnEncryptionSetting**連接字串關鍵字設**啟用**。
    - 不會存取任何加密資料行的個別查詢設定 SQLServerStatementColumnEncryptionSetting.Disabled。 這項設定將會停用呼叫 sys.sp_describe_parameter_encryption 以及嘗試解密結果集內的任何值。
    - 設定 SQLServerStatementColumnEncryptionSetting.ResultSet 個別查詢沒有任何參數要求加密，但從加密資料行擷取資料。 這項設定將會停用呼叫 sys.sp_describe_parameter_encryption 和參數加密。 查詢將能夠解密來自加密資料行的結果。
- 如果用戶端應用程式透過資料庫連接傳送的大多數查詢都不會存取加密資料行，請使用下列方針：
    - 設定**columnEncryptionSetting**連接字串關鍵字設**已停用**。
    - 如有任何參數需要加密的個別查詢設定 SQLServerStatementColumnEncryptionSetting.Enabled。 此設定可讓呼叫 sys.sp_describe_parameter_encryption 以及解密擷取自加密資料行的任何查詢結果。
    - 設定 SQLServerStatementColumnEncryptionSetting.ResultSet 並沒有任何參數要求加密，但從加密資料行擷取資料的查詢。 這項設定將會停用呼叫 sys.sp_describe_parameter_encryption 和參數加密。 查詢將能夠解密來自加密資料行的結果。

SQLServerStatementColumnEncryptionSetting 設定不會用來略過加密並存取純文字資料。 如需有關如何在陳述式上設定資料行加密的詳細資訊，請參閱[一律加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。  

在下列範例中，永遠加密已停用資料庫連接。 此查詢的應用程式問題有參數以 LastName 資料行未加密為目標。 查詢會從加密的 SSN 和 BirthDate 資料行擷取資料。 在這種情況下，不需要呼叫 sys.sp_describe_parameter_encryption 以擷取加密中繼資料。 不過，查詢結果的解密必須啟用，讓應用程式可以從兩個加密的資料行接收純文字值。 請確認用於 SQLServerStatementColumnEncryptionSetting.ResultSet 設定。

```
// Assumes the same table definition as in Section "Retrieving and modifying data in encrypted columns"
// where only SSN and BirthDate columns are encrypted in the database.
String connectionUrl = "jdbc:sqlserver://localhost;databaseName=ae;user=sa;password=******;"
        + "keyStoreAuthentication=JavaKeyStorePassword;"
        + "keyStoreLocation=" + keyStoreLocation + ";"
        + "keyStoreSecret=******;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);

String filterRecord="SELECT FirstName, LastName, SSN, BirthDate FROM " + tblName + " WHERE LastName = ?";
PreparedStatement selectStatement = connection.prepareStatement(
        filterRecord,
        ResultSet.TYPE_FORWARD_ONLY,
        ResultSet.CONCUR_READ_ONLY,
        connection.getHoldability(),
        SQLServerStatementColumnEncryptionSetting.ResultSetOnly);
selectStatement.setString(1, "Abel");
ResultSet rs = selectStatement.executeQuery();
while(rs.next()) {
    System.out.println("First name: " + rs.getString("FirstName"));
    System.out.println("Last name: " + rs.getString("LastName"));
    System.out.println("SSN: " + rs.getString("SSN"));
    System.out.println("Date of Birth: " + rs.getDate("BirthDate"));
}
rs.close();
selectStatement.close();
connection.close();
```

### <a name="column-encryption-key-caching"></a>資料行加密金鑰快取
若要減少資料行主要金鑰存放區來解密資料行加密金鑰的呼叫次數，Microsoft JDBC Driver for SQL Server 會快取在記憶體中的純文字資料行加密金鑰。 從資料庫中繼資料中接收加密的資料行加密金鑰值之後，驅動程式會先嘗試尋找對應加密金鑰值的純文字資料行加密金鑰。 驅動程式會呼叫金鑰存放區包含資料行主要金鑰，只有當快取中找不到加密的資料行加密金鑰值。

您可以使用 SQLServerConnection 類別中的 API，setColumnEncryptionKeyCacheTtl()，快取中設定存留時間值的資料行加密金鑰的項目。 資料行加密金鑰項目在快取中的預設存留時間值為 2 小時。 若要關閉快取，請使用值為 0。 若要設定任何存留時間值，請使用下列 API:

```
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

例如，若要設定存留時間值為 10 分鐘，請使用：

```
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

做為時間單位支援只天、 小時、 分鐘或秒數。  

## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>複製使用 SQLServerBulkCopy 的加密的資料
使用 SQLServerBulkCopy，您可以複製已加密並儲存到另一個資料表的一個資料表中不需要解密資料的資料。 若要這麼做︰

- 請確定目標資料表的加密組態與來源資料表的組態完全一致。 特別的是，這兩個資料表必須有相同的資料行加密，而且必須使用相同的加密類型和相同的加密金鑰來加密資料行。 如果任何目標資料行加密的方式不同於其對應的來源資料行，您將無法解密目標資料表中的資料複製作業之後。 資料會損毀。
- 設定這兩個資料庫連線到來源資料表和目標資料表沒有啟用 永遠加密。
- 設定 allowEncryptedValueModifications 選項。 如需詳細資訊，請參閱[JDBC 驅動程式使用大量複製](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)。

> [!NOTE]
> 當這個選項可能會導致這些資料庫損毀，因為 Microsoft JDBC Driver for SQL Server 不會檢查資料確實加密，或是正確加密使用相同的加密指定 AllowEncryptedValueModifications 時請特別小心類型、 演算法和金鑰設成目標資料行。

## <a name="see-also"></a>另請參閱
[Always Encrypted (資料庫引擎)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
