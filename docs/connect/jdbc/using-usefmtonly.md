---
title: 正在透過 useFmtOnly 來抓取 JAVA.sql.parametermetadata |Microsoft Docs
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
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025499"
---
# <a name="retrieving-parametermetadata-via-usefmtonly"></a>透過 useFmtOnly 抓取 JAVA.sql.parametermetadata
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  適用于 SQL Server 的 Microsoft JDBC Driver 包含從伺服器 ( **useFmtOnly**) 查詢參數中繼資料的替代方式。 這項功能最初是在驅動程式7.4 版中引進, 而且必須是解決已知問題`sp_describe_undeclared_parameters`的因應措施。
  
  驅動程式主要使用預存`sp_describe_undeclared_parameters`程式來查詢參數中繼資料, 因為在大部分情況下, 這是針對參數中繼資料抓取的建議方法。 不過, 在下列使用案例中, 執行預存程式目前會失敗:
  
-   針對 Always Encrypted 資料行
  
-   對暫存資料表和資料表變數執行
  
-   針對 views 
  
  這些使用案例的建議解決方案是剖析使用者的參數和資料表目標的 SQL 查詢, 然後使用`SELECT` `FMTONLY` [已啟用] 執行查詢。 下列程式碼片段會協助將功能視覺化。
  
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
 功能**useFmtOnly**預設為關閉。 使用者可以藉由指定`useFmtOnly=true`, 透過連接字串來啟用這項功能。 例如： `jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;useFmtOnly=true;`＞。
 
 或者, 也可以透過`SQLServerDataSource`取得此功能。
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
 
 此功能也適用于語句層級。 使用者可以透過`PreparedStatement.setUseFmtOnly(boolean)`開啟/關閉功能。
> [!NOTE]  
>  驅動程式會優先處理 [連接層級] 屬性上的 [語句層級] 屬性。

## <a name="using-the-feature"></a>使用此功能
  一旦啟用, 驅動程式就會在內部開始使用新功能, `sp_describe_undeclared_parameters`而不是查詢參數中繼資料。 使用者不需要採取任何進一步的動作。
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
>  此功能僅支援`SELECT/INSERT/UPDATE/DELETE`查詢。 查詢的開頭應為4個支援的其中一個關鍵字, 或是一個[通用資料表運算式](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql?view=sql-server-2017), 後面接著其中一個支援的查詢。 不支援通用資料表運算式中的參數。

## <a name="known-issues"></a>已知問題
  目前有些功能問題是 SQL 剖析邏輯中的缺陷所致。 這些問題可能會在後續的功能更新中獲得解決, 並在下方記載其相關的因應措施建議。
  
A. 使用「向前宣告」別名
```sql
CREATE TABLE Foo(c1 int)

DELETE fooAlias FROM Foo fooAlias WHERE c1 > ?; --Invalid object name 'fooAlias'

--Workaround #1: Specify AS keyword
DELETE fooAlias FROM Foo AS fooAlias WHERE c1 > ?;
--Workaround #2: Use the table name
DELETE Foo FROM Foo fooAlias WHERE c1 > ?;
```

B. 當資料表具有共用資料行名稱時, 不明確的資料行名稱
```sql
CREATE TABLE Foo(c1 int, c2 int, c3 int)
CREATE TABLE Bar(c1 int, c2 int, c3 int)

SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar WHERE c1 > ? and c2 < ? and c3 = ?); --Ambiguous Column Name

--Workaround: Use aliases
SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar b WHERE b.c1 = ? and b.c2 = ? and b.c3 = ?);
```

C. 從具有參數的子查詢中選取
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
  
  
