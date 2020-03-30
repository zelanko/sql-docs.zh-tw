---
title: 剖析結果 | Microsoft Docs
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
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027865"
---
# <a name="parsing-the-results"></a>剖析結果

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

此文章說明 SQL Server 希望使用者能夠透過何種方式完整處理從任何查詢傳回的結果。

## <a name="update-counts-and-result-sets"></a>更新計數與結果集

此節將討論從 SQL Server 傳回的兩個最常見結果：更新計數與結果集。 一般而言，使用者執行的任何查詢都會導致傳回其中一個結果；在處理結果時，使用者應同時處理以上兩者。

下列程式碼是示範使用者可如何逐一查看伺服器所有結果的範例：
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
當您執行會產生錯誤或參考用訊息的陳述式時，SQL Server 會根據它是否可以產生執行計畫而以不同的方式回應。 錯誤訊息可以在陳述式執行之後立即擲回，或可能需要個別的結果集。 在後者的情況下，應用程式需要剖析結果集以擷取例外狀況。

當 SQL Server 無法產生執行計畫時，會立即擲回例外狀況。

```java
String SQL = "SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    statement.execute(SQL);
} catch (SQLException e) {
    e.printStackTrace();
}
```

當 SQL Server 在結果集中傳回錯誤訊息時，就必須處理結果集以擷取例外狀況。

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

如果陳述式執行會產生多個結果集，就必須處理每個結果集，直到遇到發生例外狀況的集合為止。

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

在 `String SQL = "SELECT * FROM nonexistentTable; SELECT 1;";` 的情況下，會在 `execute()` 上立即擲回例外狀況，而完全不會執行 `SELECT 1`。

如果 SQL Server 的錯誤分為 `0` 至 `9` 的嚴重性，會將其視為參考用訊息並以 `SQLWarning` 的方式傳回。

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
