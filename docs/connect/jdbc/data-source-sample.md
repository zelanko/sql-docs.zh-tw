---
title: 資料來源範例 |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b4a933ee-f2c6-4e0d-a96d-6dd061abf759
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9b5da0ee2138296a4b0c7bf12e6e33a06d029cd
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786251"
---
# <a name="data-source-sample"></a>資料來源範例

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

此 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 範例應用程式示範如何使用資料來源物件來連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 它也示範如何使用預存程序，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫擷取資料。

此範例的程式碼檔案名稱為 ConnectDataSource.java，可以在下列位置找到：

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\connections
```

## <a name="requirements"></a>需求

若要執行此範例應用程式，您必須將 Classpath 設定為包含 mssql-jdbc jar 檔案。 您也必須存取 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫。 如需如何設定 classpath 的詳細資訊，請參閱[使用 JDBC 驅動程式](../../connect/jdbc/using-the-jdbc-driver.md)。

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供 mssql-jdbc 類別庫檔案，可根據您慣用的 Java Runtime Environment (JRE) 設定來使用。 如需有關選擇哪個 JAR 檔案的詳細資訊，請參閱[JDBC 驅動程式的系統需求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。

## <a name="example"></a>範例

在下列範例中，範例程式碼會使用 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 物件的 setter 方法來設定各種連線屬性，然後呼叫 SQLServerDataSource 物件的 [getConnection](../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md) 方法傳回 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 物件。

接下來，範例程式碼會使用 SQLServerConnection 物件的 [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) 方法建立 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 物件，然後呼叫 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md) 方法來執行預存程序。

最後，範例會使用從 executeQuery 方法傳回的 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 物件，逐一查看預存程序所傳回的結果。

```java
import java.sql.CallableStatement;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;

import com.microsoft.sqlserver.jdbc.SQLServerDataSource;

public class ConnectDataSource {

    public static void main(String[] args) {

        // Create datasource.
        SQLServerDataSource ds = new SQLServerDataSource();
        ds.setUser("<user>");
        ds.setPassword("<password>");
        ds.setServerName("<server>");
        ds.setPortNumber(<port>);
        ds.setDatabaseName("AdventureWorks");

        try (Connection con = ds.getConnection();
                CallableStatement cstmt = con.prepareCall("{call dbo.uspGetEmployeeManagers(?)}");) {
            // Execute a stored procedure that returns some data.
            cstmt.setInt(1, 50);
            ResultSet rs = cstmt.executeQuery();

            // Iterate through the data in the result set and display it.
            while (rs.next()) {
                System.out.println("EMPLOYEE: " + rs.getString("LastName") + ", " + rs.getString("FirstName"));
                System.out.println("MANAGER: " + rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));
                System.out.println();
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

[連接及擷取資料](../../connect/jdbc/connecting-and-retrieving-data.md)
