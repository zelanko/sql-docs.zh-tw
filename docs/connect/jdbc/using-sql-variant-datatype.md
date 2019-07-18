---
title: 使用 Sql_variant 資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c004bc40ed0c85b82612be9069e1a53041c8095c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66798593"
---
# <a name="using-sqlvariant-data-type"></a>使用 Sql_variant 資料類型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

從 6.3.0 版開始，JDBC 驅動程式支援 sql_variant 資料類型。 使用資料表值參數和大量複製之類的功能，但有一些限制稍後提及此頁面時，也支援 Sql_variant。 並非所有的資料類型可以儲存在 sql_variant 資料類型。 如需支援的與 sql_variant 資料類型的清單，請檢查 SQL Server [Docs](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql)。

##  <a name="populating-and-retrieving-a-table"></a>填入並擷取資料表：
假設一項具有 sql_variant 資料行的資料表：

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

範例指令碼來插入 using 陳述式的值：

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

插入的值使用準備陳述式：

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

如果已知傳入之資料的基礎類型，就可以使用個別的 setter。 比方說，`preparedStatement.setInt()`插入的整數值時，可以使用。

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

從資料表讀取值，可以使用個別的 getter。 例如，`getInt()`或`getString()`如果已知來自伺服器的值，就可以使用方法：    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sqlvariant"></a>搭配 sql_variant 使用預存程序：   
如需預存程序：     

```java
String sql = "CREATE PROCEDURE " + inputProc + " @p0 sql_variant OUTPUT AS SELECT TOP 1 @p0=col1 FROM sampleTable ";
``` 
    
必須註冊輸出參數：

```java
try (CallableStatement callableStatement = con.prepareCall(" {call " + inputProc + " (?) }")) {
    callableStatement.registerOutParameter(1, microsoft.sql.Types.SQL_VARIANT);      
    callableStatement.execute();
}
```

## <a name="limitations-of-sqlvariant"></a>Sql_variant 的限制：
- 當您使用 TVP 填入資料表時`datetime` / `smalldatetime` / `date` sql_variant，在儲存值呼叫`getDateTime()` / `getSmallDateTime()` / `getDate()`上結果集無法運作，而且會擲回下列例外狀況：
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    因應措施： 使用`getString()`或`getObject()`改。 
    
- 使用 TVP 填入資料表，並傳送 sql_variant 的 null 值不支援，而且會擲回例外狀況：
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>另請參閱

[了解 JDBC Driver 資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
