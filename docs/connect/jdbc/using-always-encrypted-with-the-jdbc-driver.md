---
title: "JDBC 驅動程式搭配使用一律加密 |Microsoft 文件"
ms.custom: 
ms.date: 12/30/2016
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
caps.latest.revision: "64"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ec20c538020cd9d81e8df262dca3f5b171dbc7a7
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>搭配使用一律加密與 JDBC 驅動程式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文提供有關如何開發使用的 Java 應用程式資訊[永遠加密](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7)和 Microsoft JDBC Driver 6.0 （或更新版本） for SQL Server。

一律加密可讓用戶端加密機密資料，並永遠不會顯示資料或 SQL Server 或 Azure SQL Database 的加密金鑰。 永遠加密啟用 SQL Server 驅動程式，例如 Microsoft JDBC Driver 6.0 （或更高），進而達成此目的透過無障礙地加密與解密用戶端應用程式中的機密資料。 驅動程式會自動判斷哪一個查詢參數對應至敏感性資料庫資料行 （使用 永遠加密保護），並再將值傳遞至 SQL Server 或 Azure SQL Database 會加密這些參數的值。 同樣地，驅動程式會以清晰簡明的方式，將擷取自查詢結果的加密資料庫資料行資料進行解密。 如需詳細資訊，請瀏覽[一律加密 (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7)和[一律加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。  


## <a name="prerequisites"></a>必要條件

- 在資料庫中設定永遠加密。 這牽涉到佈建永遠加密金鑰，以及設定加密所選資料庫資料行。 如果您的資料庫尚未設定 [永遠加密]，請遵循 [Getting Started with Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_5)(永遠加密快速入門) 中的指示操作。
- 請確定 Microsoft JDBC Driver 6.0 （或更新版本） 的開發電腦上安裝 SQL Server。 
-   下載並安裝 Java 密碼編譯延伸模組 (JCE) 無限制的強度管轄權原則檔。  請務必閱讀 ZIP 檔案中的讀我檔案，以了解安裝指示及可能的匯出/匯入問題相關詳細資訊。  
  
    -   如果使用 sqljdbc41.jar，可以從下載原則檔[下載 Java 密碼編譯延伸模組 (JCE) 無限制的強度管轄權原則檔 7](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)  
  
    -   如果使用 sqljdbc42.jar，可以從下載原則檔[下載 Java 密碼編譯延伸模組 (JCE) 無限制的強度管轄權原則檔 8](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)   
    
## <a name="enabling-always-encrypted-for-application-queries"></a>為應用程式查詢啟用 [永遠加密]  
若要啟用參數的加密及解密目標加密資料行的查詢結果的最簡單方式是藉由設定的值**columnEncryptionSetting**連接字串關鍵字設**啟用**。

JDBC 驅動程式中啟用 永遠加密的連接字串範例如下：
  
```  
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;"; 
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);
     
```  
  
此外，以下是使用 SQLServerDataSource 物件的對等範例。  
  
```  
SQLServerDataSource ds = new SQLServerDataSource();  
ds.setServerName("localhost");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");  
SQLServerConnection con = (SQLServerConnection) ds.getConnection(); 
```    

個別查詢也可以啟用 [永遠加密]。 請參閱**控制效能影響的永遠加密**下一節。 請注意，啟用 [永遠加密] 並不足以保證加密或解密成功。 您還需要確定︰
- 應用程式要有 [檢視任何資料行的主要金鑰定義] 和 [檢視任何資料行的加密金鑰定義] 資料庫權限，才能存取資料庫中永遠加密金鑰的相關中繼資料。 如需詳細資料，請參閱[一律加密 (Database Engine) ](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_7)的＜權限＞一節。
- 應用程式可以加密查詢的資料庫資料行，存取保護資料行加密金鑰的資料行主要金鑰。 請注意，使用您需要提供額外的認證，連接字串中的 Java 金鑰存放區提供者。 請參閱**使用 Java 金鑰存放區提供者**> 一節以取得詳細資料。

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>設定如何將 java.sql.Time 值傳送至伺服器

**SendTimeAsDatetime**連接屬性用來設定如何將 java.sql.Time 值傳送至伺服器。 當 sendTimeAsDatetime = false，值傳送為 SQL Server 時間類型的時間及何時 sendTimeAsDatetime = true 時，值傳送為 datetime 類型的時間。 請注意，加密 time 資料行，則 sendTimeAsDatetime 屬性必須是 false 因為加密資料行不支援時間轉換成日期時間。 另外請注意，此屬性為預設值為 true，因此在使用加密的時間資料行，您必須將它設定為 false。 否則驅動程式將會擲回例外狀況。 SQLServerConnection 類別有兩種方法，開頭為 6.0 版的驅動程式，以程式設計方式設定這個屬性的值：
 
* public void setSendTimeAsDatetime (sendTimeAsDateTimeValue 布林值)
* public boolean getSendTimeAsDatetime()

如需這個屬性的詳細資訊請造訪[如何設定 java.sql.Time 值傳送給伺服器](https://msdn.microsoft.com/library/ff427224(v=sql.110).aspx)。 

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>設定字串值如何傳送至伺服器

**SendStringParametersAsUnicode**連接屬性用來設定如何將字串值傳送至 SQL Server。 如果設定為"true"，String 參數傳送到伺服器以 Unicode 格式。 如果設定為"false"，String 參數會以非 Unicode 格式 （例如 ASCII/MBCS) 而非 Unicode 傳送。 這個屬性的預設值為"true"。 當啟用 永遠加密，並 char/varchar/varchar(max) 資料行已加密，值**sendStringParametersAsUnicode**必須設為 true （或保留為預設值）。 插入資料至 char/varchar/varchar(max) 加密資料行，如果這個屬性設定為 false 時，Microsoft JDBC Driver for SQL Server 將會擲回例外狀況。 如需有關這個屬性的詳細資訊，請瀏覽[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。 
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>擷取和修改加密資料行中的資料

一旦您啟用 永遠加密的應用程式查詢，您可以使用標準的 JDBC Api 來擷取或修改加密的資料庫資料行中的資料。 假設您的應用程式具有必要的資料庫權限，可以存取資料行主要金鑰，Microsoft JDBC Driver for SQL Server 會加密目標加密資料行，以及解密資料的任何查詢參數擷取自加密資料行傳回的純文字值的 JDBC 型別，對應至 SQL Server 設定資料庫結構描述中的資料行資料類型。
如未啟用 [永遠加密]，使用目標加密資料行參數的查詢就會失敗。 只要查詢沒有以加密資料行為目標的參數，查詢就仍然可以從加密資料行擷取資料。 不過，Microsoft JDBC Driver for SQL Server 不會嘗試解密擷取自加密資料行的任何值，而且應用程式將會收到二進位的加密的資料 （以位元組陣列）。

下表摘要說明查詢的行為，視 [永遠加密] 是否啟用而定︰

|查詢特性 | [永遠加密] 已啟用，且應用程式可以存取金鑰和金鑰中繼資料|[永遠加密] 已啟用，但應用程式不能存取金鑰或金鑰中繼資料 | [永遠加密] 已停用|
|:---|:---|:---|:---|
| 有以加密資料行為目標之參數的查詢。 | 以清晰簡明的方式加密參數值。 | 錯誤 | 錯誤|
| 查詢從加密的資料行擷取資料，沒有任何以加密資料行為目標的參數。| 以清晰簡明的方式解密來自加密資料行的結果。 應用程式接收加密的資料行設定之 SQL Server 類型對應的 JDBC 資料類型的純文字值。 | 錯誤 | 不解密來自加密資料行的結果。 應用程式收到位元組陣列 (byte[]) 形態的加密值。
      
 
### <a name="inserting-and-retrieving-encrypted-data-examples"></a>插入及擷取加密的資料範例 
以下範例將說明擷取和修改加密資料行中的資料。 這些範例假設目標資料表具有下列結構描述。 請注意，SSN 和 BirthDate 資料行均已加密。

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
 
### <a name="inserting-data-example"></a>插入資料範例

本例會將資料列插入病患資料表。 請注意下列事項：
- 範例程式碼中沒有任何需要加密的特定項目。 Microsoft JDBC Driver for SQL Server 會自動偵測，並會加密目標加密資料行的參數。 這讓加密對應用程式變得透明化。 
- 插入至資料庫資料行，包括加密的資料行的值會當做參數使用 SQLServerPreparedStatement 傳遞。 雖然使用參數是選擇性的值傳送至非加密的資料行 （不過，強烈建議因有利於防止 SQL 資料隱碼） 時，才能進行加密的資料行為目標的值。 如果傳遞做為內嵌在查詢陳述式中的常值插入加密的資料行中的值，則查詢會失敗，因為 Microsoft JDBC Driver for SQL Server 會無法判斷目標加密資料行中的值，因此它不會加密值。 結果，伺服器會因與加密資料行不相容而拒絕它們。
- 列印程式的所有值都會以純文字形式 Microsoft JDBC Driver for SQL Server 會以透明的方式解密擷取自加密資料行的資料。
- 如果您要查閱使用的子句，WHERE 子句中使用的值必須傳送做為參數，如此當 Microsoft JDBC Driver for SQL Server 以透明的方式加密它，再傳送至資料庫。 下列範例中，請注意，SSN 傳遞做為參數，但是 LastName 被當做為 LastName 的常值中不會加密。
- SSN 資料行為目標的參數使用的 setter 方法是 setString()，對應到 char/varchar SQL Server 資料類型。 如果這個參數，所使用的 setter 方法為 setNString()，對應至 nchar/nvarchar，則查詢會失敗，因為永遠加密 不支援加密的 nchar/nvarchar 值轉換成加密的 char/varchar 值。  

```
String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
try  
{           
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

下例示範根據加密值篩選資料，以及從加密資料行擷取純文字資料。 請注意下列事項：
- 使 Microsoft JDBC Driver for SQL Server 可以明確地加密它傳送至資料庫之前，先傳遞做為參數，用在 WHERE 子句來篩選 SSN 資料行需要的值。
- 列印程式的所有值都會以純文字形式 Microsoft JDBC Driver for SQL Server 會以透明的方式解密從 SSN 和 BirthDate 資料行擷取的資料。

> [!NOTE]  
>  如果使用具確定性的加密來進行加密，則查詢可執行資料行的相等比較。 如需詳細資訊，請參閱**選取具確定性或隨機化加密**區段[一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)主題。  

```
String connectionString =  "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;" ;
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
catch (Exception e)  
{  
    e.printStackTrace();  
}
```
  
### <a name="retrieving-encrypted-data-example"></a>擷取加密的資料範例

如未啟用 [永遠加密]，只要查詢沒有以加密資料行為目標的參數，查詢就仍然可以從加密資料行擷取資料。

下列範例會示範從加密資料行擷取二進位的加密資料。 請注意下列事項：

- 因為連接字串未啟用 [永遠加密]，所以查詢會以位元組陣列 (程式會將值轉換為字串) 傳回加密的 SSN 和 BirthDate 值。
- 從加密資料行擷取資料但停用 [永遠加密] 的查詢可以有參數，只要沒有任何參數以加密資料行為目標。 上述依 LastName 篩選的查詢，在資料庫中未加密。 如果依 SSN 或 BirthDate 篩選查詢，查詢會失敗。

```
String connectionString  = "jdbc:sqlserver://localhost:1433;" + "databaseName=Clinic;user=sa;password=******";

String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;"; 
 
try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))  
{  
    selectStatement.setString(1, "Abel");  
    ResultSet rs = selectStatement.executeQuery();   
    while(rs.next())
    {  
        System.out.println("SSN: " + rs.getString("SSN") +
         ", FirstName: " + rs.getString("FirstName") + 
        ", LastName:"+ rs.getString("LastName")+ 
        ", Date of Birth: " + rs.getString("BirthDate"));  
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

[永遠加密] 支援極少數的加密資料類型轉換。 請參閱[一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)支援的類型轉換詳細清單。 以下是避免資料類型轉換錯誤時可以做的事，請確定︰

- 您的適當 setter 方法傳遞時使用加密的資料行為目標之參數的值以便參數的 SQL Server 資料類型可能是完全相同做為目標資料行或參數的 SQL Server 資料類型轉換的類型目標支援的資料行的類型。 請注意新的 API 方法已加入 SQLServerPreparedStatement、 SQLServerCallableStatement 和 SQLServerResultSet 類別傳遞參數對應到特定的 SQL Server 資料類型。 例如，如果未加密的資料行可以使用 setTimestamp() 方法將參數 datetime2 或 datetime 資料行。 但是，資料行加密時必須使用表示在資料庫中資料行的類型的確切方法。 例如，將值傳遞至加密的 datetime2 資料行，並將值傳遞到加密的日期時間資料行使用 setDateTime() 使用 setTimestamp()。 請參閱[一律加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)的新應用程式開發介面的完整清單。 
- 以小數和數值 SQL Server 資料類型資料行為目標之參數的有效位數和小數位數，和為目標資料行設定的有效位數和小數位數相同。 請注意，已加入新的應用程式開發介面方法給 SQLServerPreparedStatement、 SQLServerCallableStatement 和 SQLServerResultSet 類別，以接受有效位數和小數位數，以及代表 decimal 和 numeric 資料類型的參數/資料行的資料值。 請參閱[一律加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)的新/多載的應用程式開發介面的完整清單。  
- 小數秒數有效位數/小數位數 datetime2、 datetimeoffset 或時間 SQL Server 資料類型資料行為目標的參數不大於目標資料行，修改的目標資料行值的查詢中。 請注意，已加入新的應用程式開發介面方法給 SQLServerPreparedStatement、 SQLServerCallableStatement 和 SQLServerResultSet 類別，以接受小數秒有效位數/小數位數以及代表這些資料型別參數的資料值。 請參閱[一律加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)的新/多載的應用程式開發介面的完整清單。   

### <a name="errors-due-to-incorrect-connection-properties"></a>因為不正確的連接屬性的錯誤
本章節描述如何設定以使用一律加密資料的連接設定。 加密的資料類型支援有限的轉換，因為 'sendTimeAsDatetime' 和 'sendStringParametersAsUnicode' 的連線設定使用加密的資料行時，就會需要適當的組態設定。 請確認： 
- [sendTimeAsDatetime](https://msdn.microsoft.com/library/ff427224(v=sql.110).aspx)連接設定為 false，將資料插入加密時間資料行時。 如需詳細資訊，請參閱 '設定 java.sql.Time 值如何傳送至伺服器' 區段。
- [sendStringParametersAsUnicode](../../connect/jdbc/setting-the-connection-properties.md)連接設定設定為 true （或保留為預設值） 時將資料插入加密的 char/varchar/varchar(max) 資料行。 如需詳細資訊，請參閱 '設定字串值如何傳送至伺服器' 區段。

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>因為傳遞純文字，而不是加密的值發生錯誤

任何以加密資料行為目標的值都需要在應用程式內加密。 嘗試對加密資料行插入/修改或以純文字值篩選，會造成類似下面的錯誤︰


```
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

若要避免這類錯誤，請確定︰
- 永遠加密 已啟用的應用程式 （連接字串，或以特定的查詢） 的加密的資料行為目標的查詢。
- 您使用備妥的陳述式和參數來傳送資料的目標加密資料行。 下列範例會顯示錯誤篩選常值/常數對加密資料行 (SSN)，而不是做為參數傳遞常值內的查詢。 此查詢會失敗。

```
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");  
```

## <a name="working-with-column-master-key-stores"></a>使用資料行主要金鑰存放區
若要加密參數值或解密查詢結果中的資料，Microsoft JDBC Driver for SQL Server 需要取得目標資料行設定資料行加密金鑰。 資料行加密金鑰會儲存在資料庫中繼資料中的加密形式。 每個資料行加密金鑰都有對應的資料行主要金鑰，主要金鑰是用於加密資料行加密金鑰。 資料庫中繼資料不儲存資料行主要金鑰，它只包含金鑰存放區的相關資訊，金鑰存放區包含特定的資料行主要金鑰以及金鑰存放區的金鑰位置。

若要取得純文字值的資料行加密金鑰，Microsoft JDBC Driver for SQL Server 會先取得有關資料行加密金鑰和其對應資料行主要金鑰的中繼資料，然後它會使用資訊的中繼資料中向下鍵存放區，包含資料行主要金鑰和解密加密資料行加密金鑰。 Microsoft JDBC Driver for SQL Server 與金鑰存放區，使用資料行主要金鑰存放區提供者 – 這是類別的執行個體衍生自通訊**SQLServerColumnEncryptionKeyStoreProvider**類別。


### <a name="using-built-in-column-master-key-store-providers"></a>使用內建資料行主要金鑰存放區提供者
  
Microsoft JDBC Driver for SQL Server 隨附於下列內建的資料行主要金鑰存放區提供者。 請注意，這些提供者的某些預先註冊使用特定提供者名稱 （用來查閱提供者），而且有些需要額外的認證或明確註冊。

| 類別 | 描述 | 提供者 (查閱) 名稱 |預先註冊嗎？|
|:---|:---|:---|:---|
|**SQLServerColumnEncryptionAzureKeyVaultProvider**| Azure 金鑰保存庫的金鑰存放區提供者。| AZURE_KEY_VAULT|否|
|**SQLServerColumnEncryptionCertificateStoreProvider**| Windows 憑證存放區提供者。|MSSQL_CERTIFICATE_STORE|是
|**SQLServerColumnEncryptionJavaKeyStoreProvider**| Java 金鑰存放區提供者|MSSQL_JAVA_KEYSTORE|是|

預先註冊的金鑰存放區提供者就不需要變更任何應用程式程式碼以使用這些提供者，但請注意下列：

- 您 (或您的 DBA) 需要確認設定在資料行主要金鑰中繼資料的提供者名稱是否正確，且資料行主要金鑰路徑符合指定提供者有效的金鑰路徑格式。 建議您使用 SQL Server Management Studio 等工具設定金鑰，這樣在發出 CREATE COLUMN MASTER KEY (Transact-SQL) 陳述式時，會自動產生有效的提供者名稱和金鑰路徑。
- 您需要確定應用程式可以存取金鑰存放區中的金鑰。 這可能牽涉到授與應用程式金鑰和/或金鑰存放區的存取權 (視金鑰存放區而定)，或執行其他的金鑰存放區特定組態步驟。 例如，使用 SQLServerColumnEncryptionJavaKeyStoreProvider 您需要提供的位置和連線內容中的金鑰存放區的密碼。 

所有這些金鑰存放區提供者是以下更詳細說明。
  
### <a name="using-azure-key-vault-provider"></a>使用 Azure 金鑰保存庫提供者
Azure 金鑰保存庫是存放和管理永遠加密資料行主要金鑰的方便選項 (尤其是當應用程式裝載在 Azure 時)。 Microsoft JDBC Driver for SQL Server 包含內建的提供者，SQLServerColumnEncryptionAzureKeyVaultProvider，具有索引鍵儲存在 Azure 金鑰保存庫中的應用程式。 此提供者的名稱是 AZURE_KEY_VAULT。 若要使用 Azure 金鑰保存庫的存放區提供者，應用程式開發人員需要在 Azure 中建立保存庫和金鑰設定應用程式存取金鑰。 如需有關如何設定金鑰保存庫及建立資料行主要金鑰是指[Azure 金鑰保存庫-Step by Step 如需有關設定金鑰保存庫](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)和[Azure 金鑰保存庫中建立資料行主要金鑰](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2).  
  
若要使用 Azure 金鑰保存庫，用戶端應用程式需要 SQLServerColumnEncryptionAzureKeyVaultProvider 具現化，並向驅動程式。

初始化 SQLServerColumnEncryptionAzureKeyVaultProvider 的範例如下：  
  
```  
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey); 
```

應用程式建立 SQLServerColumnEncryptionAzureKeyVaultProvider 的執行個體之後，應用程式必須登錄 Microsoft JDBC Driver for SQL Server 使用的執行個體Sqlserverconnection.registercolumnencryptionkeystoreproviders （） 方法。 強烈建議，使用預設查詢名稱 AZURE_KEY_VAULT，可以藉由呼叫 SQLServerColumnEncryptionAzureKeyVaultProvider.getName() API 取得註冊執行個體。 使用預設名稱，可讓您使用工具，例如 SQL Server Management Studio 或 PowerShell，來佈建和管理永遠加密金鑰 （工具來產生資料行主要金鑰的中繼資料物件使用的預設名稱）。 下列範例會顯示註冊 Azure 金鑰保存庫提供者。 如需有關 sqlserverconnection.registercolumnencryptionkeystoreproviders （） 方法的詳細資訊，請參閱[一律加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。 

```
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();   
keyStoreMap.put(akvProvider.getName(), akvProvider);   
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);   
```
  
> [!IMPORTANT]  
>  JDBC 驅動程式的 Azure 金鑰保存庫實作具有這些程式庫 （GitHub) 的相依性：  
>   
>  [azure-sdk-如-java](https://github.com/Azure/azure-sdk-for-java)  
>   
>  [azure-activedirectory-程式庫-如-java 文件庫](https://github.com/AzureAD/azure-activedirectory-library-for-java)  
  
### <a name="using-windows-certificate-store-provider"></a>使用 Windows 憑證存放區提供者
SQLServerColumnEncryptionCertificateStoreProvider 可以用來將資料行主要金鑰儲存在 Windows 憑證存放區。 使用 [SQL Server Management Studio (SSMS) 永遠加密精靈] 或其他支援的工具來建立資料行主要金鑰和資料行加密金鑰定義資料庫中。 相同的精靈可以用來產生自我簽署的憑證是在 Windows 憑證存放區為資料行主要金鑰用於永遠加密的資料。 如需有關資料行主要金鑰和資料行加密金鑰的 T-SQL 語法瀏覽[CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)和[CREATE COLUMN 如此 KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md)分別。

SQLServerColumnEncryptionCertificateStoreProvider 名稱是"MSSQL_CERTIFICATE_STORE 」，而且可以進行查詢 getName() 應用程式開發介面的提供者物件。 它會自動註冊的驅動程式，並可以順暢地使用，而不需要任何應用程式變更。

> [!IMPORTANT]  
>  適用於只有 Windows 作業系統與具有相依性所提供的驅動程式套件中的 sqljdbc_auth.dll SQLServerColumnEncryptionCertificateStoreProvider 實作 JDBC 驅動程式。  若要使用此提供者，將 sqljdbc_auth.dll 檔案複製到安裝 JDBC 驅動程式的電腦上的 Windows 系統路徑的目錄。 或者，您也可以設定 java.libary.path 系統屬性來指定 sqljdbc_auth.dll 的目錄。 如果您執行的是 32 位元的 Java Virtual Machine (JVM)，即使作業系統為 x64 版，也請使用 x86 資料夾中的 sqljdbc_auth.dll 檔案。 如果您是在 x64 處理器上執行 64 位元的 JVM，請使用 x64 資料夾中的 sqljdbc_auth.dll 檔案。 例如，如果您使用 32 位元的 JVM，JDBC 驅動程式安裝在預設目錄，您可以指定 DLL 的位置啟動的 Java 應用程式時，請使用下列虛擬機器 (VM) 引數：  
`-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`
        
### <a name="using-java-key-store-provider"></a>使用 Java 金鑰存放區提供者  
JDBC 驅動程式隨附內建金鑰存放區提供者實作 Java 金鑰存放區。 此驅動程式會自動具現化，並註冊 Java 金鑰存放區，提供者，如果**keyStoreAuthentication**連接字串屬性的連接字串中且設定為"JavaKeyStorePassword 」 （，請參閱以下詳細說明）。 Java 金鑰存放區提供者的名稱是 MSSQL_JAVA_KEYSTORE。 此名稱也可以查詢 SQLServerColumnEncryptionJavaKeyStoreProvider.getName() api。 

導入三個新的連接字串關鍵字可讓用戶端應用程式，以宣告方式指定驅動程式必須向 Java 金鑰存放區的認證。 驅動程式會初始化提供者，根據特定連線的連接字串，下列三個屬性的值。 
  
 **keyStoreAuthentication:**識別要使用金鑰存放區。 Microsoft JDBC Driver 6.0 for SQL Server，您可以驗證這個屬性只能透過 Java 金鑰存放區。 Java 金鑰存放區中，這個屬性的值必須是"JavaKeyStorePassword"。   
  
 **keyStoreLocation:**儲存資料行主要金鑰的 Java keystore 檔案路徑。 請注意，路徑中包含的金鑰存放區檔案名稱。  
  
 **keyStoreSecret:**密碼/密碼用於 keystore 和索引鍵。 請注意，使用 Java 金鑰存放區的金鑰存放區和金鑰的密碼必須相同。  

以下是在提供連接字串中的這些認證的範例：

    String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
    
這些設定也可以使用 SQLServerDataSource 物件的設定/取得。 請參閱[一律加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)如需詳細資訊。     
  
JDBC 驅動程式會自動具現化 SQLServerColumnEncryptionJavaKeyStoreProvider 時這些認證會在連接屬性。 
  
### <a name="creating-a-column-master-key-for-the-java-key-store"></a>建立 Java 金鑰存放區資料行主要金鑰
SQLServerColumnEncryptionJavaKeyStoreProvider 可以搭配 JKS 或 PKCS12 金鑰存放區型別。 若要建立或匯入要與此提供者所使用的金鑰會使用 Java [keytool](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html)公用程式。 請注意，金鑰必須有自己的金鑰存放區為相同的密碼。 以下是如何建立公開金鑰和其相關聯的私密金鑰使用 keytool 公用程式的範例。

    keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks    

此命令會建立公開金鑰，並將其包裝的自我簽署憑證，然後儲存在金鑰存放區以及與其相關聯的私密金鑰 ' keystore.jks X.509 中。 別名 'AlwaysEncryptedKey' 識別的金鑰存放區中此項目。 

以下是相同的使用 PKCS12 storetype 的範例。 

    keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword   

請注意，如果是金鑰存放區類型 PKCS12 keytool 公用金鑰密碼和金鑰的密碼不會提示必須提供-keypass 選項，因為 SQLServerColumnEncryptionJavaKeyStoreProvider 需要金鑰存放區和索引鍵有相同的密碼。

您也可以從 Windows 憑證存放區，以.pfx 格式匯出憑證，並使用可搭配 SQLServerColumnEncryptionJavaKeyStoreProvider。 匯出的憑證也可匯入 Java 金鑰存放區為 JKS 金鑰存放區型別。 

建立 keytool 項目之後，您必須在需要金鑰存放區提供者名稱和金鑰路徑的資料庫中建立的資料行主要金鑰中繼資料。 如需有關如何建立資料行主要金鑰中繼資料瀏覽[CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)。 SQLServerColumnEncryptionJavaKeyStoreProvider，機碼路徑中的索引鍵的別名。 而 SQLServerColumnEncryptionJavaKeyStoreProvider 名稱為 'MSSQL_JAVA_KEYSTORE'。 您也可以查詢此使用 getName() SQLServerColumnEncryptionJavaKeyStoreProvider 類別的公用 API 的名稱。 

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
>  內建在 SQL Server management Studio 功能無法建立資料行主要金鑰定義 Java 金鑰存放區，您必須使用 T-SQL 命令。  
  
### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>建立 Java 金鑰存放區資料行加密金鑰
請注意，SQL Server management Studio 或任何其他工具沒有可用來建立資料行使用 Java 金鑰存放區中的資料行主要金鑰的加密金鑰。 用戶端應用程式必須建立以程式設計方式使用 SQLServerColumnEncryptionJavaKeyStoreProvider 類別資料行加密金鑰。 如需詳細資訊，請造訪 '使用資料行主要金鑰存放區提供者進行程式設計的金鑰佈建' 區段。 

  
### <a name="implementing-a-custom-column-master-key-store-provider"></a>實作自訂資料行主要金鑰存放區提供者
如果您想要將資料行主要金鑰儲存在現有的提供者不支援的金鑰存放區，您可以實作自訂提供者擴充 SQLServerColumnEncryptionKeyStoreProvider 類別，以及註冊使用的提供者Sqlserverconnection.registercolumnencryptionkeystoreproviders （） 方法。
  
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

當存取加密資料行時，Microsoft JDBC Driver for SQL Server 會明確地尋找並呼叫正確的資料行主要金鑰存放區提供者來解密資料行加密金鑰。 一般來說，一般應用程式程式碼不會直接呼叫資料行主要金鑰存放區提供者。 但是您可以明確具現化和呼叫提供者，以程式設計方式佈建和管理永遠加密金鑰︰產生加密的資料行加密金鑰和解密資料行加密金鑰 (例如作為部分資料行主要金鑰輪替)。 如需詳細資訊，請參閱 [永遠加密的金鑰管理概觀](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。
請注意，只有使用自訂的金鑰存放區提供者時，才可能需要實作您自己的金鑰管理工具。 在使用儲存在 Windows 憑證存放區或 Azure 金鑰保存庫中的金鑰時，您可以使用現有的工具，例如 SQL Server Management Studio 或 PowerShell，來管理和佈建金鑰。 當使用 Java 金鑰存放區中的金鑰時，您需要以程式設計方式佈建金鑰。 下列範例中，說明如何使用 SQLServerColumnEncryptionJavaKeyStoreProvider 類別來加密金鑰儲存在 Java 金鑰存放區索引鍵。

```  
import java.sql.*;
import javax.xml.bind.DatatypeConverter;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programatically for the Java Key Store.
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
                 * For more details on the syntax refer: 
                 * https://msdn.microsoft.com/library/mt146372.aspx
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
         * Following arguments needed by  SQLServerColumnEncryptionJavaKeyStoreProvider
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
  
## <a name="force-encryption-on-input-parameters"></a>輸入參數上強制加密
  
使用永遠加密時，[強制加密] 功能會強制加密參數。 如果使用強制加密，而且 SQL Server 通知驅動程式參數不需要加密，使用參數的查詢將會失敗。 此屬性會針對受到安全性攻擊危害的 SQL Server 提供額外的保護，此類 SQL Server 會將不正確的加密中繼資料提供給用戶端，而可能導致資料洩露。 設定 * 方法在 SQLServerPreparedStatement 和 SQLServerCallableStatement 類別和更新\*SQLServerResultSet 類別的方法多載接受布林值的引數來指定 強制加密設定。 如果這個引數的值為 false，驅動程式將不會強制加密參數。 強制加密 」 設定為 true，查詢參數時才會傳送如果目的地資料行已加密，並啟用 永遠加密的連接時或在陳述式。 這可提供一層額外的安全性，確保沒有資料會不小心傳送以 SQL Server 以純文字形式預期要加密時。  
  
 [強制加密] 設定使用 SQLServerPreparedStatement 和 SQLServerCallableStatement 方法多載資訊，請參閱[一律加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-performance-impact-of-always-encrypted"></a>控制永遠加密的影響效能

因為 [永遠加密] 是用戶端加密技術，大部分的效能額外負荷是在用戶端觀察到，不是在資料庫觀察到。 除了加密和解密作業成本之外，用戶端其他的效能額外負荷來源如下︰
- 額外反覆存取資料庫以擷取查詢參數的中繼資料。
- 呼叫資料行主要金鑰存放區以存取資料行主要金鑰。

本章節描述 Microsoft JDBC 驅動程式中的內建效能最佳化，適用於 SQL Server 和如何控制上述兩個因素對效能的影響。

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>控制反覆存取以擷取查詢參數的中繼資料

如果啟用 永遠加密的連接，根據預設，會呼叫 Microsoft JDBC Driver for SQL Server [sys.sp_describe_parameter_encryption](https://msdn.microsoft.com/library/mt631693.aspx?f=255&MSPPError=-2147217396)每個參數化查詢，傳遞 （不含任何查詢陳述式參數值） 到 SQL Server。 [sys.sp_describe_parameter_encryption](https://msdn.microsoft.com/library/mt631693.aspx?f=255&MSPPError=-2147217396)會分析查詢陳述式，以找出任何參數需要加密，且因此，對每個會傳回加密相關的資訊，讓 Microsoft JDBC Driver for SQL Server若要加密參數值。 上述行為可對用戶端應用程式確保高透明度。 應用程式 （及應用程式開發人員） 不需要留意哪些查詢存取加密資料行，只要目標加密資料行的值會傳遞至 Microsoft JDBC Driver for SQL Server 做為參數。


#### <a name="setting-always-encrypted-at-the-query-level"></a>在查詢層級設定 [永遠加密]

若要控制擷取參數化查詢之加密中繼資料的效能影響，您可以為個別查詢啟用 [永遠加密]，而不是設定它進行連接。 如此一來，您可以確保只有您知道有以加密資料行為目標之參數的查詢可以叫用 sys.sp_describe_parameter_encryption。 不過請注意，如此一來會降低加密的透明度︰如果您變更資料庫資料行的加密屬性，您可能需要變更應用程式的程式碼，以配合結構描述的變更。


若要控制個別查詢的永遠加密行為，您必須設定個別的陳述式物件，藉由傳遞列舉 SQLServerStatementColumnEncryptionSetting，指定將如何傳送和接收時讀取和寫入資料針對該特定陳述式的加密資料行。 以下是一些實用的方針：
- 如果用戶端應用程式透過資料庫連接傳送的大多數查詢都會存取加密資料行：
    - 將 columnEncryptionSetting 連接字串關鍵字設定為 已啟用。
    - 不會存取任何加密資料行的個別查詢設定 SQLServerStatementColumnEncryptionSetting.Disabled。 這會停用呼叫 sys.sp_describe_parameter_encryption 以及嘗試解密結果集內的任何值。
    - 設定 SQLServerStatementColumnEncryptionSetting.ResultSet 的個別查詢沒有任何參數要求加密，但會從加密資料行擷取資料。 這會停用呼叫 sys.sp_describe_parameter_encryption 和參數加密。 查詢將能夠解密來自加密資料行的結果。
- 如果用戶端應用程式透過資料庫連接傳送的大多數查詢都不會存取加密資料行：
    - ColumnEncryptionSetting 連接字串關鍵字設為停用。
    - 如有任何參數需要加密的個別查詢設定 SQLServerStatementColumnEncryptionSetting.Enabled。 這可以呼叫 sys.sp_describe_parameter_encryption 以及解密擷取自加密資料行的任何查詢結果。
    - 設定 SQLServerStatementColumnEncryptionSetting.ResultSet 並沒有任何參數要求加密，但會從加密資料行擷取資料的查詢。 這會停用呼叫 sys.sp_describe_parameter_encryption 和參數加密。 查詢將能夠解密來自加密資料行的結果。

請注意，SQLServerStatementColumnEncryptionSetting 設定不會用來略過加密並存取純文字資料。 如需有關如何在陳述式上設定資料行加密的詳細資訊，請參閱[一律加密 API 參考 JDBC 驅動程式](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。  

下例中，資料庫連接已停用 [永遠加密]。 應用程式發出的查詢具有以 LastName 資料行為目標的參數，而此資料行未加密。 查詢會從加密的 SSN 和 BirthDate 資料行擷取資料。 在這種情況下，不需要呼叫 sys.sp_describe_parameter_encryption 以擷取加密中繼資料。 不過，需要啟用查詢結果的解密，以使應用程式從兩個加密資料行接收純文字值。 請確認用於 SQLServerStatementColumnEncryptionSetting.ResultSet 設定。

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

若要減少資料行主要金鑰存放區來解密資料行加密金鑰的呼叫次數，Microsoft JDBC Driver for SQL Server 會快取在記憶體中的純文字資料行加密金鑰。 從資料庫中繼資料中接收加密的資料行加密金鑰值之後，驅動程式會先嘗試尋找對應加密金鑰值的純文字資料行加密金鑰。 只有在快取中找不到加密的資料行加密金鑰值時，驅動程式才會呼叫包含資料行主要金鑰的金鑰存放區。

您可以使用 SQLServerConnection 類別中的 API，setColumnEncryptionKeyCacheTtl()，快取中設定存留時間值的資料行加密金鑰的項目。 資料行加密金鑰項目在快取中的預設存留時間值是 2 小時。 若要關閉快取使用值為 0。 若要設定存留時間值使用任何下列 API:
    
    SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
   
例如，若要設定存留時間值為 10 分鐘，請使用
    
    SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)

請注意，支援只有天、 小時、 分鐘或秒數做為時間單位。  


## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>複製使用 SQLServerBulkCopy 的加密資料

使用 SQLServerBulkCopy，您可以複製資料，這是已加密並儲存在某個資料表，另一個資料表，而無須解密資料。 若要這麼做︰

- 請確定目標資料表的加密組態與來源資料表的組態完全一致。 特別是，這兩份資料表都必須加密相同的資料行，且這些資料行必須使用相同的加密類型和相同的加密金鑰來加密。 注意︰如果任一目標資料行的加密方式不同於其對應的來源資料行，您將無法在複製作業後，解密目標資料表中的資料。 資料會損毀。
- 設定這兩個資料庫對來源資料表和目標資料表的連線，但不啟用 [永遠加密]。 
- 設定 allowEncryptedValueModifications 選項。 請參閱[JDBC 驅動程式使用大量複製](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)如需詳細資訊。
 
注意： 這可能會導致這些資料庫損毀，因為 Microsoft JDBC Driver for SQL Server 不會檢查資料確實加密，或是正確加密使用相同的加密，請指定 AllowEncryptedValueModifications 時，請使用警告類型、 演算法和金鑰設成目標資料行。

## <a name="see-also"></a>請參閱＜  
 [一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
  
