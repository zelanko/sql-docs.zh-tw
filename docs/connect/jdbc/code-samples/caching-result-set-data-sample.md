---
title: "快取結果集資料範例 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 13a95ebb-996c-4713-a1bd-5834fe22a334
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 29ef11c103d357bf9d73555b6d41f1a4125e6aa9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="caching-result-set-data-sample"></a>快取結果集資料範例
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  這[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]範例應用程式示範如何從資料庫擷取大型資料集，然後控制會在用戶端快取使用的資料列數目[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md)方法[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件。  
  
> [!NOTE]  
>  限制在用戶端上快取的列數不同於限制結果集可以包含的總列數。 若要控制結果集中所包含的資料列總數，請使用[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)方法[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件，都繼承[SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)和[SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)物件。  
  
 若要設定的用戶端上快取的資料列數目的限制，您必須先使用伺服器端資料指標建立時的其中一個陳述式物件特別地陳述要建立陳述式物件時使用的資料指標類型。 例如，JDBC 驅動程式提供 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY 資料指標類型，也就是僅向前快轉，唯讀的伺服器端資料指標搭配[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫。  
  
> [!NOTE]  
>  除了使用 SQL Server 特定資料指標類型，另一種方法是使用 selectMethod 連接字串屬性，並將其值設為 "cursor"。 如需有關 JDBC 驅動程式所支援的資料指標類型的詳細資訊，請參閱[了解資料指標類型](../../../connect/jdbc/understanding-cursor-types.md)。  
  
 您已執行的陳述式物件中包含的查詢，並傳回的資料是用戶端結果集之後，您可以呼叫 setFetchSize 方法，來控制多少資料從資料庫擷取一次。 例如，如果有一個資料表包含 100 列資料，但您將提取大小設為 10，則任何時間點只會在用戶端上快取 10 列資料。 雖然這會減慢資料的處理速度，但是它具有在用戶端上使用更少記憶體的優點，當您需要處理大量資料時，此優點特別有用。  
  
 此範例的程式碼檔案名稱為 cacheRS.java，可以在下列位置找到它：  
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \samples\resultsets  
  
## <a name="requirements"></a>需求  
 若要執行此範例應用程式，您必須將 Classpath 設定為包含 sqljdbc.jar 檔案或 sqljdbc4.jar 檔案。 如果 Classpath 遺漏 sqljdbc.jar 或 sqljdbc4.jar 的項目，範例應用程式將會擲回「找不到類別」的一般例外狀況。 您也會需要存取[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]範例資料庫。 如需如何設定 classpath 的詳細資訊，請參閱[使用 JDBC 驅動程式](../../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]提供 sqljdbc.jar 和 sqljdbc4.jar 類別庫檔案，可根據您慣用的 Java Runtime Environment (JRE) 設定。 如需選擇哪個 JAR 檔案的詳細資訊，請參閱[JDBC 驅動程式的系統需求](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>範例  
 在下列範例中，範例程式碼會連接到[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]範例資料庫。 然後它會使用 SQL 陳述式與[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件，指定伺服器端資料指標類型，然後執行 SQL 陳述式並將放入 SQLServerResultSet 物件傳回的資料。  
  
 接著，範例程式碼呼叫自訂 timerTest 方法，傳遞引數的提取大小使用和結果集。 TimerTest 方法之結果集所使用的 setFetchSize 方法的提取大小、 設定開始時間的測試，然後再逐一查看結果集，`While`迴圈。 只要`While`迴圈一結束，程式碼設定停止時間，測試，然後顯示結果，包括提取大小、 處理、 資料列數目的測試並執行測試所花的時間。  
  
```java
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.SQLServerResultSet;  
  
public class cacheRS {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
            "databaseName=AdventureWorks;integratedSecurity=true;";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
  
         // Create and execute an SQL statement that returns a large  
         // set of data and then display it.  
         String SQL = "SELECT * FROM Sales.SalesOrderDetail;";  
         stmt = con.createStatement(SQLServerResultSet.TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, +  
               SQLServerResultSet.CONCUR_READ_ONLY);  
  
         // Perform a fetch for every row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(1, rs);  
         rs.close();  
  
         // Perform a fetch for every tenth row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(10, rs);  
         rs.close();  
  
         // Perform a fetch for every 100th row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(100, rs);  
         rs.close();  
  
         // Perform a fetch for every 1000th row in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(1000, rs);  
         rs.close();  
  
         // Perform a fetch for every 128th row (the default) in the result set.  
         rs = stmt.executeQuery(SQL);  
         timerTest(0, rs);  
         rs.close();  
      }  
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
  
      finally {  
         if (rs != null) try { rs.close(); } catch(Exception e) {}  
         if (stmt != null) try { stmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
      }  
   }  
  
   private static void timerTest(int fetchSize, ResultSet rs) {  
      try {  
  
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
  
      } catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用結果集](../../../connect/jdbc/working-with-result-sets.md)  
  
  

