---
title: "連接 URL 範例 |Microsoft 文件"
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
ms.assetid: 96fabc42-59d1-4cc0-93c5-db00cbe55e95
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9bbb062925c0c0ee1c14c0f2190101c8967d0c65
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="connection-url-sample"></a>連接 URL 範例
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  這[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]範例應用程式示範如何連接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]使用連接 URL 的資料庫。 它也會示範如何從資料擷取[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]資料庫使用的 SQL 陳述式。  
  
 此範例的程式碼檔案名稱為 connectURL.java，可以在下列位置找到它：  
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \samples\connections  
  
## <a name="requirements"></a>需求  
 若要執行此範例應用程式，您必須將 Classpath 設定為包含 sqljdbc.jar 檔案或 sqljdbc4.jar 檔案。 如果 Classpath 遺漏 sqljdbc.jar 或 sqljdbc4.jar 的項目，範例應用程式將會擲回「找不到類別」的一般例外狀況。 您也會需要存取[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)]範例資料庫。 如需如何設定 classpath 的詳細資訊，請參閱[使用 JDBC 驅動程式](../../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]提供 sqljdbc.jar 和 sqljdbc4.jar 類別庫檔案，可根據您慣用的 Java Runtime Environment (JRE) 設定。 如需選擇哪個 JAR 檔案的詳細資訊，請參閱[JDBC 驅動程式的系統需求](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>範例  
 在下列範例中，範例程式碼在連接 URL 中，設定各種連接屬性，然後呼叫 getConnection 方法，要傳回之 DriverManager 類別[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)物件。  
  
 接著，範例程式碼會使用[createStatement](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)建立物件的 SQLServerConnection 方法[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)物件，然後[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)方法呼叫以執行 SQL 陳述式。  
  
 最後，此範例會使用[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) executeQuery 方法來逐一查看的 SQL 陳述式所傳回的結果所傳回物件。  
  
```java  
import java.sql.*;  
  
public class connectURL {  
  
   public static void main(String[] args) {  
  
      // Create a variable for the connection string.  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;" +  
         "databaseName=AdventureWorks;user=UserName;password=*****";  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         // Establish the connection.  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
  
         // Create and execute an SQL statement that returns some data.  
         String SQL = "SELECT TOP 10 * FROM Person.Contact";  
         stmt = con.createStatement();  
         rs = stmt.executeQuery(SQL);  
  
         // Iterate through the data in the result set and display it.  
         while (rs.next()) {  
            System.out.println(rs.getString(4) + " " + rs.getString(6));  
         }  
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
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [連接及擷取資料](../../../connect/jdbc/connecting-and-retrieving-data.md)  
  
  

