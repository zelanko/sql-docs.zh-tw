---
title: 使用連線 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cf8ee392-8a10-40a3-ae32-31c7b1efdd04
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 267605b6a89f323570cfacfc66517b028ef716a2
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025468"
---
# <a name="working-with-a-connection"></a>使用連線

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

下列各節將提供使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 的 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 類別來連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫之不同方法的範例。

> [!NOTE]  
> 如果您使用 JDBC 驅動程式連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時發生問題，請參閱[連線能力疑難排解](../../connect/jdbc/troubleshooting-connectivity.md)，以取得如何更正此問題的建議。

## <a name="creating-a-connection-by-using-the-drivermanager-class"></a>使用 DriverManager 類別建立連線

建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫連線最簡單的方式為載入 JDBC 驅動程式，並呼叫 DriverManager 類別的 getConnection 方法，如下所示：

```java
Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = DriverManager.getConnection(connectionUrl);  
```

此技術將使用驅動程式清單中第一個可用的驅動程式 (可與指定之 URL 順利進行連接)，以建立資料庫連接。

> [!NOTE]  
> 使用 sqljdbc4.jar 類別庫時，應用程式不需要使用 Class.forName 方法來明確註冊或載入此驅動程式。 呼叫 DriverManager 類別的 getConnection 方法時，系統會從已註冊的 JDBC 驅動程式集合中找出適當的驅動程式。 如需詳細資訊，請參閱＜使用 JDBC Driver＞。

## <a name="creating-a-connection-by-using-the-sqlserverdriver-class"></a>使用 SQLServerDriver 類別建立連線

如果您必須在 DriverManager 的驅動程式清單中指定特定的驅動程式，您可使用 [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) 類別的 [connect](../../connect/jdbc/reference/connect-method-sqlserverdriver.md) 方法建立資料庫連線，如下所示：

```java
Driver d = (Driver) Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver").newInstance();  
String connectionUrl = "jdbc:sqlserver://localhost;database=AdventureWorks;integratedSecurity=true;"  
Connection con = d.connect(connectionUrl, new Properties());  
```

## <a name="creating-a-connection-by-using-the-sqlserverdatasource-class"></a>使用 SQLServerDataSource 類別建立連線

如果您必須使用 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 類別建立連線，您可在呼叫 [getConnection](../../connect/jdbc/reference/getconnection-method.md) 方法之前使用該類別的各種 setter 方法，如下所示：

```java
SQLServerDataSource ds = new SQLServerDataSource();  
ds.setUser("MyUserName");  
ds.setPassword("*****");  
ds.setServerName("localhost");  
ds.setPortNumber(1433);
ds.setDatabaseName("AdventureWorks");  
Connection con = ds.getConnection();  
```

## <a name="creating-a-connection-that-targets-a-very-specific-data-source"></a>建立以相當特定的資料來源為目標的連線

如果您必須建立以相當特定的資料來源為目標的資料庫連接，有一些方法可供您採用。 每種方法均視您使用連接 URL 所設定的屬性而定。

若要連接到遠端伺服器的預設執行個體，請使用下列方法：

```java
String url = "jdbc:sqlserver://MyServer;integratedSecurity=true;"
```

若要連接到伺服器上的特定通訊埠，請使用下列方法：

```java
String url = "jdbc:sqlserver://MyServer:1533;integratedSecurity=true;"
```

若要連接到伺服器上的具名執行個體，請使用下列方法：

```java
String url = "jdbc:sqlserver://209.196.43.19;instanceName=INSTANCE1;integratedSecurity=true;"
```

若要連接到伺服器上的特定資料庫，請使用下列方法：

```java
String url = "jdbc:sqlserver://172.31.255.255;database=AdventureWorks;integratedSecurity=true;"
```

如需更多連線 URL 範例，請參閱[建立連線 URL](../../connect/jdbc/building-the-connection-url.md)。

## <a name="creating-a-connection-with-a-custom-login-time-out"></a>建立具有自訂登入逾時的連線

如果您必須調整伺服器負載或網路流量，您可建立具有特定登入逾時值 (以秒計) 的連接，如下所示：

```java
String url = "jdbc:sqlserver://MyServer;loginTimeout=90;integratedSecurity=true;"
```

## <a name="create-a-connection-with-application-level-identity"></a>建立具有應用程式層級身分識別的連線

如果您必須使用記錄及設定檔作業，您將必須識別來自特定應用程式的連接，如下所示：

```java
String url = "jdbc:sqlserver://MyServer;applicationName=MYAPP.EXE;integratedSecurity=true;"
```

## <a name="closing-a-connection"></a>關閉連線

您可呼叫 SQLServerConnection 類別的 [close](../../connect/jdbc/reference/close-method-sqlserverconnection.md) 方法以明確關閉資料庫連線，如下所示：

```java
con.close();
```

如此將釋放出 SQLServerConnection 物件正在使用的資料庫資源，或將連線傳回共用狀況中的連線集區。

> [!NOTE]  
> 呼叫 close 方法也會回復任何暫止交易。

## <a name="see-also"></a>另請參閱

[使用 JDBC 驅動程式連線到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
