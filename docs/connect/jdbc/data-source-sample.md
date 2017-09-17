---
title: "資料來源範例 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b4a933ee-f2c6-4e0d-a96d-6dd061abf759
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4c72d8ce8c6ed87687cb9db69c52e20aebe9e15f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="data-source-sample"></a>資料來源範例
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  這[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]範例應用程式示範如何連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]資料庫使用資料來源物件。 它也會示範如何從資料擷取[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]使用預存程序的資料庫。  
  
 此範例的程式碼檔案名稱為 connectDS.java，可以在下列位置找到它：  
  
 \<*安裝目錄*> \sqljdbc_\<*版本*>\\<*語言*> \samples\connections  
  
## <a name="requirements"></a>需求  
 若要執行此範例應用程式，您必須將 Classpath 設定為包含 sqljdbc.jar 檔案或 sqljdbc4.jar 檔案。 如果 Classpath 遺漏 sqljdbc.jar 或 sqljdbc4.jar 的項目，範例應用程式將會擲回「找不到類別」的一般例外狀況。 您也會需要存取[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]範例資料庫。 如需如何設定 classpath 的詳細資訊，請參閱[使用 JDBC 驅動程式](../../connect/jdbc/using-the-jdbc-driver.md)。  
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]提供 sqljdbc.jar 和 sqljdbc4.jar 類別庫檔案，可根據您慣用的 Java Runtime Environment (JRE) 設定。 如需選擇哪個 JAR 檔案的詳細資訊，請參閱[JDBC 驅動程式的系統需求](../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)。  
  
## <a name="example"></a>範例  
 在下列範例中，範例程式碼會設定各種連接屬性所使用的 setter 方法[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)物件，然後呼叫[getConnection](../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)方法要傳回的 SQLServerDataSource 物件[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md)物件。  
  
 接著，範例程式碼會使用[prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)建立物件的 SQLServerConnection 方法[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)物件，然後[executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)方法會呼叫來執行預存程序。  
  
 最後，此範例會使用[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) executeQuery 方法來逐一查看預存程序所傳回的結果所傳回物件。  
  
```java
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  
  
public class connectDS {  
  
   public static void main(String[] args) {  
  
      // Declare the JDBC objects.  
      Connection con = null;  
      CallableStatement cstmt = null;  
      ResultSet rs = null;  
  
      try {  
         // Establish the connection.   
         SQLServerDataSource ds = new SQLServerDataSource();  
         ds.setUser("UserName");  
         ds.setPassword("*****");  
         ds.setServerName("localhost");  
         ds.setPortNumber(1433);   
         ds.setDatabaseName("AdventureWorks");  
         con = ds.getConnection();  
  
         // Execute a stored procedure that returns some data.  
         cstmt = con.prepareCall("{call dbo.uspGetEmployeeManagers(?)}");  
         cstmt.setInt(1, 50);  
         rs = cstmt.executeQuery();  
  
         // Iterate through the data in the result set and display it.  
         while (rs.next()) {  
            System.out.println("EMPLOYEE: " + rs.getString("LastName") +   
               ", " + rs.getString("FirstName"));  
            System.out.println("MANAGER: " + rs.getString("ManagerLastName") +   
               ", " + rs.getString("ManagerFirstName"));  
            System.out.println();  
         }  
      }  
  
      // Handle any errors that may have occurred.  
      catch (Exception e) {  
         e.printStackTrace();  
      }  
      finally {  
         if (rs != null) try { rs.close(); } catch(Exception e) {}  
         if (cstmt != null) try { cstmt.close(); } catch(Exception e) {}  
         if (con != null) try { con.close(); } catch(Exception e) {}  
         System.exit(1);  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [連接及擷取資料](../../connect/jdbc/connecting-and-retrieving-data.md)  
  
  
