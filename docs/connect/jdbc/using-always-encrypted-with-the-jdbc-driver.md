---
title: JDBC 驅動程式搭配使用 Always Encrypted |Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4659c6571f8afbcdb757141e03df51ac54d0835e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52510724"
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>搭配使用 Always Encrypted 與 JDBC 驅動程式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

此頁面提供有關如何開發 Java 應用程式使用的資訊[Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)和 Microsoft JDBC Driver 6.0 （或更新版本） for SQL Server。

Always Encrypted 可讓用戶端加密敏感性資料，而且永遠不會向 SQL Server 或 Azure SQL Database 顯示資料或加密金鑰。 Microsoft JDBC Driver 6.0 (或更高版本) for SQL Server 等啟用了 Always Encrypted 的驅動程式，以清晰簡明的方式加密與解密用戶端應用程式中的敏感性資料，達成此行為。 驅動程式會自動判斷哪一個查詢參數對應至 Always Encrypted 的資料庫資料行，然後加密這些參數的值後, 才會將它們傳送到 SQL Server 或 Azure SQL Database。 同樣地，驅動程式會以清晰簡明的方式，將擷取自查詢結果的加密資料庫資料行資料進行解密。 如需詳細資訊，請參閱 < [Always Encrypted （資料庫引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)並[永遠加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。

## <a name="prerequisites"></a>Prerequisites
- 請確定 Microsoft JDBC Driver 6.0 （或更新版本） 的開發電腦上安裝 SQL Server。 
- 下載並安裝 Java 密碼編譯延伸模組 (JCE) 無限制的強度管轄權原則檔。  請務必閱讀 ZIP 檔案中的讀我檔案，以了解安裝指示及可能的匯出/匯入問題相關詳細資料。  

    - 如果使用 mssql-jdbc-X.X.X.jre7.jar 或 sqljdbc41.jar，則可以從[下載 Java 密碼編譯延伸模組 (JCE) 無限制的強度管轄權原則檔 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html) 下載原則檔

    - 如果使用 mssql-jdbc-X.X.X.jre8.jar 或 sqljdbc42.jar，則可以從[下載 Java 密碼編譯延伸模組 (JCE) 無限制的強度管轄權原則檔 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) 下載原則檔

    - 如果使用 mssql jdbc X.X.X.jre9.jar，任何原則檔案不需要下載。 在 Java 9 的管轄權原則預設為無限制的強度的加密。

## <a name="working-with-column-master-key-stores"></a>使用資料行主要金鑰存放區
若要加密或解密加密的資料行的資料，SQL Server 會維護資料行加密金鑰。 資料行加密金鑰是以加密形式存放在資料庫中繼資料。 每個資料行加密金鑰都有對應的資料行主要金鑰，主要金鑰是用於加密資料行加密金鑰。 資料庫中繼資料不包含資料行主要金鑰。 這些金鑰是僅會保留用戶端。 不過資料庫中繼資料包含資料行主要金鑰相對於用戶端的儲存位置的相關資訊。 例如，資料庫中繼資料可能假設，保存資料行主要金鑰是 Windows 憑證存放區，以及用來加密和解密的特定憑證是在 Windows 憑證存放區中的特定路徑上找到的金鑰存放區。 如果用戶端會有該憑證的存取權的 Windows 憑證存放區，它可以取得憑證。 憑證可用來解密資料行加密金鑰。 然後該加密金鑰可用來解密或加密使用該資料行加密金鑰的加密資料行的資料。

Microsoft JDBC Driver for SQL Server 通訊金鑰儲存區，使用資料行主要金鑰存放區提供者，也就是類別的執行個體衍生自**SQLServerColumnEncryptionKeyStoreProvider**。

### <a name="using-built-in-column-master-key-store-providers"></a>使用內建資料行主要金鑰存放區提供者
Microsoft JDBC Driver for SQL Server 隨附於下列內建的資料行主要金鑰存放區提供者。 這些提供者的一些預先註冊使用特定提供者名稱 （用以查閱提供者而定） 和一些需要額外的認證或明確註冊。

| 類別                                                 | Description                                        | 提供者 (查閱) 名稱  | 預先註冊嗎？ |
| :---------------------------------------------------- | :------------------------------------------------- | :---------------------- | :----------------- |
| **SQLServerColumnEncryptionAzureKeyVaultProvider**    | Azure 金鑰保存庫金鑰儲存區提供者。 | AZURE_KEY_VAULT         | 否                 |
| **SQLServerColumnEncryptionCertificateStoreProvider** | Windows 憑證存放區的提供者。      | MSSQL_CERTIFICATE_STORE | 是                |
| **SQLServerColumnEncryptionJavaKeyStoreProvider**     | Java 金鑰存放區提供者                   | MSSQL_JAVA_KEYSTORE     | 是                |

預先註冊的金鑰儲存區提供者，您不需要變更任何應用程式程式碼以使用這些提供者，但請注意下列項目：

- 您 (或您的 DBA) 需要確認設定在資料行主要金鑰中繼資料的提供者名稱是否正確，且資料行主要金鑰路徑符合指定提供者有效的金鑰路徑格式。 建議您使用 SQL Server Management Studio 等工具設定金鑰，這樣在發出 CREATE COLUMN MASTER KEY (Transact-SQL) 陳述式時，會自動產生有效的提供者名稱和金鑰路徑。
- 確定您的應用程式可以存取金鑰儲存區中的金鑰。 這可能牽涉到授與應用程式金鑰及/或金鑰存放區的存取權 (視金鑰存放區而定)，或執行其他的金鑰存放區特定設定步驟。 例如，使用 SQLServerColumnEncryptionJavaKeyStoreProvider，您需要提供位置和連接屬性中的金鑰存放區的密碼。 

所有這些金鑰儲存區提供者都是以更多詳細資料，請依照下列各節中所述。 您只需要實作一個使用 Always Encrypted 的金鑰儲存區提供者。

### <a name="using-azure-key-vault-provider"></a>使用 Azure 金鑰保存庫提供者
Azure Key Vault 是存放和管理 Always Encrypted 資料行主要金鑰的方便選項 (尤其是當應用程式裝載在 Azure 時)。 Microsoft JDBC Driver for SQL Server 包含的內建提供者，SQLServerColumnEncryptionAzureKeyVaultProvider，使金鑰儲存在 Azure 金鑰保存庫中的應用程式。 此提供者的名稱是 AZURE_KEY_VAULT。 若要使用 Azure Key Vault 存放區提供者，應用程式開發人員必須在 Azure Key Vault 中建立保存庫和金鑰，並在 Azure Active Directory 中建立的應用程式註冊。 已註冊的應用程式必須授與取得，解密、 加密、 解除包裝金鑰、 包裝金鑰，以及確認權限定義而建立的 Always Encrypted 金鑰保存庫的存取原則中。 如需有關如何設定金鑰保存庫，並建立資料行主要金鑰的詳細資訊，請參閱 < [Azure Key Vault-逐步解說](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)並[在 Azure Key Vault 中建立資料行主要金鑰](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault)。

對於在此頁面上，如果您已建立 Azure Key Vault 的範例為基礎的資料行主要金鑰和使用 SQL Server Management Studio 的資料行加密金鑰，來重新建立它們的 T-SQL 指令碼可能會看起來類似此範例中使用它自己的特定**KEY_路徑**並**ENCRYPTED_VALUE**:

```sql
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

```java
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**clientID**是 Azure Active Directory 執行個體中的應用程式註冊的應用程式識別碼。 **clientKey**金鑰密碼下註冊該應用程式至 Azure 金鑰保存庫中提供 API 存取權。

應用程式建立 SQLServerColumnEncryptionAzureKeyVaultProvider 的執行個體之後，應用程式必須向使用 sqlserverconnection.registercolumnencryptionkeystoreproviders （） 方法的驅動程式的執行個體。 強烈建議使用預設查閱名稱 AZURE_KEY_VAULT，可以藉由呼叫 SQLServerColumnEncryptionAzureKeyVaultProvider.getName() API 取得註冊執行個體。 使用預設名稱，可讓您使用 SQL Server Management Studio 或 PowerShell 等工具來佈建和管理永遠加密金鑰 （這些工具會使用來產生資料行主要金鑰中繼資料物件的預設名稱）。 下列範例會示範 Azure Key Vault 提供者進行登錄。 如需有關 sqlserverconnection.registercolumnencryptionkeystoreproviders （） 方法的詳細資訊，請參閱[永遠加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。

```java
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
>  如果您使用 Azure Key Vault 金鑰儲存區提供者時，JDBC 驅動程式的 Azure 金鑰保存庫實作會有這些程式庫 （從 GitHub) 必須隨附於應用程式的相依性：
>
>  [azure sdk-針對-java](https://github.com/Azure/azure-sdk-for-java)
>
>  [azure active directory-程式庫-針對-java 程式庫](https://github.com/AzureAD/azure-activedirectory-library-for-java)
>
> 如何在 Maven 專案中加入這些相依性的範例，請參閱[下載 ADAL4J 和 AKV 相依性使用 Apache Maven](https://github.com/Microsoft/mssql-jdbc/wiki/Download-ADAL4J-And-AKV-Dependencies-with-Apache-Maven)

### <a name="using-windows-certificate-store-provider"></a>使用 Windows 憑證存放區提供者
SQLServerColumnEncryptionCertificateStoreProvider 可用來將資料行主要金鑰儲存在 Windows 憑證存放區。 若要建立的資料行主要金鑰和資料行加密金鑰定義在資料庫中，使用 [SQL Server Management Studio (SSMS) 永遠加密精靈] 或其他支援的工具。 相同的精靈可用來產生自我簽署的憑證可用來當做資料行主要金鑰的永遠加密資料的 Windows 憑證存放區。 如需有關資料行主要金鑰和資料行加密金鑰的 T-SQL 語法的詳細資訊，請參閱 < [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)並[CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md)分別。

SQLServerColumnEncryptionCertificateStoreProvider 的名稱是 MSSQL_CERTIFICATE_STORE，而且可以進行查詢 getName() API 提供者物件。 它會自動註冊驅動程式，並可順暢地不搭配任何應用程式變更。

對於在此頁面上，如果您已建立 Windows 憑證存放區的範例為基礎的資料行主要金鑰和使用 SQL Server Management Studio 的資料行加密金鑰，來重新建立它們的 T-SQL 指令碼可能會看起來類似此範例中使用它自己的特定**KEY_PATH**並**ENCRYPTED_VALUE**:

```sql
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
> 雖然這篇文章中的其他金鑰儲存區提供者可用的所有驅動程式支援的平台上，就有一個 SQLServerColumnEncryptionCertificateStoreProvider 實作 JDBC 驅動程式可在 Windows 作業系統上。 它會相依於所提供的驅動程式套件中的 sqljdbc_auth.dll 時。 若要使用此提供者，請將 sqljdbc_auth.dll 檔案複製到安裝 JDBC 驅動程式之電腦上 Windows 系統路徑中的目錄。 或者，您也可以設定 java.libary.path 系統屬性來指定 sqljdbc_auth.dll 的目錄。 如果您執行的是 32 位元的 Java Virtual Machine (JVM)，即使作業系統為 x64 版，也請使用 x86 資料夾中的 sqljdbc_auth.dll 檔案。 如果您是在 x64 處理器上執行 64 位元的 JVM，請使用 x64 資料夾中的 sqljdbc_auth.dll 檔案。 例如，如果您要使用 32 位元 JVM，且 JDBC 驅動程式安裝在預設目錄中，您就可以在 Java 應用程式啟動時，使用下列虛擬機器 (VM) 引數來指定 DLL 的位置：`-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### <a name="using-java-key-store-provider"></a>使用 Java 金鑰存放區提供者
JDBC 驅動程式隨附於 Java 金鑰存放區的內建金鑰存放區提供者實作。 如果**keyStoreAuthentication**連接字串屬性中的連接字串和設為"JavaKeyStorePassword"，驅動程式會自動具現化，並註冊 Java 金鑰存放區提供者。 Java 金鑰存放區提供者的名稱是 MSSQL_JAVA_KEYSTORE。 此名稱也可以使用 SQLServerColumnEncryptionJavaKeyStoreProvider.getName() API 來查詢。 

有三個連接字串屬性可讓用戶端應用程式，以指定的驅動程式必須向 Java 金鑰存放區的認證。 驅動程式初始化這些連接字串中的三個屬性的值為基礎的提供者。

**keyStoreAuthentication:** 識別要使用 Java 金鑰存放區。 Microsoft JDBC driver 6.0 或更新版本的 SQL Server，您可以向 Java 金鑰存放區，只能透過這個屬性。 Java 金鑰存放區中，此屬性的值必須是`JavaKeyStorePassword`。

**keyStoreLocation:** 儲存資料行主要金鑰的 Java 金鑰存放區檔案的路徑。 路徑中包含的金鑰儲存區檔案名稱。

**keyStoreSecret:** 密碼/密碼，才能使用 keystore 以及索引鍵。 使用 Java 金鑰存放區，金鑰儲存區和金鑰的密碼必須相同。

提供這些認證連接字串中的範例如下：

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

您也可以取得或設定使用 SQLServerDataSource 物件的這些設定。 如需詳細資訊，請參閱 <<c0> [ 永遠加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。

這些認證會出現在 連接屬性時，JDBC 驅動程式會自動執行個體化 SQLServerColumnEncryptionJavaKeyStoreProvider。

### <a name="creating-a-column-master-key-for-the-java-key-store"></a>建立 Java 金鑰存放區的資料行主要金鑰
SQLServerColumnEncryptionJavaKeyStoreProvider 可以搭配 JKS 或 PKCS12 金鑰儲存區類型。 若要建立或匯入要與此提供者所使用的金鑰使用 Java [keytool](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html)公用程式。 此金鑰必須具備作為金鑰存放區本身相同的密碼。 如何建立公開金鑰和其相關聯的私密金鑰使用 keytool 公用程式的範例如下：

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

此命令會建立公用金鑰，並將它包裝在自我簽署憑證，它會儲存在金鑰存放區 'keystore.jks' 及其相關聯的私密金鑰的 X.509。 此金鑰儲存區中的項目會識別別名 'AlwaysEncryptedKey'。

以下是相同的使用 PKCS12 存放區類型的範例：

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

如果金鑰儲存區屬於型別 PKCS12，keytool 公用程式不會提示輸入金鑰的密碼和金鑰的密碼必須提供-keypass 選項，因為 SQLServerColumnEncryptionJavaKeyStoreProvider 需要金鑰存放區和索引鍵具有相同密碼。

您也可以從 Windows 憑證存放區，以.pfx 格式匯出憑證，並可使用 SQLServerColumnEncryptionJavaKeyStoreProvider。 匯出的憑證也可匯入 Java 金鑰存放區為 JKS 金鑰儲存區類型。

建立之後 keytool 項目，請在資料庫中，需要金鑰存放區提供者名稱和金鑰路徑建立資料行主要金鑰中繼資料。 如需有關如何建立資料行主要金鑰中繼資料的詳細資訊，請參閱 < [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)。 SQLServerColumnEncryptionJavaKeyStoreProvider，機碼路徑是索引鍵的別名以及 SQLServerColumnEncryptionJavaKeyStoreProvider 的名稱是 'MSSQL_JAVA_KEYSTORE'。 您也可以查詢此使用 getName() SQLServerColumnEncryptionJavaKeyStoreProvider 類別的公用 API 的名稱。 

建立資料行主要金鑰的 T-SQL 語法是：

```sql
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
)
```

'AlwaysEncryptedKey' 上面所建立，為資料行主要金鑰定義：

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```

> [!NOTE]
> 內建的 SQL Server management Studio 功能無法建立 Java 金鑰存放區的資料行主要金鑰定義。 必須以程式設計方式使用 T-SQL 命令。

### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>建立 Java 金鑰存放區的資料行加密金鑰
SQL Server Management Studio 或任何其他工具，都無法用來建立資料行使用 Java 金鑰存放區中的資料行主要金鑰的加密金鑰。 用戶端應用程式必須建立以程式設計方式使用 SQLServerColumnEncryptionJavaKeyStoreProvider 類別資料行加密金鑰。 如需詳細資訊，請參閱 <<c0> [ 使用資料行主要金鑰存放區提供者以程式設計方式佈建金鑰](#using-column-master-key-store-providers-for-programmatic-key-provisioning)。

### <a name="implementing-a-custom-column-master-key-store-provider"></a>實作自訂資料行主要金鑰存放區提供者
如果您想要將資料行主要金鑰儲存在現有提供者不支援的金鑰存放區中，您可以擴充 SQLServerColumnEncryptionKeyStoreProvider 類別 以及使用 SQLServerConnection.registerColumnEncryptionKeyStoreProviders() 方法來註冊提供者，以實作自訂提供者。

```java
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

```java
SQLServerColumnEncryptionKeyStoreProvider storeProvider = new MyCustomKeyStore();
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(storeProvider.getName(), storeProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

## <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>使用資料行主要金鑰存放區提供者以程式設計方式佈建金鑰
當存取加密的資料行時，Microsoft JDBC Driver for SQL Server 會以清晰簡明的方式尋找並呼叫正確的資料行主要金鑰存放區提供者，來解密資料行加密金鑰。 一般來說，一般應用程式程式碼不會直接呼叫資料行主要金鑰存放區提供者。 不過，您可能會具現化並呼叫提供者以程式設計方式佈建和管理永遠加密金鑰。 此步驟可能會為了產生加密的資料行加密金鑰，例如作為部分資料行主要金鑰輪替，解密資料行加密金鑰。 如需詳細資訊，請參閱 [永遠加密的金鑰管理概觀](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。

如果使用自訂的金鑰存放區提供者，則可能需要實作您自己的金鑰管理工具。 當使用儲存在 Windows 憑證存放區，或在 Azure Key Vault 的金鑰時，您可以使用現有的工具，例如 SQL Server Management Studio 或 PowerShell 來管理和佈建金鑰。 當使用 Java 金鑰存放區中的金鑰時，您需要以程式設計方式佈建金鑰。 下列範例說明使用 SQLServerColumnEncryptionJavaKeyStoreProvider 類別來利用 Java 金鑰存放區中儲存的金鑰加密金鑰。

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programmatically for the Java Key Store.
 */
public class AlwaysEncrypted {
    // Alias of the key stored in the keystore.
    private static String keyAlias = "<provide key alias>";

    // Name by which the column master key will be known in the database.
    private static String columnMasterKeyName = "MyCMK";

    // Name by which the column encryption key will be known in the database.
    private static String columnEncryptionKey = "MyCEK";

    // The location of the keystore.
    private static String keyStoreLocation = "C:\\Dev\\Always Encrypted\\keystore.jks";

    // The password of the keystore and the key.
    private static char[] keyStoreSecret = "********".toCharArray();

    /**
     * Name of the encryption algorithm used to encrypt the value of the column encryption key. The algorithm for the system providers must be
     * RSA_OAEP.
     */
    private static String algorithm = "RSA_OAEP";

    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";

        try (Connection connection = DriverManager.getConnection(connectionUrl);
                Statement statement = connection.createStatement();) {

            // Instantiate the Java Key Store provider.
            SQLServerColumnEncryptionKeyStoreProvider storeProvider = new SQLServerColumnEncryptionJavaKeyStoreProvider(keyStoreLocation,
                    keyStoreSecret);

            byte[] encryptedCEK = getEncryptedCEK(storeProvider);

            /**
             * Create column encryption key For more details on the syntax, see:
             * https://docs.microsoft.com/sql/t-sql/statements/create-column-encryption-key-transact-sql Encrypted column encryption key first needs
             * to be converted into varbinary_literal from bytes, for which byteArrayToHex() is used.
             */
            String createCEKSQL = "CREATE COLUMN ENCRYPTION KEY "
                    + columnEncryptionKey
                    + " WITH VALUES ( "
                    + " COLUMN_MASTER_KEY = "
                    + columnMasterKeyName
                    + " , ALGORITHM =  '"
                    + algorithm
                    + "' , ENCRYPTED_VALUE =  0x"
                    + byteArrayToHex(encryptedCEK)
                    + " ) ";
            statement.executeUpdate(createCEKSQL);
            System.out.println("Column encryption key created with name : " + columnEncryptionKey);
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static byte[] getEncryptedCEK(SQLServerColumnEncryptionKeyStoreProvider storeProvider) throws SQLServerException {
        String plainTextKey = "You need to give your plain text";

        // plainTextKey has to be 32 bytes with current algorithm supported
        byte[] plainCEK = plainTextKey.getBytes();

        // This will give us encrypted column encryption key in bytes
        byte[] encryptedCEK = storeProvider.encryptColumnEncryptionKey(keyAlias, algorithm, plainCEK);

        return encryptedCEK;
    }

    public static String byteArrayToHex(byte[] a) {
        StringBuilder sb = new StringBuilder(a.length * 2);
        for (byte b : a)
            sb.append(String.format("%02x", b).toUpperCase());
        return sb.toString();
    }
}
```

## <a name="enabling-always-encrypted-for-application-queries"></a>為應用程式查詢啟用 [永遠加密]
加密參數及解密以加密資料行為目標的查詢結果，最簡單的方式是將 **columnEncryptionSetting** 連接字串關鍵字的值設定為 [啟用]。

下列連接字串是在 JDBC 驅動程式中啟用 Always Encrypted 的範例：

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionUrl);
```

下列程式碼是使用 SQLServerDataSource 物件的對等範例：

```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("<server>");
ds.setPortNumber(<port>);
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");
SQLServerConnection con = (SQLServerConnection) ds.getConnection();
```

個別查詢也可以啟用 [永遠加密]。 如需詳細資訊，請參閱 <<c0> [ 控制永遠加密的效能影響](#controlling-the-performance-impact-of-always-encrypted)。 啟用 Always Encrypted 並不足以保證加密或解密成功。 您還需要確定︰
- 應用程式要有 [檢視任何資料行的主要金鑰定義] 和 [檢視任何資料行的加密金鑰定義] 資料庫權限，才能存取資料庫中永遠加密金鑰的相關中繼資料。 如需詳細資料，請參閱 [Always Encrypted (資料庫引擎) 的權限](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)。
- 應用程式可以存取保護資料行加密金鑰的資料行主要金鑰，這些加密金鑰會加密查詢的資料庫資料行。 若要使用的 Java 金鑰存放區提供者，您需要提供額外的認證，連接字串中。 如需詳細資訊，請參閱 < [Using Java 金鑰存放區提供者](#using-java-key-store-provider)。

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>設定 java.sql.Time 值如何傳送給伺服器
**sendTimeAsDatetime** 連線屬性是用來設定 java.sql.Time 值傳送到伺服器的方式。 設定為 false 時，時間值傳送為 SQL Server 的時間型別。 何時設定為 true 時，值傳送為 datetime 類型的時間。 如果時間資料行已加密，請**sendTimeAsDatetime**屬性必須為 false，因為加密資料行不支援時間轉換成日期時間。 也請注意，此屬性依預設為 true，因此使用加密的時間資料行時您必須將它設定為 false。 否則，此驅動程式將會擲回例外狀況。 SQLServerConnection 類別從驅動程式 6.0 版開始，有兩種方法，以程式設計方式設定這個屬性的值：
 
* public void setSendTimeAsDatetime (布林 sendTimeAsDateTimeValue)
* public boolean getSendTimeAsDatetime()

如需有關這個屬性的詳細資訊，請參閱 <<c0> [ 如何設定 java.sql.Time 值傳送給伺服器](configuring-how-java-sql-time-values-are-sent-to-the-server.md)。

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>設定如何將字串值傳送到伺服器
**SendStringParametersAsUnicode**連接屬性用來設定如何將字串值傳送至 SQL Server。 如果設定為 true，則以 Unicode 格式將 String 參數傳送到伺服器。 如果設為 false，字串參數會以非 Unicode 格式，例如 ASCII 或 MBCS，而非 Unicode 傳送。 這個屬性的預設值是 True。 當啟用 永遠加密和 char/varchar/varchar(max) 資料行已加密，值**sendStringParametersAsUnicode**必須設定為 false。 如果這個屬性設為 true，此驅動程式將會擲回例外狀況時解密資料加密的 char/varchar/varchar(max) 行包含 Unicode 字元的資料。 如需有關這個屬性的詳細資訊，請參閱 <<c0> [ 設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>擷取和修改加密資料行中的資料
一旦為應用程式查詢啟用 Always Encrypted，您可以使用標準的 JDBC Api 來擷取或修改加密的資料庫資料行中的資料。 如果您的應用程式具有必要的資料庫權限，而且可以存取資料行主要金鑰，驅動程式會加密任何查詢參數的目標加密資料行，以及解密擷取自加密資料行的資料。

若未啟用 Always Encrypted，使用目標加密資料行參數的查詢就會失敗。 只要查詢沒有以加密資料行為目標的參數，查詢就仍然可以從加密資料行擷取資料。 不過，驅動程式不會嘗試解密任何從加密資料行擷取的值，而應用程式會收到二進位的加密資料 (以位元組陣列形式)。

下表摘要說明查詢的行為，視 Always Encrypted 是否啟用而定：

| 查詢特性                                                                           | [永遠加密] 已啟用，且應用程式可以存取金鑰和金鑰中繼資料                                                                                                                        | Always Encrypted 已啟用，但應用程式不能存取金鑰或金鑰中繼資料 | [永遠加密] 已停用                                                                                        |
| :--------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------ |
| 有以加密資料行為目標之參數的查詢。                                           | 以清晰簡明的方式加密參數值。                                                                                                                                                           | 錯誤                                                                             | 錯誤                                                                                                               |
| 查詢從加密的資料行擷取資料，沒有任何以加密資料行為目標的參數。 | 以清晰簡明的方式解密來自加密資料行的結果。 應用程式會收到 JDBC 資料類型的純文字值，該資料類型對應至針對加密資料行設定的 SQL Server 類型。 | 錯誤                                                                             | 不會解密來自加密資料行的結果。 應用程式收到位元組陣列 (byte[]) 形態的加密值。 |

### <a name="inserting-and-retrieving-encrypted-data-examples"></a>插入及擷取加密的資料範例

以下範例將說明擷取和修改加密資料行中的資料。 此範例假設目標資料表具有下列結構描述和加密的 SSN 和 BirthDate 資料行。 如果您已設定名為資料行主要金鑰 」 MyCMK"和資料行加密金鑰名為"MyCEK 」 （如上述的金鑰儲存區提供者章節中所述），您可以建立使用此指令碼的資料表：

```sql
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

每個 Java 程式碼範例中，您必須將金鑰儲存區專屬的程式碼中所述的位置。

如果您使用 Azure Key Vault 金鑰儲存區提供者：

```java
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

如果您使用 Windows 憑證存放區的金鑰儲存區提供者：

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

如果您使用 Java 金鑰存放區的金鑰儲存區提供者：

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### <a name="inserting-data-example"></a>插入資料範例

本例會將資料列插入病患資料表。 請注意下列項目：

- 範例程式碼中沒有任何需要加密的特定項目。 Microsoft JDBC Driver for SQL Server 會自動偵測，並會加密目標加密資料行的參數。 此行為可讓加密對應用程式變得透明化。
- 插入至資料庫資料行，包括加密的資料行的值會傳遞做為參數使用 SQLServerPreparedStatement。 雖然將值傳送到未加密的資料行時，使用參數是選擇性項目 (還是強烈建議使用，因有利於防止 SQL 插入式攻擊)，但它對以加密資料行為目標的值卻是必要項目。 如果傳遞做為內嵌在查詢陳述式中的常值插入至加密的資料行的值，則查詢會失敗，因為驅動程式將無法判斷目標加密資料行的值，而且它不會加密值。 結果，伺服器會因與加密資料行不相容而拒絕它們。
- 程式列印的所有值都是純文字格式，Microsoft JDBC Driver for SQL Server 會以清晰簡明的方式解密從已加密資料行擷取的資料。
- 如果您要進行查閱，使用 WHERE 子句中的 WHERE 子句必須用來使驅動程式可以明確地將它加密再將它傳送至資料庫，做為參數傳遞的值。 在下列範例中，SSN 做為參數傳遞，但 LastName 傳遞做為常值 [姓氏] 不會加密。
- SSN 資料行為目標的參數所使用的 setter 方法是以 setstring （），這會對應到 char/varchar SQL Server 資料類型。 如果用於此參數的 setter 方法為對應至 nchar/nvarchar 的 setNString()，則查詢會失敗；因為 Always Encrypted 不支援從加密的 nchar/nvarchar 值轉換成加密的 char/varchar 值。

```java
// <Insert keystore-specific code here>
try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
        PreparedStatement insertStatement = sourceConnection.prepareStatement("INSERT INTO [dbo].[Patients] VALUES (?, ?, ?, ?)")) {
    insertStatement.setString(1, "795-73-9838");
    insertStatement.setString(2, "Catherine");
    insertStatement.setString(3, "Abel");
    insertStatement.setDate(4, Date.valueOf("1996-09-10"));
    insertStatement.executeUpdate();
    System.out.println("1 record inserted.\n");
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="retrieving-plaintext-data-example"></a>擷取純文字資料範例

下列範例會示範根據加密值篩選資料，以及從加密資料行擷取純文字資料。 請注意下列項目：

- 在 WHERE 子句中用來篩選 SSN 資料行的值，需要以參數形式傳遞，如此 Microsoft JDBC Driver for SQL Server 可以清晰簡明的方式加密它，再將它傳送至資料庫。
- 程式列印的所有值都是純文字格式，Microsoft JDBC Driver for SQL Server 會以清晰簡明的方式解密從 SSN 和 BirthDate 資料行擷取的資料。

> [!NOTE]
> 如果使用具確定性的加密來加密資料行，則查詢可執行資料行的相等比較。 如需詳細資訊，請參閱[選擇 Always Encrypted (資料庫引擎) 的決定性加密或隨機加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)。

```java
// <Insert keystore-specific code here>
try (Connection connection = DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = connection
                .prepareStatement("\"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = ?;\"");) {
    selectStatement.setString(1, "795-73-9838");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("SSN: " + rs.getString("SSN") + ", FirstName: " + rs.getString("FirstName") + ", LastName:"
                + rs.getString("LastName") + ", Date of Birth: " + rs.getString("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="retrieving-encrypted-data-example"></a>擷取加密的資料範例

若未啟用 Always Encrypted，只要查詢沒有以加密資料行為目標的參數，查詢就仍然可以從加密資料行擷取資料。

下列範例會示範從加密資料行擷取二進位的加密資料。 請注意下列項目：

- 因為連接字串未啟用 Always Encrypted，所以查詢會以位元組陣列 (程式會將值轉換為字串) 傳回加密的 SSN 和 BirthDate 值。
- 從加密資料行擷取資料但停用 [永遠加密] 的查詢可以有參數，只要沒有任何參數以加密資料行為目標。 下列查詢依 LastName 篩選，在資料庫中未加密。 如果依 SSN 或 BirthDate 篩選查詢，查詢會失敗。

```java
try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = sourceConnection
                .prepareStatement("SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;");) {

    selectStatement.setString(1, "Abel");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("SSN: " + rs.getString("SSN") + ", FirstName: " + rs.getString("FirstName") + ", LastName:"
                + rs.getString("LastName") + ", Date of Birth: " + rs.getString("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>避免常見的加密資料行查詢問題

本節描述從 Java 應用程式查詢加密資料行時常見的錯誤類別，以及如何避免的一些指導方針。

### <a name="unsupported-data-type-conversion-errors"></a>不支援的資料類型轉換錯誤

[永遠加密] 支援極少數的加密資料類型轉換。 如需支援的類型轉換詳細清單，請參閱 [Always Encrypted (資料庫引擎)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。 以下是避免資料類型轉換錯誤時可以執行的事項。 請確認：

- 傳遞參數值的目標加密資料行時，您可以使用適當的 setter 方法。 請確定參數的 SQL Server 資料型別正是與目標資料行的類型相同，或將參數的 SQL Server 資料類型轉換成目標型別資料行的支援。 API 方法已加入為 SQLServerPreparedStatement、 SQLServerCallableStatement 和 SQLServerResultSet 類別來傳送對應至特定的 SQL Server 資料類型的參數。 例如，如果不會加密資料行，您可以使用 setTimestamp() 方法，將參數傳遞至 datetime2 或 datetime 資料行。 但是，加密資料行時，您必須使用實際的方法，表示在資料庫中的資料行的型別。 例如，將值傳遞至加密的 datetime2 資料行，並將值傳遞至加密的日期時間資料行使用 setDateTime() 使用 setTimestamp()。 請參閱[永遠加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)的新 Api 的完整清單。
- 以小數和數值 SQL Server 資料類型資料行為目標之參數的有效位數和小數位數，和為目標資料行設定的有效位數和小數位數相同。 API 方法已加入為 SQLServerPreparedStatement、 SQLServerCallableStatement 和 SQLServerResultSet 類別接受的精確度和小數位數，以及代表 decimal 與 numeric 資料類型的參數/資料行的資料值。 請參閱[永遠加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)的新/多載 Api 的完整清單。  
- 小數秒數有效位數/小數位數以 datetime2、 datetimeoffset 或時間 SQL Server 資料類型資料行為目標的參數不大於目標資料行的查詢中，修改目標資料行的值的小數秒數有效位數/調整. 已新增 API 方法給 SQLServerPreparedStatement、 SQLServerCallableStatement 和 SQLServerResultSet 的類別，以接受小數秒數有效位數/小數位數以及代表這些資料型別參數的資料值。 如需新/多載的 api 的完整清單，請參閱[永遠加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。

### <a name="errors-due-to-incorrect-connection-properties"></a>不正確的連接屬性所造成的錯誤

本節說明如何設定連線設定正確使用永遠加密的資料。 加密的資料類型支援有限的轉換，因為**sendTimeAsDatetime**並**sendStringParametersAsUnicode**連接設定使用加密的資料行時，需要適當的設定。 請確認：

- [sendTimeAsDatetime](setting-the-connection-properties.md)連接設定為 false，將資料插入加密時間資料行時。 如需詳細資訊，請參閱 <<c0> [ 設定 java.sql.Time 值如何傳送至伺服器](configuring-how-java-sql-time-values-are-sent-to-the-server.md)。
- [sendStringParametersAsUnicode](setting-the-connection-properties.md)連接設定設定為 true （或保留為預設值） 時將資料插入加密的 char/varchar/varchar(max) 資料行。

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>因為傳送純文字，而不是傳送加密值所造成的錯誤。

任何以加密資料行為目標的值都需要在應用程式內加密。 嘗試對加密資料行插入/修改或以純文字值篩選，會造成類似下面的錯誤：

```java
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

若要避免這類錯誤，請確定︰

- (針對連接字串或特定查詢) 以加密資料行為目標的應用程式查詢已啟用 Always Encrypted。
- 您使用已備妥的陳述式和參數來傳送資料的目標加密資料行。 下列範例示範對加密資料行 (SSN) 以常值/常數錯誤篩選 (不是以參數形式在內部傳遞常值)。 此查詢將會失敗：

```java
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## <a name="force-encryption-on-input-parameters"></a>在 輸入參數上強制加密

使用永遠加密時，[強制加密] 功能會強制執行加密參數。 如果使用強制加密但 SQL Server 向驅動程式告知參數不需要加密，使用該參數的查詢就會失敗。 此屬性會針對受到安全性攻擊危害的 SQL Server 提供額外的保護，此類 SQL Server 會將不正確的加密中繼資料提供給用戶端，而可能導致資料洩露。 SQLServerPreparedStatement 和 SQLServerCallableStatement 類別和更新中的 set * 方法\*SQLServerResultSet 類別的方法多載接受布林值的引數，以指定 [強制加密] 設定。 如果這個引數的值為 false，驅動程式將不會強制加密參數。 強制加密 」 設定為 true 時，查詢參數才會傳送目的地資料行已加密，並啟用 永遠加密連接或陳述式。 使用這個屬性會提供一層額外的安全性，確保，驅動程式不會不小心將資料傳送到 SQL Server 以純文字時預期會有加密。

如需有關 SQLServerPreparedStatement 和 SQLServerCallableStatement 方法多載具有 [強制加密] 設定，請參閱[永遠加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>控制 Always Encrypted 的效能影響

因為 Always Encrypted 是用戶端加密技術，大部分的效能額外負荷是在用戶端觀察到，不是在資料庫觀察到。 除了加密和解密作業成本之外，用戶端其他的效能額外負荷來源如下：

- 額外反覆存取資料庫以擷取查詢參數的中繼資料。
- 呼叫資料行主要金鑰存放區以存取資料行主要金鑰。

本節描述 Microsoft JDBC Driver for SQL Server 的內建效能最佳化，以及如何控制上述兩個因素對效能的影響。

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>控制反覆存取以擷取查詢參數的中繼資料

如果連線已啟用 Always Encrypted，驅動程式預設會針對每個參數化查詢呼叫 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)，將查詢陳述式 (不含任何參數值) 傳遞至 SQL Server。 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) 會分析查詢陳述式，找出是否有任何參數需要加密；如果有，則對每個需要加密的參數傳回加密相關資訊，讓驅動程式加密參數值。 此行為可對用戶端應用程式確保高透明度。 只要應用程式會使用參數來傳遞目標的驅動程式的加密資料行的值，則應用程式 （及應用程式開發人員） 不需要知道哪些查詢存取加密資料行中。

### <a name="setting-always-encrypted-at-the-query-level"></a>在查詢層級設定 [永遠加密]

若要控制擷取參數化查詢之加密中繼資料的效能影響，您可以為個別查詢啟用 Always Encrypted，而不是設定它進行連線。 如此一來，您可以確保只有已知以加密資料行為目標之參數的查詢才能叫用 sys.sp_describe_parameter_encryption。 不過請注意，如此一來會降低加密的透明度︰如果您變更資料庫資料行的加密屬性，您可能需要變更應用程式的程式碼，以配合結構描述變更。

若要控制個別查詢的 Always Encrypted 行為，您需要設定個別的陳述式物件，藉由傳遞列舉，SQLServerStatementColumnEncryptionSetting，指定將如何傳送和接收時讀取和寫入資料針對該特定的陳述式的加密資料行。 以下是一些實用的方針：

- 如果用戶端應用程式透過資料庫連線傳送的大多數查詢都會存取加密資料行，請使用下列指導方針：

    - 將 **columnEncryptionSetting** 連接字串關鍵字設定為 [啟用]。
    - 對不會存取任何加密資料行的個別查詢設定 SQLServerStatementColumnEncryptionSetting.Disabled。 此設定將停用呼叫 sys.sp_describe_parameter_encryption 以及嘗試解密結果集內的任何值。
    - 對沒有任何參數要求加密，但會從加密資料行擷取資料的個別查詢設定 SQLServerStatementColumnEncryptionSetting.ResultSet。 此設定會停用呼叫 sys.sp_describe_parameter_encryption 和參數加密。 查詢將能夠解密來自加密資料行的結果。

- 如果用戶端應用程式透過資料庫連線傳送的大多數查詢都不會存取加密資料行，請使用下列指導方針：

    - 將 **columnEncryptionSetting** 連接字串關鍵字設定為 [停用]。
    - 對有任何參數需要加密的個別查詢設定 SQLServerStatementColumnEncryptionSetting.Enabled。 此設定會啟用呼叫 sys.sp_describe_parameter_encryption 以及解密擷取自加密資料行的任何查詢結果。
    - 對沒有任何參數要求加密，但會從加密資料行擷取資料的查詢設定 SQLServerStatementColumnEncryptionSetting.ResultSet。 此設定會停用呼叫 sys.sp_describe_parameter_encryption 和參數加密。 查詢將能夠解密來自加密資料行的結果。

SQLServerStatementColumnEncryptionSetting 設定不能略過加密並存取純文字資料。 如需有關如何設定資料行加密的陳述式的詳細資訊，請參閱[永遠加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。  

在下列範例中，資料庫連線已停用 Always Encrypted。 應用程式發出的查詢具有以 LastName 資料行為目標的參數，而此資料行未加密。 查詢會從加密的 SSN 和 BirthDate 資料行擷取資料。 在這種情況下，不需要呼叫 sys.sp_describe_parameter_encryption 以擷取加密中繼資料。 不過，需要啟用查詢結果的解密，以使應用程式從兩個加密資料行接收純文字值。 SQLServerStatementColumnEncryptionSetting.ResultSet 設定用來確保。

```java
// Assumes the same table definition as in Section "Retrieving and modifying data in encrypted columns"
// where only SSN and BirthDate columns are encrypted in the database.
String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>;" 
        + "keyStoreAuthentication=JavaKeyStorePassword;"
        + "keyStoreLocation=<keyStoreLocation>" 
        + "keyStoreSecret=<keyStoreSecret>;";

String filterRecord = "SELECT FirstName, LastName, SSN, BirthDate FROM " + tableName + " WHERE LastName = ?";

try (SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionUrl);
        PreparedStatement selectStatement = connection.prepareStatement(filterRecord, ResultSet.TYPE_FORWARD_ONLY, ResultSet.CONCUR_READ_ONLY,
                connection.getHoldability(), SQLServerStatementColumnEncryptionSetting.ResultSetOnly);) {

    selectStatement.setString(1, "Abel");
    ResultSet rs = selectStatement.executeQuery();
    while (rs.next()) {
        System.out.println("First name: " + rs.getString("FirstName"));
        System.out.println("Last name: " + rs.getString("LastName"));
        System.out.println("SSN: " + rs.getString("SSN"));
        System.out.println("Date of Birth: " + rs.getDate("BirthDate"));
    }
}
// Handle any errors that may have occurred.
catch (SQLException e) {
    e.printStackTrace();
}
```

### <a name="column-encryption-key-caching"></a>資料行加密金鑰快取

為減少資料行主要金鑰存放區的呼叫次數以解密資料行加密金鑰，Microsoft JDBC Driver for SQL Server 會快取記憶體中的純文字資料行加密金鑰。 從資料庫中繼資料中接收加密的資料行加密金鑰值之後，驅動程式會先嘗試尋找對應加密金鑰值的純文字資料行加密金鑰。 只有在快取中找不到加密的資料行加密金鑰值時，驅動程式才會呼叫包含資料行主要金鑰的金鑰存放區。

您可以使用 SQLServerConnection 類別中的 API，setColumnEncryptionKeyCacheTtl()，快取中設定的存留時間值的資料行加密金鑰項目。 資料行加密金鑰項目在快取的預設存留時間值是兩個小時。 若要關閉快取，請使用值為 0。 若要設定任何存留時間值，請使用下列 API:

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

例如，若要設定存留時間值為 10 分鐘，請使用：

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

做為時間單位支援只天、 小時、 分鐘或秒數。  

## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>複製使用 SQLServerBulkCopy 的加密的資料

使用 SQLServerBulkCopy，您可以將已加密並儲存在某個資料表的資料，複製到另一個資料表，而不需要解密資料。 若要這麼做︰

- 請確定目標資料表的加密組態與來源資料表的組態完全一致。 特別是，這兩個資料表都必須加密相同的資料行，且這些資料行必須使用相同的加密類型和相同的加密金鑰來加密。 如果任一目標資料行的加密方式不同於其對應的來源資料行，您將無法在複製作業後，解密目標資料表中的資料。 資料會損毀。
- 設定這兩個資料庫對來源資料表和目標資料表的連線，但不啟用 Always Encrypted。
- 設定 allowEncryptedValueModifications 選項。 如需詳細資訊，請參閱 < [JDBC 驅動程式使用大量複製](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)。

> [!NOTE]
> 指定 AllowEncryptedValueModifications 時請小心，此選項可能會導致資料庫損毀；因為 Microsoft JDBC Driver for SQL Server 不會檢查資料是否確實加密，或是否使用和目標資料行相同的加密類型、演算法和金鑰正確加密。

## <a name="see-also"></a>另請參閱

[一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
