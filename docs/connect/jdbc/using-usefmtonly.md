---
title: 透過 useFmtOnly 擷取 ParameterMetaData | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: ''
author: rene-ye
ms.author: v-reye
manager: kenvh
ms.openlocfilehash: 6877a6421622ab52a92b89502c68f47c4c315d93
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "69025499"
---
# <a name="retrieving-parametermetadata-via-usefmtonly"></a>透過 useFmtOnly 擷取 ParameterMetaData
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Microsoft JDBC Driver for SQL Server 包含從伺服器查詢參數中繼資料的另一種方式：**useFmtOnly**。 此功能最初是在驅動程式 7.4 版中所引進，而且需要用來作為 `sp_describe_undeclared_parameters` 中已知問題的因應措施。
  
  驅動程式主要使用預存程序 `sp_describe_undeclared_parameters` 來查詢參數中繼資料，因為在大多數情況下，這是用於擷取參數中繼資料的建議方法。 不過，在下列使用案例中，執行預存程序目前會失敗：
  
-   對 Always Encrypted 資料行執行
  
-   對暫存資料表和資料表變數執行
  
-   對檢視執行 
  
  這些使用案例的建議解決方案是針對參數和資料表目標剖析使用者的 SQL 查詢，然後執行已啟用 `SELECT` 的 `FMTONLY` 查詢。 下列程式碼片段有助於將功能視覺化。
  
```sql
--create a normal table 'Foo' and a temporary table 'Bar'
CREATE TABLE Foo(c1 int);
CREATE TABLE #Bar(c1 int);

EXEC sp_describe_undeclared_parameters N'SELECT * FROM Foo WHERE c1 = @p0' --works fine
EXEC sp_describe_undeclared_parameters N'SELECT * FROM #Bar WHERE c1 = @p0' --fails with "Invalid object name '#Bar'"

SET FMTONLY ON;
SELECT c1 FROM Foo; --works
SET FMTONLY OFF;
SET FMTONLY ON;
SELECT c1 FROM #Bar; --works
SET FMTONLY OFF;
```
 
## <a name="turning-the-feature-onoff"></a>開啟/關閉功能 
 **useFmtOnly** 功能預設為關閉。 使用者可以藉由指定 `useFmtOnly=true`，透過連接字串啟用此功能。 例如： `jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;useFmtOnly=true;` 。
 
 或者，也可以透過 `SQLServerDataSource` 取得此功能。
 ```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName(<server>);
ds.setPortNumber(<port>);
ds.setDatabaseName("<databaseName>");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setUseFmtOnly(true);
try (Connection c = ds.getConnection()) {
    // do work with connection
}
 ```
 
 此功能也適用於陳述式層級。 使用者可以透過 `PreparedStatement.setUseFmtOnly(boolean)` 開啟/關閉此功能。
> [!NOTE]  
>  驅動程式會優先處理連線層級屬性上的陳述式層級屬性。

## <a name="using-the-feature"></a>使用此功能
  一旦啟用之後，驅動程式就會在查詢參數中繼資料時，於內部開始使用此新功能，而不使用 `sp_describe_undeclared_parameters`。 使用者不需採取任何進一步的動作。
```java
final String sql = "INSERT INTO #Bar VALUES (?)";
try (Connection c = DriverManager.getConnection(URL, USERNAME, PASSWORD)) {
    try (Statement s = c.createStatement()) {
        s.execute("CREATE TABLE #Bar(c1 int)");
    }
    try (PreparedStatement p1 = c.prepareStatement(sql); PreparedStatement p2 = c.prepareStatement(sql)) {
        ((SQLServerPreparedStatement) p1).setUseFmtOnly(true);
        ParameterMetaData pmd1 = p1.getParameterMetaData();
        System.out.println(pmd1.getParameterTypeName(1)); // prints int
        ParameterMetaData pmd2 = p2.getParameterMetaData(); // throws exception, Invalid object name '#Bar'
    }
}
```
> [!NOTE]  
>  此功能僅支援 `SELECT/INSERT/UPDATE/DELETE` 查詢。 查詢的開頭應為 4 個支援的關鍵字之一或一個[通用資料表運算式](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql?view=sql-server-2017)，後面接著其中一個支援的查詢。 不支援在通用資料表運算式內使用參數。

## <a name="known-issues"></a>已知問題
  目前有些功能問題是 SQL 剖析邏輯中的缺陷所致。 這些問題可能會在未來對此功能的更新中獲得解決，並在下方記載其相關的因應措施建議。
  
A. 使用「向前宣告」別名
```sql
CREATE TABLE Foo(c1 int)

DELETE fooAlias FROM Foo fooAlias WHERE c1 > ?; --Invalid object name 'fooAlias'

--Workaround #1: Specify AS keyword
DELETE fooAlias FROM Foo AS fooAlias WHERE c1 > ?;
--Workaround #2: Use the table name
DELETE Foo FROM Foo fooAlias WHERE c1 > ?;
```

B. 當資料表具有共用資料行名稱時，不明確的資料行名稱
```sql
CREATE TABLE Foo(c1 int, c2 int, c3 int)
CREATE TABLE Bar(c1 int, c2 int, c3 int)

SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar WHERE c1 > ? and c2 < ? and c3 = ?); --Ambiguous Column Name

--Workaround: Use aliases
SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar b WHERE b.c1 = ? and b.c2 = ? and b.c3 = ?);
```

C. 來自具有參數之子查詢的 SELECT
```sql

CREATE TABLE Foo(c1 int)

SELECT * FROM (SELECT * FROM Foo WHERE c1 = ?) WHERE c1 = ?; --Incorrect syntax near '?'

--Workaround: N/A
```

D. SET 子句中的子查詢
```sql
CREATE TABLE Foo(c1 int)

UPDATE Foo SET c1 = (SELECT c1 FROM Foo) WHERE c1 = ?; --Incorrect syntax near ')'

--Workaround: Add a 'delimiting' condition
UPDATE Foo SET c1 = (SELECT c1 FROM Foo HAVING (HASH JOIN)) WHERE c1 = ?;
```

## <a name="see-also"></a>另請參閱  
 [設定連接屬性](../../connect/jdbc/setting-the-connection-properties.md)  
  
  
