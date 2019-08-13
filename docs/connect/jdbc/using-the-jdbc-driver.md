---
title: 使用 JDBC Driver | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6faaf05b-8b70-4ed2-9b44-eee5897f1cd0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b00cd72309fde42ab794d7a365be2a736e3671e0
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893660"
---
# <a name="using-the-jdbc-driver"></a>使用 JDBC 驅動程式

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本節針對使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 建立與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的簡易連線，提供快速入門指示。 連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫之前，您必須先在本機電腦或伺服器上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，而且必須在本機電腦上安裝 JDBC 驅動程式。  
  
## <a name="choosing-the-right-jar-file"></a>選擇正確的 JAR 檔案

Microsoft JDBC Driver 提供各種與您慣用之 Java Runtime Environment (JRE) 設定一致的 Jar 以供使用，如下：

Microsoft JDBC Driver 7.4 for SQL Server 提供 **mssql-jdbc-7.4.1.jre8.jar**、**mssql-jdbc-7.4.1.jre11.jar** 及 **mssql-jdbc-7.4.1.jre12.jar** 類別庫檔案。

Microsoft JDBC Driver 7.2 for SQL Server 提供 **mssql-jdbc-7.2.2.jre8.jar** 和 **mssql-jdbc-7.2.2.jre11.jar** 類別庫檔案。

Microsoft JDBC Driver 7.0 for SQL Server 提供 **mssql-jdbc-7.0.0.jre8.jar** 和 **mssql-jdbc-7.0.0.jre10.jar** 類別庫檔案。

Microsoft JDBC Driver 6.4 for SQL Server 提供 **mssql-jdbc-6.4.0.jre7.jar**、**mssql-jdbc-6.4.0.jre8.jar** 及 **mssql-jdbc-6.4.0.jre9.jar** 類別庫檔案。

Microsoft JDBC Driver 6.2 for SQL Server 提供 **mssql-jdbc-6.2.2.jre7.jar** 和 **mssql-jdbc-6.2.2.jre8.jar** 類別庫檔案。
  
Microsoft JDBC Driver 6.0 和 4.2 for SQL Server 提供 **sqljdbc41.jar** 和 **sqljdbc42.jar** 類別庫檔案。
  
Microsoft JDBC Driver 4.1 for SQL Server 提供 **sqljdbc41.jar** 類別庫檔案。

您的選擇也會決定可用的功能。 如需選擇哪個 JAR 檔案的詳細資訊，請參閱 [JDBC Driver 的系統需求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="setting-the-classpath"></a>設定 Classpath

Microsoft JDBC 驅動程式 jar 不是 Java SDK 的一部分，而且必須包含於使用者應用程式的 Classpath 中。

如果使用 JDBC Driver 4.1 或 4.2，設定 Classpath 以包含來自個別驅動程式下載的 **sqljdbc41.jar** 或 **sqljdbc42.jar** 檔案。

如果使用 JDBC Driver 6.2，設定 Classpath 以包含 **mssql-6.2.2.jre7.jar** 或 **mssql-6.2.2.jre8.jar**。

如果使用 JDBC Driver 6.4，請設定 Classpath 以包含 **mssql-jdbc-6.4.0.jre7.jar**、**mssql-jdbc-6.4.0.jre8.jar** 或 **mssql-jdbc-6.4.0.jre9.jar**。

如果使用 JDBC Driver 7.0，設定 Classpath 以包含 **mssql-jdbc-7.0.0.jre8.jar** 或 **mssql-jdbc-7.0.0.jre10.jar**。

如果使用 JDBC Driver 7.2，設定 Classpath 以包含 **mssql-jdbc-7.2.2.jre8.jar** 或 **mssql-jdbc-7.2.2.jre11.jar**。

如果使用 JDBC Driver 7.4，請設定 classpath 以包含 **mssql-jdbc-7.4.1.jre8.jar**、**mssql-jdbc-7.4.1.jre11.jar** 或 **mssql-jdbc-7.4.1.jre12.jar**。

如果 Classpath 遺漏了適用於正確 Jar 檔案的項目，則應用程式將擲回常見的 `Class not found` 例外狀況。  

### <a name="for-microsoft-jdbc-driver-74"></a>對於 Microsoft JDBC Driver 7.4

**mssql-jdbc-7.4.1.jre8.jar**、**mssql-jdbc-7.4.1.jre11.jar** 或 **mssql-jdbc-7.4.1.jre12.jar** 檔案會安裝在下列位置：

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.4.1.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.4.1.jre11.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.4.1.jre12.jar
```

下列程式碼片段是用於 Windows 應用程式的 CLASSPATH 陳述式範例：

`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 7.4 for SQL Server\sqljdbc_7.4\enu\mssql-jdbc-7.4.1.jre11.jar`

下列程式碼片段是用於 Unix/Linux 應用程式的 CLASSPATH 陳述式範例：

`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_7.4/enu/mssql-jdbc-7.4.1.jre11.jar`

確定 CLASSPATH 陳述式僅包含一個 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，例如 **mssql-jdbc-7.4.1.jre8.jar**、**mssql-jdbc-7.4.1.jre11.jar**或 **mssql-jdbc-7.4.1.jre12.jar**。

### <a name="for-microsoft-jdbc-driver-72"></a>對於 Microsoft JDBC Driver 7.2

**mssql-jdbc-7.2.2.jre8.jar** 或 **mssql-jdbc-7.2.2.jre11.jar** 檔案會安裝在下列位置：

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.2.2.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.2.2.jre11.jar
```

下列程式碼片段是用於 Windows 應用程式的 CLASSPATH 陳述式範例：

`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 7.2 for SQL Server\sqljdbc_7.2\enu\mssql-jdbc-7.2.2.jre11.jar`

下列程式碼片段是用於 Unix/Linux 應用程式的 CLASSPATH 陳述式範例：

`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_7.2/enu/mssql-jdbc-7.2.2.jre11.jar`

確定 CLASSPATH 陳述式僅包含一個 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，例如 **mssql-jdbc-7.2.2.jre8.jar** 或 **mssql-jdbc-7.2.2.jre11.jar**。
  
### <a name="for-microsoft-jdbc-driver-70"></a>對於 Microsoft JDBC Driver 7.0

**mssql-jdbc-7.0.0.jre8.jar** 或 **mssql-jdbc-7.0.0.jre10.jar** 檔案會安裝在下列位置：

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.0.0.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-7.0.0.jre10.jar
```

下列程式碼片段是用於 Windows 應用程式的 CLASSPATH 陳述式範例：  

`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 7.0 for SQL Server\sqljdbc_7.0\enu\mssql-jdbc-7.0.0.jre10.jar`  
  
下列程式碼片段是用於 Unix/Linux 應用程式的 CLASSPATH 陳述式範例：  
  
`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_7.0/enu/mssql-jdbc-7.0.0.jre10.jar`  
  
確定 CLASSPATH 陳述式僅包含一個 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，例如 **mssql-jdbc-7.0.0.jre8.jar** 或 **mssql-jdbc-7.0.0.jre10.jar**。

### <a name="for-microsoft-jdbc-driver-64"></a>對於 Microsoft JDBC Driver 6.4

**mssql-jdbc-6.4.0.jre7.jar**、**mssql-jdbc-6.4.0.jre8.jar 或 **mssql-jdbc-6.4.0.jre9.jar** 檔案會安裝在下列位置：  

```bash  
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.4.0.jre7.jar
  
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.4.0.jre8.jar

\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.4.0.jre9.jar
```

下列程式碼片段是用於 Windows 應用程式的 CLASSPATH 陳述式範例：  
  
`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.4 for SQL Server\sqljdbc_6.4\enu\mssql-jdbc-6.4.0.jre9.jar`  
  
下列程式碼片段是用於 Unix/Linux 應用程式的 CLASSPATH 陳述式範例：  
  
`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.4/enu/mssql-jdbc-6.4.0.jre9.jar`  
  
確定 CLASSPATH 陳述式僅包含一個 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，例如 **mssql-jdbc-6.4.0.jre7.jar**、**mssql-jdbc-6.4.0.jre8.jar 或 **mssql-jdbc-6.4.0.jre9.jar**。

### <a name="for-microsoft-jdbc-driver-62"></a>對於 Microsoft JDBC Driver 6.2

**mssql-jdbc-6.2.2.jre7.jar** 或 **mssql-jdbc-6.2.2.jre8.jar** 檔案會安裝在下列位置：

```bash
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.2.2.jre7.jar
  
\<installation directory>\sqljdbc_<version>\<language>\mssql-jdbc-6.2.2.jre8.jar
```

下列程式碼片段是用於 Windows 應用程式的 CLASSPATH 陳述式範例：  
  
`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.2 for SQL Server\sqljdbc_6.2\enu\mssql-jdbc-6.2.2.jre8.jar`  
  
下列程式碼片段是用於 Unix/Linux 應用程式的 CLASSPATH 陳述式範例：  
  
`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_6.2/enu/mssql-jdbc-6.2.2.jre8.jar`  
  
確定 CLASSPATH 陳述式僅包含一個 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，例如 mssql-jdbc-6.2.2.jre7.jar 或 mssql-jdbc-6.2.2.jre8.jar。  

### <a name="for-microsoft-jdbc-driver-41-42-and-60"></a>對於 Microsoft JDBC Driver 4.1、4.2 及 6.0

sqljdbc.jar 檔案、sqljdbc4.jar 檔案、sqljdbc41.jar 或 sqljdbc42.jar 檔案安裝於下列位置：  

```bash
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc.jar  
  
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc4.jar  
  
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc41.jar  
  
\<installation directory>\sqljdbc_<version>\<language>\sqljdbc42.jar  
```

下列程式碼片段是用於 Windows 應用程式的 CLASSPATH 陳述式範例：  
  
`CLASSPATH =.;C:\Program Files\Microsoft JDBC Driver 6.0 for SQL Server\sqljdbc_4.2\enu\sqljdbc42.jar`  
  
下列程式碼片段是用於 Unix/Linux 應用程式的 CLASSPATH 陳述式範例：  

`CLASSPATH =.:/home/usr1/mssqlserverjdbc/Driver/sqljdbc_4.2/enu/sqljdbc42.jar`  
  
請確定 CLASSPATH 陳述式只包含一個 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，例如 sqljdbc.jar、sqljdbc4.jar、sqljdbc41.jar 或 sqljdbc42.jar 的其中一個。  
  
> [!NOTE]  
> 在 Windows 系統上，若目錄名稱超過 8.3 檔案名稱慣例或資料夾名稱具有空格，可能會導致 classpaths 的問題。 如果您認為發生這類問題，則應該將 sqljdbc.jar 檔案、sqljdbc4.jar 檔案或 sqljdbc41.jar 檔案暫時移至像是 `C:\Temp` 的簡單目錄名稱、變更 classpath，並判斷這樣做是否可解決問題。  
  
### <a name="applications-that-are-run-directly-at-the-command-prompt"></a>直接在命令提示字元下執行的應用程式

Classpath 是設定在作業系統中。 請將 sqljdbc.jar、sqljdbc4.jar 或 sqljdbc41.jar 附加至系統的 Classpath。 另外，您也可以在執行應用程式的 Java 命令列上，使用 `java -classpath` 選項來指定 classpath。  
  
### <a name="applications-that-run-in-an-ide"></a>在 IDE 中執行的應用程式  

每一個 IDE 供應商都會提供不同的方法，在其 IDE 中設定 Classpath。 只在作業系統中設定 Classpath 將無法作用。 您必須將 sqljdbc.jar、sqljdbc4.jar 或 sqljdbc41.jar 加入 IDE classpath 中。  
  
### <a name="servlets-and-jsps"></a>Servlet 及 JSP  

Servlet 和 JSP 是在 servlet/JSP 引擎中執行，例如 Tomcat。 Classpath 必須根據 servlet/JSP 引擎文件來設定。 只在作業系統中設定 Classpath 將無法作用。 有些 servlet/JSP 引擎提供設定畫面，您可以用來設定引擎的 Classpath。 在此情況下，您必須將正確的 JDBC 驅動程式 JAR 檔附加到現有的引擎 Classpath 中，並重新啟動引擎。 在其他情況下，您可以在引擎安裝期間，將 sqljdbc.jar、sqljdbc4.jar 或 sqljdbc41.jar 複製到特定目錄 (例如 lib) 來部署該驅動程式。 引擎驅動程式 Classpath 也可以指定在引擎專屬的組態檔中。  
  
### <a name="enterprise-java-beans"></a>Enterprise Java Bean  

Enterprise Java Bean (EJB) 是在 EJB 容器中執行。 EJB 容器的來源是各種供應商。 Java Applet 會在瀏覽器中執行，但是您可以從 Web 伺服器下載。 將 sqljdbc.jar、sqljdbc4.jar 或 sqljdbc41.jar 複製到網頁伺服器的根目錄，並在 applet 的 HTML 封存索引標籤中指定 JAR 檔案的名稱，例如 `<applet ... archive=mssql-jdbc-***.jar>`。  
  
## <a name="making-a-simple-connection-to-a-database"></a>與資料庫建立簡單連接

使用 sqljdbc.jar 類別庫時，應用程式必須先依照下列方式註冊此驅動程式：  
  
`Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");`  

載入驅動程式時，您可以使用連線 URL 和 DriverManager 類別的 getConnection 方法來建立連線：

```java
String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
   "databaseName=AdventureWorks;user=MyUserName;password=*****;";  
Connection con = DriverManager.getConnection(connectionUrl);  
```

從 JDBC API 4.0 起，`DriverManager.getConnection()` 方法已進階成自動載入 JDBC 驅動程式。 因此，使用驅動程式 jar 程式庫時，應用程式不需要呼叫 `Class.forName` 方法來註冊或載入驅動程式。  
  
呼叫 DriverManager 類別的 getConnection 方法時，系統會從已註冊的 JDBC 驅動程式集合中找出適當的驅動程式。 sqljdbc4.jar、sqljdbc41.jar 或 sqljdbc42.jar 檔案會包括 "META-INF/services/java.sql.Driver" 檔案，其中包含 **com.microsoft.sqlserver.jdbc.SQLServerDriver** 作為已註冊的驅動程式。 目前使用 Class.forName 方法來載入驅動程式的現有應用程式將繼續運作而不進行修改。  
  
> [!NOTE]  
> sqljdbc4.jar、sqljdbc41.jar 或 sqljdbc42.jar 類別庫無法搭配舊版的 Java Runtime Environment (JRE) 使用。 如需 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 所支援的 JRE 版本清單，請參閱 [JDBC Driver 的系統需求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  

如需如何使用資料來源來連線以及使用連線 URL 的詳細資訊，請參閱[建置連線 URL](../../connect/jdbc/building-the-connection-url.md) 和[設定連線屬性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
## <a name="see-also"></a>另請參閱  

[JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
