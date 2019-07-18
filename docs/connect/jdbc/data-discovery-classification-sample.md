---
title: SQL 資料探索與分類 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ae1ea54ae5f980c84e83922ffcfb9ad6ac83ded9
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782056"
---
# <a name="sql-data-discovery-and-classification"></a>SQL 資料探索與分類

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

這[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]範例應用程式示範如何使用結果集 getter 方法來擷取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]「 SQL 資料探索與分類資訊 」 保留這類資訊的資料表。
  
此範例的程式碼檔名為 DataDiscoveryAndClassification.java，並可以在下列位置找到它：  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\dataclassification  
```

## <a name="requirements"></a>需求  

若要執行此範例應用程式，您必須將 Classpath 設定為包含 mssql-jdbc jar 檔案。 您也必須存取 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫。 如需如何設定 classpath 的詳細資訊，請參閱[使用 JDBC 驅動程式](../../connect/jdbc/using-the-jdbc-driver.md)。

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerResultSet;
import com.microsoft.sqlserver.jdbc.dataclassification.SensitivityProperty;


public class DataDiscoveryAndClassification {

    private static boolean featureSupported = false;

    public static void main(String[] args) {

        // Provides table name to be used for running test.
        String tableName = "JDBC_SQL_DATA_DISCOVERY_CLASSIFICATION";

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;username=<user>;password=<password>;";

        // Establish the connection.
        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement()) {
            verifySupportability(stmt);
            if (featureSupported) {
                createTable(stmt, tableName);
                runTests(stmt, tableName);
                drop_table(stmt, tableName);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * Verifies if SQL Discovery and Classification feature is applicable on target server.
     * 
     * @param stmt
     *        Statement object to work with
     */
    private static void verifySupportability(Statement stmt) {
        try {
            stmt.execute("SELECT * FROM SYS.SENSITIVITY_CLASSIFICATIONS");
            featureSupported = true;
        } catch (SQLException e) {
            // Error Code 208 : Object Not Found
            if (e.getErrorCode() == 208) {
                featureSupported = false;
                System.err.println("This feature is not supported on the target SQL Server.");
            }
        }
    }

    /**
     * Creates table for the test and sets tags for Sensitivity Classification
     * 
     * @param stmt
     *        Statement to work with
     * @param tableName
     *        Table to be created
     * @throws SQLException
     *         If an exception occurs
     */
    private static void createTable(Statement stmt, String tableName) throws SQLException {
        // Creates table for storing Supplier data
        stmt.execute("CREATE TABLE " + tableName + " (" + "[Id] [int] IDENTITY(1,1) NOT NULL,"
                + "[CompanyName] [nvarchar](40) NOT NULL," + "[ContactName] [nvarchar](50) NULL,"
                + "[ContactTitle] [nvarchar](40) NULL," + "[City] [nvarchar](40) NULL,"
                + "[Country] [nvarchar](40) NULL," + "[Phone] [nvarchar](30) MASKED WITH (FUNCTION = 'default()') NULL,"
                + "[Fax] [nvarchar](30) MASKED WITH (FUNCTION = 'default()') NULL," + "CONSTRAINT [PK_" + tableName
                + "] PRIMARY KEY CLUSTERED" + "([Id] ASC "
                + ")WITH (STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF) ON [PRIMARY]" + ") ON [PRIMARY]");

        // Set Sensitivity Classification tags to table columns
        stmt.execute("ADD SENSITIVITY CLASSIFICATION TO " + tableName
                + ".CompanyName WITH (LABEL='PII', LABEL_ID='L1', INFORMATION_TYPE='Company name', INFORMATION_TYPE_ID='COMPANY')");
        stmt.execute("ADD SENSITIVITY CLASSIFICATION TO " + tableName
                + ".ContactName WITH (LABEL='PII', LABEL_ID='L1', INFORMATION_TYPE='Person name', INFORMATION_TYPE_ID='NAME')");
        stmt.execute("ADD SENSITIVITY CLASSIFICATION TO " + tableName
                + ".Phone WITH (LABEL='PII', LABEL_ID='L1', INFORMATION_TYPE='Contact Information', INFORMATION_TYPE_ID='CONTACT')");
        stmt.execute("ADD SENSITIVITY CLASSIFICATION TO " + tableName
                + ".Fax WITH (LABEL='PII', LABEL_ID='L1', INFORMATION_TYPE='Contact Information', INFORMATION_TYPE_ID='CONTACT')");
    }

    /**
     * Runs query to fetch ResultSet from target table
     * 
     * @param stmt
     *        Statement to work with
     * @param tableName
     *        Name of table to fetch results from
     * @throws SQLException
     *         If an exception occurs
     */
    private static void runTests(Statement stmt, String tableName) throws SQLException {
        String query = "SELECT * FROM " + tableName;
        try (SQLServerResultSet rs = (SQLServerResultSet) stmt.executeQuery(query)) {
            printSensitivityClassification(rs);
        }
    }

    /**
     * Prints Sensitivity Classification data as received in ResultSet
     * 
     * @param rs
     *        Active ResultSet to read data from
     * @throws SQLException
     *         If an exception occurs
     */
    private static void printSensitivityClassification(SQLServerResultSet rs) throws SQLException {
        if (null != rs.getSensitivityClassification()) {
            for (int columnPos = 0; columnPos < rs.getSensitivityClassification().getColumnSensitivities().size();
                    columnPos++) {
                for (SensitivityProperty sp : rs.getSensitivityClassification().getColumnSensitivities().get(columnPos)
                        .getSensitivityProperties()) {
                    if (sp.getLabel() != null) {
                        System.out.println("Labels received for Column : " + columnPos);
                        System.out.println("Label ID: " + sp.getLabel().getId());
                        System.out.println("Label Name: " + sp.getLabel().getName());
                        System.out.println();
                    }

                    if (sp.getInformationType() != null) {
                        System.out.println("Information Types received for Column : " + columnPos);
                        System.out.println("Information Type ID: " + sp.getInformationType().getId());
                        System.out.println("Information Type Name: " + sp.getInformationType().getName());
                        System.out.println();
                    }
                }
            }
        }
    }

    /**
     * Drops the table created for test
     * 
     * @param stmt
     *        Statement to work with
     * @param tableName
     *        Table Name to be used
     * @throws SQLException
     *         If an exception occurs
     */
    private static void drop_table(Statement stmt, String tableName) throws SQLException {
        stmt.execute("DROP TABLE " + tableName);
    }
}
```

## <a name="see-also"></a>另請參閱

[範例 JDBC 驅動程式應用程式](../../connect/jdbc/sample-jdbc-driver-applications.md)  
