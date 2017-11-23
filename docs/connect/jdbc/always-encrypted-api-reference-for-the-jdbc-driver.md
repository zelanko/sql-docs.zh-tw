---
title: "永遠加密的 JDBC 驅動程式 API 參考 |Microsoft 文件"
ms.custom: 
ms.date: 11/10/2016
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7c0d47b3ef5dc4bb01cbc667299902aa283eb039
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="always-encrypted-api-reference-for-the-jdbc-driver"></a>永遠加密的 JDBC 驅動程式 API 參考
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  一律加密可讓用戶端將用戶端應用程式內的機密資料進行加密，且永遠不會顯示 SQL Server 的加密金鑰。 安裝在用戶端電腦上且啟用一律加密的驅動程式，透過自動將 SQL Server 用戶端應用程式中的機密資料進行加密與解密，進而達成此目的。 驅動程式會先將敏感資料行中的資料進行加密，才會將資料傳遞至 SQL Server，並自動重寫查詢以保留應用程式的語意。 同樣地，驅動程式會以透明的方式，將查詢結果中加密資料庫資料行所儲存的資料進行解密。 如需詳細資訊，請參閱[一律加密 (Database Engine)](../../relational-databases/security/encryption/always-encrypted-database-engine.md)和[使用一律加密與 JDBC 驅動程式](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  永遠加密已才支援的 Microsoft JDBC Driver 6.0 或更新版本的 SQL Server 2016 的 SQL Server。  
  
 針對使用一律加密的用戶端應用程式所用，JDBC 驅動程式 API 有幾項新項目及修改項目。  
  
 **SQLServerConnection 類別**  
  
|名稱|說明|  
|----------|-----------------|  
|新的連接字串關鍵字：<br /><br /> columnEncryptionSetting|columnEncryptionSetting = Enabled 啟用一律加密功能，針對連接和 columnEncryptionSetting = Disabled 會加以停用。 接受的值為 Enabled/Disabled。 預設值為 Disabled。|  
|新方法：<br /><br /> 公用靜態 void setColumnEncryptionTrustedMasterKeyPaths (地圖 < 字串、 列出\<字串 >> trustedKeyPaths)<br /><br /> 公用靜態 void updateColumnEncryptionTrustedMasterKeyPaths (字串伺服器，清單\<字串 > trustedKeyPaths)<br /><br /> 公用靜態 void removeColumnEncryptionTrustedMasterKeyPaths (字串 server)|可讓您的資料庫伺服器設定/更新/移除受信任的金鑰路徑的清單。 如果驅動程式在處理應用程式查詢時，接收到不在清單上的金鑰路徑，則查詢會失敗。 此屬性會針對受到安全性攻擊危害的 SQL Server 提供額外的保護，此類 SQL Server 會提供假的金鑰路徑，而可能會導致遺漏金鑰存放區認證。|  
|新方法：<br /><br /> 公用的靜態對應 < 字串、 列出\<字串 >> getColumnEncryptionTrustedMasterKeyPaths()|會傳回資料庫伺服器的受信任金鑰路徑清單。|  
|新方法：<br /><br /> 公用靜態 void registerColumnEncryptionKeyStoreProviders (地圖\<字串、 SQLServerColumnEncryptionKeyStoreProvider > clientKeyStoreProviders)|可讓您註冊自訂金鑰存放區提供者。 它是一個字典，會將金鑰存放區提供者名稱對應至金鑰存放區提供者實作。<br /><br /> 若要使用 JVM 金鑰存放區，您需要使用 JVM 金鑰存放區認證將 SQLServerColumnEncryptionJVMKeyStoreProvider 物件具現化，並將其向驅動程式註冊。 此提供者的名稱必須是 'MSSQL_JVM_KEYSTORE'。<br /><br /> 若要使用 Azure 金鑰保存庫存放區需要具現化 SQLServerColumnEncryptionAzureKeyStoreProvider 物件，並向驅動程式。 此提供者的名稱必須是 'AZURE_KEY_VAULT'。|
|公用的最後一個布林 getSendTimeAsDatetime()|傳回 sendTimeAsDatetime 連接屬性的設定。|
|public void setSendTimeAsDatetime (sendTimeAsDateTimeValue 布林值)|修改 sendTimeAsDatetime 連接屬性的設定。|

 **SQLServerConnectionPoolProxy 類別**
|名稱|Description|  
|----------|-----------------|  
|公用的最後一個布林 getSendTimeAsDatetime()|傳回 sendTimeAsDatetime 連接屬性的設定。|
|public void setSendTimeAsDatetime (sendTimeAsDateTimeValue 布林值)|修改 sendTimeAsDatetime 連接屬性的設定。|
     
  
 **SQLServerDataSource 類別**  
  
|名稱|Description|  
|----------|-----------------|  
|public void setColumnEncryptionSetting (字串 columnEncryptionSetting)|啟用/停用資料來源物件的一律加密功能。<br /><br /> 預設值為 Disabled。|  
|公開金鑰字串 getColumnEncryptionSetting()|擷取資料來源物件的一律加密功能設定。|
|public void setKeyStoreAuthentication (字串 keyStoreAuthentication)|設定識別的金鑰存放區的名稱。 支援的值是"JavaKeyStorePassword 」 的 identifiying Java 金鑰存放區。<br/><br/>預設值是 null。|
|公開金鑰字串 getKeyStoreAuthentication()|取得資料來源物件之 keyStoreAuthentication 設定的值。|
|public void setKeyStoreSecret (字串 keyStoreSecret)|設定 Java keystore 的密碼。 請注意，對於 Java 金鑰存放區提供者金鑰存放區和金鑰的密碼必須相同。 請注意，keyStoreAuthentication 必須使用 「 JavaKeyStorePassword 」 來設定。|
|public void setKeyStoreLocation (字串 keyStoreLocation)|設定包括 Java 金鑰存放區的檔案名稱的位置。 請注意，keyStoreAuthentication 必須使用 「 JavaKeyStorePassword 」 來設定。|
|公開金鑰字串 getKeyStoreLocation()|擷取 Java 金鑰存放區 keyStoreLocation。|
  
 **SQLServerColumnEncryptionJavaKeyStoreProvider 類別**  
  
 Java 金鑰存放區的金鑰存放區提供者實作。 這個類別可讓您使用以資料行主要金鑰儲存在 Java 金鑰存放區中的憑證。  
  
 建構函式  
  
|名稱|Description|  
|----------|-----------------|  
|公用 SQLServerColumnEncryptionJavaKeyStoreProvider （字串 keyStoreLocation、 char [] keyStoreSecret）|Java 金鑰存放區的金鑰存放區提供者。|  
  
 方法  
  
|名稱|Description|  
|----------|-----------------|  
|公用位元組 [] decryptColumnEncryptionKey 字串 masterKeyPath、 字串 encryptionAlgorithm (位元組 [] encryptedColumnEncryptionKey）|將資料行加密金鑰的指定加密值解密。 加密的值必須使用具指定金鑰路徑的憑證，以及指定的演算法，進而加以加密。<br /><br /> **金鑰路徑的格式應為下列其中一項：**<br /><br /> 憑證指紋：<certificate_thumbprint><br /><br /> 別名：<certificate_alias><br /><br /> （覆寫 SQLServerColumnEncryptionKeyStoreProvider。 （字串、 字串、 Byte[]).) decryptColumnEncryptionKey|  
|公用位元組 [] encryptColumnEncryptionKey 字串 masterKeyPath、 字串 encryptionAlgorithm (位元組 [] plainTextColumnEncryptionKey）|使用具指定金鑰路徑的憑證，以及指定的演算法，將資料行加密金鑰加密。<br /><br /> **金鑰路徑的格式應為下列其中一項：**<br /><br /> 憑證指紋：<certificate_thumbprint><br /><br /> 別名：<certificate_alias><br /><br /> （覆寫 SQLServerColumnEncryptionKeyStoreProvider。 （字串、 字串、 Byte[]).) encryptColumnEncryptionKey|  
|public void setName （名稱）|設定此金鑰存放區提供者的名稱。|
|公開金鑰字串 getName （)|取得此金鑰存放區提供者的名稱。|
  
 **SQLServerColumnEncryptionAzureKeyVaultProvider 類別**  
  
 Azure 金鑰保存庫的金鑰存放區提供者實作。 這個類別可讓您使用以資料行主要金鑰儲存在 Azure 金鑰保存庫中的索引鍵。  
  
 建構函式  
  
|名稱|Description|  
|----------|-----------------|  
|公用 SQLServerColumnEncryptionAzureKeyVaultProvider （SQLServerKeyVaultAuthenticationCallback authenticationCallback、 ExecutorService executorService）|Azure 金鑰保存庫的金鑰存放區提供者。  您必須提供要擷取存取權杖的 Azure 金鑰保存庫中的索引鍵的 SQLServerKeyVaultAuthenticationCallback 介面的實作。|  
  
 方法  
  
|名稱|Description|  
|----------|-----------------|  
|公用位元組 [] decryptColumnEncryptionKey 字串 masterKeyPath、 字串 encryptionAlgorithm (位元組 [] encryptedColumnEncryptionKey）|將資料行加密金鑰的指定加密值解密。 加密的值必須是使用指定的資料行索引鍵 IDmaster 金鑰並使用指定的演算法。 <br />（覆寫 SQLServerColumnEncryptionKeyStoreProvider。 （字串、 字串、 Byte[]).) decryptColumnEncryptionKey|  
|公用位元組 [] encryptColumnEncryptionKey 字串 masterKeyPath、 字串 encryptionAlgorithm (位元組 [] columnEncryptionKey）|加密資料行加密金鑰使用指定的資料行主要金鑰，並使用指定的演算法。 <br />（覆寫 SQLServerColumnEncryptionKeyStoreProvider。 （字串、 字串、 Byte[]).) encryptColumnEncryptionKey|  
|public void setName （名稱）|設定此金鑰存放區提供者的名稱。|
|公開金鑰字串 getName （)|取得此金鑰存放區提供者的名稱。|  
  
  
 **SQLServerKeyVaultAuthenticationCallback 介面**  
  
 這個介面包含 Azure 金鑰保存庫驗證，也就是由使用者所實作的一種方法。  
  
 方法  
  
|名稱|Description|  
|----------|-----------------|  
|公開金鑰字串 getAccessToken （字串授權單位、 字串資源、 字串範圍）。|需要覆寫方法。 方法用來取得存取權杖至 Azure 金鑰保存庫。|  
  
 **SQLServerColumnEncryptionKeyStoreProvider 類別**  
  
 擴充此類別來實作自訂金鑰存放區提供者。  
  
|名稱|Description|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|所有金鑰存放區提供者的基底類別。 自訂提供者必須衍生自這個類別並覆寫其成員函式，然後再使用 SQLServerConnection 註冊。 registerColumnEncryptionKeyStoreProviders()。|  
  
 方法  
  
|名稱|Description|  
|----------|-----------------|  
|public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)|用來將資料行加密金鑰的指定加密值解密的基底類別方法。 加密的值必須使用具指定金鑰路徑的資料行主要金鑰，以及指定的演算法，進而加以加密。|  
|public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)|基底類別方法，使用具指定金鑰路徑的資料行主要金鑰，以及指定的演算法，進而將資料加密金鑰加密。|
|公用抽象 void setName （名稱）|設定此金鑰存放區提供者的名稱。|
|公用抽象字串 getName()|取得此金鑰存放區提供者的名稱。|  
  
 在新的或多載方法**SQLServerPreparedStatement**類別  
  
|名稱|Description|  
|----------|-----------------|  
|public void setBigDecimal (int parameterIndex，x，int 精確度 BigDecimal int 小數位數)<br /><br /> public void setObject （int parameterIndex，物件 x、 int targetSqlType、 整數有效位數，int 小數位數）<br /><br /> public void setObject （int parameterIndex，物件 x、 SQLType targetSqlType、 整數有效位數，整數小數位數）<br /><br /> public void setTime （int parameterIndex，java.sql.Time x int 小數位數）<br /><br /> public void setTimestamp （int parameterIndex，java.sql.Timestamp，int 標尺 x） <br />public void setDateTimeOffset （int parameterIndex、 microsoft.sql.DateTimeOffset x int 小數位數）|這些方法多載與有效位數或小數位數引數或同時支援 「 永遠加密的特定資料類型需要精確度及小數位數資訊。|  
|public void setMoney (int parameterIndex，BigDecimal x)<br /><br /> public void setSmallMoney (int parameterIndex，BigDecimal x)<br /><br /> public void setUniqueIdentifier （int parameterIndex、 字串 guid）<br /><br /> public void setDateTime (int parameterIndex java.sql.Timestamp x)<br /><br /> public void setSmallDateTime (int parameterIndex java.sql.Timestamp x)|這些方法會加入至支援 「 永遠加密的資料類型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime。 <br/><br/>請注意，現有的 setTimestamp() 方法使用參數值傳送到加密的 datetime2 資料行。 加密的 datetime 和 smalldatetime 資料行的新方法 setDateTime() 和 setSmallDateTime() 分別使用。|  
|公用最終的 void setBigDecimal （int parameterIndex，BigDecimal x int 有效位數、 int、 小數位數，則為 true 的 forceEncrypt）<br /><br /> 公用最終 void setMoney (int parameterIndex，x，布林 forceEncrypt BigDecimal)<br /><br /> 公用最終 void setSmallMoney (int parameterIndex，x，布林 forceEncrypt BigDecimal)<br /><br /> 公用最終的 void setBoolean （int parameterIndex、 布林 x、 布林 forceEncrypt）<br /><br /> 公用最終的 void setByte （int parameterIndex、 x、 布林 forceEncrypt 位元組）<br /><br /> 公用最終的 void setBytes （int parameterIndex、 位元組 x[]、 布林 forceEncrypt）<br /><br /> 公用最終的 void setUniqueIdentifier （int parameterIndex、 guid 字串、 布林 forceEncrypt）<br /><br /> 公用最終的 void setDouble （int parameterIndex、 double x，布林 forceEncrypt）<br /><br /> 公用最終的 void setFloat （int parameterIndex、 浮點數 x，布林 forceEncrypt）<br /><br /> 公用最終的 void setInt int parameterIndex、 int 值 (boolean forceEncrypt）<br /><br /> 公用最終的 void setLong （int parameterIndex、 長時間 x、 布林 forceEncrypt）<br /><br /> 公用的最終 setObject （int parameterIndex，物件 x int targetSqlType、 整數、 整數位數 int 小數位數，則為 true 的 forceEncrypt）<br /><br /> 公用最終的 void setObject （int parameterIndex，物件 x SQLType targetSqlType、 整數、 整數位數整數小數位數，則為 true 的 forceEncrypt）<br /><br /> 公用最終的 void setShort （int parameterIndex、 簡短的 x、 布林 forceEncrypt）<br /><br /> 公用最終 void setString (int parameterIndex，字串 str 布林 forceEncrypt)<br /><br /> 公用最終的 void setNString int parameterIndex、 字串值 (boolean forceEncrypt）<br /><br /> 公用的最終 void setTime (int parameterIndex，x、 int、 小數位數 java.sql.Time 布林 forceEncrypt)<br /><br /> 公用的最終 void setTimestamp (int parameterIndex，java.sql.Timestamp，int 小數位數 x 布林 forceEncrypt)<br /><br /> 公用的最終 void setDateTimeOffset (int parameterIndex，x、 int、 小數位數 microsoft.sql.DateTimeOffset 布林 forceEncrypt)<br /><br /> 公用最終的 void setDateTime （int parameterIndex，java.sql.Timestamp 布林 forceEncrypt x）<br /><br /> 公用最終的 void setSmallDateTime （int parameterIndex，java.sql.Timestamp 布林 forceEncrypt x）<br /><br /> 公用的最終 void setDate (int parameterIndex，java.sql.Date，java.util.Calendar cal x 布林 forceEncrypt)<br /><br /> 公用的最終 void setTime (int parameterIndex，java.sql.Time，java.util.Calendar cal x 布林 forceEncrypt)<br /><br /> 公用的最終 void setTimestamp (int parameterIndex，java.sql.Timestamp，java.util.Calendar cal x 布林 forceEncrypt)|指定的參數設定為給定的 java 值。<br /><br /> 如果布林 forceEncrypt 設為 true，查詢參數才會設定如果指定的資料行已加密，並啟用 永遠加密的連接時或在陳述式。<br /><br /> 如果布林 forceEncrypt 設為 false，驅動程式將不會強制加密參數。|  
  
 在新的或多載方法**SQLServerCallableStatement**類別  
  
|名稱|Description|  
|----------|-----------------|  
|public void registerOutParameter （int parameterIndex int sqlType、 int、 整數位數 int 小數位數）<br /><br /> public void registerOutParameter （int parameterIndex SQLType sqlType、 int、 整數位數 int 小數位數）<br /><br /> public void registerOutParameter （字串參數名稱 int sqlType、 int、 整數位數 int 小數位數）<br /><br /> public void registerOutParameter （字串參數名稱 SQLType sqlType、 int、 整數位數 int 小數位數）<br />public void setBigDecimal （字串參數名稱 BigDecimal bd、 int、 整數位數 int 小數位數）<br /><br /> public void setTime 字串參數名稱、 java.sql.Time t (int 小數位數）<br /><br /> public void setTimestamp （字串參數名稱、 java.sql.Timestamp t，int 小數位數）<br /><br /> public void setDateTimeOffset 字串參數名稱、 microsoft.sql.DateTimeOffset t (int 小數位數）<br/><br/>公用最終的 void setObject （字串 sCol，物件 x、 int targetSqlType、 整數有效位數，int 小數位數）|這些方法多載與有效位數或小數位數引數或同時支援 「 永遠加密的特定資料類型需要精確度及小數位數資訊。|  
|public void setDateTime (字串參數名稱，java.sql.Timestamp x)<br /><br /> public void setSmallDateTime (字串參數名稱，java.sql.Timestamp x)<br /><br /> public void setUniqueIdentifier （字串參數名稱、 guid 字串）<br /><br /> public void setMoney （字串參數名稱、 BigDecimal bd）<br /><br /> public void setSmallMoney （字串參數名稱、 BigDecimal bd）<br/><br/>公用的時間戳記 getDateTime （int 索引）<br/><br/>公用的時間戳記 getDateTime (字串 sCol)<br/><br/>公用的時間戳記 getDateTime （int 索引、 行事曆 cal）<br/><br/>公用的時間戳記 getSmallDateTime （int 索引）<br/><br/>公用的時間戳記 getSmallDateTime (字串 sCol)<br/><br/>公用的時間戳記 getSmallDateTime （int 索引、 行事曆 cal）<br/><br/>公用的時間戳記 getSmallDateTime （名稱、 行事曆 cal）<br/><br/>公用 BigDecimal getMoney （int 索引）<br/><br/>公用 BigDecimal getMoney (字串 sCol)<br/><br/>公用 BigDecimal getSmallMoney （int 索引）<br/><br/>公用 BigDecimal getSmallMoney (字串 sCol)|這些方法會加入至支援 「 永遠加密的資料類型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime。 <br/><br/>請注意，現有的 setTimestamp() 方法使用參數值傳送到加密的 datetime2 資料行。 加密的 datetime 和 smalldatetime 資料行的新方法 setDateTime() 和 setSmallDateTime() 分別使用。|  
|public void setObject （字串參數名稱、 Object o、 int n、 int m、 布林 forceEncrypt）<br /><br /> public void setObject （字串參數名稱、 物件 obj、 SQLType jdbcType、 int 規模、 布林 forceEncrypt）<br /><br /> public void setDate (字串參數名稱、 x、 行事曆 c java.sql.Date 布林 forceEncrypt)<br /><br /> public void setTime （字串參數名稱、 java.sql.Time t、 int 規模、 布林 forceEncrypt）<br /><br /> public void setTime (字串參數名稱、 x、 行事曆 c java.sql.Time 布林 forceEncrypt)<br /><br /> public void setDateTime （字串參數名稱、 x、 布林 forceEncrypt java.sql.Timestamp）<br /><br /> public void setDateTimeOffset （字串參數名稱、 microsoft.sql.DateTimeOffset t、 int 規模、 布林 forceEncrypt）<br /><br /> public void setSmallDateTime （字串參數名稱、 x、 布林 forceEncrypt java.sql.Timestamp）<br /><br /> public void setTimestamp （字串參數名稱、 java.sql.Timestamp t，int 規模、 布林 forceEncrypt）<br /><br /> public void setTimestamp （字串參數名稱、 x、 布林 forceEncrypt java.sql.Timestamp）<br /><br /> public void setUniqueIdentifier （字串參數名稱、 guid 字串、 布林 forceEncrypt）<br /><br /> public void setBytes （字串參數名稱、 位元組 [] b、 布林 forceEncrypt）<br /><br /> public void setByte 字串參數名稱、 位元組 b (forceEncrypt 布林值）<br /><br /> public void setString （字串參數名稱、 s 字串、 布林 forceEncrypt）<br /><br /> 公用最終的 void setNString 字串參數名稱、 字串值 (boolean forceEncrypt）<br /><br /> public void setMoney （字串參數名稱、 BigDecimal bd，布林 forceEncrypt）<br /><br /> public void setSmallMoney （字串參數名稱、 BigDecimal bd，布林 forceEncrypt）<br /><br /> public void setBigDecimal （字串參數名稱、 BigDecimal bd、 int 有效位數、 int 規模、 布林 forceEncrypt）<br /><br /> public void setDouble （字串參數名稱、 double d、 布林 forceEncrypt）<br /><br /> public void setFloat （字串參數名稱、 float f、 布林 forceEncrypt）<br /><br /> public void setInt (字串參數名稱、 int i、 布林 forceEncrypt)<br /><br /> public void setLong （字串參數名稱、 長時間 l、 布林 forceEncrypt）<br /><br /> public void setShort （字串參數名稱、 short s、 布林 forceEncrypt）<br /><br /> public void setBoolean parameterNames 字串、 布林值 b (布林 forceEncrypt）<br/><br/>public void setTimeStamp (字串 sCol、 x、 行事曆 c java.sql.Timestamp 布林 forceEncrypt)|指定的參數設定為給定的 java 值。<br /><br /> 如果布林 forceEncrypt 設為 true，查詢參數才會設定如果指定的資料行已加密，並啟用 永遠加密的連接時或在陳述式。<br /><br /> 如果布林 forceEncrypt 設為 false，驅動程式將不會強制加密參數。|
 

 在新的或多載方法**SQLServerResultSet**類別  
  
|名稱|Description|  
|----------|-----------------|  
|公開金鑰字串 getUniqueIdentifier (int columnIndex)<br/><br/>公開金鑰字串 getUniqueIdentifier (字串 columnLabel)<br/><br/>   公用 java.sql.Timestamp getDateTime (int columnIndex) <br/><br/> 公用 java.sql.Timestamp getDateTime (字串 columnName)   <br/><br/> 公用 java.sql.Timestamp getDateTime （int columnIndex、 行事曆 cal）   <br/><br/>公用 java.sql.Timestamp getDateTime （字串 colName、 行事曆 cal）    <br/><br/>公用 java.sql.Timestamp getSmallDateTime (int columnIndex)    <br/><br/> 公用 java.sql.Timestamp getSmallDateTime (字串 columnName)   <br/><br/> 公用 java.sql.Timestamp getSmallDateTime （int columnIndex、 行事曆 cal）   <br/><br/> 公用 java.sql.Timestamp getSmallDateTime （字串 colName、 行事曆 cal）   <br/><br/>  公用 BigDecimal getMoney (int columnIndex)  <br/><br/> 公用 BigDecimal getMoney (字串 columnName)   <br/><br/> 公用 BigDecimal getSmallMoney (int columnIndex)   <br/><br/>  公用 BigDecimal getSmallMoney (字串 columnName)  <br/><br/>public void updateMoney (字串 columnName，BigDecimal x)    <br/><br/>  public void updateSmallMoney (字串 columnName，BigDecimal x)  <br/><br/>     public void updateDateTime (int 索引 java.sql.Timestamp x) <br/><br/> public void updateSmallDateTime (int 索引 java.sql.Timestamp x) |這些方法會加入至支援 「 永遠加密的資料類型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime。 <br/><br/>請注意現有 updateTimestamp() 方法用來更新加密的 datetime2 資料行。 加密的 datetime 和 smalldatetime 資料行的新方法 updateDateTime() 和 updateSmallDateTime() 分別使用。|
|public void updateBoolean （int 索引、 布林 x、 布林 forceEncrypt）  <br/><br/>  public void updateByte （int 索引、 x、 布林 forceEncrypt 位元組）  <br/><br/>  public void updateShort （int 索引、 簡短的 x、 布林 forceEncrypt）  <br/><br/> public void updateInt （int 索引、 x、 布林 forceEncrypt int）   <br/><br/>  public void updateLong （int 索引、 長時間 x、 布林 forceEncrypt）  <br/><br/> public void updateFloat （int 索引、 浮點數 x，布林 forceEncrypt）   <br/><br/> public void updateDouble （int 索引、 double x，布林 forceEncrypt）   <br/><br/> public void updateMoney （int 索引、 x、 布林 forceEncrypt BigDecimal）   <br/><br/>  public void updateMoney (字串 columnName，x，布林 forceEncrypt BigDecimal)  <br/><br/> public void updateSmallMoney （int 索引、 x、 布林 forceEncrypt BigDecimal）   <br/><br/>  public void updateSmallMoney (字串 columnName，x，布林 forceEncrypt BigDecimal)  <br/><br/> public void updateBigDecimal （int 索引，BigDecimal x 整數的有效位數、 整數、 小數位數，則為 true 的 forceEncrypt）   <br/><br/>  public void updateString （int columnIndex、 stringValue 字串、 布林 forceEncrypt）  <br/><br/>  public void updateNString （int columnIndex、 nString 字串、 布林 forceEncrypt）  <br/><br/>  public void updateNString （字串 columnLabel、 nString 字串、 布林 forceEncrypt）  <br/><br/> public void updateBytes （int 索引、 位元組 x[]、 布林 forceEncrypt）   <br/><br/>  public void updateDate （int 索引、 x、 布林 forceEncrypt java.sql.Date）  <br/><br/> public void updateTime (int 索引，x，整數小數位數，java.sql.Time 布林 forceEncrypt)   <br/><br/> public void updateTimestamp (int 索引，java.sql.Timestamp，int 小數位數 x 布林 forceEncrypt)   <br/><br/> public void updateDateTime (int 索引，x，整數小數位數，java.sql.Timestamp 布林 forceEncrypt)   <br/><br/> public void updateSmallDateTime (int 索引，x，整數小數位數，java.sql.Timestamp 布林 forceEncrypt)   <br/><br/>  public void updateDateTimeOffset (int 索引，x、 整數、 小數位數 microsoft.sql.DateTimeOffset 布林 forceEncrypt)  <br/><br/> public void updateUniqueIdentifier （int 索引、 x、 布林 forceEncrypt 字串）    <br/><br/>  公用 void updateObject （int 索引物件 x、 int 有效位數、 int、 小數位數，則為 true 的 forceEncrypt）  <br/><br/>  public void updateObject （int 索引、 物件 obj、 SQLType targetSqlType、 int 規模、 布林 forceEncrypt）  <br/><br/> public void updateBoolean （columnName 字串、 布林 x、 布林 forceEncrypt）    <br/><br/>  public void updateByte （columnName 字串、 布林 forceEncrypt x 位元組）  <br/><br/>  public void updateShort （字串 columnName、 簡短的 x、 布林 forceEncrypt）  <br/><br/> public void updateInt （columnName 字串、 布林 forceEncrypt x int）   <br/><br/>   public void updateLong 字串 columnName、 長時間 x (forceEncrypt 布林值） <br/><br/>  public void updateFloat （字串 columnName、 浮點數 x，布林 forceEncrypt）  <br/><br/>  public void updateDouble 字串 columnName、 double x (forceEncrypt 布林值）  <br/><br/> public void updateBigDecimal (字串 columnName，x，布林 forceEncrypt BigDecimal)   <br/><br/>  public void updateBigDecimal （字串 columnName，BigDecimal x 整數的有效位數、 整數、 小數位數，則為 true 的 forceEncrypt）  <br/><br/> public void updateString (字串 columnName，x，布林 forceEncrypt 字串)   <br/><br/>  public void updateBytes （columnName 字串、 位元組 x[]、 布林 forceEncrypt）  <br/><br/> public void updateDate （columnName 字串、 布林 forceEncrypt x java.sql.Date）   <br/><br/>  public void updateTime (字串 columnName、 x、 int、 小數位數 java.sql.Time 布林 forceEncrypt)  <br/><br/>  public void updateTimestamp (字串 columnName、 x、 int、 小數位數 java.sql.Timestamp 布林 forceEncrypt)  <br/><br/> public void updateDateTime (字串 columnName、 x、 int、 小數位數 java.sql.Timestamp 布林 forceEncrypt)   <br/><br/>  public void updateSmallDateTime (字串 columnName、 x、 int、 小數位數 java.sql.Timestamp 布林 forceEncrypt)  <br/><br/>  public void updateDateTimeOffset (字串 columnName、 x、 int、 小數位數 microsoft.sql.DateTimeOffset 布林 forceEncrypt)  <br/><br/>  public void updateUniqueIdentifier (字串 columnName，x，布林 forceEncrypt 字串)<br/><br/>public void updateObject （字串 columnName，物件 x、 int 有效位數，int 小數位數，則為 true 的 forceEncrypt）<br/><br/>public void updateObject （columnName 字串、 物件 obj、 SQLType targetSqlType、 int 規模、 布林 forceEncrypt）|更新指定的資料行，為給定的 java 值。<br/><br/>如果布林 forceEncrypt 設為 true，資料行才會設定如果它已經加密，並啟用 永遠加密的連接時或在陳述式。<br/><br/>如果布林 forceEncrypt 設為 false，驅動程式將不會強制加密參數。|

  
中的新類型**microsoft.sql.Types**類別
|名稱|Description|  
|----------|-----------------|  
|DATETIME、 SMALLDATETIME、 MONEY、 SMALLMONEY、 GUID|用戶端傳送的參數值時，使用這些類型做為目標的 SQL 型別**加密**datetime、 smalldatetime、 money、 smallmoney、 uniqueidentifier 資料行使用 setObject()/updateObject() API 方法。|  
  
  
 **SQLServerStatementColumnEncryptionSetting 列舉**  
  
 指定將如何傳送和接收時讀取和寫入加密的資料行的資料。 根據您的特定查詢，可能會降低效能的影響略過使用非加密的資料行時，永遠加密驅動程式的處理。 請注意，這些設定不能用來略過加密並存取純文字資料。  
  
 **語法**  
  
```  
Public enum  SQLServerStatementColumnEncryptionSetting  
```  
  
 **成員**  
  
|名稱|Description|  
|----------|-----------------|  
|UseConnectionSetting|指定命令應該預設為 Always Encrypted 設定連接字串中。|  
|已啟用|啟用永遠加密的查詢。|  
|ResultSetOnly|指定驅動程式的一律加密常式應該處理命令的結果。 此命令沒有任何參數需要加密時，請使用此值。|  
|已停用|停用永遠加密的查詢。|  
  
 AE 的陳述式層級設定會新增到 SQLServerConnection 類別以及 SQLServerConnectionPoolProxy 類別。 這些類別中的下列方法會多載，以新的設定。  
  
|名稱|Description|  
|----------|-----------------|  
|陳述式的公用 createStatement n int，int nConcur、 int statementHoldability (SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|建立會產生具有指定的型別、 並行、 保留性和資料行加密設定的結果集物件的陳述式物件。|  
|公用 CallableStatement prepareCall 字串 sql、 n int，int nConcur、 int statementHoldability (SQLServerStatementColumnEncryptionSetting stmtColEncSetiing）|建立 CallableStatement 物件將會產生具有給定型的別、 並行和保留性的結果集物件的指定資料行加密設定。|  
|public PreparedStatement prepareStatement 字串 sql、 int autogeneratedKeys (SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|建立 PreparedStatement 物件匯入功能來擷取自動產生的索引鍵的特定資料行加密設定。|  
|public PreparedStatement prepareStatement sql 字串、 字串 [] columnNames (SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|建立 PreparedStatement 物件將會產生結果集物件，具有給定的資料行名稱的指定資料行加密設定。|  
|public PreparedStatement prepareStatement （sql 字串、 int [] columnIndexes、 SQLServerStatementColumnEncryptionSetting stmtColEncSetting|建立 PreparedStatement 物件將會產生結果集物件，具有給定的資料行索引的給定資料行加密設定。|  
|public PreparedStatement prepareStatement 字串 sql、 n int，int nConcur、 int nHold (SQLServerStatementColumnEncryptionSetting stmtColEncSetting）|建立 PreparedStatement 物件將會產生具有給定型的別、 並行和保留性的結果集物件的指定資料行加密設定。|  
  
> [!NOTE]  
>  如果查詢永遠加密已停用，而且查詢有參數需要加密 （參數對應到加密的資料行），則查詢會失敗。  
>   
>  如果查詢永遠加密已停用，而且查詢會傳回結果中加密的資料行，則查詢會傳回加密的值。 加密的值將會擁有 varbinary 資料類型。  
  
## <a name="see-also"></a>請參閱＜  
 [搭配使用一律加密與 JDBC 驅動程式](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  
  
