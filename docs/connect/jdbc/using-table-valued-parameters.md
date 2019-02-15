---
title: 使用資料表值參數 |Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 57fa8d097b2a6cedc5bf96dc4ee75471c7d27266
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 02/05/2019
ms.locfileid: "55737019"
---
# <a name="using-table-valued-parameters"></a>使用資料表值參數

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

資料表值參數提供從用戶端應用程式，將多個資料列的資料封送至 SQL Sever 的簡便方式，而不需多次來回存取或特殊的伺服器端邏輯才能處理資料。 您可以使用資料表值參數，以一個參數化命令在用戶端應用程式中封裝資料列的資料，並傳送至伺服器。 內送資料列會儲存在資料表變數中，可以再由使用 TRANSACT-SQL。  
  
可以使用標準的 TRANSACT-SQL SELECT 陳述式來存取資料表值參數中的資料行值。 資料表值參數強型別，其結構會自動進行驗證。 資料表值參數的大小只受到伺服器記憶體使用。  
  
> [!NOTE]  
> 使用從 Microsoft JDBC Driver 6.0 for SQL Server 資料表值參數的支援。
>
> 您無法在資料表值參數中傳回資料。 資料表值參數是僅輸入;不支援 OUTPUT 關鍵字。  
  
 如需有關資料表值參數的詳細資訊，請參閱下列資源。  
  
| 資源                                                                                                             | Description                                                                         |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| [資料表值參數 (Database Engine)](https://go.microsoft.com/fwlink/?LinkId=98363)中 SQL Server 線上叢書 | 描述如何建立及使用資料表值參數                             |
| [使用者定義資料表類型](https://go.microsoft.com/fwlink/?LinkId=98364)中 SQL Server 線上叢書                  | 描述用來宣告資料表值參數的使用者定義資料表類型 |
| [Microsoft SQL Server Database Engine](https://go.microsoft.com/fwlink/?LinkId=120507) CodePlex 的區段        | 包含範例，示範如何使用 SQL Server 特性與功能  |
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>在舊版的 SQL Server 中傳遞多個資料列  

SQL Server 2008 導入資料表值參數之前，將多個資料列傳遞至預存程序或參數化的 SQL 命令的選項有所限制。 開發人員可以選擇將多個資料列傳遞至伺服器的下列選項：  
  
- 您可以使用一系列個別的參數來代表多個資料行和資料列中的值。 可以使用此方法中傳遞的資料量會受到允許的參數數目。 SQL Server 程序可以有最多 2100年參數。 伺服器端邏輯，才能將這些值組合成資料表變數或暫存資料表進行處理。  
  
- 包裝成分隔的字串或 XML 文件的多個資料值，然後將這些文字值傳遞至程序或陳述式。 這需要的程序或陳述式來包含邏輯所需的驗證資料結構和包裝的值。  
  
- 建立一系列個別的 SQL 陳述式會影響多個資料列的資料修改。 變更可以個別提交給伺服器，或將它們批次處理成為群組。 不過，即使在包含多個陳述式的批次提交，每個陳述式會分別在伺服器上執行。  
  
- 使用 bcp 公用程式或[SQLServerBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy(v=vs.110).aspx)將多個資料列載入資料表的物件。 雖然這項技術非常有效率，但它不支援伺服器端處理，除非將資料載入暫存資料表或資料表變數。  
  
## <a name="creating-table-valued-parameter-types"></a>建立資料表值參數類型  

資料表值參數以使用 TRANSACT-SQL 來定義的強型別資料表結構為基礎`CREATE TYPE`陳述式。 您必須建立資料表類型，並在 SQL Server 中定義的結構，才能在用戶端應用程式中使用資料表值參數。 如需建立資料表類型的詳細資訊，請參閱[使用者定義資料表類型](https://go.microsoft.com/fwlink/?LinkID=98364)SQL Server 線上叢書 》 中。  

```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```

建立資料表類型之後, 您可以宣告資料表值參數，根據該型別。 下列 TRANSACT-SQL 片段將示範如何宣告資料表值參數在預存程序定義中。 請注意，`READONLY`關鍵字所宣告的資料表值參數。  

```sql
CREATE PROCEDURE usp_UpdateCategories
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```

## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>使用資料表值參數 & Amp;#40;transact-SQL&AMP;#41; 修改資料  

資料表值參數可以用於執行單一陳述式來影響多個資料列的集合為基礎的資料修改。 例如，您可以選取所有資料列中的資料表值參數，並將其插入至資料庫資料表，或您可以建立的 update 陳述式的資料表值參數加入您想要更新的資料表。  
  
下列 TRANSACT-SQL UPDATE 陳述式示範如何使用資料表值參數聯結至 Categories 資料表。 當您使用的資料表值參數使用 FROM 子句中聯結時，您必須也別名，如下所示，其中資料表值參數的別名設定為"ec":  

```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```

此 TRANSACT-SQL 範例會示範如何從單一集合式作業中執行 INSERT 資料表值參數中選取資料列。

```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```

## <a name="limitations-of-table-valued-parameters"></a>資料表值參數的限制

有數個資料表值參數的限制：  
  
- 您無法將資料表值參數傳遞到使用者定義函數。  
  
- 資料表值參數僅支援 UNIQUE 或 PRIMARY KEY 條件約束的建立索引。 SQL Server 不會維護資料表值參數的統計資料。  
  
- 資料表值參數是唯讀的 TRANSACT-SQL 程式碼中。 您無法更新的資料表值參數的資料列的資料行值，也無法插入或刪除資料列。 若要修改傳遞至預存程序或參數化陳述式資料表值參數中的資料，您必須插入資料到暫存資料表或資料表變數。  
  
- 您無法使用 ALTER TABLE 陳述式來修改資料表值參數的設計。

- 您可以串流處理的資料表值參數中的大型物件。  
  
## <a name="configuring-a-table-valued-parameter"></a>設定資料表值參數

從 Microsoft JDBC Driver 6.0 for SQL Server，使用參數化陳述式或參數化的預存程序支援資料表值參數。 資料表值參數可以從 SQLServerDataTable，從結果集填入，或從使用者提供 ISQLServerDataRecord 介面的實作。 設定時已備妥查詢的資料表值參數，您必須指定類型名稱必須符合先前建立的伺服器上的相容型別名稱。  
  
下列兩個程式碼片段示範如何設定的資料表值參數，SQLServerPreparedStatement 和 SQLServerCallableStatement 插入資料。 這裡 sourceTVPObject 可以 SQLServerDataTable、 ResultSet 或 ISQLServerDataRecord 物件。 此範例假設連接是使用中的連接物件。  

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
> 請參見**JDBC 驅動程式的資料表值參數 API**下方的 Api 可讓您設定資料表值參數的完整清單。  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>將資料表值參數傳遞為 SQLServerDataTable 物件  

從 Microsoft JDBC Driver 6.0 for SQL Server，SQLServerDataTable 類別代表關聯式資料的記憶體中資料表。 此範例示範如何建構使用 SQLServerDataTable 物件的記憶體中資料的資料表值參數。 程式碼第一次建立 SQLServerDataTable 物件，定義其結構描述，並使用資料填入資料表。 程式碼接著會設定會將此資料表做為資料表值參數傳遞至 SQL Server SQLServerPreparedStatement。  

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
> 請參見**JDBC 驅動程式的資料表值參數 API**下方的 Api 可讓您設定資料表值參數的完整清單。  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>將資料表值參數傳遞為結果集物件  

此範例示範如何將串流處理結果集的資料表值參數的資料之資料列。 第一次從來源資料表中擷取資料的程式碼建立 SQLServerDataTable 物件，定義其結構描述，並使用資料填入資料表。 程式碼接著會設定會將此資料表做為資料表值參數傳遞至 SQL Server SQLServerPreparedStatement。  

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
> 請參見**JDBC 驅動程式的資料表值參數 API**下方的 Api 可讓您設定資料表值參數的完整清單。  

## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>將資料表值參數傳遞做為 ISQLServerDataRecord 物件  

從 Microsoft JDBC Driver 6.0 for SQL Server，新介面 ISQLServerDataRecord 是適用於串流資料 （取決於如何使用者提供它的實作） 使用的資料表值參數。 下列範例會示範如何實作 ISQLServerDataRecord 介面以及如何將它傳遞做為資料表值參數。 為了簡單起見，下列範例會將硬式編碼值只在一個資料列傳遞至資料表值參數。 在理想情況下，使用者會實作這個介面的資料流的資料列從任何來源，例如從文字檔案。  

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
> 請參見**JDBC 驅動程式的資料表值參數 API**下方的 Api 可讓您設定資料表值參數的完整清單。

## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>資料表值參數 API 的 JDBC 驅動程式

### <a name="sqlservermetadata"></a>SQLServerMetaData

此類別代表資料行的中繼資料。 它用於 ISQLServerDataRecord 介面，以傳遞給資料表值參數的資料行中繼資料。 此類別中的方法包括：  

| [屬性]                                                                                                                                                                             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 公用 SQLServerMetaData 字串 columnName、 int sqlType、 int 有效位數、 int 小數位數、 布林 useServerDefault、 布林 isUniqueKey、 SQLServerSortOrder sortOrder (int sortOrdinal） | 初始化具有指定的資料行名稱、 sql 類型、 有效位數、 小數位數和伺服器預設的 SQLServerMetaData 的新執行個體。 這種形式的建構函式會藉由讓您可以指定資料行是否為資料表值參數、 資料行和排序資料行的序數排序順序中唯一支援資料表值參數。 <br/><br/>useServerDefault-可讓您指定這個資料行是否應該使用預設的伺服器值;預設值為 false。<br>isUniqueKey-表示資料表值參數中的資料行是否是唯一的;預設值為 false。<br>sortOrder-指出資料行的排序次序預設值為 SQLServerSortOrder.Unspecified。<br>sortOrdinal-指定排序資料行序數從 0; sortOrdinal 啟動預設值為-1。 |
| 公用 SQLServerMetaData （columnName 字串、 int sqlType）                                                                                                                        | 初始化 SQLServerMetaData 使用的資料行名稱和 sql 類型的新執行個體。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| 公用 SQLServerMetaData （字串 columnName，int sqlType，int 長度）                                                                                                                        | 初始化 SQLServerMetaData （適用於字串資料） 使用的資料行名稱、 sql 型別和長度的新執行個體。 長度用來區分大型字串與字串長度少於 4000 個字元。 在 JDBC 驅動程式 7.2 版中引進。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| 公用 SQLServerMetaData （字串 columnName、 int sqlType、 int 有效位數、 int 小數位數）                                                                                              | 初始化 SQLServerMetaData 使用的資料行名稱、 sql 類型、 有效位數和小數位數的新執行個體。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Public SQLServerMetaData(SQLServerMetaData sqlServerMetaData)                                                                                                                    | 初始化的新執行個體 SQLServerMetaData 從另一個 SQLServerMetaData 物件。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| public String getColumName()                                                                                                                                                     | 擷取的資料行名稱。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| public int getSqlType()                                                                                                                                                          | 擷取 java sql 型別。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| 公用 int getPrecision()                                                                                                                                                        | 擷取傳遞給資料行類型的有效位數。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getScale()                                                                                                                                                            | 擷取的小數位數傳遞至資料行的類型。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public SQLServerSortOrder getSortOrder()                                                                                                                                         | 擷取的排序次序。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getSortOrdinal()                                                                                                                                                      | 擷取的排序序數。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public boolean isUniqueKey()                                                                                                                                                     | 傳回資料行是否為唯一。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public boolean useServerDefault()                                                                                                                                                | 傳回資料行是否使用預設的伺服器值。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
  
### <a name="sqlserversortorder"></a>SQLServerSortOrder

定義排序次序的列舉。 可能的值為遞增、 遞減和未指定。
  
### <a name="sqlserverdatatable"></a>SQLServerDataTable

此類別代表記憶體中資料表，以搭配資料表值參數。 此類別中的方法包括：  

| [屬性]                                                          | Description                                          |
| ------------------------------------------------------------- | ---------------------------------------------------- |
| Public SQLServerDataTable()                                   | 初始化 SQLServerDataTable 的新執行個體。    |
| public Iterator<Entry\<Integer, Object[]>> getIterator()      | 擷取資料表的資料列的迭代器。 |
| public void addColumnMetadata(String columnName, int sqlType) | 將指定的資料行的中繼資料。              |
| public void addColumnMetadata(SQLServerDataColumn column)     | 將指定的資料行的中繼資料。              |
| public void addRow （物件...的值）                          | 將一個資料列加入至資料表中。              |
| public Map\<Integer, SQLServerDataColumn> getColumnMetadata() | 擷取此資料表的資料行中繼資料。       |
| public void clear()                                           | 清除此資料表。                              |

### <a name="sqlserverdatacolumn"></a>SQLServerDataColumn

此類別代表記憶體中資料表的 SQLServerDataTable 所代表的資料行。 此類別中的方法包括：  

| [屬性]                                                       | Description                                                                      |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------- |
| 公用 SQLServerDataColumn （columnName 字串、 int sqlType） | 初始化具有資料行名稱和類型的 SQLServerDataColumn 的新執行個體。 |
| public String getColumnName()                              | 擷取的資料行名稱。                                                       |
| public int getColumnType()                                 | 擷取的資料行類型。                                                       |

### <a name="isqlserverdatarecord"></a>ISQLServerDataRecord

此類別代表使用者可以實作資料串流到的資料表值參數的介面。 在此介面的方法包括：  
  
| [屬性]                                                    | Description                                                                                             |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData getColumnMetaData(int column); | 擷取指定資料行索引的資料行中繼資料。                                               |
| public int getColumnCount();                            | 擷取資料行的總數。                                                                  |
| public Object[] getRowData();                           | 取得目前資料列的資料當作物件的陣列。                                          |
| public boolean next();                                  | 移至下一個資料列。 如果移動成功，而且沒有下一個資料列，則為 false 的否則，傳回 True。 |

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

已新增下列方法來支援資料表值參數傳遞至此類別。  

| [屬性]                                                                                                    | Description                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 公用最終的 void setStructured （int parameterIndex，字串 tvpName，SQLServerDataTable tvpDataTable）    | 會填入資料表的資料表值參數。 parameterIndex 是參數索引，tvpName 是資料表值參數的名稱，tvpDataTable 是來源資料的資料表物件。                                                                                                          |
| 公用最終的 void setStructured （int parameterIndex，字串 tvpName，結果集 tvpResultSet）             | 從另一個資料表中擷取一個結果集填入的資料表值參數。 parameterIndex 是參數索引，tvpName 是資料表值參數的名稱，tvpResultSet 是來源的結果集物件。                                                                               |
| 公用最終的 void setStructured （int parameterIndex，字串 tvpName，ISQLServerDataRecord tvpDataRecord） | 填入資料表值參數與 ISQLServerDataRecord 物件。 ISQLServerDataRecord 用於串流資料，而且使用者會決定如何使用它。 parameterIndex 是參數索引，tvpName 是資料表值參數的名稱，tvpDataRecord 是 ISQLServerDataRecord 物件。 |
  
### <a name="sqlservercallablestatement"></a>SQLServerCallableStatement

已新增下列方法來支援資料表值參數傳遞至此類別。  
  
| [屬性]                                                                                                        | Description                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 公用最終的 void setStructured （字串 paratemeterName，字串 tvpName，SQLServerDataTable tvpDataTable）    | 填入資料表值參數傳遞至具有資料表的預存程序。 paratemeterName 是參數的名稱，tvpName 是 TVP，型別的名稱，tvpDataTable 是資料的資料表物件。                                                                                                                 |
| 公用最終的 void setStructured （字串 paratemeterName，字串 tvpName，結果集 tvpResultSet）             | 填入資料表值參數傳遞至預存程序中，使用另一個資料表中擷取一個結果集。 paratemeterName 是參數的名稱，tvpName 是 TVP，型別的名稱，tvpResultSet 是來源的結果集物件。                                                                              |
| 公用最終的 void setStructured （字串 paratemeterName，字串 tvpName，ISQLServerDataRecord tvpDataRecord） | 填入資料表值參數傳遞至預存程序與 ISQLServerDataRecord 物件。 ISQLServerDataRecord 用於串流資料，而且使用者會決定如何使用它。 paratemeterName 是參數的名稱，tvpName 是 TVP，型別的名稱，tvpDataRecord 是 ISQLServerDataRecord 物件。 |

## <a name="see-also"></a>另請參閱

[JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
