---
title: 快取結果集資料範例 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 13a95ebb-996c-4713-a1bd-5834fe22a334
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f59c7010875824b65d6b7d12129056f02537e908
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "69028426"
---
# <a name="caching-result-set-data-sample"></a>快取結果集資料範例

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

此 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 範例應用程式示範如何從資料庫擷取大型資料集，然後使用 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 物件的 [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) 方法控制用戶端上快取的資料列數。

> [!NOTE]  
> 限制在用戶端上快取的列數不同於限制結果集可以包含的總列數。 若要控制結果集中包含的總資料列數，請使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 物件的 [setMaxRows](../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) 方法，[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 物件兩者也繼承此方法。

若要對用戶端上快取的資料列數設定限制，您必須先在建立其中一個 Statement 物件時使用伺服器端資料指標，方法為特別陳述要在建立 Statement 物件時使用的資料指標類型。 例如，JDBC 驅動程式提供 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY 資料指標類型，這是與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫搭配使用之快速順向且唯讀的伺服器端資料指標。

> [!NOTE]  
> 除了使用 SQL Server 特定資料指標類型，另一種方法是使用 selectMethod 連接字串屬性，並將其值設為 "cursor"。 如需 JDBC 驅動程式支援之資料指標類型的詳細資訊，請參閱[了解資料指標類型](../../connect/jdbc/understanding-cursor-types.md)。

在執行 Statement 物件中包含的查詢並將資料傳回給用戶端作為結果集之後，您可以呼叫 setFetchSize 方法，控制一次可從資料庫擷取多少資料。 例如，如果有一個資料表包含 100 列資料，但您將提取大小設為 10，則任何時間點只會在用戶端上快取 10 列資料。 雖然這會減慢資料的處理速度，但是它具有在用戶端上使用更少記憶體的優點，當您需要處理大量資料時，此優點特別有用。

此範例的程式碼檔案名稱為 CacheResultSet.java，並位於下列位置：

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\resultsets
```

## <a name="requirements"></a>需求

若要執行此範例應用程式，您必須將 Classpath 設定為包含 mssql-jdbc jar 檔案。 您也需要擁有 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫的存取權。 如需如何設定 classpath 的詳細資訊，請參閱[使用 JDBC 驅動程式](../../connect/jdbc/using-the-jdbc-driver.md)。

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供 mssql-jdbc 類別庫檔案，可根據您慣用的 Java Runtime Environment (JRE) 設定來使用。 如需選擇哪個 JAR 檔案的詳細資訊，請參閱 [JDBC Driver 的系統需求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。

## <a name="example"></a>範例

在下列範例中，範例程式碼會建立與 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫的連線。 然後，它會將 SQL 陳述式與 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 物件搭配使用、指定伺服器端資料指標類型，然後執行 SQL 陳述式，並且將所傳回的資料放入 SQLServerResultSet 物件中。

接下來，範例程式碼會呼叫自訂 timerTest 方法，將要使用的提取大小及結果集當成引數來傳遞。 timerTest 方法接著會使用 setFetchSize 方法設定結果集的提取大小，並設定測試的開始時間，然後使用 `While` 迴圈逐一查看結果集。 `While` 迴圈一結束，程式碼就會設定測試的停止時間，然後顯示測試的結果，包括提取大小、已處理的資料列數，以及執行測試所花的時間。

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;

import com.microsoft.sqlserver.jdbc.SQLServerResultSet;

public class CacheResultSet {

    @SuppressWarnings("serial")
    public static void main(String[] args) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl);
                Statement stmt = con.createStatement(SQLServerResultSet.TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, SQLServerResultSet.CONCUR_READ_ONLY);) {

            String SQL = "SELECT * FROM Sales.SalesOrderDetail;";

            for (int n : new ArrayList<Integer>() {
                {
                    add(1);
                    add(10);
                    add(100);
                    add(1000);
                    add(0);
                }
            }) {
                // Perform a fetch for every nth row in the result set.
                try (ResultSet rs = stmt.executeQuery(SQL)) {
                    timerTest(n, rs);
                }
            }
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static void timerTest(int fetchSize,
            ResultSet rs) throws SQLException {

        // Declare the variables for tracking the row count and elapsed time.
        int rowCount = 0;
        long startTime = 0;
        long stopTime = 0;
        long runTime = 0;

        // Set the fetch size then iterate through the result set to
        // cache the data locally.
        rs.setFetchSize(fetchSize);
        startTime = System.currentTimeMillis();
        while (rs.next()) {
            rowCount++;
        }
        stopTime = System.currentTimeMillis();
        runTime = stopTime - startTime;

        // Display the results of the timer test.
        System.out.println("FETCH SIZE: " + rs.getFetchSize());
        System.out.println("ROWS PROCESSED: " + rowCount);
        System.out.println("TIME TO EXECUTE: " + runTime);
        System.out.println();
    }
}

```

## <a name="see-also"></a>另請參閱

[使用結果集](../../connect/jdbc/working-with-result-sets.md)
