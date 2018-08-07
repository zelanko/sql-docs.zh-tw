---
title: 包裝函式和介面 |Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 27fc9b72-9f21-4728-abcb-5c015f28a6ab
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58276b03877423afe86f9c68841656b00ce0a8c6
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/02/2018
ms.locfileid: "39457782"
---
# <a name="wrappers-and-interfaces"></a>包裝函式與介面

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支援的介面可讓您建立類別的 Proxy，而所支援的包裝函式則可讓您透過 Proxy 介面存取 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 特定的 JDBC API 延伸模組。

## <a name="wrappers"></a>包裝函式

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支援 java.sql.Wrapper 介面。 這個介面會提供一項機制，可讓您透過 Proxy 介面存取 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 特定的 JDBC API 延伸模組。

Java.sql.Wrapper 介面會定義兩個方法： **isWrapperFor**並**unwrap**。 **isWrapperFor** 方法會檢查指定的輸入物件是否實作這個介面。 **unwrap** 方法會傳回實作這個介面的物件，以便允許存取 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 特定的方法。

**isWrapperFor**並**unwrap**方法會公開，如下所示：

- [isWrapperFor 方法 &#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md)

- [unwrap 方法 &#40;SQLServerCallableStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)

- [isWrapperFor 方法 &#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)

- [unwrap 方法 &#40;SQLServerConnectionPoolDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)

- [isWrapperFor 方法 &#40;SQLServerDataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)

- [unwrap 方法&#40;SQLServerDataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)

- [isWrapperFor 方法 &#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)

- [unwrap 方法 &#40;SQLServerPreparedStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)

- [isWrapperFor 方法 &#40;SQLServerStatement&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)

- [unwrap 方法&#40;SQLServerStatement&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)

- [isWrapperFor 方法 &#40;SQLServerXADataSource&#41;](../../connect/jdbc/reference/iswrapperfor-method-sqlserverxadatasource.md)

- [unwrap 方法&#40;SQLServerXADataSource&#41;](../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)

## <a name="interfaces"></a>介面

從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC Driver 3.0 開始，介面可供應用程式伺服器存取相關聯類別中的驅動程式特定方法。 應用程式伺服器可以透過建立 Proxy、公開介面中 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 特定的功能來包裝類別。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 支援擁有 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 特定方法與常數的介面，讓應用程式伺服器可以建立類別的 Proxy。

這些介面衍生自標準的 Java 介面，讓您在物件解除包裝之後，可以使用相同的物件存取驅動程式特定的功能或一般 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 功能。

加入以下介面：

- [ISQLServerCallableStatement](../../connect/jdbc/reference/isqlservercallablestatement-interface.md)

- [ISQLServerConnection](../../connect/jdbc/reference/isqlserverconnection-interface.md)

- [ISQLServerDataSource](../../connect/jdbc/reference/isqlserverdatasource-interface.md)

- [ISQLServerPreparedStatement](../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)

- [ISQLServerResultSet](../../connect/jdbc/reference/isqlserverresultset-interface.md)

- [ISQLServerStatement](../../connect/jdbc/reference/isqlserverstatement-interface.md)

## <a name="example"></a>範例

### <a name="description"></a>Description

此範例示範如何從 DataSource 物件存取 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 特定的函式。 此 DataSource 類別可能已經由應用程式伺服器包裝。 若要存取 JDBC 驅動程式特定函式或常數，您可以解除包裝資料來源成為 SQLServerDataSource 介面，然後使用此介面中宣告的函式。

### <a name="code"></a>程式碼

```java
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
