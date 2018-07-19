---
title: 使用 JDBC 驅動程式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6faaf05b-8b70-4ed2-9b44-eee5897f1cd0
caps.latest.revision: 54
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03ea3e895fb7d70b392e0c25372536770308049d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32852613"
---
# <a name="using-the-jdbc-driver"></a>使用 JDBC 驅動程式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  本節提供快速入門指示來進行的簡單連接[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫使用[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]。 在連接之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]必須先安裝在本機電腦或伺服器上，而且必須在本機電腦上安裝 JDBC 驅動程式。  
  
## <a name="choosing-the-right-jar-file"></a>選擇正確的 JAR 檔案  
 提供 SQL Server 的 Microsoft JDBC 驅動程式 6.4 **mssql-jdbc-6.4.0.jre7.jar**， **mssql-jdbc-6.4.0.jre8.jar**，和**mssql-jdbc-6.4.0.jre9.jar**類別庫根據您慣用的 Java Runtime Environment (JRE) 設定使用的檔案。  
 
 提供 SQL Server 的 Microsoft JDBC 驅動程式 6.2 **mssql-jdbc-6.2.1.jre7.jar**，和**mssql-jdbc-6.2.1.jre8.jar**類別，可根據您慣用的 Java 執行階段程式庫檔案Environment (JRE) 設定。  
  
  Microsoft JDBC Drivers 6.0 與 4.2 for SQL Server 提供**sqljdbc41.jar**，和**sqljdbc42.jar**類別庫檔案，可根據您慣用的 Java Runtime Environment (JRE) 設定。  
  
 Microsoft JDBC Driver 4.1 for SQL Server 提供**sqljdbc41.jar**類別程式庫檔案，可根據您慣用的 Java Runtime Environment (JRE) 設定。  
    
 您的選擇也會決定可用的功能。 如需選擇哪個 JAR 檔案的詳細資訊，請參閱[JDBC 驅動程式的系統需求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="setting-the-classpath"></a>設定 Classpath  
 JDBC Driver 不屬於 Java SDK 的一部分。 如果您想要使用它，您必須設定 classpath 以包含**sqljdbc.jar**檔案， **sqljdbc4.jar**檔案， **sqljdbc41.jar**檔案，或**sqljdbc42.jar**檔案。 如果使用 JDBC 驅動程式 6.2，設定 classpath 以包含**mssql-jdbc-6.2.1.jre7.jar**或**mssql-jdbc-6.2.1.jre8.jar**。 如果使用 JDBC 驅動程式 6.4，設定 classpath 以包含**mssql-jdbc-6.4.0.jre7.jar**， **mssql-jdbc-6.4.0.jre8.jar**或**mssql-jdbc-6.4.0.jre9.jar**。 如果 classpath 遺漏一個項目，則您的應用程式會擲回常見的「找不到類別」例外狀況。  
  
### <a name="for-microsoft-jdbc-driver-64"></a>For Microsoft JDBC Driver 6.4
 **Mssql-jdbc-6.4.0.jre7.jar**， **mssql-jdbc-6.4.0.jre8.jar**或**mssql-jdbc-6.4.0.jre9.jar**檔案會安裝在下列位置：  
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \mssql-jdbc-6.4.0.jre7.jar 
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \mssql-jdbc-6.4.0.jre8.jar
 
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \mssql-jdbc-6.4.0.jre9.jar
  
 以下是用於 Windows 應用程式的 CLASSPATH 陳述式範例：  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_6.4\enu\mssql-jdbc-6.4.0.jre9.jar`  
  
 以下是用於 Unix/Linux 應用程式的 CLASSPATH 陳述式範例：  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.4/enu/mssql-jdbc-6.4.0.jre9.jar`  
  
 您必須確定 CLASSPATH 陳述式包含只有一個[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，例如 mssql-jdbc-6.4.0.jre7.jar、 mssql-jdbc-6.4.0.jre8.jar 或 mssql-jdbc-6.4.0.jre9.jar。   

### <a name="for-microsoft-jdbc-driver-62"></a>For Microsoft JDBC Driver 6.2
 **Mssql-jdbc-6.2.1.jre7.jar**或**mssql-jdbc-6.2.1.jre8.jar**檔案會安裝在下列位置：  
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \mssql-jdbc-6.2.1.jre7.jar 
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \mssql-jdbc-6.2.1.jre8.jar
  
 以下是用於 Windows 應用程式的 CLASSPATH 陳述式範例：  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.2 for SQL Server\sqljdbc_6.2\enu\mssql-jdbc-6.2.1.jre8.jar`  
  
 以下是用於 Unix/Linux 應用程式的 CLASSPATH 陳述式範例：  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.2/enu/mssql-jdbc-6.2.1.jre8.jar`  
  
 您必須確定 CLASSPATH 陳述式包含只有一個[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，例如 mssql-jdbc-6.2.1.jre7.jar 或 mssql-jdbc-6.2.1.jre8.jar。  

### <a name="for-microsoft-jdbc-driver-41-42-and-60"></a>Microsoft JDBC driver 4.1、 4.2 與 6.0
 sqljdbc.jar 檔案、sqljdbc4.jar 檔案、sqljdbc41.jar 或 sqljdbc42.jar 檔案安裝於下列位置：  
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \sqljdbc.jar  
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \sqljdbc4.jar  
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \sqljdbc41.jar  
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \sqljdbc42.jar  
  
 以下是用於 Windows 應用程式的 CLASSPATH 陳述式範例：  
  
 `CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.0 for SQL Server\sqljdbc_4.2\enu\sqljdbc42.jar`  
  
 以下是用於 Unix/Linux 應用程式的 CLASSPATH 陳述式範例：  
  
 `CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_4.2/enu/sqljdbc42.jar`  
  
 您必須確定 CLASSPATH 陳述式包含只有一個[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，例如 sqljdbc.jar、 sqljdbc4.jar、 sqljdbc41.jar 或 sqljdbc42.jar。  
  
> [!NOTE]  
>  在 Windows 系統上，若目錄名稱超過 8.3 檔案名稱慣例或資料夾名稱具有空格，可能會導致 classpaths 的問題。 如果您懷疑這些類型的問題，您應該暫時進入 sqljdbc.jar 檔案、 sqljdbc4.jar 檔案或 sqljdbc41.jar 檔案的簡單目錄名稱例如`C:\Temp`、 變更 classpath，並判斷是否有解決問題。  
  
### <a name="applications-that-are-run-directly-at-the-command-prompt"></a>直接在命令提示字元下執行的應用程式  
 Classpath 是設定在作業系統中。 請將 sqljdbc.jar、sqljdbc4.jar 或 sqljdbc41.jar 附加至系統的 Classpath。 或者，您可以藉由執行應用程式的 Java 命令列上指定 classpath`java -classpath`選項。  
  
### <a name="applications-that-run-in-an-ide"></a>在 IDE 中執行的應用程式  
 每一個 IDE 供應商都會提供不同的方法，在其 IDE 中設定 Classpath。 只在作業系統中設定 Classpath 將無法作用。 您必須將 sqljdbc.jar、sqljdbc4.jar 或 sqljdbc41.jar 加入 IDE classpath 中。  
  
### <a name="servlets-and-jsps"></a>Servlet 及 JSP  
 Servlet 和 JSP 是在 servlet/JSP 引擎中執行，例如 Tomcat。 Classpath 必須根據 servlet/JSP 引擎文件來設定。 只在作業系統中設定 Classpath 將無法作用。 有些 servlet/JSP 引擎提供設定畫面，您可以用來設定引擎的 Classpath。 在此情況下，您必須將正確的 JDBC 驅動程式 JAR 檔附加到現有的引擎 Classpath 中，並重新啟動引擎。 在其他情況下，您可以在引擎安裝期間，將 sqljdbc.jar、sqljdbc4.jar 或 sqljdbc41.jar 複製到特定目錄 (例如 lib) 來部署該驅動程式。 引擎驅動程式 Classpath 也可以指定在引擎特定組態檔中。  
  
### <a name="enterprise-java-beans"></a>Enterprise Java Bean  
 Enterprise Java Bean (EJB) 是在 EJB 容器中執行。 EJB 容器的來源是各種供應商。 Java Applet 會在瀏覽器中執行，但是您可以從 Web 伺服器下載。 將 sqljdbc.jar、 sqljdbc4.jar 或 sqljdbc41.jar 複製到 web 伺服器的根目錄，並在 applet 的 HTML 封存索引標籤中指定 JAR 檔案的名稱，例如`<applet ... archive=sqljdbc.jar>`。  
  
## <a name="making-a-simple-connection-to-a-database"></a>與資料庫建立簡單連接  
 使用 sqljdbc.jar 類別庫時，應用程式必須先依照下列方式註冊此驅動程式：  
  
 `Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");`  
  
 載入驅動程式時，您可以使用連接 URL 和 DriverManager 類別 getConnection 方法，來建立連接：  
  
```  
String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
   "databaseName=AdventureWorks;user=MyUserName;password=*****;";  
Connection con = DriverManager.getConnection(connectionUrl);  
```  
  
 在 JDBC API 4.0 中，DriverManager.getConnection 方法已強化成可自動載入 JDBC 驅動程式。 因此，應用程式不需要呼叫 Class.forName 方法，以註冊或使用 sqljdbc4.jar、 sqljdbc41.jar 或 sqljdbc42.jar 類別庫時載入驅動程式。  
  
 DriverManager 類別的 getConnection 方法呼叫時，就有一個適當的驅動程式位於從已註冊的 JDBC 驅動程式的集合。 sqljdbc4.jar、 sqljdbc41.jar 或 sqljdbc42.jar 檔案包含"META-INF/services/java.sql.Driver 」 檔案，其中包含**com.microsoft.sqlserver.jdbc.SQLServerDriver**作為已註冊的驅動程式。 現有的應用程式，目前載入的驅動程式使用 Class.forName 方法，將繼續運作而不需修改。  
  
> [!NOTE]  
>  sqljdbc4.jar、sqljdbc41.jar 或 sqljdbc42.jar 類別庫無法搭配舊版的 Java Runtime Environment (JRE) 使用。 請參閱[JDBC 驅動程式的系統需求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)所支援的 JRE 版本清單[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]。  
  
 如需如何連接資料來源及使用連接 URL 的詳細資訊，請參閱[建立連接 URL](../../connect/jdbc/building-the-connection-url.md)和[設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
## <a name="see-also"></a>另請參閱  
 [JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
