---
title: "步驟 3： 連接到 SQL 使用 Java 的概念證明 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1504a348-1774-47ab-8967-288ec3985ae4
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6bdda6d24e2f1437eb251315d5b91efc7ab1016d
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-java"></a>步驟 3： 連接到 SQL 使用 Java 的概念證明
  
此範例中，應該考量只概念證明。 範例程式碼為了清楚起見，已簡化，並不一定代表由 Microsoft 所建議的最佳作法。  
  
## <a name="step-1--connect"></a>步驟 1： 連接  
  
用於連接到 SQL Database 連接類別。   
  
```java  
  
    // Use the JDBC driver  
    import java.sql.*;  
    import com.microsoft.sqlserver.jdbc.*;  
      
        public class SQLDatabaseConnection {  
      
            // Connect to your database.  
            // Replace server name, username, and password with your credentials  
            public static void main(String[] args) {  
                String connectionString =  
                    "jdbc:sqlserver://yourserver.database.windows.net:1433;"  
                    + "database=AdventureWorks;"  
                    + "user=yourusername@yourserver;"  
                    + "password=yourpassword;"  
                    + "encrypt=true;"  
                    + "trustServerCertificate=false;"  
                    + "hostNameInCertificate=*.database.windows.net;"  
                    + "loginTimeout=30;";  
              
                // Declare the JDBC objects.  
                Connection connection = null;  
                              
                try {  
                    connection = DriverManager.getConnection(connectionString);  
      
                }  
                catch (Exception e) {  
                    e.printStackTrace();  
                }  
                finally {  
                    if (connection != null) try { connection.close(); } catch(Exception e) {}  
                }  
            }  
        }  
```  
  
## <a name="step-2-execute-a-query"></a>步驟 2： 執行查詢  
在此範例中，連接到 Azure SQL Database、 執行 SELECT 陳述式，並傳回選取的資料列。   
  
```java  
    // Use the JDBC driver  
    import java.sql.*;  
    import com.microsoft.sqlserver.jdbc.*;  
      
        public class SQLDatabaseConnection {  
      
            // Connect to your database.  
            // Replace server name, username, and password with your credentials  
            public static void main(String[] args) {  
                String connectionString =  
                    "jdbc:sqlserver://yourserver.database.windows.net:1433;"  
                    + "database=AdventureWorks;"  
                    + "user=yourusername@yourserver;"  
                    + "password=yourpassword;"  
                    + "encrypt=true;"  
                    + "trustServerCertificate=false;"  
                    + "hostNameInCertificate=*.database.windows.net;"  
                    + "loginTimeout=30;";  
              
                // Declare the JDBC objects.  
                Connection connection = null;  
                Statement statement = null;   
                ResultSet resultSet = null;  
                              
                try {  
                    connection = DriverManager.getConnection(connectionString);  
      
                    // Create and execute a SELECT SQL statement.  
                    String selectSql = "SELECT TOP 10 Title, FirstName, LastName from SalesLT.Customer";  
                    statement = connection.createStatement();  
                    resultSet = statement.executeQuery(selectSql);  
      
                    // Print results from select statement  
                    while (resultSet.next())   
                    {  
                        System.out.println(resultSet.getString(2) + " "  
                            + resultSet.getString(3));  
                    }  
                }  
                catch (Exception e) {  
                    e.printStackTrace();  
                }  
                finally {  
                    // Close the connections after the data has been handled.  
                    if (resultSet != null) try { resultSet.close(); } catch(Exception e) {}  
                    if (statement != null) try { statement.close(); } catch(Exception e) {}  
                    if (connection != null) try { connection.close(); } catch(Exception e) {}  
                }  
            }  
        }  
```  
  
## <a name="step-3-insert-a-row"></a>步驟 3： 插入資料列  
在此範例中，執行 INSERT 陳述式，傳遞參數，並擷取自動產生主索引鍵值。   
  
```java  
    // Use the JDBC driver  
    import java.sql.*;  
    import com.microsoft.sqlserver.jdbc.*;  
      
        public class SQLDatabaseConnection {  
      
            // Connect to your database.  
            // Replace server name, username, and password with your credentials  
            public static void main(String[] args) {  
                String connectionString =  
                    "jdbc:sqlserver://yourserver.database.windows.net:1433;"  
                    + "database=AdventureWorks;"  
                    + "user=yourusername@yourserver;"  
                    + "password=yourpassword;"  
                    + "encrypt=true;"  
                    + "trustServerCertificate=false;"  
                    + "hostNameInCertificate=*.database.windows.net;"  
                    + "loginTimeout=30;";  
              
                // Declare the JDBC objects.  
                Connection connection = null;  
                Statement statement = null;   
                ResultSet resultSet = null;  
                PreparedStatement prepsInsertProduct = null;  
                  
                try {  
                    connection = DriverManager.getConnection(connectionString);  
      
                    // Create and execute an INSERT SQL prepared statement.  
                    String insertSql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) VALUES "  
                        + "('NewBike', 'BikeNew', 'Blue', 50, 120, '2016-01-01');";  
      
                    prepsInsertProduct = connection.prepareStatement(  
                        insertSql,  
                        Statement.RETURN_GENERATED_KEYS);  
                    prepsInsertProduct.execute();  
                      
                    // Retrieve the generated key from the insert.  
                    resultSet = prepsInsertProduct.getGeneratedKeys();  
                      
                    // Print the ID of the inserted row.  
                    while (resultSet.next()) {  
                        System.out.println("Generated: " + resultSet.getString(1));  
                    }  
                }  
                catch (Exception e) {  
                    e.printStackTrace();  
                }  
                finally {  
                    // Close the connections after the data has been handled.  
                    if (prepsInsertProduct != null) try { prepsInsertProduct.close(); } catch(Exception e) {}  
                    if (resultSet != null) try { resultSet.close(); } catch(Exception e) {}  
                    if (statement != null) try { statement.close(); } catch(Exception e) {}  
                    if (connection != null) try { connection.close(); } catch(Exception e) {}  
                }  
            }  
        }  
```  
  
## <a name="additional-samples"></a>其他範例  
[範例 JDBC 驅動程式應用程式](../../connect/jdbc/sample-jdbc-driver-applications.md)
