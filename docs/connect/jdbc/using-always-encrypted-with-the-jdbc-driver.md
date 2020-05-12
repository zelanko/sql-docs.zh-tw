---
title: 搭配使用 Always Encrypted 與 JDBC 驅動程式
description: 了解如何在您的 Java 應用程式中搭配使用 Always Encrypted 和 JDBC Driver for SQL Server 來加密伺服器上的敏感性資料。
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c63c15ad0a435235f246945d25c732798fb758df
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2020
ms.locfileid: "82886351"
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>搭配使用 Always Encrypted 與 JDBC 驅動程式

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

此頁面提供有關如何使用 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 與 Microsoft JDBC Driver 6.0 (或更高版本) for SQL Server 來開發 Java 應用程式的相關資訊。

Always Encrypted 可讓用戶端加密敏感性資料，而且永遠不會向 SQL Server 或 Azure SQL Database 顯示資料或加密金鑰。 Microsoft JDBC Driver 6.0 (或更高版本) for SQL Server 等啟用了 Always Encrypted 的驅動程式，以清晰簡明的方式加密與解密用戶端應用程式中的敏感性資料，達成此行為。 驅動程式會自動判斷哪一個查詢參數對應至 Always Encrypted 資料庫資料行，然後在對那些參數的值進行加密後，再將其傳遞至 SQL Server 或 Azure SQL Database。 同樣地，驅動程式會以清晰簡明的方式，將擷取自查詢結果的加密資料庫資料行資料進行解密。 如需詳細資訊，請參閱 [Always Encrypted (資料庫引擎)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 和 [JDBC 驅動程式的 Always Encrypted API 參考](always-encrypted-api-reference-for-the-jdbc-driver.md)。

## <a name="prerequisites"></a>Prerequisites
- 確定已在您的開發電腦上安裝 Microsoft JDBC Driver 6.0 (或更高版本) for SQL Server。 
- 下載並安裝 Java 密碼編譯延伸模組 (JCE) 無限制的強度管轄權原則檔。  請務必閱讀 ZIP 檔案中的讀我檔案，以了解安裝指示及可能的匯出/匯入問題相關詳細資料。  

    - 如果使用 mssql-jdbc-X.X.X.jre7.jar 或 sqljdbc41.jar，則可以從[下載 Java 密碼編譯延伸模組 (JCE) 無限制的強度管轄權原則檔 7](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html) 下載原則檔

    - 如果使用 mssql-jdbc-X.X.X.jre8.jar 或 sqljdbc42.jar，則可以從[下載 Java 密碼編譯延伸模組 (JCE) 無限制的強度管轄權原則檔 8](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) 下載原則檔

    - 如果使用 mssql-jdbc-X.X.X.jre9.jar，則不需要下載任何原則檔案。 Java 9 中的轄權原則預設為無限制的強度加密。

## <a name="working-with-column-master-key-stores"></a>使用資料行主要金鑰存放區
為了針對加密的資料行將資料加密或解密，SQL Server 會維護資料行加密金鑰。 資料行加密金鑰是以加密形式存放在資料庫中繼資料。 每個資料行加密金鑰都有對應的資料行主要金鑰，主要金鑰是用於加密資料行加密金鑰。 資料庫中繼資料不會包含資料行主要金鑰。 只有用戶端才會保存那些金鑰。 不過，資料庫中繼資料會包含資料行主要金鑰針對用戶端之相對儲存位置的相關資訊。 例如，資料庫中繼資料可能會表示保存資料行主要金鑰的金鑰儲存區是 Windows 憑證存放區，且用來進行加密和解密的特定憑證是位於 Windows 憑證存放區內的特定路徑上。 如果用戶端可以存取 Windows 憑證存放區中的憑證，其便能取得該憑證。 憑證接著便可以用來將資料行加密金鑰解密。 然後該加密金鑰便可以用來針對使用該資料行加密金鑰的加密資料行，進行資料的解密或加密。

Microsoft JDBC Driver for SQL Server 會使用資料行主要金鑰存放區提供者與金鑰儲存區進行通訊，其為衍生自 **SQLServerColumnEncryptionKeyStoreProvider** 的類別執行個體。

### <a name="using-built-in-column-master-key-store-providers"></a>使用內建資料行主要金鑰存放區提供者
Microsoft JDBC Driver for SQL Server 隨附下列內建的資料行主要金鑰存放區提供者。 某些提供者已預先註冊特定的提供者名稱 (用來查詢該提供者)，而有些則需要額外的認證或明確的註冊。

| 類別                                                 | 描述                                        | 提供者 (查閱) 名稱  | 是否已預先註冊？ |
| :---------------------------------------------------- | :------------------------------------------------- | :---------------------- | :----------------- |
| **SQLServerColumnEncryptionAzureKeyVaultProvider**    | Azure Key Vault 金鑰儲存區的提供者。 | AZURE_KEY_VAULT         | 在 JDBC 驅動程式 7.4.1 版之前為「否」  ，但從 JDBC 驅動程式 7.4.1 版開始則為「是」  。 |
| **SQLServerColumnEncryptionCertificateStoreProvider** | Windows 憑證存放區的提供者。      | MSSQL_CERTIFICATE_STORE | _是_                |
| **SQLServerColumnEncryptionJavaKeyStoreProvider**     | Java 金鑰儲存區的提供者。                  | MSSQL_JAVA_KEYSTORE     | _是_                |
|||||

針對預先註冊的金鑰儲存區提供者，您不需要做出任何應用程式程式碼變更即可使用這些提供者，但請注意下列項目︰

- 您 (或您的 DBA) 需要確認設定在資料行主要金鑰中繼資料的提供者名稱是否正確，且資料行主要金鑰路徑符合指定提供者有效的金鑰路徑格式。 建議您使用 SQL Server Management Studio 等工具設定金鑰，這樣在發出 CREATE COLUMN MASTER KEY (Transact-SQL) 陳述式時，會自動產生有效的提供者名稱和金鑰路徑。
- 確定您的應用程式可以存取金鑰儲存區中的金鑰。 這可能牽涉到授與應用程式金鑰及/或金鑰存放區的存取權 (視金鑰存放區而定)，或執行其他的金鑰存放區特定設定步驟。 例如，針對使用 SQLServerColumnEncryptionJavaKeyStoreProvider，您需要在連線屬性中提供金鑰儲存區的位置和密碼。 

下列各節將會更加詳細地描述這些金鑰儲存區提供者。 您只需要實作單一金鑰儲存區提供者以使用 Always Encrypted。

### <a name="using-azure-key-vault-provider"></a>使用 Azure 金鑰保存庫提供者

Azure Key Vault 是存放和管理 Always Encrypted 資料行主要金鑰的方便選項 (尤其是當應用程式裝載在 Azure 時)。 針對在 Azure Key Vault 中儲存金鑰的應用程式，Microsoft JDBC Driver for SQL Server 包含內建提供者 SQLServerColumnEncryptionAzureKeyVaultProvider。 此提供者的名稱為 AZURE_KEY_VAULT。 若要使用 Azure Key Vault 存放區提供者，應用程式開發人員必須在 Azure Key Vault 中建立存放區和金鑰，然後在 Azure Active Directory 中建立應用程式註冊。 必須在針對搭配 Always Encrypted 使用所建立的金鑰保存庫的已定義存取原則中，為註冊的應用程式授與 [取得]、[解密]、[加密]、[將金鑰解除包裝]、[包裝金鑰] 及 [驗證] 權限。 如需如何設定金鑰保存庫及建立資料行主要金鑰的詳細資訊，請參閱 [Azure Key Vault - 逐步執行](/archive/blogs/kv/azure-key-vault-step-by-step) \(英文\) 及[在 Azure 金鑰保存庫中建立資料行主要金鑰](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault)。

使用 Azure Key Vault 提供者時，JDBC 驅動程式會根據信任的端點清單來驗證資料行主要金鑰路徑。 從驅動程式 8.2.2 版開始，這份清單即為可設定的：在應用程式的工作目錄中建立 "mssql-jdbc.properties" 檔案，將 `AKVTrustedEndpoints` 屬性設為以分號分隔的清單。 如果值以分號開頭，則會延伸預設清單；否則會取代預設清單。

針對本頁面上的範例，如果您已使用 SQL Server Management Studio 建立以 Azure Key Vault 為基礎的資料行主要金鑰及資料行加密金鑰，用來加以重新建立的 T-SQL 指令碼看起來可能會和此範例類似，但會具有其特定的 **KEY_PATH** 和 **ENCRYPTED_VALUE**：

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',
    KEY_PATH = N'https://<MyKeyValutName>.vault.azure.net:443/keys/Always-Encrypted-Auto1/c61f01860f37302457fa512bb7e7f4e8'
);

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x01BA000001680074507400700073003A002F002F006400610076006...
);
```

使用 JDBC 驅動程式的應用程式可以使用 Azure Key Vault。 Azure Key Vault 此使用方式的語法或陳述式從 JDBC 驅動程式 7.4.1 版開始出現變更。

#### <a name="jdbc-driver-741-or-later"></a>JDBC 驅動程式 7.4.1 或更新版本

此節會涉及 JDBC 驅動程式 7.4.1 版或更新版本。

使用 JDBC 驅動程式的用戶端應用程式，可以透過在 JDBC 連接字串中提及 `keyVaultProviderClientId=<ClientId>;keyVaultProviderClientKey=<ClientKey>` 來設定以使用 Azure Key Vault。

以下是在 JDBC 連接字串中提供此設定資訊的範例。

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyVaultProviderClientId=<ClientId>;keyVaultProviderClientKey=<ClientKey>";
```
當連線屬性中存在這些認證時，JDBC 驅動程式會自動具現化 **SQLServerColumnEncryptionAzureKeyVaultProvider** 物件。

#### <a name="jdbc-driver-version-prior-to-741"></a>早於 7.4.1 版的 JDBC 驅動程式

此節會涉及早於 7.4.1 版的 JDBC 驅動程式。

使用 JDBC 驅動程式的用戶端應用程式必須具現化 **SQLServerColumnEncryptionAzureKeyVaultProvider** 物件，然後向驅動程式註冊該物件。

```java
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**clientID** 是 Azure Active Directory 執行個體中應用程式註冊的應用程式識別碼。 **clientKey** 是在該應用程式底下註冊的金鑰密碼，其能為 API 提供 Azure Key Vault 的存取。

在應用程式建立 SQLServerColumnEncryptionAzureKeyVaultProvider 的執行個體之後，該應用程式必須使用 SQLServerConnection.registerColumnEncryptionKeyStoreProviders() 方法向驅動程式註冊該執行個體。 強烈建議使用預設查詢名稱 AZURE_KEY_VAULT 來註冊執行個體，其可透過呼叫 SQLServerColumnEncryptionAzureKeyVaultProvider.getName() API 來取得。 使用預設名稱將能讓您使用 SQL Server Management Studio 或 PowerShell 之類的工具來佈建及管理 Always Encrypted 金鑰 (這些工具會使用預設名稱來針對資料行主要金鑰產生中繼資料物件)。 下列範例顯示註冊 Azure Key Vault 提供者。 如需 SQLServerConnection.registerColumnEncryptionKeyStoreProviders() 方法的詳細資訊，請參閱 [JDBC 驅動程式的 Always Encrypted API 參考](always-encrypted-api-reference-for-the-jdbc-driver.md)。

```java
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
>  如果您使用 Azure Key Vault 金鑰儲存區提供者，JDBC 驅動程式的 Azure Key Vault 實作會具有針對這些 (來自 GitHub 的) 程式庫的相依性，您必須將其包含在您的應用程式中：
>
>  [azure-sdk-for-java](https://github.com/Azure/azure-sdk-for-java)
>
>  [azure-activedirectory-library-for-java 程式庫](https://github.com/AzureAD/azure-activedirectory-library-for-java)
>
> 如需如何將這些相依性包含在 Maven 專案中的範例，請參閱[搭配 Apache Maven 下載 ADAL4J 和 AKV 相依性](https://github.com/Microsoft/mssql-jdbc/wiki/Download-ADAL4J-And-AKV-Dependencies-with-Apache-Maven) \(英文\)

### <a name="using-windows-certificate-store-provider"></a>使用 Windows 憑證存放區提供者
SQLServerColumnEncryptionCertificateStoreProvider 可用來將資料行主要金鑰儲存在 Windows 憑證存放區。 使用 [SQL Server Management Studio (SSMS) Always Encrypted] 精靈或其他支援的工具來在資料庫中建立資料行主要金鑰和資料行加密金鑰定義。 相同的精靈也可以用來在 Windows 憑證存放區中產生自我簽署憑證，以作為 Always Encrypted 資料的資料行主要金鑰使用。 如需資料行主要金鑰和資料行加密金鑰 T-SQL 語法的詳細資訊，請分別參閱[建立資料行主要金鑰](../../t-sql/statements/create-column-master-key-transact-sql.md)和[建立資料行加密金鑰](../../t-sql/statements/create-column-encryption-key-transact-sql.md)。

SQLServerColumnEncryptionCertificateStoreProvider 的名稱為 MSSQL_CERTIFICATE_STORE，且可以由提供者物件的 getName() API 進行查詢。 其會由驅動程式自動註冊，並可以在無需任何應用程式變更的情況下順暢地使用。

針對本頁面上的範例，如果您已使用 SQL Server Management Studio 建立以 Windows 憑證存放區為基礎的資料行主要金鑰及資料行加密金鑰，用來加以重新建立的 T-SQL 指令碼看起來可能會和此範例類似，但會具有其特定的 **KEY_PATH** 和 **ENCRYPTED_VALUE**：

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',
    KEY_PATH = N'CurrentUser/My/A2A91F59C461B559E4D962DA9D2BC6131B32CB91'
);

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E0074007500730065007200...
);
```

> [!IMPORTANT]
> 雖然此文章中的其他金鑰儲存區提供者皆可在驅動程式所支援的所有平台上使用，JDBC 驅動程式的 SQLServerColumnEncryptionCertificateStoreProvider 實作僅適用於 Windows 作業系統。 其具有針對 mssql-jdbc_auth-\<版本>-\<架構>.dll 的相依性，該檔案於驅動程式套件中提供。 若要使用此提供者，請將 mssql-jdbc_auth-\<版本>-\<>.dll 檔案複製到 JDBC 驅動程式安裝電腦上 Windows 系統路徑中的目錄。 或者，您也可以設定 java.library.path 系統屬性來指定 mssql-jdbc_auth-\<版本>-\<架構>.dll 的目錄。 如果您正在執行 32 位元的 Java 虛擬機器 (JVM)，則即使作業系統為 x64 版，也請使用 x86 資料夾中的 mssql-jdbc_auth-\<版本>-x86.dll 檔案。 如果您是在 x64 處理器上執行 64 位元的 JVM，請使用 x64 資料夾中的 mssql-jdbc_auth-\<版本>-x64.dll 檔案。 例如，如果您要使用 32 位元 JVM，且 JDBC 驅動程式安裝在預設目錄中，您就可以在 Java 應用程式啟動時，使用下列虛擬機器 (VM) 引數來指定 DLL 的位置：`-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### <a name="using-java-key-store-provider"></a>使用 Java Key Store 提供者
JDBC 驅動程式隨附於 Java 金鑰存放區的內建金鑰存放區提供者實作。 如果 **keyStoreAuthentication** 連接字串屬性存在於連接字串中，且已設定為 "JavaKeyStorePassword"，驅動程式會自動具現化並註冊 Java Key Store 的提供者。 Java Key Store 提供者的名稱是 MSSQL_JAVA_KEYSTORE。 此名稱也可使用 SQLServerColumnEncryptionJavaKeyStoreProvider.getName() API 來查詢。 

有三個連接字串屬性允許用戶端應用程式指定驅動程式針對 Java Key Store 進行驗證所需的認證。 驅動程式會根據連接字串中這三個屬性的值來初始化提供者。

**keyStoreAuthentication：** 識別要使用的 Java Key Store。 在使用 Microsoft JDBC Driver 6.0 (和更新版本) for SQL Server 的情況下，您只能透過此屬性來針對 Java Key Store 進行驗證。 針對 Java Key Store，此屬性的值必須是 `JavaKeyStorePassword`。

**keyStoreLocation：** 儲存資料行主要金鑰之 Java Key Store 檔案的路徑。 路徑包含金鑰儲存區檔案名稱。

**keyStoreSecret：** 要用於金鑰儲存區及金鑰的祕密/密碼。 若要使用 Java Key Store，則金鑰儲存區和金鑰的密碼必須相同。

以下是在連接字串中提供這些認證的範例：

```java
String connectionUrl = "jdbc:sqlserver://<server>:<port>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

您也可以使用 SQLServerDataSource 物件來取得或設定這些設定。 如需詳細資訊，請參閱 [JDBC 驅動程式的 Always Encrypted API 參考](always-encrypted-api-reference-for-the-jdbc-driver.md)。

當連線屬性中存在這些認證時，JDBC 驅動程式會自動具現化 SQLServerColumnEncryptionJavaKeyStoreProvider。

### <a name="creating-a-column-master-key-for-the-java-key-store"></a>建立 Java Key Store 的資料行主要金鑰
SQLServerColumnEncryptionJavaKeyStoreProvider 可以搭配 JKS 或 PKCS12 金鑰儲存區類型使用。 若要建立或匯入金鑰以搭配此提供者使用，請使用 Java [keytool](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html) \(英文\) 公用程式。 金鑰的密碼必須和金鑰儲存區本身相同。 以下是如何使用 keytool 公用程式建立公開金鑰及其相關聯之私密金鑰的範例：

```console
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

此命令會建立公開金鑰並將其包裝在 X.509 自我簽署憑證中，該憑證會連同其相關聯的私密金鑰儲存在金鑰儲存區 `keystore.jks` 中。 此項目在金鑰儲存區中是透過別名 `AlwaysEncryptedKey` 來識別。

以下是相同的範例，但使用的是 PKCS12 儲存區類型：

```console
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

如果金鑰儲存區是 PKCS12 類型，keytool 公用程式並不會提示輸入金鑰密碼，且金鑰密碼必須使用 `-keypass` 選項來提供，因為 **SQLServerColumnEncryptionJavaKeyStoreProvider** 要求金鑰儲存區和金鑰具有相同的密碼。

您也可以從 Windows 憑證存放區以 .pfx 格式匯出憑證，並搭配 **SQLServerColumnEncryptionJavaKeyStoreProvider** 使用。 匯出的憑證也可以作為 JKS 金鑰儲存區類型匯入 Java Key Store。

在建立 keytool 項目之後，請在資料庫中建立資料行主要金鑰中繼資料，其需要金鑰儲存區提供者名稱和金鑰路徑。 如需如何建立資料行主要金鑰中繼資料的詳細資訊，請參閱[建立資料行主要金鑰](../../t-sql/statements/create-column-master-key-transact-sql.md)。 針對 SQLServerColumnEncryptionJavaKeyStoreProvider，金鑰路徑只是金鑰的別名，而 SQLServerColumnEncryptionJavaKeyStoreProvider 的名稱是 `MSSQL_JAVA_KEYSTORE`。 您也可以使用 SQLServerColumnEncryptionJavaKeyStoreProvider 類別的 getName() 公用 API 來查詢此名稱。 

用來建立資料行主要金鑰的 T-SQL 語法是：

```sql
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
);
```

針對上面所建立的 'AlwaysEncryptedKey'，資料行主要金鑰定義將會是：

```sql
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
);
```

> [!NOTE]
> 內建的 SQL Server Management Studio 功能無法針對 Java Key Store 建立資料行主要金鑰定義。 T-SQL 命令必須以程式設計方式使用。

### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>建立 Java Key Store 的資料行加密金鑰
SQL Server Management Studio 或任何其他工具皆無法用來透過 Java Key Store 中的資料行主要金鑰建立資料行加密金鑰。 用戶端應用程式必須使用 SQLServerColumnEncryptionJavaKeyStoreProvider 類別以程式設計方式建立資料行加密金鑰。 如需詳細資訊，請參閱[使用資料行主要金鑰存放區提供者以程式設計方式佈建金鑰](#using-column-master-key-store-providers-for-programmatic-key-provisioning)。

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
當存取加密的資料行時，Microsoft JDBC Driver for SQL Server 會以清晰簡明的方式尋找並呼叫正確的資料行主要金鑰存放區提供者，來解密資料行加密金鑰。 一般來說，一般應用程式程式碼不會直接呼叫資料行主要金鑰存放區提供者。 不過，您可以透過程式設計方式具現化並呼叫提供者，來佈建及管理 Always Encrypted 金鑰。 例如，您可執行此步驟來產生加密的資料行加密金鑰，並以資料行主要金鑰變換之一部分的方式將資料行加密金鑰解密。 如需詳細資訊，請參閱 [永遠加密的金鑰管理概觀](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。

如果使用自訂的金鑰存放區提供者，則可能需要實作您自己的金鑰管理工具。 使用存放在 Windows 憑證存放區或 Azure Key Vault 中的金鑰時，您可以使用現有工具 (例如 SQL Server Management Studio 或 PowerShell) 來管理和佈建金鑰。 使用儲存在 Java Key Store 中的金鑰時，您需要以程式設計方式佈建金鑰。 下列範例說明如何使用 SQLServerColumnEncryptionJavaKeyStoreProvider 類別來搭配儲存在 Java Key Store 中的金鑰將金鑰加密。

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
加密參數及解密以加密資料行為目標的查詢結果，最簡單的方式是將 **columnEncryptionSetting** 連接字串關鍵字的值設定為 [啟用]  。

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

個別查詢也可以啟用 [永遠加密]。 如需詳細資訊，請參閱[控制 Always Encrypted 的效能影響](#controlling-the-performance-impact-of-always-encrypted)。 啟用 Always Encrypted 並不足以保證加密或解密成功。 您還需要確定︰
- 應用程式要有 [檢視任何資料行的主要金鑰定義]  和 [檢視任何資料行的加密金鑰定義]  資料庫權限，才能存取資料庫中永遠加密金鑰的相關中繼資料。 如需詳細資料，請參閱 [Always Encrypted (資料庫引擎) 的權限](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)。
- 應用程式可以存取保護資料行加密金鑰的資料行主要金鑰，這些加密金鑰會加密查詢的資料庫資料行。 若要使用 Java Key Store 提供者，您需要在連接字串中提供其他認證。 如需詳細資訊，請參閱[使用 Java Key Store 提供者](#using-java-key-store-provider)。

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>設定 java.sql.Time 值如何傳送給伺服器
**sendTimeAsDatetime** 連線屬性是用來設定 java.sql.Time 值傳送到伺服器的方式。 設定為 false 時，會以 SQL Server 時間類型的形式傳送時間值。 設定為 true 時，會以日期時間類型的形式傳送時間值。 如果時間資料行已加密，**sendTimeAsDatetime** 屬性必須為 false，因為加密的資料行不支援從時間轉換成日期時間。 另請注意，此屬性預設為 true，因此使用加密的時間資料行時，您必須將其設定為 false。 否則，驅動程式將會擲回例外狀況。 從驅動程式的 6.0 版開始，SQLServerConnection 類別具有兩個程式設計方法來設定此屬性的值：
 
* public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
* public boolean getSendTimeAsDatetime()

如需此屬性的詳細資訊，請參閱[設定 java.sql.Time 值如何傳送給伺服器](configuring-how-java-sql-time-values-are-sent-to-the-server.md)。

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>設定 String 值如何傳送給伺服器
**sendStringParametersAsUnicode** 連線屬性是用來設定如何將 String 值傳送至 SQL Server。 如果設定為 true，則以 Unicode 格式將 String 參數傳送到伺服器。 如果設定為 false，String 參數就會以非 Unicode 格式 (例如 ASCII 或 MBCS) 傳送，而非 Unicode 格式。 這個屬性的預設值是 True。 當 Always Encrypted 已啟用且 char/varchar/varchar(max) 資料行已加密時，**sendStringParametersAsUnicode** 的值必須設定為 false。 如果此屬性設定為 true，在將來自具有 Unicode 字元的加密 char/varchar/varchar(max) 資料行的資料解密時，驅動程式將會擲回例外狀況。 如需此屬性的詳細資訊，請參閱[設定連線屬性](setting-the-connection-properties.md)。
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>擷取和修改加密資料行中的資料
在您針對應用程式查詢啟用 Always Encrypted 之後，您可以使用標準 JDBC API 來擷取或修改加密資料庫資料行中的資料。 如果您的應用程式具有必要的資料庫權限，而且能夠存取資料行主要金鑰，則驅動程式會加密所有以加密資料行為目標的查詢參數，並將對擷取自加密資料行的資料解密。

若未啟用 Always Encrypted，使用目標加密資料行參數的查詢就會失敗。 只要查詢沒有以加密資料行為目標的參數，查詢就仍然可以從加密資料行擷取資料。 不過，驅動程式不會嘗試解密任何從加密資料行擷取的值，而應用程式會收到二進位的加密資料 (以位元組陣列形式)。

下表摘要說明查詢的行為，視 Always Encrypted 是否啟用而定：

| 查詢特性                                                                           | [永遠加密] 已啟用，且應用程式可以存取金鑰和金鑰中繼資料                                                                                                                        | Always Encrypted 已啟用，但應用程式不能存取金鑰或金鑰中繼資料 | [永遠加密] 已停用                                                                                        |
| :--------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------ |
| 有以加密資料行為目標之參數的查詢。                                           | 以清晰簡明的方式加密參數值。                                                                                                                                                           | 錯誤                                                                             | 錯誤                                                                                                               |
| 查詢從加密的資料行擷取資料，沒有任何以加密資料行為目標的參數。 | 以清晰簡明的方式解密來自加密資料行的結果。 應用程式會收到 JDBC 資料類型的純文字值，該資料類型對應至針對加密資料行設定的 SQL Server 類型。 | 錯誤                                                                             | 不會解密來自加密資料行的結果。 應用程式收到位元組陣列 (byte[]) 形態的加密值。 |

### <a name="inserting-and-retrieving-encrypted-data-examples"></a>插入及擷取加密的資料範例

以下範例將說明擷取和修改加密資料行中的資料。 這些範例假設具有下列結構描述及加密 SSN 和 BirthDate 資料行的目標資料表。 如果您已設定名為 "MyCMK" 的資料行主要金鑰，以及名為 "MyCEK" 的資料行加密金鑰 (如先前的金鑰儲存區提供者小節中所述)，您可以使用此指令碼來建立資料表：

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
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY]);
 GO
```

針對每個 Java 程式碼範例，您必須在所註記的位置中插入金鑰儲存區特定的程式碼。

如果您是使用 Azure Key Vault 金鑰儲存區提供者：

```java
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

如果您是使用 Windows 憑證存放區金鑰儲存區提供者：

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;";
```

如果您是使用 Java Key Store 金鑰儲存區提供者：

```java
    String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### <a name="inserting-data-example"></a>插入資料範例

本例會將資料列插入病患資料表。 請注意下列項目：

- 範例程式碼中沒有任何需要加密的特定項目。 The Microsoft JDBC Driver for SQL Server 會自動偵測以加密資料行為目標的參數並加以加密。 此行為可讓加密對應用程式變得透明化。
- 針對插入至資料庫資料行的值 (包括加密的資料行)，會使用 SQLServerPreparedStatement 傳遞為參數。 雖然將值傳送到未加密的資料行時，使用參數是選擇性項目 (還是強烈建議使用，因有利於防止 SQL 插入式攻擊)，但它對以加密資料行為目標的值卻是必要項目。 如果將插入加密資料行中的值當作內嵌在查詢陳述式中的常值傳遞，則查詢會失敗，因為驅動程式無法判斷目標加密資料行中的值，且其不會將那些值加密。 結果，伺服器會因與加密資料行不相容而拒絕它們。
- 程式列印的所有值都是純文字格式，Microsoft JDBC Driver for SQL Server 會以清晰簡明的方式解密從已加密資料行擷取的資料。
- 如果您正在使用 WHERE 子句進行查閱，用於 WHERE 子句中的值需要以參數形式傳遞，來使驅動程式能先透明地加以加密，再將其傳送至資料庫。 在下列範例中，會以參數形式傳遞 SSN，但會以常值形式傳遞 LastName，因為 LastName 不會加密。
- 用於以 SSN 資料行為目標之參數的 setter 方法為 setString()，其會對應至 char/varchar SQL Server 資料類型。 針對此參數，若其使用的 setter 方法為對應至 nchar/nvarchar 的 setNString()，則查詢會失敗；因為 Always Encrypted 不支援從已加密 nchar/nvarchar 值轉換成加密的 char/varchar 值。

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

- 您在針對以加密資料行為目標的參數傳遞值時，是使用適當的 setter 方法。 確定參數的 SQL Server 資料類型和目標資料行完全相同，或支援將參數的 SQL Server 資料類型轉換成資料行的目標類型。 已將 API 方法新增至 SQLServerPreparedStatement、SQLServerCallableStatement 及 SQLServerResultSet 類別，來傳遞對應特定 SQL Server 資料類型的參數。 例如，如果資料行未加密，您可以使用 setTimestamp() 方法來傳遞參數至 datetime2 或 datetime 資料行。 但在資料行已加密的情況下，您必須使用代表資料庫中資料行類型的確切方法。 例如，使用 setTimestamp() 來將值傳遞至加密的 datetime2 資料行，並使用 setDateTime() 來將值傳遞至加密的 datetime 資料行。 請參閱 [JDBC 驅動程式的 Always Encrypted API 參考](always-encrypted-api-reference-for-the-jdbc-driver.md)來取得新 API 的完整清單。
- 以小數和數值 SQL Server 資料類型資料行為目標之參數的有效位數和小數位數，和為目標資料行設定的有效位數和小數位數相同。 已將 API 方法新增至 SQLServerPreparedStatement、SQLServerCallableStatement 及 SQLServerResultSet 類別，以接受有效位數和小數位數，以及代表十進位和數值資料類型之參數/資料行的資料值。 請參閱 [JDBC 驅動程式的 Always Encrypted API 參考](always-encrypted-api-reference-for-the-jdbc-driver.md)以取得新的/多載 API 的完整清單。  
- 以 datetime2、datetimeoffset 或 time SQL Server 資料類型的資料行為目標之參數的小數秒數的有效位數/小數位數，不大於修改目標資料行值的查詢中目標資料行的小數秒數的有效位數/小數位數。 已將 API 方法新增至 SQLServerPreparedStatement、SQLServerCallableStatement 及 SQLServerResultSet 類別，以接受小數秒數的有效位數/小數位數，以及代表這些資料類型之參數的資料值。 如需新的/多載 API 的完整清單，請參閱 [JDBC 驅動程式的 Always Encrypted API 參考](always-encrypted-api-reference-for-the-jdbc-driver.md)。

### <a name="errors-due-to-incorrect-connection-properties"></a>不正確連線屬性所導致的錯誤

此節說明如何正確設定連線設定以使用 Always Encrypted 資料。 由於加密的資料類型所支援的轉換有限，**sendTimeAsDatetime** 和 **sendStringParametersAsUnicode** 連線設定在使用加密的資料行時必須進行適當的設定。 請確認：

- 將資料插入加密的時間資料行時，[sendTimeAsDatetime](setting-the-connection-properties.md) 連線設定已設定為 false。 如需詳細資訊，請參閱[設定 java.sql.Time 值如何傳送給伺服器](configuring-how-java-sql-time-values-are-sent-to-the-server.md)。
- 將資料插入加密的 char/varchar/varchar(max) 資料行時，[sendStringParametersAsUnicode](setting-the-connection-properties.md) 連線設定已設定為 true (或保留預設值)。

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>因為傳送純文字，而不是傳送加密值所造成的錯誤。

任何以加密資料行為目標的值都需要在應用程式內加密。 嘗試對加密資料行插入/修改或以純文字值篩選，會造成類似下面的錯誤：

```java
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

若要避免這類錯誤，請確定︰

- (針對連接字串或特定查詢) 以加密資料行為目標的應用程式查詢已啟用 Always Encrypted。
- 您使用陳述式及參數來傳送以加密資料行為目標的資料。 下列範例示範對加密資料行 (SSN) 以常值/常數錯誤篩選 (不是以參數形式在內部傳遞常值)。 此查詢將會失敗：

```java
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## <a name="force-encryption-on-input-parameters"></a>針對輸入參數強制加密

「強制加密」功能會在使用 Always Encrypted 時強制參數的加密。 如果使用強制加密但 SQL Server 向驅動程式告知參數不需要加密，使用該參數的查詢就會失敗。 此屬性會針對受到安全性攻擊危害的 SQL Server 提供額外的保護，此類 SQL Server 會將不正確的加密中繼資料提供給用戶端，而可能導致資料洩露。 SQLServerPreparedStatement 與 SQLServerCallableStatement 類別中的 set* 方法，以及 SQLServerResultSet 類別中的 update\* 方法已進行多載，以接受布林值引數來指定強制加密設定。 如果此引數的值為 false，驅動程式不會針對參數強制加密。 如果強制加密已設定為 true，查詢參數將只會在連線或陳述式上的目的地資料行已加密且 Always Encrypted 已啟用的情況下加以傳送。 使用此屬性可以提供額外的安全性層，確保驅動程式不會錯誤地將預期要加密的資料以純文字的形式傳送到 SQL Server。

如需已搭配強制加密設定進行多載的 SQLServerPreparedStatement 和 SQLServerCallableStatement 方法的詳細資訊，請參閱 [JDBC 驅動程式的 Always Encrypted API 參考](always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>控制 Always Encrypted 的效能影響

因為 Always Encrypted 是用戶端加密技術，大部分的效能額外負荷是在用戶端觀察到，不是在資料庫觀察到。 除了加密和解密作業成本之外，用戶端其他的效能額外負荷來源如下：

- 額外反覆存取資料庫以擷取查詢參數的中繼資料。
- 呼叫資料行主要金鑰存放區以存取資料行主要金鑰。

本節描述 Microsoft JDBC Driver for SQL Server 的內建效能最佳化，以及如何控制上述兩個因素對效能的影響。

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>控制反覆存取以擷取查詢參數的中繼資料

如果連線已啟用 Always Encrypted，驅動程式預設會針對每個參數化查詢呼叫 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)，將查詢陳述式 (不含任何參數值) 傳遞至 SQL Server。 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md) 會分析查詢陳述式，找出是否有任何參數需要加密；如果有，則對每個需要加密的參數傳回加密相關資訊，讓驅動程式加密參數值。 此行為可對用戶端應用程式確保高透明度。 只要應用程式是使用參數來將以加密資料行為目標的值傳遞到驅動程式，應用程式 (及應用程式開發人員) 便不需要知道哪些查詢會存取加密的資料行。

### <a name="setting-always-encrypted-at-the-query-level"></a>在查詢層級設定 [永遠加密]

若要控制擷取參數化查詢之加密中繼資料的效能影響，您可以為個別查詢啟用 Always Encrypted，而不是設定它進行連線。 如此一來，您可以確保只有已知以加密資料行為目標之參數的查詢才能叫用 sys.sp_describe_parameter_encryption。 不過請注意，如此一來會降低加密的透明度︰如果您變更資料庫資料行的加密屬性，您可能需要變更應用程式的程式碼，以配合結構描述變更。

若要控制個別查詢的 Always Encrypted 行為，您需要透過傳遞列舉 SQLServerStatementColumnEncryptionSetting 來設定個別陳述式物件，該列舉會指定在針對該特定陳述式讀取及寫入加密的資料行時，資料的傳送及接收方式。 以下是一些實用的方針：

- 如果用戶端應用程式透過資料庫連線傳送的大多數查詢都會存取加密資料行，請使用下列指導方針：

    - 將 **columnEncryptionSetting** 連接字串關鍵字設定為 [啟用]  。
    - 對不會存取任何加密資料行的個別查詢設定 SQLServerStatementColumnEncryptionSetting.Disabled。 此設定將停用呼叫 sys.sp_describe_parameter_encryption 以及嘗試解密結果集內的任何值。
    - 對沒有任何參數要求加密，但會從加密資料行擷取資料的個別查詢設定 SQLServerStatementColumnEncryptionSetting.ResultSet。 此設定會停用呼叫 sys.sp_describe_parameter_encryption 和參數加密。 查詢將能夠解密來自加密資料行的結果。

- 如果用戶端應用程式透過資料庫連線傳送的大多數查詢都不會存取加密資料行，請使用下列指導方針：

    - 將 **columnEncryptionSetting** 連接字串關鍵字設定為 [停用]  。
    - 對有任何參數需要加密的個別查詢設定 SQLServerStatementColumnEncryptionSetting.Enabled。 此設定會啟用呼叫 sys.sp_describe_parameter_encryption 以及解密擷取自加密資料行的任何查詢結果。
    - 對沒有任何參數要求加密，但會從加密資料行擷取資料的查詢設定 SQLServerStatementColumnEncryptionSetting.ResultSet。 此設定會停用呼叫 sys.sp_describe_parameter_encryption 和參數加密。 查詢將能夠解密來自加密資料行的結果。

SQLServerStatementColumnEncryptionSetting 設定不能用來略過加密並存取純文字資料。 如需如何設定陳述式上資料行加密的詳細資訊，請參閱 [JDBC 驅動程式的 Always Encrypted API 參考](always-encrypted-api-reference-for-the-jdbc-driver.md)。  

在下列範例中，資料庫連線已停用 Always Encrypted。 應用程式發出的查詢具有以 LastName 資料行為目標的參數，而此資料行未加密。 查詢會從加密的 SSN 和 BirthDate 資料行擷取資料。 在這種情況下，不需要呼叫 sys.sp_describe_parameter_encryption 以擷取加密中繼資料。 不過，需要啟用查詢結果的解密，以使應用程式從兩個加密資料行接收純文字值。 SQLServerStatementColumnEncryptionSetting.ResultSet 設定是用來確保這點。

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

您可以使用 SQLServerConnection 類別中的 setColumnEncryptionKeyCacheTtl() API，針對快取中的資料行加密金鑰項目設定存留時間值。 快取中資料行加密金鑰項目的預設存留時間值是兩小時。 若要關閉快取，請使用 0 的值。 若要設定任何存留時間值，請使用下列 API：

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

例如，若要設定 10 分鐘的存留時間值，請使用：

```java
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

僅支援使用 DAYS、HOURS、MINUTES 或 SECONDS 作為時間單位。  

## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>使用 SQLServerBulkCopy 複製加密的資料

使用 SQLServerBulkCopy，您可以將已加密並儲存在某個資料表的資料，複製到另一個資料表，而不需要解密資料。 若要這樣做：

- 請確定目標資料表的加密組態與來源資料表的組態完全一致。 特別是，這兩個資料表都必須加密相同的資料行，且這些資料行必須使用相同的加密類型和相同的加密金鑰來加密。 如果任一目標資料行的加密方式不同於其對應的來源資料行，您將無法在複製作業後，解密目標資料表中的資料。 資料會損毀。
- 設定這兩個資料庫對來源資料表和目標資料表的連線，但不啟用 Always Encrypted。
- 設定 allowEncryptedValueModifications 選項。 如需詳細資訊，請參閱[搭配 JDBC 驅動程式使用大量複製](using-bulk-copy-with-the-jdbc-driver.md)。

> [!NOTE]
> 指定 AllowEncryptedValueModifications 時請小心，此選項可能會導致資料庫損毀；因為 Microsoft JDBC Driver for SQL Server 不會檢查資料是否確實加密，或是否使用和目標資料行相同的加密類型、演算法和金鑰正確加密。

## <a name="see-also"></a>另請參閱

[Always Encrypted (資料庫引擎)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
