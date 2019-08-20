---
title: 剖析結果 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: rene-ye
ms.author: v-reye
manager: kenvh
ms.openlocfilehash: 127c97ec155ef1e19df4103b12a6e10b8b67fe74
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027865"
---
# <a name="parsing-the-results"></a>剖析結果

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文說明 SQL Server 希望使用者能夠完整處理從任何查詢傳回的結果。

## <a name="update-counts-and-result-sets"></a>更新計數和結果集

本節將討論從 SQL Server 傳回的兩個最常見的結果: 更新計數和結果集。 一般而言, 使用者執行的任何查詢都會導致傳回其中一個結果。在處理結果時, 使用者應同時處理這兩項。

下列程式碼是使用者可以如何逐一查看伺服器所有結果的範例:
```java
try (Connection connection = DriverManager.getConnection(URL); Statement statement = connection.createStatement()) {
    boolean resultsAvailable = statement.execute(USER_SQL);
    int updateCount = -2;
    while (true) {
        updateCount = statement.getUpdateCount();
        if (!resultsAvailable && updateCount == -1)
            break;
        if (resultsAvailable) {
            // handle ResultSet
        } else {
            // handle Update Count
        }
        resultsAvailable = statement.getMoreResults();
    }
}
```

## <a name="exceptions"></a>例外狀況
當您執行會產生錯誤或參考用訊息的語句時, SQL Server 會根據它是否可以產生執行計畫而有不同的回應。 錯誤訊息可以在語句執行之後立即擲回, 或可能需要個別的結果集。 在後者的情況下, 應用程式需要剖析結果集以取得例外狀況。

當 SQL Server 無法產生執行計畫時, 就會立即擲回例外狀況。

```java
String SQL = "SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    statement.execute(SQL);
} catch (SQLException e) {
    e.printStackTrace();
}
```

當 SQL Server 在結果集中傳回錯誤訊息時, 就必須處理結果集以取得例外狀況。

```java
String SQL = "SELECT 1/0;";
try (Statement statement = connection.createStatement();) {
    boolean hasResult = statement.execute(SQL);
    if (hasResult) {
        try (ResultSet rs = statement.getResultSet()) {
            // Exception is thrown on next().
            while (rs.next()) {}
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

如果語句執行會產生多個結果集, 則必須處理每個結果集, 直到到達具有例外狀況的集合為止。

```java
String SQL = "SELECT 1; SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    // Does not throw an exception on execute().
    boolean hasResult = statement.execute(SQL);
    while (hasResult) {
        try (ResultSet rs = statement.getResultSet()) {
            while (rs.next()) {
                System.out.println(rs.getString(1));
            }
        }
        // Moves the next result set that generates the exception.
        hasResult = statement.getMoreResults();
    }
} catch (SQLException e) {
    e.printStackTrace();
}
```

若是`String SQL = "SELECT * FROM nonexistentTable; SELECT 1;";`, 則會`execute()`立即擲回例外狀況, 而且`SELECT 1`完全不會執行。

如果 SQL Server 的錯誤的嚴重性`0` `9`為, 則會將它視為參考用訊息, 並傳回做`SQLWarning`為。

```java
String SQL = "RAISERROR ('WarningLevel5', 5, 2);";
try (Statement statement = connection.createStatement();) {
    boolean hasResult = statement.execute(SQL);
    SQLWarning warning = statement.getWarnings();
    System.out.println(warning);
}
```

## <a name="see-also"></a>另請參閱

[JDBC 驅動程式概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)
