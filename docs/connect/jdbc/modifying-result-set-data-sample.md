---
title: "修改結果集資料範例 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b5ae54dc-2a79-4664-bb21-cacdb7d745e1
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 28d0c574b9666853ee2ed78ae3666a312208e240
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="modifying-result-set-data-sample"></a>修改結果集資料範例
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  這[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]範例應用程式示範如何擷取可更新的資料集[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫。 然後，使用的方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)物件，它會將插入、 修改與最後刪除資料列集中的資料。  
  
 此範例的程式碼檔案名稱為 updateRS.java，可以在下列位置找到它：  
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \samples\resultsets  
  
## <a name="requirements"></a>需求  
 若要執行此範例應用程式，您必須將 Classpath 設定為包含 sqljdbc.jar 檔案或 sqljdbc4.jar 檔案。 如果 Classpath 遺漏 sqljdbc.jar 或 sqljdbc4.jar 的項目，範例應用程式將會擲回「找不到類別」的一般例外狀況。 您也會需要存取[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫。 如需如何設定 classpath 的詳細資訊，請參閱[使用 JDBC 驅動程式](../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供 sqljdbc.jar 和 sqljdbc4.jar 類別庫檔案，可根據您慣用的 Java Runtime Environment (JRE) 設定。 如需選擇哪個 JAR 檔案的詳細資訊，請參閱[JDBC 驅動程式的系統需求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>範例  
 在下列範例中，範例程式碼會連接到[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫。 然後，使用 SQL 陳述式與[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)物件，然後執行 SQL 陳述式，並將它傳回成為可更新的 SQLServerResultSet 物件的資料放。  
  
 接著，範例程式碼會使用[moveToInsertRow](../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md)方法來移動的結果集資料指標來插入資料列中，使用一系列的[updateString](../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)方法，以將資料插入新的資料列，然後再呼叫[insertRow](../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md)方法，將新的回資料庫的資料列。  
  
 插入新的資料列，範例程式碼擷取先前插入的資料列，會使用 SQL 陳述式，然後使用 updateString 的組合和[updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)方法來更新資料的資料列，並將它重新存回資料庫中。  
  
 最後，範例程式碼擷取先前更新的資料列，並再將它刪除從資料庫使用[deleteRow](../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md)方法。  
  
```java
import java.sql.*;  
  
public class updateRS {  
  
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
  
         // Create and execute an SQL statement, retrieving an updateable result set.  
         String SQL = "SELECT * FROM HumanResources.Department;";  
         stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);  
         rs = stmt.executeQuery(SQL);  
  
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
      catch (Exception e) {  
         e.printStackTrace();  
      }  
  
      finally {  
         if (rs != null) try { rs.close(); } catch(Exception e) {}  
         if (stmt != null) try { stmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
      }  
   }  
  
   private static void displayRow(String title, ResultSet rs) {  
      try {  
         System.out.println(title);  
         while (rs.next()) {  
            System.out.println(rs.getString("Name") + " : " + rs.getString("GroupName"));  
            System.out.println();  
         }  
      } catch (Exception e) {  
         e.printStackTrace();  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用結果集](../../connect/jdbc/working-with-result-sets.md)  
  
  

