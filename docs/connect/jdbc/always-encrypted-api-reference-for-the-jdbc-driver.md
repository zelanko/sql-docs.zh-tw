---
title: JDBC Driver 的 Always Encrypted API 參考 | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1605b608550446ecb31a79e6074a7e8cfa7ea916
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52420699"
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
|新方法：<br /><br /> `public static void setColumnEncryptionTrustedMasterKeyPaths(Map<String, List\<String>> trustedKeyPaths)`<br /><br /> `public static void updateColumnEncryptionTrustedMasterKeyPaths(String server, List\<String> trustedKeyPaths)`<br /><br /> `public static void removeColumnEncryptionTrustedMasterKeyPaths(String server)`|可讓您為資料庫伺服器設定/更新/移除受信任的金鑰路徑清單。 如果驅動程式在處理應用程式查詢時接收到不在清單上的金鑰路徑，則查詢會失敗。 此屬性會針對受到安全性攻擊危害的 SQL Server 提供額外的保護，這類 SQL Server 會傳送假的金鑰路徑，而可能會導致遺漏金鑰存放區認證。|  
|新方法：<br /><br /> `public static Map<String, List\<String>> getColumnEncryptionTrustedMasterKeyPaths()`|會傳回資料庫伺服器的受信任金鑰路徑清單。|  
|新方法：<br /><br /> `public static void registerColumnEncryptionKeyStoreProviders (Map\<String, SQLServerColumnEncryptionKeyStoreProvider> clientKeyStoreProviders)`|可讓您註冊自訂金鑰存放區提供者。 它是一個字典，會將金鑰存放區提供者名稱對應至金鑰存放區提供者實作。<br /><br /> 若要使用 JVM 金鑰存放區，您需要使用 JVM 金鑰存放區認證將 SQLServerColumnEncryptionJVMKeyStoreProvider 物件具現化，並向驅動程式註冊它。 此提供者的名稱必須為 'MSSQL_JVM_KEYSTORE'。<br /><br /> 若要使用 Azure Key Vault 存放區，您需要具現化 SQLServerColumnEncryptionAzureKeyStoreProvider 物件，並向驅動程式。 此提供者的名稱必須是 'AZURE_KEY_VAULT'。|
|`public final boolean getSendTimeAsDatetime()`|傳回 sendTimeAsDatetime 連接屬性的設定。|
|`public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)`|修改 sendTimeAsDatetime 連接屬性的設定。|

 **SQLServerConnectionPoolProxy 類別**
|[屬性]|Description|  
|----------|-----------------|  
|`public final boolean getSendTimeAsDatetime()` | 傳回 sendTimeAsDatetime 連接屬性的設定。|
|`public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)` | 修改 sendTimeAsDatetime 連接屬性的設定。|
     
  
 **SQLServerDataSource 類別**  
  
|[屬性]|Description|  
|----------|-----------------|  
|`public void setColumnEncryptionSetting(String columnEncryptionSetting)`|啟用/停用資料來源物件的一律加密功能。<br /><br /> 預設值為 Disabled。|  
|`public String getColumnEncryptionSetting()`|擷取資料來源物件的一律加密功能設定。|
|`public void setKeyStoreAuthentication(String keyStoreAuthentication)`|設定可識別金鑰存放區的名稱。 支援的值是**JavaKeyStorePassword**識別 Java 金鑰存放區。<br/><br/>預設值是 null。|
|`public String getKeyStoreAuthentication()`|取得資料來源物件之 keyStoreAuthentication 設定的值。|
|`public void setKeyStoreSecret(String keyStoreSecret)`|設定 Java keystore 的密碼。 金鑰儲存區和金鑰的密碼必須相同。 請注意，必須使用設定該 keyStoreAuthentication **JavaKeyStorePassword**。|
|`public void setKeyStoreLocation(String keyStoreLocation)`|設定包括 Java 金鑰存放區的檔案名稱的位置。 請注意，必須使用設定該 keyStoreAuthentication **JavaKeyStorePassword**。|
|`public String getKeyStoreLocation()`|擷取 keyStoreLocation Java 金鑰存放區。|
  
 **SQLServerColumnEncryptionJavaKeyStoreProvider 類別**  
  
 Java 金鑰存放區的金鑰存放區提供者實作。 此類別可讓您將儲存在 Java 金鑰存放區中的憑證，當成資料行主要金鑰使用。  
  
 建構函式  
  
|[屬性]|Description|  
|----------|-----------------|  
|`public SQLServerColumnEncryptionJavaKeyStoreProvider (String keyStoreLocation, char[] keyStoreSecret)`|Java 金鑰存放區的金鑰存放區提供者。|  
  
 方法  
  
|[屬性]|Description|  
|----------|-----------------|  
|`public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)`|將資料行加密金鑰的指定加密值解密。 加密的值必須使用具指定金鑰路徑的憑證，以及指定的演算法，進而加以加密。<br /><br /> **金鑰路徑的格式應為下列其中一項：**<br /><br /> 憑證指紋：<certificate_thumbprint><br /><br /> 別名：<certificate_alias><br /><br /> 覆寫 SQLServerColumnEncryptionKeyStoreProvider。 （字串、 字串、 Byte[]).) decryptColumnEncryptionKey|  
|`public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)`|使用具指定金鑰路徑的憑證，以及指定的演算法，將資料行加密金鑰加密。<br /><br /> **金鑰路徑的格式應為下列其中一項：**<br /><br /> 憑證指紋：<certificate_thumbprint><br /><br /> 別名：<certificate_alias><br /><br /> 覆寫 SQLServerColumnEncryptionKeyStoreProvider。 （字串、 字串、 Byte[]).) encryptColumnEncryptionKey|  
|`public void setName (String name)`|設定此金鑰存放區提供者的名稱。|
|`public String getName ()`|取得此金鑰存放區提供者的名稱。|
  
 **SQLServerColumnEncryptionAzureKeyVaultProvider 類別**  
  
 Azure Key Vault 的金鑰存放區提供者實作。 這個類別可讓您使用 Azure Key Vault 中儲存為資料行主要金鑰的金鑰。  
  
 建構函式  
  
|[屬性]|Description|  
|----------|-----------------|  
|`public SQLServerColumnEncryptionAzureKeyVaultProvider (String clientId, String clientKey)`|Azure Key Vault 的金鑰存放區提供者。  您需要提供識別碼和用戶端要求權杖來向 Azure Key Vault 的金鑰。|  
  
 方法  
  
|[屬性]|Description|  
|----------|-----------------|  
| `public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)` | Decryptes 加密資料行加密金鑰 (CEK)。 使用主要金鑰路徑所指定的非對稱金鑰的 RSA 加密演算法可完成此解密。<br />覆寫 SQLServerColumnEncryptionKeyStoreProvider。 （字串、 字串、 Byte[]).) decryptColumnEncryptionKey |  
| `public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] columnEncryptionKey)` | 加密資料行加密金鑰，讓指定的演算法指定的資料行主要金鑰。<br />覆寫 SQLServerColumnEncryptionKeyStoreProvider。 （字串、 字串、 Byte[]).) encryptColumnEncryptionKey |  
|`public void setName (String name)`|設定此金鑰存放區提供者的名稱。|
|`public String getName ()`|取得此金鑰存放區提供者的名稱。|  
  
  
 **SQLServerKeyVaultAuthenticationCallback 介面**  
  
 這個介面包含 Azure 金鑰保存庫驗證，也就是由使用者所實作的其中一個方法。  
  
 方法  
  
|[屬性]|Description|  
|----------|-----------------|  
|`public String getAccessToken(String authority, String resource, String scope);`|此方法需要覆寫。 方法用來取得存取權杖至 Azure 金鑰保存庫。|  
  
 **SQLServerColumnEncryptionKeyStoreProvider 類別**  
  
 擴充此類別來實作自訂金鑰存放區提供者。  
  
|[屬性]|Description|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|所有金鑰存放區提供者的基底類別。 自訂提供者必須衍生自此類別並覆寫其成員函式，然後使用 SQLServerConnection 予以註冊。 registerColumnEncryptionKeyStoreProviders()。|  
  
 方法  
  
|[屬性]|Description|  
|----------|-----------------|  
|`public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)`|用來將資料行加密金鑰的指定加密值解密的基底類別方法。 加密的值必須使用具有指定金鑰路徑的資料行主要金鑰和指定的演算法，進而加以加密。|  
|`public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)`|基底類別方法，使用具指定金鑰路徑的資料行主要金鑰，以及指定的演算法，進而將資料加密金鑰加密。|
|`public abstract void setName(String name)`|設定此金鑰存放區提供者的名稱。|
|`public abstract String getName()`|取得此金鑰存放區提供者的名稱。|  
  
 在新的或多載方法**SQLServerPreparedStatement**類別  
  
|[屬性]|Description|  
|----------|-----------------|  
|`public void setBigDecimal(int parameterIndex, BigDecimal x, int precision, int scale)`<br /><br /> `public void setObject(int parameterIndex, Object x, int targetSqlType, Integer precision, int scale)`<br /><br /> `public void setObject(int parameterIndex, Object x, SQLType targetSqlType, Integer precision, Integer scale)`<br /><br /> `public void setTime(int parameterIndex, java.sql.Time x, int scale)`<br /><br /> `public void setTimestamp(int parameterIndex, java.sql.Timestamp x, int scale)` <br />`public void setDateTimeOffset(int parameterIndex, microsoft.sql.DateTimeOffset x, int scale)`|這些方法多載與有效位數或小數位數引數或兩者皆可支援 「 永遠加密 」 的特定資料類型，需要有效位數和小數位數資訊。|  
|`public void setMoney(int parameterIndex, BigDecimal x)`<br /><br /> `public void setSmallMoney(int parameterIndex, BigDecimal x)`<br /><br /> `public void setUniqueIdentifier(int parameterIndex, String guid)`<br /><br /> `public void setDateTime(int parameterIndex, java.sql.Timestamp x)`<br /><br /> `public void setSmallDateTime(int parameterIndex, java.sql.Timestamp x)`|這些方法會加入至資料類型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime 的支援 「 永遠加密。 <br/><br/>請注意，現有`setTimestamp()`方法用於將參數值傳送到已加密的 datetime2 資料行。 對於加密的 datetime 和 smalldatetime 資料行，請使用新的方法`setDateTime()`和`setSmallDateTime()`分別。|  
|`public final void setBigDecimal(int parameterIndex, BigDecimal x, int precision, int scale, boolean forceEncrypt)`<br /><br /> `public final void setMoney(int parameterIndex, BigDecimal x, boolean forceEncrypt)`<br /><br /> `public final void setSmallMoney(int parameterIndex, BigDecimal x, boolean forceEncrypt)`<br /><br /> `public final void setBoolean(int parameterIndex, boolean x, boolean forceEncrypt)`<br /><br /> `public final void setByte(int parameterIndex, byte x, boolean forceEncrypt)`<br /><br /> `public final void setBytes(int parameterIndex, byte x[], boolean forceEncrypt)`<br /><br /> `public final void setUniqueIdentifier(int parameterIndex, String guid, boolean forceEncrypt)`<br /><br /> `public final void setDouble(int parameterIndex, double x, boolean forceEncrypt)`<br /><br /> `public final void setFloat(int parameterIndex, float x, boolean forceEncrypt)`<br /><br /> `public final void setInt(int parameterIndex, int value, boolean forceEncrypt)`<br /><br /> `public final void setLong(int parameterIndex, long x, boolean forceEncrypt)`<br /><br /> `public final setObject(int parameterIndex, Object x, int targetSqlType, Integer precision, int scale, boolean forceEncrypt)`<br /><br /> `public final void setObject(int parameterIndex, Object x, SQLType targetSqlType, Integer precision, Integer scale, boolean forceEncrypt)`<br /><br /> `public final void setShort(int parameterIndex, short x, boolean forceEncrypt)`<br /><br /> `public final void setString(int parameterIndex, String str, boolean forceEncrypt)`<br /><br /> `public final void setNString(int parameterIndex, String value, boolean forceEncrypt)`<br /><br /> `public final void setTime(int parameterIndex, java.sql.Time x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setTimestamp(int parameterIndex, java.sql.Timestamp x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setDateTimeOffset(int parameterIndex, microsoft.sql.DateTimeOffset x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setDateTime(int parameterIndex, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public final void setSmallDateTime(int parameterIndex, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public final void setDate(int parameterIndex, java.sql.Date x, java.util.Calendar cal, boolean forceEncrypt)`<br /><br /> `public final void setTime(int parameterIndex, java.sql.Time x, java.util.Calendar cal, boolean forceEncrypt)`<br /><br /> `public final void setTimestamp(int parameterIndex, java.sql.Timestamp x, java.util.Calendar cal, boolean forceEncrypt)`|將指定的參數設定為指定的 Java 值。<br /><br /> 如果布林 forceEncrypt 設為 true 時，查詢參數將才可設定指定資料行已加密，並啟用 永遠加密連接或陳述式。<br /><br /> 如果布林 forceEncrypt 設為 false 時，驅動程式將不會強制加密參數。|  
  
 在新的或多載方法**SQLServerCallableStatement**類別  
  
|[屬性]|Description|  
|----------|-----------------|  
|`public void registerOutParameter(int parameterIndex, int sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(int parameterIndex, SQLType sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(String parameterName, int sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(String parameterName, SQLType sqlType, int precision, int scale)`<br />`public void setBigDecimal(String parameterName, BigDecimal bd, int precision, int scale)`<br /><br /> `public void setTime(String parameterName, java.sql.Time t, int scale)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp t, int scale)`<br /><br /> `public void setDateTimeOffset(String parameterName, microsoft.sql.DateTimeOffset t, int scale)`<br/><br/>`public final void setObject(String sCol, Object x, int targetSqlType, Integer precision, int scale)`|這些方法多載與有效位數或小數位數引數或兩者皆可支援 「 永遠加密 」 的特定資料類型，需要有效位數和小數位數資訊。|  
|`public void setDateTime(String parameterName, java.sql.Timestamp x)`<br /><br /> `public void setSmallDateTime(String parameterName, java.sql.Timestamp x)`<br /><br /> `public void setUniqueIdentifier(String parameterName, String guid)`<br /><br /> `public void setMoney(String parameterName, BigDecimal bd)`<br /><br /> `public void setSmallMoney(String parameterName, BigDecimal bd)`<br/><br/>`public Timestamp getDateTime(int index)`<br/><br/>`public Timestamp getDateTime(String sCol)`<br/><br/>`public Timestamp getDateTime(int index, Calendar cal)`<br/><br/>`public Timestamp getSmallDateTime(int index)`<br/><br/>`public Timestamp getSmallDateTime(String sCol)`<br/><br/>`public Timestamp getSmallDateTime(int index, Calendar cal)`<br/><br/>`public Timestamp getSmallDateTime(String name, Calendar cal)`<br/><br/>`public BigDecimal getMoney(int index)`<br/><br/>`public BigDecimal getMoney(String sCol)`<br/><br/>`public BigDecimal getSmallMoney(int index)`<br/><br/>`public BigDecimal getSmallMoney(String sCol)`|這些方法會加入至資料類型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime 的支援 「 永遠加密。 <br/><br/>請注意，現有`setTimestamp()`方法用於將參數值傳送到已加密的 datetime2 資料行。 對於加密的 datetime 和 smalldatetime 資料行，請使用新的方法`setDateTime()`和`setSmallDateTime()`分別。|  
|`public void setObject(String parameterName, Object o, int n, int m, boolean forceEncrypt)`<br /><br /> `public void setObject(String parameterName, Object obj, SQLType jdbcType, int scale, boolean forceEncrypt)`<br /><br /> `public void setDate(String parameterName, java.sql.Date x, Calendar c, boolean forceEncrypt)`<br /><br /> `public void setTime(String parameterName, java.sql.Time t, int scale, boolean forceEncrypt)`<br /><br /> `public void setTime(String parameterName, java.sql.Time x, Calendar c, boolean forceEncrypt)`<br /><br /> `public void setDateTime(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setDateTimeOffset(String parameterName, microsoft.sql.DateTimeOffset t, int scale, boolean forceEncrypt)`<br /><br /> `public void setSmallDateTime(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp t, int scale, boolean forceEncrypt)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setUniqueIdentifier(String parameterName, String guid, boolean forceEncrypt)`<br /><br /> `public void setBytes(String parameterName, byte[] b, boolean forceEncrypt)`<br /><br /> `public void setByte(String parameterName, byte b, boolean forceEncrypt)`<br /><br /> `public void setString(String parameterName, String s, boolean forceEncrypt)`<br /><br /> `public final void setNString(String parameterName, String value, boolean forceEncrypt)<br /><br /> public void setMoney(String parameterName, BigDecimal bd, boolean forceEncrypt)`<br /><br /> `public void setSmallMoney(String parameterName, BigDecimal bd, boolean forceEncrypt)`<br /><br /> `public void setBigDecimal(String parameterName, BigDecimal bd, int precision, int scale, boolean forceEncrypt)`<br /><br /> `public void setDouble(String parameterName, double d, boolean forceEncrypt)`<br /><br /> `public void setFloat(String parameterName, float f, boolean forceEncrypt)`<br /><br /> `public void setInt(String parameterName, int i, boolean forceEncrypt)`<br /><br /> `public void setLong(String parameterName, long l, boolean forceEncrypt)`<br /><br /> `public void setShort(String parameterName, short s, boolean forceEncrypt)`<br /><br /> `public void setBoolean(String parameterNames, boolean b, boolean forceEncrypt)`<br/><br/>`public void setTimeStamp(String sCol, java.sql.Timestamp x, Calendar c, Boolean forceEncrypt)`|將指定的參數設定為指定的 Java 值。<br /><br /> 如果布林 forceEncrypt 設為 true 時，查詢參數將才可設定指定資料行已加密，並啟用 永遠加密連接或陳述式。<br /><br /> 如果布林 forceEncrypt 設為 false 時，驅動程式將不會強制加密參數。|
 

 在新的或多載方法**SQLServerResultSet**類別  
  
|[屬性]|Description|  
|----------|-----------------|  
|`public String getUniqueIdentifier(int columnIndex)`<br/><br/>`public String getUniqueIdentifier(String columnLabel)`<br/><br/>   `public java.sql.Timestamp getDateTime(int columnIndex)` <br/><br/> `public java.sql.Timestamp getDateTime(String columnName)`   <br/><br/> `public java.sql.Timestamp getDateTime(int columnIndex, Calendar cal)`   <br/><br/>`public java.sql.Timestamp getDateTime(String colName, Calendar cal)`    <br/><br/>`public java.sql.Timestamp getSmallDateTime(int columnIndex)`    <br/><br/> `public java.sql.Timestamp getSmallDateTime(String columnName)`   <br/><br/> `public java.sql.Timestamp getSmallDateTime(int columnIndex, Calendar cal)`   <br/><br/> `public java.sql.Timestamp getSmallDateTime(String colName, Calendar cal)`   <br/><br/>  `public BigDecimal getMoney(int columnIndex)`  <br/><br/> `public BigDecimal getMoney(String columnName)`   <br/><br/> `public BigDecimal getSmallMoney(int columnIndex)`   <br/><br/>  `public BigDecimal getSmallMoney(String columnName)`  <br/><br/>`public void updateMoney(String columnName, BigDecimal x)`    <br/><br/>  `public void updateSmallMoney(String columnName, BigDecimal x)`  <br/><br/>     `public void updateDateTime(int index, java.sql.Timestamp x)` <br/><br/> `public void updateSmallDateTime(int index, java.sql.Timestamp x)` |這些方法會新增至支援的資料類型 money、 smallmoney、 uniqueidentifier、 datetime 和 smalldatetime 的 Always Encrypted。 <br/><br/>請注意，現有`updateTimestamp()`方法用來更新加密的 datetime2 資料行。 對於加密的 datetime 和 smalldatetime 資料行，請使用新的方法`updateDateTime()`和`updateSmallDateTime()`分別。|
|`public void updateBoolean(int index, boolean x, boolean forceEncrypt)`  <br/><br/>  `public void updateByte(int index, byte x, boolean forceEncrypt)`  <br/><br/>  `public void updateShort(int index, short x, boolean forceEncrypt)`  <br/><br/> `public void updateInt(int index, int x, boolean forceEncrypt)`   <br/><br/>  `public void updateLong(int index, long x, boolean forceEncrypt)`  <br/><br/> `public void updateFloat(int index, float x, boolean forceEncrypt)`   <br/><br/> `public void updateDouble(int index, double x, boolean forceEncrypt)`   <br/><br/> `public void updateMoney(int index, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateMoney(String columnName, BigDecimal x, boolean forceEncrypt)`  <br/><br/> `public void updateSmallMoney(int index, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateSmallMoney(String columnName, BigDecimal x, boolean forceEncrypt)`  <br/><br/> `public void updateBigDecimal(int index, BigDecimal x, Integer precision, Integer scale, boolean forceEncrypt)`   <br/><br/>  `public void updateString(int columnIndex, String stringValue, boolean forceEncrypt)`  <br/><br/>  `public void updateNString(int columnIndex, String nString, boolean forceEncrypt)`  <br/><br/>  `public void updateNString(String columnLabel, String nString, boolean forceEncrypt)`  <br/><br/> `public void updateBytes(int index, byte x[], boolean forceEncrypt)   <br/><br/>  public void updateDate(int index, java.sql.Date x, boolean forceEncrypt)`  <br/><br/> `public void updateTime(int index, java.sql.Time x, Integer scale, boolean forceEncrypt)`   <br/><br/> `public void updateTimestamp(int index, java.sql.Timestamp x, int scale, boolean forceEncrypt)`   <br/><br/> `public void updateDateTime(int index, java.sql.Timestamp x, Integer scale, boolean forceEncrypt)`   <br/><br/> `public void updateSmallDateTime(int index, java.sql.Timestamp x, Integer scale, boolean forceEncrypt)`   <br/><br/>  `public void updateDateTimeOffset(int index, microsoft.sql.DateTimeOffset x, Integer scale, boolean forceEncrypt)`  <br/><br/> `public void updateUniqueIdentifier(int index, String x, boolean forceEncrypt)`    <br/><br/>  `public void updateObject(int index, Object x, int precision, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateObject(int index, Object obj, SQLType targetSqlType, int scale, boolean forceEncrypt)`  <br/><br/> `public void updateBoolean(String columnName, boolean x, boolean forceEncrypt)`    <br/><br/>  `public void updateByte(String columnName, byte x, boolean forceEncrypt)`  <br/><br/>  `public void updateShort(String columnName, short x, boolean forceEncrypt)`  <br/><br/> `public void updateInt(String columnName, int x, boolean forceEncrypt)`   <br/><br/>   `public void updateLong(String columnName, long x, boolean forceEncrypt)` <br/><br/>  `public void updateFloat(String columnName, float x, boolean forceEncrypt)`  <br/><br/>  `public void updateDouble(String columnName, double x, boolean forceEncrypt)  <br/><br/> public void updateBigDecimal(String columnName, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateBigDecimal(String columnName, BigDecimal x, Integer precision, Integer scale, boolean forceEncrypt)`  <br/><br/> `public void updateString(String columnName, String x, boolean forceEncrypt)`   <br/><br/>  `public void updateBytes(String columnName, byte x[], boolean forceEncrypt)`  <br/><br/> `public void updateDate(String columnName, java.sql.Date x, boolean forceEncrypt)`   <br/><br/>  `public void updateTime(String columnName, java.sql.Time x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateTimestamp(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`  <br/><br/> `public void updateDateTime(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`   <br/><br/>  `public void updateSmallDateTime(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateDateTimeOffset(String columnName, microsoft.sql.DateTimeOffset x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateUniqueIdentifier(String columnName, String x, boolean forceEncrypt)`<br/><br/>`public void updateObject(String columnName, Object x, int precision, int scale, boolean forceEncrypt)`<br/><br/>`public void updateObject(String columnName, Object obj, SQLType targetSqlType, int scale, boolean forceEncrypt)`|為給定的 java 值更新指定的資料行。<br/><br/>如果布林 forceEncrypt 設為 true，資料行才會設定如果已加密，並啟用 永遠加密連接或陳述式。<br/><br/>如果布林 forceEncrypt 設為 false 時，驅動程式將不會強制加密參數。|

  
在新的型別**microsoft.sql.Types**類別
|[屬性]|Description|  
|----------|-----------------|  
|DATETIME、 SMALLDATETIME、 MONEY、 SMALLMONEY、 GUID|用戶端傳送的參數值時，使用這些類型做為目標 SQL 型別**加密**datetime、 smalldatetime、 money、 smallmoney、 使用 uniqueidentifier 資料行將`setObject()/updateObject()`API 方法。|  
  
  
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
|`public Statement createStatement(int nType, int nConcur, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|建立會產生具有給定型的別、 並行處理、 保留性和資料行加密設定的結果集物件的陳述式物件。|  
|`public CallableStatement prepareCall(String sql, int nType, int nConcur, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetiing)`|建立 CallableStatement 物件將會產生具有給定型的別、 並行和保留性的結果集物件的指定資料行加密設定。|  
|`public PreparedStatement prepareStatement(String sql, int autogeneratedKeys, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|建立 PreparedStatement 物件能夠擷取自動產生金鑰的指定資料行加密設定。|  
|`public PreparedStatement prepareStatement(String sql, String[] columnNames, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|建立 PreparedStatement 物件將會產生結果集物件，指定資料行名稱的指定資料行加密設定。|  
|`public PreparedStatement prepareStatement(String sql, int[] columnIndexes, SQLServerStatementColumnEncryptionSetting stmtColEncSetting`|建立 PreparedStatement 物件將會產生具有指定資料行索引的結果集物件的指定資料行加密設定。|  
|`public PreparedStatement prepareStatement(String sql, int nType, int nConcur, int nHold, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|建立 PreparedStatement 物件將會產生具有給定型的別、 並行和保留性的結果集物件的指定資料行加密設定。|  
  
> [!NOTE]  
>  如果 Always Encrypted 的查詢已停用，而且查詢具有需要加密 （參數對應至加密資料行） 的參數，則查詢會失敗。  
>   
>  如果 Always Encrypted 的查詢已停用，而且查詢會從加密資料行中傳回結果，查詢會傳回加密的值。 加密的值必須為 varbinary 資料型別。  
  
 ## <a name="see-also"></a>另請參閱  
 [搭配使用一律加密與 JDBC 驅動程式](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  

