---
title: 使用資料表值參數 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98863afb5a47eddfd311563bd03a1c7c7120b161
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025711"
---
# <a name="using-table-valued-parameters"></a>使用資料表值參數

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

資料表值參數提供從用戶端應用程式，將多個資料列的資料封送至 SQL Sever 的簡便方式，而不需多次來回存取或特殊的伺服器端邏輯才能處理資料。 您可以使用資料表值參數，以一個參數化命令在用戶端應用程式中封裝資料列的資料，並傳送至伺服器。 傳入的資料列會儲存於資料表變數中，之後可使用 Transact-SQL 進行運算。  
  
資料表值參數中的資料行值可以使用標準的 Transact-sql SELECT 語句來存取。 資料表值參數是強型別, 而且其結構會自動驗證。 資料表值參數的大小只受限於伺服器記憶體。  
  
> [!NOTE]  
> 從 Microsoft JDBC Driver 6.0 for SQL Server 開始提供資料表值參數的支援。
>
> 您無法以資料表值參數傳回資料。 資料表值參數是僅限輸入;不支援 OUTPUT 關鍵字。  
  
 如需有關資料表值參數的詳細資訊, 請參閱下列資源。  
  
| 資源                                                                                                             | 描述                                                                         |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| SQL Server 線上叢書中的[資料表值參數 (資料庫引擎)](https://go.microsoft.com/fwlink/?LinkId=98363) | 描述如何建立及使用資料表值參數                             |
| SQL Server 線上叢書中的[使用者定義資料表類型](https://go.microsoft.com/fwlink/?LinkId=98364)                  | 描述用來宣告資料表值參數的使用者定義資料表類型 |
| CodePlex 的[Microsoft SQL Server 資料庫引擎](https://go.microsoft.com/fwlink/?LinkId=120507)區段        | 包含示範如何使用 SQL Server 特性和功能的範例  |
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>在舊版 SQL Server 中傳遞多個資料列  

在將資料表值參數引進 SQL Server 2008 之前, 將多個資料列傳遞至預存程式或參數化 SQL 命令的選項受到限制。 開發人員可以從下列選項中選擇, 將多個資料列傳遞至伺服器:  
  
- 使用一系列的個別參數來代表多個資料行和資料列中的值。 使用這個方法可以傳遞的資料量受限於允許的參數數目。 SQL Server 程式最多可以有2100個參數。 需要伺服器端邏輯, 才能將這些個別的值組合成資料表變數或臨時表進行處理。  
  
- 將多個資料值組合成分隔字串或 XML 檔, 然後將這些文字值傳遞給程式或語句。 這需要程式或語句包含驗證資料結構和 unbundling 值所需的邏輯。  
  
- 針對會影響多個資料列的資料修改, 建立一系列個別的 SQL 語句。 變更可以個別提交至伺服器, 或批次處理成群組。 不過, 即使是以包含多個語句的批次提交, 每個語句都會在伺服器上個別執行。  
  
- 使用 bcp utility 程式或[SQLServerBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy(v=vs.110).aspx)物件, 將許多資料列載入資料表。 雖然這項技術非常有效率, 但除非將資料載入臨時表或資料表變數中, 否則不支援伺服器端處理。  
  
## <a name="creating-table-valued-parameter-types"></a>建立資料表值參數類型  

資料表值參數是以使用 transact-sql `CREATE TYPE`語句所定義的強型別資料表結構為基礎。 您必須先建立資料表類型並在 SQL Server 中定義結構, 然後才能在用戶端應用程式中使用資料表值參數。 如需建立資料表類型的詳細資訊, 請參閱 SQL Server 線上叢書中的[使用者定義資料表類型](https://go.microsoft.com/fwlink/?LinkID=98364)。  

```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```

建立資料表類型之後, 您可以根據該類型來宣告資料表值參數。 下列 Transact-sql 片段示範如何在預存程序定義中宣告資料表值參數。 請注意, 需要關鍵字來宣告資料表值參數。`READONLY`  

```sql
CREATE PROCEDURE usp_UpdateCategories
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```

## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>使用資料表值參數修改資料 (Transact-SQL)  

資料表值參數可用於以集合為基礎的資料修改 (藉由執行單一語句來影響多個資料列)。 例如, 您可以選取資料表值參數中的所有資料列, 並將它們插入資料庫資料表中, 或者您可以藉由將資料表值參數聯結至您要更新的資料表來建立 update 語句。  
  
下列 Transact-sql UPDATE 語句示範如何藉由將資料表值參數聯結至 category 資料表來使用它們。 當您在 FROM 子句中使用資料表值參數搭配聯結時, 您也必須將它設為別名, 如下所示, 其中資料表值參數的別名為 "ec":  

```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```

此 Transact-sql 範例示範如何從資料表值參數中選取資料列, 以在單一集合式作業中執行插入。

```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```

## <a name="limitations-of-table-valued-parameters"></a>資料表值參數的限制

資料表值參數有幾項限制:  
  
- 您無法將資料表值參數傳遞給使用者定義函數。  
  
- 資料表值參數只能編制索引, 以支援 UNIQUE 或 PRIMARY KEY 條件約束。 SQL Server 不會維護資料表值參數的統計資料。  
  
- 資料表值參數在 Transact-sql 程式碼中是唯讀的。 您無法更新資料表值參數資料列中的資料行值, 也無法插入或刪除資料列。 若要在資料表值參數中修改傳遞至預存程式或參數化語句的資料, 您必須將資料插入臨時表或資料表變數中。  
  
- 您不能使用 ALTER TABLE 語句來修改資料表值參數的設計。

- 您可以在資料表值參數中串流大型物件。  
  
## <a name="configuring-a-table-valued-parameter"></a>設定資料表值參數

從 Microsoft JDBC Driver 6.0 for SQL Server 開始, 使用參數化語句或參數化預存程式即可支援資料表值參數。 資料表值參數可以從 SQLServerDataTable、結果集, 或從使用者提供的 ISQLServerDataRecord 介面實作為填入。 為備妥的查詢設定資料表值參數時, 您必須指定必須符合先前在伺服器上所建立之相容型別的名稱的型別名稱。  
  
下列兩個程式碼片段示範如何使用 SQLServerPreparedStatement 和 SQLServerCallableStatement 來設定資料表值參數, 以插入資料。 這裡的 sourceTVPObject 可以是 SQLServerDataTable, 或 ResultSet 或 ISQLServerDataRecord 物件。 範例假設連接是使用中的連線物件。  

```java
// Using table-valued parameter with a SQLServerPreparedStatement.  
SQLServerPreparedStatement pStmt =
    (SQLServerPreparedStatement) connection.prepareStatement("INSERT INTO dbo.Categories SELECT * FROM ?");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);  
pStmt.execute();  
```

```java
// Using table-valued parameter with a SQLServerCallableStatement.  
SQLServerCallableStatement pStmt =
    (SQLServerCallableStatement) connection.prepareCall("exec usp_InsertCategories ?");
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);;  
pStmt.execute();  
```

> [!NOTE]  
> 如需可用於設定資料表值參數之 Api 的完整清單, 請參閱下列**JDBC 驅動程式的資料表值參數 API**一節。  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>將資料表值參數傳遞為 SQLServerDataTable 物件  

從 Microsoft JDBC Driver 6.0 for SQL Server 開始, SQLServerDataTable 類別代表關聯式資料的記憶體中資料表。 這個範例示範如何使用 SQLServerDataTable 物件, 從記憶體中的資料來建立資料表值參數。 此程式碼會先建立 SQLServerDataTable 物件、定義其架構, 並在資料表中填入資料。 然後, 程式碼會設定 SQLServerPreparedStatement, 以將此資料表當做資料表值參數傳遞給 SQL Server。  

```java
/* Assumes connection is an active Connection object. */

// Create an in-memory data table.  
SQLServerDataTable sourceDataTable = new SQLServerDataTable();
  
// Define metadata for the data table.  
sourceDataTable.addColumnMetadata("CategoryID" ,java.sql.Types.INTEGER);
sourceDataTable.addColumnMetadata("CategoryName" ,java.sql.Types.NVARCHAR);
  
// Populate the data table.  
sourceDataTable.addRow(1, "CategoryNameValue1");
sourceDataTable.addRow(2, "CategoryNameValue2");
  
// Pass the data table as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
            "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceDataTable);  
pStmt.execute();  
```

> [!NOTE]  
> 如需可用於設定資料表值參數之 Api 的完整清單, 請參閱下列**JDBC 驅動程式的資料表值參數 API**一節。  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>以 ResultSet 物件的形式傳遞資料表值參數  

這個範例示範如何將資料列從結果集串流至資料表值參數。 程式碼會先從中的來源資料表抓取資料, 以建立 SQLServerDataTable 物件、定義其架構, 並在資料表中填入資料。 然後, 程式碼會設定 SQLServerPreparedStatement, 以將此資料表當做資料表值參數傳遞給 SQL Server。  

```java
/* Assumes connection is an active Connection object. */

// Create the source ResultSet object. Here SourceCategories is a table defined with the same schema as Categories table.
ResultSet sourceResultSet = connection.createStatement().executeQuery("SELECT * FROM SourceCategories");  

// Pass the source result set as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceResultSet);  
pStmt.execute();  
```

> [!NOTE]  
> 如需可用於設定資料表值參數之 Api 的完整清單, 請參閱下列**JDBC 驅動程式的資料表值參數 API**一節。  

## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>將資料表值參數傳遞為 ISQLServerDataRecord 物件  

從 Microsoft JDBC Driver 6.0 for SQL Server 開始, 有一個新的介面 ISQLServerDataRecord 可供串流資料使用 (視使用者如何為其提供其執行方式而定)。 下列範例示範如何執行 ISQLServerDataRecord 介面, 以及如何將它當做資料表值參數傳遞。 為了簡單起見, 下列範例只會將具有硬式編碼值的一個資料列傳遞至資料表值參數。 在理想的情況下, 使用者會執行此介面來串流任何來源的資料列, 例如, 從文字檔。  

```java
class MyRecords implements ISQLServerDataRecord  
{  
    int currentRow = 0;  
    Object[] row = new Object[2];  
  
    MyRecords(){  
        // Constructor. This implementation has just one row.
        row[0] = new Integer(1);  
        row[1] = "categoryName1";  
    }  
  
    public int getColumnCount(){  
        // Return the total number of columns, for this example it is 2.  
        return 2;  
    }  
  
    public SQLServerMetaData getColumnMetaData(int columnIndex) {  
        // Return the column metadata.  
        if (1 == columnIndex)  
            return new SQLServerMetaData("CategoryID", java.sql.Types.INTEGER);  
        else  
            return new SQLServerMetaData("CategoryName", java.sql.Types.NVARCHAR);  
    }  
  
    public Object[] getRowData(){  
        // Return the columns in the current row as an array of objects. This implementation has just one row.  
        return row;
    }  
  
    public boolean next(){  
        // Move to the next row. This implementation has just one row, after processing the first row, return false.  
        currentRow++;  
        if (1 == currentRow)  
            return true;  
        else  
            return false;  
    }
}

// Following code demonstrates how to pass MyRecords object as a table-valued parameter.  
MyRecords sourceRecords = new MyRecords();  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceRecords);  
pStmt.execute();  
```

> [!NOTE]  
> 如需可用於設定資料表值參數之 Api 的完整清單, 請參閱下列**JDBC 驅動程式的資料表值參數 API**一節。

## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>JDBC 驅動程式的資料表值參數 API

### <a name="sqlservermetadata"></a>SQLServerMetaData

此類別代表資料行的中繼資料。 它會在 ISQLServerDataRecord 介面中用來將資料行中繼資料傳遞至資料表值參數。 此類別中的方法包括:  

| 名稱                                                                                                                                                                             | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData (字串 columnName, int sqlType, int precision, int scale, boolean useServerDefault, boolean isUniqueKey, SQLServerSortOrder sortOrder, int sortOrdinal) | 使用指定的資料行名稱、sql 類型、有效位數、小數位數和伺服器預設值, 初始化 SQLServerMetaData 的新實例。 這種形式的此格式器可讓您指定資料行在資料表值參數中是否為唯一、資料行的排序次序, 以及排序資料行的序數, 藉此支援資料表值參數。 <br/><br/>useServerDefault-指定這個資料行是否應該使用預設的伺服器值。預設值為 false。<br>isUniqueKey-指出資料表值參數中的資料行是否為唯一的;預設值為 false。<br>sortOrder-指出資料行的排序次序;預設值為 SQLServerSortOrder。未指定。<br>sortOrdinal-指定排序資料行的序數;sortOrdinal 從0開始;預設值為-1。 |
| public SQLServerMetaData (字串 columnName, int sqlType)                                                                                                                        | 使用資料行名稱和 sql 類型, 初始化 SQLServerMetaData 的新實例。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| public SQLServerMetaData (字串 columnName, int sqlType, int length)                                                                                                                        | 使用資料行名稱、sql 類型和長度 (針對字串資料), 初始化 SQLServerMetaData 的新實例。 長度是用來區別長度小於4000個字元之字串的大型字串。 在 JDBC driver 7.2 版中引進。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public SQLServerMetaData (字串 columnName, int sqlType, int precision, int scale)                                                                                              | 使用資料行名稱、sql 類型、有效位數和小數位數, 初始化 SQLServerMetaData 的新實例。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Public SQLServerMetaData(SQLServerMetaData sqlServerMetaData)                                                                                                                    | 從另一個 SQLServerMetaData 物件, 初始化 SQLServerMetaData 的新實例。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| public String getColumName()                                                                                                                                                     | 抓取資料行名稱。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| public int getSqlType()                                                                                                                                                          | 抓取 java sql 型別。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| public int getPrecision ()                                                                                                                                                        | 抓取傳遞至資料行之類型的有效位數。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getScale()                                                                                                                                                            | 抓取傳遞至資料行之類型的小數值。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public SQLServerSortOrder getSortOrder()                                                                                                                                         | 抓取排序次序。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getSortOrdinal()                                                                                                                                                      | 抓取排序序數。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public boolean isUniqueKey()                                                                                                                                                     | 傳回資料行是否為唯一的。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public boolean useServerDefault()                                                                                                                                                | 傳回資料行是否使用預設的伺服器值。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
  
### <a name="sqlserversortorder"></a>SQLServerSortOrder

定義排序次序的列舉。 可能的值為遞增、遞減和未指定。
  
### <a name="sqlserverdatatable"></a>SQLServerDataTable

此類別代表要搭配資料表值參數使用的記憶體中資料表。 此類別中的方法包括:  

| 名稱                                                          | 描述                                          |
| ------------------------------------------------------------- | ---------------------------------------------------- |
| Public SQLServerDataTable()                                   | 初始化 SQLServerDataTable 的新實例。    |
| public Iterator<Entry\<Integer, Object[]>> getIterator()      | 在資料表的資料列上抓取反覆運算器。 |
| public void addColumnMetadata(String columnName, int sqlType) | 加入指定資料行的中繼資料。              |
| public void addColumnMetadata(SQLServerDataColumn column)     | 加入指定資料行的中繼資料。              |
| public void addRow (Object .。。閾值                          | 將一個資料列加入至資料表。              |
| public Map\<Integer, SQLServerDataColumn> getColumnMetadata() | 抓取此資料表的資料行中繼資料。       |
| public void clear()                                           | 清除此資料表。                              |

### <a name="sqlserverdatacolumn"></a>SQLServerDataColumn

此類別代表 SQLServerDataTable 所表示之記憶體中資料表的資料行。 此類別中的方法包括:  

| 名稱                                                       | 描述                                                                      |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------- |
| public SQLServerDataColumn (字串 columnName, int sqlType) | 使用資料行名稱和類型, 初始化 SQLServerDataColumn 的新實例。 |
| public String getColumnName()                              | 抓取資料行名稱。                                                       |
| public int getColumnType()                                 | 抓取資料行類型。                                                       |

### <a name="isqlserverdatarecord"></a>ISQLServerDataRecord

此類別代表使用者可以執行來將資料串流至資料表值參數的介面。 此介面中的方法包括:  
  
| 名稱                                                    | 描述                                                                                             |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData getColumnMetaData(int column); | 抓取指定之資料行索引的資料行中繼資料。                                               |
| public int getColumnCount();                            | 抓取資料行總數。                                                                  |
| public Object[] getRowData();                           | 取得目前資料列的資料當作物件的陣列。                                          |
| public boolean next();                                  | 移至下一個資料列。 如果移動成功且有下一個資料列, 則傳回 True, 否則傳回 false。 |

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

下列方法已加入至這個類別, 以支援傳遞資料表值參數。  

| 名稱                                                                                                    | 描述                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public final void setStructured (int parameterIndex, String tvpName, SQLServerDataTable tvpDataTable)    | 使用資料表填入資料表值參數。 parameterIndex 是參數索引, tvpName 是資料表值參數的名稱, 而 tvpDataTable 是來源資料表物件。                                                                                                          |
| public final void setStructured (int parameterIndex, String tvpName, ResultSet tvpResultSet)             | 使用從另一個資料表抓取的結果集填入資料表值參數。 parameterIndex 是參數索引, tvpName 是資料表值參數的名稱, 而 tvpResultSet 是來源結果集物件。                                                                               |
| public final void setStructured (int parameterIndex, String tvpName, ISQLServerDataRecord tvpDataRecord) | 以 ISQLServerDataRecord 物件填入資料表值參數。 ISQLServerDataRecord 用於串流資料, 而使用者決定如何使用它。 parameterIndex 是參數索引, tvpName 是資料表值參數的名稱, 而 tvpDataRecord 是 ISQLServerDataRecord 物件。 |
  
### <a name="sqlservercallablestatement"></a>SQLServerCallableStatement

下列方法已加入至這個類別, 以支援傳遞資料表值參數。  
  
| 名稱                                                                                                        | 描述                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public final void setStructured (String paratemeterName, String tvpName, SQLServerDataTable tvpDataTable)    | 使用資料表填入傳遞至預存程式的資料表值參數。 paratemeterName 是參數的名稱, tvpName 是 TVP 類型的名稱, 而 tvpDataTable 是資料表物件。                                                                                                                 |
| public final void setStructured (字串 paratemeterName, 字串 tvpName, ResultSet tvpResultSet)             | 使用從另一個資料表抓取的結果集, 填入傳遞給預存程式的資料表值參數。 paratemeterName 是參數的名稱, tvpName 是 TVP 類型的名稱, 而 tvpResultSet 是來源結果集物件。                                                                              |
| public final void setStructured (String paratemeterName, String tvpName, ISQLServerDataRecord tvpDataRecord) | 使用 ISQLServerDataRecord 物件, 填入傳遞至預存程式的資料表值參數。 ISQLServerDataRecord 用於串流資料, 而使用者決定如何使用它。 paratemeterName 是參數的名稱, tvpName 是 TVP 類型的名稱, 而 tvpDataRecord 是 ISQLServerDataRecord 物件。 |

## <a name="see-also"></a>另請參閱

[JDBC 驅動程式概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
