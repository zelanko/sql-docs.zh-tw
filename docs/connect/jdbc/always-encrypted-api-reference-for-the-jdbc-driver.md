---
title: JDBC Driver 的 Always Encrypted API 參考 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b305c9e42f1eb7dffec8bd00204723a142a6b2e
ms.sourcegitcommit: 50144371c9ee924e5c0b4b9d3d4860f531c27426
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39582164"
---
# <a name="always-encrypted-api-reference-for-the-jdbc-driver"></a>JDBC Driver 的 Always Encrypted API 參考
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  一律加密可讓用戶端將用戶端應用程式內的機密資料進行加密，且永遠不會顯示 SQL Server 的加密金鑰。 安裝在用戶端電腦上且啟用 Always Encrypted 的驅動程式，透過自動將 SQL Server 用戶端應用程式中的敏感性資料加密與解密，進而達到此功能。 驅動程式會先將敏感資料行中的資料進行加密，才會將資料傳遞至 SQL Server，並自動重寫查詢以保留應用程式的語意。 同樣地，驅動程式會以透明的方式，將查詢結果中加密資料庫資料行所儲存的資料解密。 如需詳細資訊，請參閱 < [Always Encrypted （資料庫引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)並[JDBC 驅動程式搭配使用 Always Encrypted](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  只有搭載 SQL Server 2016 且適用於 SQL Server 的 Microsoft JDBC Driver 6.0 或更高版本才支援 Always Encrypted。  
  
 ## <a name="always-encrypted-api-references"></a>Always Encrypted API 參考
 
 針對使用一律加密的用戶端應用程式所用，JDBC 驅動程式 API 有幾項新項目及修改項目。  
  
 **SQLServerConnection 類別**  
  
|[屬性]|Description|  
|----------|-----------------|  
|新的連接字串關鍵字：<br /><br /> columnEncryptionSetting|columnEncryptionSetting=Enabled 會啟用連線的 Always Encrypted 功能，而 columnEncryptionSetting=Disabled 會予以停用。 接受的值為 Enabled/Disabled。 預設值為 Disabled。|  
|新方法：<br /><br /> 公用的靜態 void setColumnEncryptionTrustedMasterKeyPaths (對應 < 字串、 列出\<字串 >> trustedKeyPaths)<br /><br /> 公用的靜態 void updateColumnEncryptionTrustedMasterKeyPaths (第伺服器字串清單\<字串 > trustedKeyPaths)<br /><br /> 公用靜態 void removeColumnEncryptionTrustedMasterKeyPaths (字串 server)|可讓您為資料庫伺服器設定/更新/移除受信任的金鑰路徑清單。 如果驅動程式在處理應用程式查詢時接收到不在清單上的金鑰路徑，則查詢會失敗。 此屬性會針對受到安全性攻擊危害的 SQL Server 提供額外的保護，這類 SQL Server 會傳送假的金鑰路徑，而可能會導致遺漏金鑰存放區認證。|  
|新方法：<br /><br /> public static Map<String, List\<String>> getColumnEncryptionTrustedMasterKeyPaths()|會傳回資料庫伺服器的受信任金鑰路徑清單。|  
|新方法：<br /><br /> public static void registerColumnEncryptionKeyStoreProviders (Map\<String, SQLServerColumnEncryptionKeyStoreProvider> clientKeyStoreProviders)|可讓您註冊自訂金鑰存放區提供者。 它是一個字典，會將金鑰存放區提供者名稱對應至金鑰存放區提供者實作。<br /><br /> 若要使用 JVM 金鑰存放區，您需要使用 JVM 金鑰存放區認證將 SQLServerColumnEncryptionJVMKeyStoreProvider 物件具現化，並向驅動程式註冊它。 此提供者的名稱必須為 'MSSQL_JVM_KEYSTORE'。<br /><br /> 若要使用 Azure Key Vault 存放區，您需要具現化 SQLServerColumnEncryptionAzureKeyStoreProvider 物件，並向驅動程式。 此提供者的名稱必須是 'AZURE_KEY_VAULT'。|
|public final boolean getSendTimeAsDatetime()|傳回 sendTimeAsDatetime 連接屬性的設定。|
|public void setSendTimeAsDatetime (布林 sendTimeAsDateTimeValue)|修改 sendTimeAsDatetime 連接屬性的設定。|

 **SQLServerConnectionPoolProxy 類別**
|[屬性]|Description|  
|----------|-----------------|  
|public final boolean getSendTimeAsDatetime()|傳回 sendTimeAsDatetime 連接屬性的設定。|
|public void setSendTimeAsDatetime (布林 sendTimeAsDateTimeValue)|修改 sendTimeAsDatetime 連接屬性的設定。|
     
  
 **SQLServerDataSource 類別**  
  
|[屬性]|Description|  
|----------|-----------------|  
|public void setColumnEncryptionSetting(String columnEncryptionSetting)|啟用/停用資料來源物件的一律加密功能。<br /><br /> 預設值為 Disabled。|  
|公用字串 getColumnEncryptionSetting()|擷取資料來源物件的一律加密功能設定。|
|public void setKeyStoreAuthentication (字串 keyStoreAuthentication)|設定可識別金鑰存放區的名稱。 支援的值是**JavaKeyStorePassword**識別 Java 金鑰存放區。<br/><br/>預設值是 null。|
|公用字串 getKeyStoreAuthentication()|取得資料來源物件之 keyStoreAuthentication 設定的值。|
|public void setKeyStoreSecret (字串 keyStoreSecret)|設定 Java keystore 的密碼。 金鑰儲存區和金鑰的密碼必須相同。 請注意，必須使用設定該 keyStoreAuthentication **JavaKeyStorePassword**。|
|public void setKeyStoreLocation (字串 keyStoreLocation)|設定包括 Java 金鑰存放區的檔案名稱的位置。 請注意，必須使用設定該 keyStoreAuthentication **JavaKeyStorePassword**。|
|公用字串 getKeyStoreLocation()|擷取 keyStoreLocation Java 金鑰存放區。|
  
 **SQLServerColumnEncryptionJavaKeyStoreProvider 類別**  
  
 Java 金鑰存放區的金鑰存放區提供者實作。 此類別可讓您將儲存在 Java 金鑰存放區中的憑證，當成資料行主要金鑰使用。  
  
 建構函式  
  
|[屬性]|Description|  
|----------|-----------------|  
|公用 SQLServerColumnEncryptionJavaKeyStoreProvider （字串 keyStoreLocation、 char [] keyStoreSecret）|Java 金鑰存放區的金鑰存放區提供者。|  
  
 方法  
  
|[屬性]|Description|  
|----------|-----------------|  
|public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)|將資料行加密金鑰的指定加密值解密。 加密的值必須使用具指定金鑰路徑的憑證，以及指定的演算法，進而加以加密。<br /><br /> **金鑰路徑的格式應為下列其中一項：**<br /><br /> 憑證指紋：<certificate_thumbprint><br /><br /> 別名：<certificate_alias><br /><br /> 覆寫 SQLServerColumnEncryptionKeyStoreProvider。 （字串、 字串、 Byte[]).) decryptColumnEncryptionKey|  
|public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)|使用具指定金鑰路徑的憑證，以及指定的演算法，將資料行加密金鑰加密。<br /><br /> **金鑰路徑的格式應為下列其中一項：**<br /><br /> 憑證指紋：<certificate_thumbprint><br /><br /> 別名：<certificate_alias><br /><br /> 覆寫 SQLServerColumnEncryptionKeyStoreProvider。 （字串、 字串、 Byte[]).) encryptColumnEncryptionKey|  
|public void setName （字串名稱）|設定此金鑰存放區提供者的名稱。|
|public String getName ()|取得此金鑰存放區提供者的名稱。|
  
 **SQLServerColumnEncryptionAzureKeyVaultProvider 類別**  
  
 Azure Key Vault 的金鑰存放區提供者實作。 這個類別可讓您使用 Azure Key Vault 中儲存為資料行主要金鑰的金鑰。  
  
 建構函式  
  
|[屬性]|Description|  
|----------|-----------------|  
|公用 SQLServerColumnEncryptionAzureKeyVaultProvider （字串 clientId、 字串 clientKey）|Azure Key Vault 的金鑰存放區提供者。  您需要提供識別碼和用戶端要求權杖來向 Azure Key Vault 的金鑰。|  
  
 方法  
  
|[屬性]|Description|  
|----------|-----------------|  
| public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey) | Decryptes 加密資料行加密金鑰 (CEK)。 使用主要金鑰路徑所指定的非對稱金鑰的 RSA 加密演算法可完成此解密。<br />覆寫 SQLServerColumnEncryptionKeyStoreProvider。 （字串、 字串、 Byte[]).) decryptColumnEncryptionKey |  
| public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] columnEncryptionKey) | 加密資料行加密金鑰，讓指定的演算法指定的資料行主要金鑰。<br />覆寫 SQLServerColumnEncryptionKeyStoreProvider。 （字串、 字串、 Byte[]).) encryptColumnEncryptionKey |  
|public void setName （字串名稱）|設定此金鑰存放區提供者的名稱。|
|public String getName ()|取得此金鑰存放區提供者的名稱。|  
  
  
 **SQLServerKeyVaultAuthenticationCallback 介面**  
  
 這個介面包含 Azure 金鑰保存庫驗證，也就是由使用者所實作的其中一個方法。  
  
 方法  
  
|[屬性]|Description|  
|----------|-----------------|  
|公用字串 getAccessToken （字串的授權單位、 字串資源、 字串範圍）;|此方法需要覆寫。 方法用來取得存取權杖至 Azure 金鑰保存庫。|  
  
 **SQLServerColumnEncryptionKeyStoreProvider 類別**  
  
 擴充此類別來實作自訂金鑰存放區提供者。  
  
|[屬性]|Description|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|所有金鑰存放區提供者的基底類別。 自訂提供者必須衍生自此類別並覆寫其成員函式，然後使用 SQLServerConnection 予以註冊。 registerColumnEncryptionKeyStoreProviders()。|  
  
 方法  
  
|[屬性]|Description|  
|----------|-----------------|  
|public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)|用來將資料行加密金鑰的指定加密值解密的基底類別方法。 加密的值必須使用具有指定金鑰路徑的資料行主要金鑰和指定的演算法，進而加以加密。|  
|public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)|基底類別方法，使用具指定金鑰路徑的資料行主要金鑰，以及指定的演算法，進而將資料加密金鑰加密。|
|公用抽象 void setName （字串名稱）|設定此金鑰存放區提供者的名稱。|
|公用抽象字串 getName()|取得此金鑰存放區提供者的名稱。|  
  
 在新的或多載方法**SQLServerPreparedStatement**類別  
  
|[屬性]|Description|  
|----------|-----------------|  
|public void setBigDecimal (int parameterIndex，x，int 精確度 BigDecimal int 小數位數)<br /><br /> public void setObject （int parameterIndex，物件 x，int targetSqlType，整數的精確度，int 小數位數）<br /><br /> public void setObject （int parameterIndex，物件 x，SQLType targetSqlType，整數的精確度，整數小數位數）<br /><br /> public void setTime （int parameterIndex，java.sql.Time x int 小數位數）<br /><br /> public void setTimestamp （int parameterIndex，java.sql.Timestamp，int 擴展 x） <br />public void setDateTimeOffset （int parameterIndex，x，int 擴展 microsoft.sql.datetimeoffset 型）|這些方法多載與有效位數或小數位數引數或兩者皆可支援 「 永遠加密 」 的特定資料類型，需要有效位數和小數位數資訊。|  
|public void setMoney (int parameterIndex，BigDecimal x)<br /><br /> public void setSmallMoney (int parameterIndex，BigDecimal x)<br /><br /> public void setUniqueIdentifier （int parameterIndex，字串的 guid）<br /><br /> public void setDateTime (int parameterIndex java.sql.Timestamp x)<br /><br /> public void setSmallDateTime (int parameterIndex java.sql.Timestamp x)|這些方法會加入至資料類型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime 的支援 「 永遠加密。 <br/><br/>請注意，現有的 setTimestamp() 方法用於將參數值傳送到已加密的 datetime2 資料行。 加密的 datetime 和 smalldatetime 資料行的新方法 setDateTime() 和 setSmallDateTime() 分別使用。|  
|公用最終的 void setBigDecimal （int parameterIndex，x，int 精確度 BigDecimal、 int、 小數位數，則為 true 的 forceEncrypt）<br /><br /> 公用的最終 void setMoney (int parameterIndex，x，則為 true 的 forceEncrypt BigDecimal)<br /><br /> 公用的最終 void setSmallMoney (int parameterIndex，x，則為 true 的 forceEncrypt BigDecimal)<br /><br /> 公用最終的 void setBoolean int parameterIndex、 布林值的 x (布林 forceEncrypt）<br /><br /> 公用最終的 void setByte （int parameterIndex，x，則為 true 的 forceEncrypt 位元組）<br /><br /> 公用最終的 void setBytes int parameterIndex、 位元組 x[] (布林 forceEncrypt）<br /><br /> 公用最終的 void setUniqueIdentifier int parameterIndex、 字串 guid (布林 forceEncrypt）<br /><br /> 公用最終的 void setDouble int parameterIndex、 double x (布林 forceEncrypt）<br /><br /> 公用最終的 void setFloat （int parameterIndex，浮點數 x，則為 true 的 forceEncrypt）<br /><br /> 公用最終的 void setInt （int parameterIndex，int 值，布林 forceEncrypt）<br /><br /> 公用最終的 void setLong int parameterIndex、 長時間 x (布林 forceEncrypt）<br /><br /> 公用的最終 setObject （int parameterIndex，物件 x、 int targetSqlType、 整數的精確度、 int、 小數位數，則為 true 的 forceEncrypt）<br /><br /> 公用最終的 void setObject （int parameterIndex，物件 x、 SQLType targetSqlType、 整數的精確度、 整數、 小數位數，則為 true 的 forceEncrypt）<br /><br /> 公用最終的 void setShort int parameterIndex、 簡短的 x (布林 forceEncrypt）<br /><br /> 公用的最終 void setString (int parameterIndex，字串 str 布林 forceEncrypt)<br /><br /> 公用最終的 void setNString int parameterIndex、 字串值 (布林 forceEncrypt）<br /><br /> 公用的最終 void setTime (第 parameterIndex int，java.sql.Time，x、 int、 小數位數，則為 true 的 forceEncrypt)<br /><br /> 公用的最終 void setTimestamp (第 parameterIndex int，java.sql.Timestamp，int、 小數位數 x，則為 true 的 forceEncrypt)<br /><br /> 公用的最終 void setDateTimeOffset (int parameterIndex，x、 int、 小數位數的 microsoft.sql.DateTimeOffset 布林 forceEncrypt)<br /><br /> 公用最終的 void setDateTime （int parameterIndex，x，則為 true 的 forceEncrypt java.sql.Timestamp）<br /><br /> 公用最終的 void setSmallDateTime （int parameterIndex，x，則為 true 的 forceEncrypt java.sql.Timestamp）<br /><br /> 公用的最終 void setDate (第 parameterIndex int，java.sql.Date，java.util.Calendar cal x 布林 forceEncrypt)<br /><br /> 公用的最終 void setTime (第 parameterIndex int，java.sql.Time，java.util.Calendar cal x 布林 forceEncrypt)<br /><br /> 公用的最終 void setTimestamp (第 parameterIndex int，java.sql.Timestamp，java.util.Calendar cal x 布林 forceEncrypt)|將指定的參數設定為指定的 Java 值。<br /><br /> 如果布林 forceEncrypt 設為 true 時，查詢參數將才可設定指定資料行已加密，並啟用 永遠加密連接或陳述式。<br /><br /> 如果布林 forceEncrypt 設為 false 時，驅動程式將不會強制加密參數。|  
  
 在新的或多載方法**SQLServerCallableStatement**類別  
  
|[屬性]|Description|  
|----------|-----------------|  
|public void registerOutParameter(int parameterIndex, int sqlType, int precision, int scale)<br /><br /> public void registerOutParameter(int parameterIndex, SQLType sqlType, int precision, int scale)<br /><br /> public void registerOutParameter(String parameterName, int sqlType, int precision, int scale)<br /><br /> public void registerOutParameter(String parameterName, SQLType sqlType, int precision, int scale)<br />public void setBigDecimal （字串參數名稱、 BigDecimal bd、 int 有效位數、 int 小數位數）<br /><br /> public void setTime 字串參數名稱、 java.sql.Time t (int 小數位數）<br /><br /> public void setTimestamp （字串參數名稱，java.sql.Timestamp t，int 小數位數）<br /><br /> public void setDateTimeOffset 字串參數名稱、 microsoft.sql.DateTimeOffset t (int 小數位數）<br/><br/>公用最終的 void setObject （字串 sCol，物件 x，int targetSqlType，整數的精確度，int 小數位數）|這些方法多載與有效位數或小數位數引數或兩者皆可支援 「 永遠加密 」 的特定資料類型，需要有效位數和小數位數資訊。|  
|public void setDateTime (字串參數名稱，java.sql.Timestamp x)<br /><br /> public void setSmallDateTime (字串參數名稱，java.sql.Timestamp x)<br /><br /> public void setUniqueIdentifier （字串參數名稱、 guid 字串）<br /><br /> public void setMoney （字串參數名稱、 BigDecimal bd）<br /><br /> public void setSmallMoney （字串參數名稱、 BigDecimal bd）<br/><br/>公用的時間戳記 getDateTime （int 索引）<br/><br/>公用的時間戳記 getDateTime (字串 sCol)<br/><br/>公用的時間戳記 getDateTime （int 索引、 行事曆 cal）<br/><br/>公用的時間戳記 getSmallDateTime （int 索引）<br/><br/>公用的時間戳記 getSmallDateTime (字串 sCol)<br/><br/>公用的時間戳記 getSmallDateTime （int 索引、 行事曆 cal）<br/><br/>公用的時間戳記 getSmallDateTime （字串名稱，行事曆 cal）<br/><br/>公用 BigDecimal getMoney （int 索引）<br/><br/>公用 BigDecimal getMoney (字串 sCol)<br/><br/>公用 BigDecimal getSmallMoney （int 索引）<br/><br/>公用 BigDecimal getSmallMoney (字串 sCol)|這些方法會加入至資料類型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime 的支援 「 永遠加密。 <br/><br/>請注意，現有的 setTimestamp() 方法用於將參數值傳送到已加密的 datetime2 資料行。 加密的 datetime 和 smalldatetime 資料行的新方法 setDateTime() 和 setSmallDateTime() 分別使用。|  
|public void setObject （字串參數名稱、 物件 o、 int n、 int m、 布林 forceEncrypt）<br /><br /> public void setObject （字串參數名稱、 物件 obj、 SQLType jdbcType、 int 小數位數、 布林 forceEncrypt）<br /><br /> public void setDate (字串參數名稱、 x、 行事曆 c java.sql.Date 布林 forceEncrypt)<br /><br /> public void setTime （字串參數名稱、 java.sql.Time t、 int 小數位數、 布林 forceEncrypt）<br /><br /> public void setTime (字串參數名稱、 x、 行事曆 c java.sql.Time 布林 forceEncrypt)<br /><br /> public void setDateTime （字串參數名稱，x，則為 true 的 forceEncrypt java.sql.Timestamp）<br /><br /> public void setDateTimeOffset （字串參數名稱、 microsoft.sql.DateTimeOffset t、 int 小數位數、 布林 forceEncrypt）<br /><br /> public void setSmallDateTime （字串參數名稱，x，則為 true 的 forceEncrypt java.sql.Timestamp）<br /><br /> public void setTimestamp （字串參數名稱、 java.sql.Timestamp t、 int 小數位數、 布林 forceEncrypt）<br /><br /> public void setTimestamp （字串參數名稱，x，則為 true 的 forceEncrypt java.sql.Timestamp）<br /><br /> public void setUniqueIdentifier （字串參數名稱、 guid 字串、 布林 forceEncrypt）<br /><br /> public void setBytes 字串參數名稱、 byte [] b (布林 forceEncrypt）<br /><br /> public void setByte 字串參數名稱、 位元組 b (布林 forceEncrypt）<br /><br /> public void setString （字串參數名稱、 s 字串、 布林 forceEncrypt）<br /><br /> 公用最終的 void setNString 字串參數名稱、 字串值 (布林 forceEncrypt）<br /><br /> public void setMoney 字串參數名稱、 BigDecimal bd (布林 forceEncrypt）<br /><br /> public void setSmallMoney 字串參數名稱、 BigDecimal bd (布林 forceEncrypt）<br /><br /> public void setBigDecimal 字串參數名稱、 BigDecimal bd、 int 有效位數、 int 小數位數 (布林 forceEncrypt）<br /><br /> public void setDouble 字串參數名稱、 double d (布林 forceEncrypt）<br /><br /> public void setFloat 字串參數名稱、 float f (布林 forceEncrypt）<br /><br /> public void setInt (字串參數名稱、 int i、 布林 forceEncrypt)<br /><br /> public void setLong 字串參數名稱、 長時間 l (布林 forceEncrypt）<br /><br /> public void setShort 字串參數名稱、 簡短 s (布林 forceEncrypt）<br /><br /> public void setBoolean parameterNames 字串、 布林值 b (布林 forceEncrypt）<br/><br/>public void setTimeStamp (字串 sCol、 x、 行事曆 c java.sql.Timestamp 布林 forceEncrypt)|將指定的參數設定為指定的 Java 值。<br /><br /> 如果布林 forceEncrypt 設為 true 時，查詢參數將才可設定指定資料行已加密，並啟用 永遠加密連接或陳述式。<br /><br /> 如果布林 forceEncrypt 設為 false 時，驅動程式將不會強制加密參數。|
 

 在新的或多載方法**SQLServerResultSet**類別  
  
|[屬性]|Description|  
|----------|-----------------|  
|公用字串 getUniqueIdentifier (int columnIndex)<br/><br/>公用字串 getUniqueIdentifier (字串 columnLabel)<br/><br/>   公用 java.sql.Timestamp getDateTime (int columnIndex) <br/><br/> 公用 java.sql.Timestamp getDateTime (字串 columnName)   <br/><br/> 公用 java.sql.Timestamp getDateTime （int columnIndex、 行事曆 cal）   <br/><br/>公用 java.sql.Timestamp getDateTime （字串 colName、 行事曆 cal）    <br/><br/>公用 java.sql.Timestamp getSmallDateTime (int columnIndex)    <br/><br/> 公用 java.sql.Timestamp getSmallDateTime (字串 columnName)   <br/><br/> 公用 java.sql.Timestamp getSmallDateTime （int columnIndex、 行事曆 cal）   <br/><br/> 公用 java.sql.Timestamp getSmallDateTime （字串 colName、 行事曆 cal）   <br/><br/>  公用 BigDecimal getMoney (int columnIndex)  <br/><br/> 公用 BigDecimal getMoney (字串 columnName)   <br/><br/> 公用 BigDecimal getSmallMoney (int columnIndex)   <br/><br/>  公用 BigDecimal getSmallMoney (字串 columnName)  <br/><br/>public void updateMoney (字串 columnName，BigDecimal x)    <br/><br/>  public void updateSmallMoney (字串 columnName，BigDecimal x)  <br/><br/>     public void updateDateTime (int 索引 java.sql.Timestamp x) <br/><br/> public void updateSmallDateTime (int 索引 java.sql.Timestamp x) |這些方法會新增至支援的資料類型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime 的 Always Encrypted。 <br/><br/>請注意，現有的 updateTimestamp() 方法用來更新加密的 datetime2 資料行。 加密的 datetime 和 smalldatetime 資料行的新方法 updateDateTime() 和 updateSmallDateTime() 分別使用。|
|public void updateBoolean int 索引、 布林值的 x (布林 forceEncrypt）  <br/><br/>  public void updateByte (x，則為 true 的 forceEncrypt 位元組中的 int index）  <br/><br/>  public void updateShort int 索引、 簡短的 x (布林 forceEncrypt）  <br/><br/> public void updateInt （int 索引、 x、 布林 forceEncrypt int）   <br/><br/>  public void updateLong int 索引、 長時間 x (布林 forceEncrypt）  <br/><br/> public void updateFloat （int 索引、 浮點數 x，布林 forceEncrypt）   <br/><br/> public void updateDouble int 索引、 雙精確度 x (布林 forceEncrypt）   <br/><br/> public void updateMoney (int index、 x、 布林 forceEncrypt BigDecimal)   <br/><br/>  public void updateMoney (字串 columnName，x，則為 true 的 forceEncrypt BigDecimal)  <br/><br/> public void updateSmallMoney (int index、 x、 布林 forceEncrypt BigDecimal)   <br/><br/>  public void updateSmallMoney (字串 columnName，x，則為 true 的 forceEncrypt BigDecimal)  <br/><br/> public void updateBigDecimal （x，整數的精確度 BigDecimal int 索引、 整數、 小數位數，則為 true 的 forceEncrypt）   <br/><br/>  public void updateString int columnIndex、 字串 stringValue (布林 forceEncrypt）  <br/><br/>  public void updateNString （int columnIndex、 字串的字串、 布林 forceEncrypt）  <br/><br/>  public void updateNString （字串 columnLabel、 字串的字串、 布林 forceEncrypt）  <br/><br/> public void updateBytes int 索引、 位元組 x[] (布林 forceEncrypt）   <br/><br/>  public void updateDate （int 索引、 x、 布林 forceEncrypt java.sql.Date）  <br/><br/> public void updateTime (int 索引、 x、 整數、 小數位數的 java.sql.Time 布林 forceEncrypt)   <br/><br/> public void updateTimestamp (int 索引，java.sql.Timestamp，int、 小數位數 x，則為 true 的 forceEncrypt)   <br/><br/> public void updateDateTime (int 索引、 x、 整數、 小數位數的 java.sql.Timestamp 布林 forceEncrypt)   <br/><br/> public void updateSmallDateTime (int 索引、 x、 整數、 小數位數的 java.sql.Timestamp 布林 forceEncrypt)   <br/><br/>  public void updateDateTimeOffset (int 索引、 x、 整數、 小數位數的 microsoft.sql.datetimeoffset 型布林 forceEncrypt)  <br/><br/> public void updateUniqueIdentifier (int index、 x、 布林 forceEncrypt 字串)    <br/><br/>  公用的 void updateObject （int 索引中，物件 x、 int 有效位數、 int、 小數位數，則為 true 的 forceEncrypt）  <br/><br/>  公用的 void updateObject （int 索引、 物件 obj、 SQLType targetSqlType、 int 小數位數、 布林 forceEncrypt）  <br/><br/> public void updateBoolean （columnName 字串、 布林值的 x、 布林 forceEncrypt）    <br/><br/>  public void updateByte （字串 columnName，x，則為 true 的 forceEncrypt 位元組）  <br/><br/>  public void updateShort 字串 columnName、 簡短的 x (布林 forceEncrypt）  <br/><br/> public void updateInt （字串 columnName，x，則為 true 的 forceEncrypt int）   <br/><br/>   public void updateLong 字串 columnName、 長時間 x (布林 forceEncrypt） <br/><br/>  public void updateFloat （字串 columnName，浮點數 x，則為 true 的 forceEncrypt）  <br/><br/>  public void updateDouble 字串 columnName、 雙精確度 x (布林 forceEncrypt）  <br/><br/> public void updateBigDecimal (字串 columnName，x，則為 true 的 forceEncrypt BigDecimal)   <br/><br/>  public void updateBigDecimal （字串 columnName，x，整數的精確度 BigDecimal、 整數、 小數位數，則為 true 的 forceEncrypt）  <br/><br/> public void updateString (字串 columnName，x，則為 true 的 forceEncrypt 字串)   <br/><br/>  public void updateBytes 字串 columnName、 位元組 x[] (布林 forceEncrypt）  <br/><br/> public void updateDate （字串 columnName，x，則為 true 的 forceEncrypt java.sql.Date）   <br/><br/>  public void updateTime (columnName 字串、 int、 小數位數 x java.sql.Time 布林 forceEncrypt)  <br/><br/>  public void updateTimestamp (columnName 字串、 int、 小數位數 x java.sql.Timestamp 布林 forceEncrypt)  <br/><br/> public void updateDateTime (columnName 字串、 int、 小數位數 x java.sql.Timestamp 布林 forceEncrypt)   <br/><br/>  public void updateSmallDateTime (columnName 字串、 int、 小數位數 x java.sql.Timestamp 布林 forceEncrypt)  <br/><br/>  public void updateDateTimeOffset (columnName 字串、 int、 小數位數 x microsoft.sql.DateTimeOffset 布林 forceEncrypt)  <br/><br/>  public void updateUniqueIdentifier (字串 columnName，x，則為 true 的 forceEncrypt 字串)<br/><br/>公用的 void updateObject （字串 columnName，物件 x、 int 有效位數、 int、 小數位數，則為 true 的 forceEncrypt）<br/><br/>公用的 void updateObject （columnName 字串、 物件 obj、 SQLType targetSqlType、 int 小數位數、 布林 forceEncrypt）|為給定的 java 值更新指定的資料行。<br/><br/>如果布林 forceEncrypt 設為 true，資料行才會設定如果已加密，並啟用 永遠加密連接或陳述式。<br/><br/>如果布林 forceEncrypt 設為 false 時，驅動程式將不會強制加密參數。|

  
在新的型別**microsoft.sql.Types**類別
|[屬性]|Description|  
|----------|-----------------|  
|DATETIME、 SMALLDATETIME、 MONEY、 SMALLMONEY、 GUID|用戶端傳送的參數值時，使用這些類型做為目標 SQL 型別**加密**datetime、 smalldatetime、 money、 smallmoney、 uniqueidentifier 資料行將使用 setObject()/updateObject() API 方法。|  
  
  
 **SQLServerStatementColumnEncryptionSetting 列舉**  
  
 指定將如何傳送和接收時讀取和寫入加密的資料行的資料。 根據您特定的查詢，略過 Always Encrypted 驅動程式的處理在使用非加密的資料行時可能會降低效能的影響。 請注意，這些設定不會用來略過加密並存取純文字資料。  
  
 **語法**  
  
```java
Public enum  SQLServerStatementColumnEncryptionSetting  
```  
  
 **成員**  
  
|[屬性]|Description|  
|----------|-----------------|  
|UseConnectionSetting|指定命令應該預設為連接字串中的 [永遠加密] 設定。|  
|已啟用|啟用 Always Encrypted 的查詢。|  
|ResultSetOnly|指定驅動程式的 Always Encrypted 常式應該處理命令的結果。 當命令沒有任何參數需要加密時，請使用此值。|  
|已停用|停用 Always Encrypted 的查詢。|  
  
 AE 的陳述式層級設定會新增至 SQLServerConnection 類別以及 SQLServerConnectionPoolProxy 類別。 這些類別中的下列方法會多載，以新的設定。  
  
|[屬性]|Description|  
|----------|-----------------|  
|公用的陳述式 createStatement （n int、 int nConcur、 int statementHoldability、 SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|建立會產生具有給定型的別、 並行處理、 保留性和資料行加密設定的結果集物件的陳述式物件。|  
|公用 CallableStatement prepareCall sql 字串、 int n、 int nConcur、 int statementHoldability (SQLServerStatementColumnEncryptionSetting stmtColEncSetiing）|建立 CallableStatement 物件將會產生具有給定型的別、 並行和保留性的結果集物件的指定資料行加密設定。|  
|公用 PreparedStatement prepareStatement sql 字串、 int autogeneratedKeys (SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|建立 PreparedStatement 物件能夠擷取自動產生金鑰的指定資料行加密設定。|  
|公用 PreparedStatement prepareStatement sql 字串、 字串 [] columnNames (SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|建立 PreparedStatement 物件將會產生結果集物件，指定資料行名稱的指定資料行加密設定。|  
|公用 PreparedStatement prepareStatement （sql 字串、 int [] columnIndexes、 SQLServerStatementColumnEncryptionSetting stmtColEncSetting|建立 PreparedStatement 物件將會產生具有指定資料行索引的結果集物件的指定資料行加密設定。|  
|公用 PreparedStatement prepareStatement （sql 字串、 int n、 int nConcur、 int nHold、 SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|建立 PreparedStatement 物件將會產生具有給定型的別、 並行和保留性的結果集物件的指定資料行加密設定。|  
  
> [!NOTE]  
>  如果 Always Encrypted 的查詢已停用，而且查詢具有需要加密 （參數對應至加密資料行） 的參數，則查詢會失敗。  
>   
>  如果 Always Encrypted 的查詢已停用，而且查詢會從加密資料行中傳回結果，查詢會傳回加密的值。 加密的值必須為 varbinary 資料型別。  
  
 ## <a name="see-also"></a>另請參閱  
 [搭配使用一律加密與 JDBC 驅動程式](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  

