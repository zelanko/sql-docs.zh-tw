---
title: "疏鬆資料行 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7d4237e0-818f-4639-9093-d5ac9683fc71
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e70b83f9c419c6d619ce4e90697e40289f4d9ae4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sparse-columns"></a>疏鬆資料行
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  疏鬆資料行為已最佳化儲存位置來保存 Null 值的一般資料行。 疏鬆資料行會減少 Null 值的空間需求，但要付出擷取非 Null 值的更多成本負擔。 當空間至少節省了百分之 20 到 40 時，請考慮使用疏鬆資料行。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC Driver 3.0 支援疏鬆資料行，當您連接到[!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]（或更新版本） 伺服器。 您可以使用[SQLServerDatabaseMetaData.getColumns](../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md)， [SQLServerDatabaseMetaData.getFunctionColumns](../../connect/jdbc/reference/getfunctioncolumns-method-sqlserverdatabasemetadata.md)，或[SQLServerDatabaseMetaData.getProcedureColumns](../../connect/jdbc/reference/getprocedurecolumns-method-sqlserverdatabasemetadata.md)若要判斷哪個資料行是疏鬆資料行，以及哪些資料行的資料行集資料行。  
  
 資料行集是計算的資料行，可使用不具型別的 XML 形式傳回所有疏鬆資料行。 當資料表中的資料行數目很大或超過 1024，或者在個別疏鬆資料行上操作很麻煩時，您應該考慮使用資料行集。 資料行集最多可以包含 30,000 個資料行。  
  
## <a name="example"></a>範例  
  
### <a name="description"></a>Description  
 此範例示範如何使用偵測資料行集。 它也會示範如何剖析資料行集的 XML 輸出以取得疏鬆資料行中的資料。  
  
 第一個程式碼清單是您應該在伺服器上執行的 Transact-SQL。  
  
 第二個程式碼清單是 Java 原始程式碼。 在編譯應用程式之前，請在連接字串中變更伺服器的名稱。  
  
### <a name="code"></a>程式碼  
  
```  
use AdventureWorks  
CREATE TABLE ColdCalling  
(  
ID int IDENTITY(1,1) PRIMARY KEY,  
[Date] date,  
[Time] time,  
PositiveFirstName nvarchar(50) SPARSE,  
PositiveLastName nvarchar(50) SPARSE,  
SpecialPurposeColumns XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  
);  
GO  
  
INSERT ColdCalling ([Date], [Time])  
VALUES ('10-13-09','07:05:24')  
GO  
  
INSERT ColdCalling ([Date], [Time], PositiveFirstName, PositiveLastName)  
VALUES ('07-20-09','05:00:24', 'AA', 'B')  
GO  
  
INSERT ColdCalling ([Date], [Time], PositiveFirstName, PositiveLastName)  
VALUES ('07-20-09','05:15:00', 'CC', 'DD')  
GO  
```  
  
### <a name="code"></a>程式碼  
  
```  
import java.sql.*;  
  
import javax.xml.parsers.DocumentBuilder;  
import javax.xml.parsers.DocumentBuilderFactory;  
  
import org.xml.sax.InputSource;  
  
import java.io.StringReader;  
  
import org.w3c.dom.Document;  
import org.w3c.dom.Node;  
import org.w3c.dom.NodeList;  
  
public class SparseColumns {  
  
   public static void main(String args[]) {  
      final String connectionUrl = "jdbc:sqlserver://my_server;databaseName=AdventureWorks;integratedSecurity=true;";  
  
      Connection conn = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         conn = DriverManager.getConnection(connectionUrl);  
  
         stmt = conn.createStatement();  
         // Determine the column set column  
         String columnSetColName = null;  
         String strCmd = "SELECT name FROM sys.columns WHERE object_id=(SELECT OBJECT_ID('ColdCalling')) AND is_column_set = 1";  
         rs = stmt.executeQuery(strCmd);  
  
         if (rs.next()) {  
            columnSetColName = rs.getString(1);  
            System.out.println(columnSetColName + " is the column set column!");  
         }  
         rs.close();  
  
         rs = null;   
  
         strCmd = "SELECT * FROM ColdCalling";  
         rs = stmt.executeQuery(strCmd);  
  
         // Iterate through the result set  
         ResultSetMetaData rsmd = rs.getMetaData();  
  
         DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();  
         DocumentBuilder db = dbf.newDocumentBuilder();  
         InputSource is = new InputSource();  
         while (rs.next()) {  
            // Iterate through the columns  
            for (int i = 1; i <= rsmd.getColumnCount(); ++i) {  
               String name = rsmd.getColumnName(i);  
               String value = rs.getString(i);  
  
               // If this is the column set column  
               if (name.equalsIgnoreCase(columnSetColName)) {  
                  System.out.println(name);  
  
                  // Instead of printing the raw XML, parse it  
                  if (value != null) {  
                     // Add artificial root node "sparse" to ensure XML is well formed  
                     String xml = "<sparse>" + value + "</sparse>";  
  
                     is.setCharacterStream(new StringReader(xml));  
                     Document doc = db.parse(is);  
  
                     // Extract the NodeList from the artificial root node that was added  
                     NodeList list = doc.getChildNodes();  
                     // This is the <sparse> node  
                     Node root = list.item(0);   
                     // These are the xml column nodes  
                     NodeList sparseColumnList = root.getChildNodes();   
  
                     // Iterate through the XML document  
                     for (int n = 0; n < sparseColumnList.getLength(); ++n) {  
                        Node sparseColumnNode = sparseColumnList.item(n);  
                        String columnName = sparseColumnNode.getNodeName();  
                        // Note that the column value is not in the sparseColumNode, it is the value of the first child of it  
                        Node sparseColumnValueNode = sparseColumnNode.getFirstChild();  
                        String columnValue = sparseColumnValueNode.getNodeValue();  
  
                        System.out.println("\t" + columnName + "\t: " + columnValue);  
                     }  
                  }  
               } else {   // Just print the name + value of non-sparse columns  
                  System.out.println(name + "\t: " + value);  
               }  
            }  
            System.out.println();//New line between rows  
         }  
      } catch (Exception e) {  
         e.printStackTrace();  
      } finally {  
         if (rs != null) {  
            try {  
               rs.close();  
            } catch (Exception e) {  
               e.printStackTrace();  
            }  
         }  
         if (stmt != null) {  
            try {  
               stmt.close();  
            } catch (Exception e) {  
               e.printStackTrace();  
            }  
         }  
         if (conn != null) {  
            try {  
               conn.close();  
            } catch (Exception e) {  
               e.printStackTrace();  
            }  
         }  
      }  
   }        
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [提升效能和可靠性，JDBC 驅動程式](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  

