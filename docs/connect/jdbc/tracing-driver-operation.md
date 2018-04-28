---
title: 追蹤驅動程式作業 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 723aeae7-6504-4585-ba8b-3525115bea8b
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ea02f1c06e942933fa7add21888447664e3608f3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="tracing-driver-operation"></a>追蹤驅動程式作業
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支援追蹤 （或記錄），協助您解決所發生的問題，JDBC 驅動程式，用於您的應用程式時使用。 若要啟用追蹤，JDBC 驅動程式會使用記錄 Api java.util.logging，提供一組類別建立記錄器和 LogRecord 物件中。  
  
> [!NOTE]  
>  若是 JDBC 驅動程式隨附的原生元件 (sqljdbc_xa.dll)，內建診斷 (BID) 架構會啟用追蹤。 如需有關 BID 的詳細資訊，請參閱[SQL Server 中的資料存取追蹤](http://go.microsoft.com/fwlink/?LinkId=70042)。  
  
 當您開發應用程式時，您可以對進行呼叫記錄器物件，進而建立 LogRecord 物件，接著會傳遞至處理常式物件的處理。 記錄器和處理常式物件的記錄級別，兩者皆使用，然後選擇性地處理記錄篩選，可管制哪些 LogRecords。 完成記錄作業時，處理常式物件可以選擇性地使用格式子物件來發行記錄資訊。  
  
 根據預設，java.util.logging 架構會將其輸出寫入到檔案。 此輸出記錄檔必須將寫入權限授與給執行 JDBC 驅動程式的內容。  
  
> [!NOTE]  
>  如需使用各種記錄物件以進行程式追蹤的詳細資訊，請參閱 Sun Microsystems 網站上的＜Java 記錄 API＞文件 (英文)。  
  
 下列章節說明記錄層次以及可以記錄的類別目錄，並提供如何在應用程式中啟用追蹤的相關資訊。  
  
## <a name="logging-levels"></a>記錄層級  
 所建立的每則記錄訊息都有相關聯的記錄層次。 記錄層次會決定記錄訊息，所定義的重要性**層級**java.util.logging 中的類別。 啟用單一層級的記錄也會啟用所有較高層級的記錄。 本節將描述公用記錄類別目錄和內部記錄類別目錄的記錄層級。 如需有關記錄類別目錄的詳細資訊，請參閱本主題的「記錄類別目錄」一節。  
  
 下表將描述公用記錄類別目錄的每個可用記錄層級。  
  
|名稱|Description|  
|----------|-----------------|  
|SEVERE|表示嚴重失敗，這是最高的記錄層級。 在 JDBC 驅動程式中，這個層次用於報告錯誤和例外狀況。|  
|WARNING|表示潛在問題。|  
|INFO|提供參考訊息。|  
|CONFIG|提供組態訊息。 請注意，JDBC Driver 目前無法提供任何組態訊息。|  
|FINE|提供基本的追蹤資訊，包括公用方法所擲回的所有例外狀況。|  
|FINER|提供詳細的追蹤資訊，包括所有公用方法的進入和結束點 (包含相關聯的參數資料類型)，以及公用類別的所有公用屬性。 此外，輸入參數、 輸出參數和方法的傳回值 CLOB、 BLOB、 NCLOB、 讀取器，除了\<資料流 > 傳回實值類型。|  
|FINEST|提供非常詳細的追蹤資訊。 這是最低的記錄層級。|  
|OFF|關閉記錄。|  
|ALL|啟用所有訊息的記錄。|  
  
 下表將描述內部記錄類別目錄的每個可用記錄層級。  
  
|名稱|Description|  
|----------|-----------------|  
|SEVERE|表示嚴重失敗，這是最高的記錄層級。 在 JDBC 驅動程式中，這個層次用於報告錯誤和例外狀況。|  
|WARNING|表示潛在問題。|  
|INFO|提供參考訊息。|  
|FINE|提供追蹤資訊，包括基本物件建立和解構。 此外，還提供了公用方法所擲回的所有例外狀況。|  
|FINER|提供詳細的追蹤資訊，包括所有公用方法的進入和結束點 (包含相關聯的參數資料類型)，以及公用類別的所有公用屬性。 此外，輸入參數、 輸出參數和方法的傳回值 CLOB、 BLOB、 NCLOB、 讀取器，除了\<資料流 > 傳回實值類型。<br /><br /> 下列記錄類別目錄存在 JDBC 驅動程式 1.2 版中，而且具有 FINE 記錄層級： [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)， [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)、 XA 和[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md). 從 2.0 版開始，這些項目已升級為 FINER 層級。|  
|FINEST|提供非常詳細的追蹤資訊。 這是最低的記錄層級。<br /><br /> 下列記錄類別目錄存在 JDBC Driver 1.2 版中，而且具有 FINEST 記錄層級：TDS.DATA 和 TDS.TOKEN。 從 2.0 版開始，它們保留 FINEST 記錄層級。|  
|OFF|關閉記錄。|  
|ALL|啟用所有訊息的記錄。|  
  
## <a name="logging-categories"></a>記錄類別目錄  
 當您建立的記錄器物件時，您必須告知物件的具名的實體或類別目錄，您有興趣從中取得記錄資訊。 JDBC Driver 支援下列公用記錄類別目錄，而且它們定義於 com.microsoft.sqlserver.jdbc 驅動程式封裝中。  
  
|名稱|Description|  
|----------|-----------------|  
|連接|記錄中的訊息[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)類別。 應用程式可以將記錄層級設定為 FINER。|  
|引數|記錄中的訊息[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)類別。 應用程式可以將記錄層級設定為 FINER。|  
|DataSource|記錄中的訊息[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)類別。 應用程式可以將記錄層級設定為 FINE。|  
|ResultSet|記錄中的訊息[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)類別。 應用程式可以將記錄層級設定為 FINER。|  
|驅動程式|記錄中的訊息[SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md)類別。 應用程式可以將記錄層級設定為 FINER。|  
  
 從 Microsoft JDBC Driver 2.0 版開始，此驅動程式也提供了 com.microsoft.sqlserver.jdbc.internals 封裝，其中包含下列內部記錄類別目錄的記錄支援。  
  
|名稱|Description|  
|----------|-----------------|  
|AuthenticationJNI|記錄檔訊息有關 Windows 整合式驗證問題 (當**authenticationScheme**連接屬性隱含或明確設定為**NativeAuthentication**)。<br /><br /> 應用程式可以將記錄層級設定為 FINEST 和 FINE。|  
|SQLServerConnection|記錄中的訊息[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)類別。 應用程式可以將記錄層級設定為 FINE 和 FINER。|  
|SQLServerDataSource|記錄中的訊息[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)， [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)，和[SQLServerPooledConnection](../../connect/jdbc/reference/sqlserverpooledconnection-class.md)類別。<br /><br /> 應用程式可以將記錄層級設定為 FINER。|  
|InputStream|記錄有關下列資料類型的訊息：java.io.InputStream、java.io.Reader 以及具有最大規範的資料類型，例如 varchar、nvarchar 和 varbinary 資料類型。<br /><br /> 應用程式可以將記錄層級設定為 FINER。|  
|SQLServerException|記錄中的訊息[SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md)類別。 應用程式可以將記錄層級設定為 FINE。|  
|SQLServerResultSet|記錄中的訊息[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)類別。 應用程式可以將記錄層級設定為 FINE、FINER 和 FINEST。|  
|SQLServerStatement|記錄中的訊息[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)類別。 應用程式可以將記錄層級設定為 FINE、FINER 和 FINEST。|  
|XA|記錄中所有 XA 交易的訊息[SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md)類別。 應用程式可以將記錄層級設定為 FINE 和 FINER。|  
|KerbAuthentication|記錄有關類型 4 Kerberos 驗證的訊息 (當**authenticationScheme**連接屬性設定為**JavaKerberos**)。 此應用程式可以將記錄層級設定為 FINE 或 FINER。|  
|TDS.DATA|記錄包含此驅動程式與 SQL Server 之間 TDS 通訊協定層級交談的訊息。 每個所傳送和接收之 TDS 封包的詳細內容都會以 ASCII 和十六進位的格式記錄。 但是，系統不會記錄登入認證 (使用者名稱和密碼)， 只會記錄所有其他資料。<br /><br /> 這個類別目錄會建立非常詳細的訊息，並只能透過將記錄層次設為 FINEST 而啟用。|  
|TDS.Channel|這個類別目錄會追蹤與 SQL Server 進行 TCP 通訊通道的動作。 記錄的訊息包括通訊端開啟和關閉，以及讀取和寫入。 此外，它也會追蹤有關與 SQL Server 建立安全通訊端層 (SSL) 連接的訊息。<br /><br /> 這個類別目錄只能透過將記錄層級設定為 FINE、FINER 或 FINEST 而啟用。|  
|TDS.Writer|這個類別目錄會追蹤 TDS 通道的寫入作業。 請注意，系統只會追蹤寫入的長度，而非內容。 當注意訊號傳送至伺服器以取消陳述式的執行時，這個類別目錄也會追蹤問題。<br /><br /> 這個類別目錄只能透過將記錄層級設定為 FINEST 而啟用。|  
|TDS.Reader|這個類別目錄會在 FINEST 層級中追蹤來自 TDS 通道的特定讀取作業。 在 FINEST 層級中，追蹤可能會相當詳細。 在 WARNING 和 SEVERE 層級中，這個類別目錄會追蹤此驅動程式關閉連接之前，從 SQL Server 收到無效 TDS 通訊協定的時間。<br /><br /> 這個類別目錄只能透過將記錄層級設定為 FINER 和 FINEST 而啟用。|  
|TDS.Command|這個類別目錄會追蹤低層級的狀態轉換以及與執行 TDS 命令，例如相關聯的其他資訊[!INCLUDE[tsql](../../includes/tsql_md.md)]陳述式執行、 ResultSet 資料指標擷取、 認可等等。<br /><br /> 這個類別目錄只能透過將記錄層級設定為 FINEST 而啟用。|  
|TDS.TOKEN|這個類別目錄只會記錄 TDS 封包中的 Token，跟 TDS.DATA 類別目錄比起來較不詳細。 它只能透過將記錄層級設定為 FINEST 而啟用。<br /><br /> 在 FINEST 層級中，這個類別目錄會在回應中處理 TDS Token 時追蹤它們。 在 SEVERE 層級中，這個類別目錄會追蹤遇到無效 TDS Token 的時間。|  
|SQLServerDatabaseMetaData|記錄中的訊息[SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)類別。 應用程式可以將記錄層級設定為 FINE。|  
|SQLServerResultSetMetaData|記錄中的訊息[SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)類別。 應用程式可以將記錄層級設定為 FINE。|  
|SQLServerParameterMetaData|記錄中的訊息[SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md)類別。 應用程式可以將記錄層級設定為 FINE。|  
|SQLServerBlob|記錄中的訊息[SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md)類別。 應用程式可以將記錄層級設定為 FINE。|  
|SQLServerClob|記錄中的訊息[SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md)類別。 應用程式可以將記錄層級設定為 FINE。|  
|SQLServerSQLXML|記錄內部 SQLServerSQLXML 類別中的訊息。 應用程式可以將記錄層級設定為 FINE。|  
|SQLServerDriver|記錄中的訊息[SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md)類別。 應用程式可以將記錄層級設定為 FINE。|  
|SQLServerNClob|記錄中的訊息[SQLServerNClob](../../connect/jdbc/reference/sqlservernclob-class.md)類別。 應用程式可以將記錄層級設定為 FINE。|  
  
## <a name="enabling-tracing-programmatically"></a>以程式設計方式啟用追蹤  
 追蹤可以啟用以程式設計方式建立記錄器物件，並指出類別會記錄。 例如，下列程式碼會顯示如何啟用 SQL 陳述式的記錄：  
  
```  
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.FINER);  
```  
  
 若要關閉程式碼中的記錄，請使用下列：  
  
```  
logger.setLevel(Level.OFF);  
```  
  
 若要記錄所有可用的類別目錄，請使用下列：  
  
```  
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc");  
logger.setLevel(Level.FINE);  
```  
  
 若要停止記錄特定的類別目錄，請使用下列：  
  
```  
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.OFF);  
```  
  
## <a name="enabling-tracing-by-using-the-loggingproperties-file"></a>使用 Logging.Properties 檔案來啟用追蹤  
 您也可以啟用追蹤使用`logging.properties`檔案，位於`lib`Java Runtime Environment (JRE) 安裝的目錄。 可以用這個檔案來設定當啟用追蹤時，所要使用的記錄器和處理常式預設值。  
  
 以下是您可以在設定範例`logging.properties`檔案：  
  
```  
# Specify the handler, the handlers will be installed during VM startup.  
handlers= java.util.logging.FileHandler  
  
# Default global logging level.  
.level= OFF  
  
# default file output is in user's home directory.  
java.util.logging.FileHandler.pattern = %h/java%u.log  
java.util.logging.FileHandler.limit = 5000000  
java.util.logging.FileHandler.count = 20  
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter  
java.util.logging.FileHandler.level = FINEST  
  
# Facility specific properties.  
com.microsoft.sqlserver.jdbc.level=FINEST  
  
```  
  
> [!NOTE]  
>  您可以在設定屬性`logging.properties`使用 LogManager 物件屬於 java.util.logging 的檔案。  
  
## <a name="see-also"></a>另請參閱  
 [診斷 JDBC Driver 問題](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
