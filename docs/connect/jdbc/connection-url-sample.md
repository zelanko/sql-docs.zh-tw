---
title: 連接 URL 範例 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 96fabc42-59d1-4cc0-93c5-db00cbe55e95
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a6e49fea6fdc9ed6d7e7497b8217bb0a16dc2c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="connection-url-sample"></a>連接 URL 範例
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  此 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 範例應用程式將示範如何使用連線 URL 來連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 資料庫。 它也示範如何使用 SQL 陳述式，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 資料庫擷取資料。  
  
 此範例的程式碼檔案名稱為 connectURL.java，可以在下列位置找到它：  
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \samples\connections  
  
## <a name="requirements"></a>需求  
 若要執行此範例應用程式，您必須將 Classpath 設定為包含 sqljdbc.jar 檔案或 sqljdbc4.jar 檔案。 如果 Classpath 遺漏 sqljdbc.jar 或 sqljdbc4.jar 的項目，範例應用程式將會擲回「找不到類別」的一般例外狀況。 您也需要擁有 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] 範例資料庫的存取權。 如需如何設定 classpath 的詳細資訊，請參閱[使用 JDBC 驅動程式](../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 提供 sqljdbc.jar 和 sqljdbc4.jar 類別庫檔案，可根據您慣用的 Java Runtime Environment (JRE) 設定使用。 如需選擇哪個 JAR 檔案的詳細資訊，請參閱[JDBC 驅動程式的系統需求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>範例  
 在下列範例中，範例程式碼會在連線 URL 中設定各種連線屬性，然後呼叫 DriverManager 類別的 getConnection 方法，以傳回 [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) 物件。  
  
 接著，範例程式碼會使用 SQLServerConnection 物件的 [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) 方法建立 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 物件，然後呼叫 [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) 方法來執行 SQL 陳述式。  
  
 最後，範例會使用從 executeQuery 方法傳回的 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) 物件，重複執行 SQL 陳述式所傳回的結果。  
  
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
 [連接及擷取資料](../../connect/jdbc/connecting-and-retrieving-data.md)  
  
  
