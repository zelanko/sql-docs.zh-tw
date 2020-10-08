---
description: 使用 Sql_variant 資料類型
title: 使用 Sql_variant 資料類型 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 198c8a21fcea9a1386effe8d30c8d954180d6dc5
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727481"
---
# <a name="using-sql_variant-data-type"></a>使用 Sql_variant 資料類型

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

從 6.3.0 版開始，JDBC 驅動程式支援 sql_variant 資料類型。 在使用資料表值參數和大量複製等功能的情況下，也支援 sql_variant，但有些限制 (將在本頁面稍後詳述)。 並非所有資料類型都可以儲存在 sql_variant 資料類型中。 如需 sql_variant 支援的資料類型清單，請查看 SQL Server [文件](../../t-sql/data-types/sql-variant-transact-sql.md)。

##  <a name="populating-and-retrieving-a-table"></a>填入及擷取資料表：
假設有一個資料表，其中有一個 sql_variant 資料行如下：

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

使用陳述式插入值的範例指令碼：

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

使用備妥的陳述式插入值：

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

如果要傳遞之資料的底層類型為已知，便可以使用相對應 setter。 例如，可以在插入整數值時使用 `preparedStatement.setInt()`。

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

若要從資料表讀取值，可以使用相對應的 getter。 例如，如果來自伺服器的值為已知，便可以使用 `getInt()` 或 `getString()` 方法：    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sql_variant"></a>搭配 sql_variant 使用預存程序：   
具有如下的預存程序：     

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

## <a name="limitations-of-sql_variant"></a>sql_variant 的限制：
- 使用 TVP 來搭配儲存在 sql_variant 中的 `datetime`/`smalldatetime`/`date` 值填入資料表時，在 ResultSet 上呼叫 `getDateTime()`/`getSmallDateTime()`/`getDate()` 並不會運作，且會擲回下列例外狀況：
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    因應措施：改為使用 `getString()` 或 `getObject()`。 
    
- 不支援使用 TVP 來填入資料表並在 sql_variant 中傳送 null 值，且會擲回例外狀況：
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>另請參閱

[了解 JDBC 驅動程式資料類型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)