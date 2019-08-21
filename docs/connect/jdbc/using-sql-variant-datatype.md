---
title: 使用 Sql_variant 資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdede5d41d5ad7fc22cfed3f1efa9f95612032ca
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025845"
---
# <a name="using-sql_variant-data-type"></a>使用 Sql_variant 資料類型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

從版本 6.3.0, JDBC 驅動程式支援 SQL_variant 資料類型。 使用資料表值參數和 BulkCopy 之類的功能時, 也支援 Sql_variant, 此頁面稍後會提到一些限制。 並非所有資料類型都可以儲存在 SQL_variant 資料類型中。 如需支援 SQL_variant 的資料類型清單, 請查看 SQL Server [檔](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql)。

##  <a name="populating-and-retrieving-a-table"></a>填入和抓取資料表:
假設有一個資料表的 SQL_variant 資料行為:

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

使用語句插入值的範例腳本:

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

使用備妥的語句來插入值:

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

如果已知所傳遞資料的基礎類型, 則可以使用個別的 setter。 例如, 插入`preparedStatement.setInt()`整數值時, 可以使用。

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

若要從資料表讀取值, 可以使用個別的 getter。 例如, 如果`getInt()`已知`getString()`來自伺服器的值, 就可以使用或方法:    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sql_variant"></a>搭配 SQL_variant 使用預存程式:   
擁有預存程式, 例如:     

```java
String sql = "CREATE PROCEDURE " + inputProc + " @p0 sql_variant OUTPUT AS SELECT TOP 1 @p0=col1 FROM sampleTable ";
``` 
    
必須註冊輸出參數:

```java
try (CallableStatement callableStatement = con.prepareCall(" {call " + inputProc + " (?) }")) {
    callableStatement.registerOutParameter(1, microsoft.sql.Types.SQL_VARIANT);      
    callableStatement.execute();
}
```

## <a name="limitations-of-sql_variant"></a>Sql_variant 的限制:
- 當您使用 TVP 來填入在 SQL_variant 中`datetime`儲存`smalldatetime` `getDateTime()` / / `date`值的資料表時, 在上呼叫/ `getSmallDateTime()` / `getDate()`ResultSet 無法運作, 而且會擲回下列例外狀況:
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    因應措施`getString()` : `getObject()`請改用或。 
    
- 不支援使用 TVP 來填入資料表, 並在 SQL_variant 中傳送 null 值, 而且會擲回例外狀況:
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>另請參閱

[了解 JDBC 驅動程式資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
