---
title: 修改結果集資料範例 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b5ae54dc-2a79-4664-bb21-cacdb7d745e1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 52ef5b12771cb7ef65f34dd7d890f19a8541d3ee
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "69028327"
---
# <a name="modifying-result-set-data-sample"></a>修改結果集資料範例

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

此 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 範例應用程式示範如何從 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫擷取可更新的資料集。 然後，使用 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的方法，它會插入、修改，最後刪除資料集中的資料列。

此範例的程式碼檔案名稱為 UpdateResultSet.java，可以在下列位置找到：

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\resultsets
```

## <a name="requirements"></a>需求

若要執行此範例應用程式，您必須將 Classpath 設定為包含 mssql-jdbc jar 檔案。 您也必須存取 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 範例資料庫。 如需如何設定 classpath 的詳細資訊，請參閱[使用 JDBC 驅動程式](../../../connect/jdbc/using-the-jdbc-driver.md)。

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 提供 mssql-jdbc 類別庫檔案，可根據您慣用的 Java Runtime Environment (JRE) 設定來使用。 如需選擇哪個 JAR 檔案的詳細資訊，請參閱 [JDBC 驅動程式的系統需求](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。

## <a name="example"></a>範例

在下列範例中，範例程式碼會建立與 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] 範例資料庫的連線。 然後，將 SQL 陳述式與 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件搭配使用，它會執行 SQL 陳述式，並且將所傳回的資料放入可更新的 SQLServerResultSet 物件中。

接下來，範例程式碼會使用 [moveToInsertRow](../../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md) 方法將結果集資料指標移至插入資料列，並使用一系列的 [updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) 方法將資料插入新資料列，然後呼叫 [insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) 方法將新資料列存回資料庫。

插入新資料列之後，範例程式碼會使用 SQL 陳述式擷取先前插入的資料列，然後使用 updateString 與 [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) 方法的組合來更新資料列，並將它重新存回資料庫。

最後，範例程式碼會擷取先前更新資料列，然後使用 [deleteRow](../../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md) 方法將它從資料庫刪除。

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class UpdateResultSet {

    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl);
                Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);) {

            // Create and execute an SQL statement, retrieving an updateable result set.
            String SQL = "SELECT * FROM HumanResources.Department;";
            ResultSet rs = stmt.executeQuery(SQL);

            // Insert a row of data.
            rs.moveToInsertRow();
            rs.updateString("Name", "Accounting");
            rs.updateString("GroupName", "Executive General and Administration");
            rs.updateString("ModifiedDate", "08/01/2006");
            rs.insertRow();

            // Retrieve the inserted row of data and display it.
            SQL = "SELECT * FROM HumanResources.Department WHERE Name = 'Accounting';";
            rs = stmt.executeQuery(SQL);
            displayRow("ADDED ROW", rs);

            // Update the row of data.
            rs.first();
            rs.updateString("GroupName", "Finance");
            rs.updateRow();

            // Retrieve the updated row of data and display it.
            rs = stmt.executeQuery(SQL);
            displayRow("UPDATED ROW", rs);

            // Delete the row of data.
            rs.first();
            rs.deleteRow();
            System.out.println("ROW DELETED");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static void displayRow(String title,
            ResultSet rs) throws SQLException {
        System.out.println(title);
        while (rs.next()) {
            System.out.println(rs.getString("Name") + " : " + rs.getString("GroupName"));
            System.out.println();
        }
    }
}

```

## <a name="see-also"></a>另請參閱

[使用結果集](../../../connect/jdbc/code-samples/working-with-result-sets.md)
