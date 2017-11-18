---
title: "包裝函式和介面 |Microsoft 文件"
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
ms.assetid: 27fc9b72-9f21-4728-abcb-5c015f28a6ab
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7de6c4bb3e3bb28fefb5eba0fa52a5de8684fa6d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="wrappers-and-interfaces"></a>包裝函式與介面
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支援的介面可讓您建立的 proxy 類別，而包裝函式，可讓您存取特有的 JDBC API 延伸模組[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]透過 proxy 介面。  
  
## <a name="wrappers"></a>包裝函式  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支援 java.sql.Wrapper 介面。 這個介面會提供一個機制來存取延伸模組特有的 JDBC api[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]透過 proxy 介面。  
  
 Java.sql.Wrapper 介面會定義兩種方法： **isWrapperFor**和**unwrap**。 **IsWrapperFor**方法會檢查指定的輸入的物件是否實作這個介面。 **Unwrap**方法會傳回實作這個介面可允許存取的物件[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]特有的方法。  
  
 **isWrapperFor**和**unwrap**方法會公開，如下所示：  
  
-   [isWrapperFor 方法 &#40;SQLServerCallableStatement &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)  
  
-   [unwrap 方法 &#40;SQLServerCallableStatement &#41;](../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)  
  
-   [isWrapperFor 方法 &#40;SQLServerConnectionPoolDataSource &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)  
  
-   [unwrap 方法 &#40;SQLServerConnectionPoolDataSource &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)  
  
-   [isWrapperFor 方法 &#40;SQLServerDataSource &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)  
  
-   [unwrap 方法 &#40;SQLServerDataSource &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)  
  
-   [isWrapperFor 方法 &#40;SQLServerPreparedStatement &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)  
  
-   [unwrap 方法 &#40;SQLServerPreparedStatement &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)  
  
-   [isWrapperFor 方法 &#40;SQLServerStatement &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)  
  
-   [unwrap 方法 &#40;SQLServerStatement &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)  
  
-   [isWrapperFor 方法 &#40;SQLServerXADataSource &#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)  
  
-   [unwrap 方法 &#40;SQLServerXADataSource &#41;](../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)  
  
## <a name="interfaces"></a>介面  
 從開始[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]JDBC Driver 3.0 中，介面可供應用程式伺服器存取相關類別的驅動程式專屬方法。 應用程式伺服器可以藉由建立 proxy、 公開來包裝類別[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]-介面中的特定功能。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支援具有介面[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]特有方法與常數，讓應用程式伺服器可以建立類別的 proxy。  
  
 這些介面衍生自標準的 Java 介面，因此您可以使用相同的物件之後解除包裝以存取驅動程式專屬功能或一般,[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]功能。  
  
 加入以下介面：  
  
-   [ISQLServerCallableStatement](../../connect/jdbc/reference/isqlservercallablestatement-interface.md)  
  
-   [ISQLServerConnection](../../connect/jdbc/reference/isqlserverconnection-interface.md)  
  
-   [ISQLServerDataSource](../../connect/jdbc/reference/isqlserverdatasource-interface.md)  
  
-   [ISQLServerPreparedStatement](../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
-   [ISQLServerResultSet](../../connect/jdbc/reference/isqlserverresultset-interface.md)  
  
-   [ISQLServerStatement](../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="example"></a>範例  
  
### <a name="description"></a>Description  
 這個範例會示範如何存取[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]-從資料來源物件的特定函式。 這個資料來源類別可能已經由應用程式伺服器包裝。 若要存取 JDBC 驅動程式專屬函數或常數，您可以解除包裝資料來源以 ISQLServerDataSource 介面，並使用這個介面中宣告的函式。  
  
### <a name="code"></a>程式碼  
  
```  
import javax.sql.*;  
import java.sql.*;  
import com.microsoft.sqlserver.jdbc.*;  
  
public class UnWrapTest {  
   public static void main(String[] args) {  
      // This is a test.  This DataSource object could be something from an appserver   
      // which has wrapped the real SQLServerDataSource with its own wrapper  
      SQLServerDataSource ds = new SQLServerDataSource();  
      checkSendStringParametersAsUnicode(ds);  
   }  
  
   // Unwrap to the ISQLServerDataSource interface to access the getSendStringParametersAsUnicode function  
   static void checkSendStringParametersAsUnicode(DataSource ds) {  
      try {  
         final ISQLServerDataSource sqlServerDataSource = ds.unwrap(ISQLServerDataSource.class);  
         boolean sendStringParametersAsUnicode = sqlServerDataSource.getSendStringParametersAsUnicode();  
  
         System.out.println("Send string as parameter value is:-" + sendStringParametersAsUnicode);  
  
      } catch (SQLException sqlE) {  
         System.out.println("Exception:-" + sqlE);  
      }  
   }  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [了解 JDBC Driver 資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  

