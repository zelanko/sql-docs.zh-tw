---
title: 連線 URL 範例 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 96fabc42-59d1-4cc0-93c5-db00cbe55e95
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4a74757846f14b2cee6f8d68cfdec87a02ded4c5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "69028137"
---
# <a name="connection-url-sample"></a>連線 URL 範例

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

此 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 範例應用程式將示範如何使用連線 URL 來連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 它也示範如何使用 SQL 陳述式，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫擷取資料。

此範例的程式碼檔案名稱為 ConnectURL.java，可在下列位置找到：

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\connections
```

## <a name="requirements"></a>需求

若要執行此範例應用程式，您必須將 Classpath 設定為包含 mssql-jdbc jar 檔案。 您也必須存取 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫。 如需如何設定 classpath 的詳細資訊，請參閱[使用 JDBC 驅動程式](../../connect/jdbc/using-the-jdbc-driver.md)。

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供 mssql-jdbc 類別庫檔案，可根據您慣用的 Java Runtime Environment (JRE) 設定來使用。 如需選擇哪個 JAR 檔案的詳細資訊，請參閱 [JDBC Driver 的系統需求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。

## <a name="example"></a>範例

在下列範例中，範例程式碼會在連線 URL 中設定各種連線屬性，然後呼叫 DriverManager 類別的 getConnection 方法，以傳回 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 物件。

接著，範例程式碼會使用 SQLServerConnection 物件的 [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 方法建立 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 物件，然後呼叫 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 方法來執行 SQL 陳述式。

最後，範例會使用從 executeQuery 方法傳回的 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 物件，重複執行 SQL 陳述式所傳回的結果。

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class ConnectURL {
    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement();) {
            String SQL = "SELECT TOP 10 * FROM Person.Contact";
            ResultSet rs = stmt.executeQuery(SQL);

            // Iterate through the data in the result set and display it.
            while (rs.next()) {
                System.out.println(rs.getString("FirstName") + " " + rs.getString("LastName"));
            }
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

## <a name="see-also"></a>另請參閱

[連線及擷取資料](../../connect/jdbc/connecting-and-retrieving-data.md)
