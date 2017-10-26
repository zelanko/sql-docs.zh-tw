---
title: "使用資料表值參數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 91777796843557cf6c5e6f7667994d7743b608a0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="using-table-valued-parameters"></a>使用資料表值參數
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  資料表值參數會提供簡單的方法，而不需多次來回存取或特殊的伺服器端邏輯來處理資料，從 SQL Server 用戶端應用程式資料的多個資料列封送處理。 您可以使用資料表值參數，是爲用戶端應用程式中的資料列，並將資料傳送至單一參數化命令中的伺服器。 可以再由使用 TRANSACT-SQL 資料表變數中儲存內送資料列。  
  
 可以使用標準的 TRANSACT-SQL SELECT 陳述式來存取資料表值參數中的資料行值。 資料表值參數強型別，其結構會自動進行驗證。 資料表值參數的大小只受到伺服器記憶體使用。  
  
> [!NOTE]  
>  使用開始使用 Microsoft JDBC Driver 6.0 for SQL Server 資料表值參數的支援。  
  
> [!NOTE]  
>  您無法在資料表值參數中傳回資料。 資料表值參數是只能接受輸入;不支援 OUTPUT 關鍵字。  
  
 如需有關資料表值參數的詳細資訊，請參閱下列資源。  
  
|資源|Description|  
|--------------|-----------------|  
|[資料表值參數 (Database Engine)](http://go.microsoft.com/fwlink/?LinkId=98363) SQL Server 線上叢書中|描述如何建立及使用資料表值參數|  
|[使用者定義資料表類型](http://go.microsoft.com/fwlink/?LinkId=98364)SQL Server 線上叢書中|描述用來宣告資料表值參數的使用者定義資料表類型|  
|[Microsoft SQL Server Database Engine](http://go.microsoft.com/fwlink/?LinkId=120507) CodePlex 區段|包含的範例會示範如何使用 SQL Server 特性與功能|  
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>在舊版的 SQL Server 中傳遞多個資料列  
 資料表值參數所導入至 SQL Server 2008 之前，將多個資料列傳遞至預存程序或參數化的 SQL 命令的選項有限制。 開發人員可以選擇下列選項，將多個資料列傳遞至伺服器：  
  
-   您可以使用一系列的個別參數來代表多個資料行和資料列中的值。 可以使用此方法來傳遞的資料數量會受限於允許的參數數目。 SQL Server 程序可以有，最多 2100年參數。 伺服器端邏輯，才能將這些值組合成資料表變數或暫存資料表進行處理。  
  
-   多個資料值包裝成分隔的字串或 XML 文件，然後將這些文字值傳遞至程序或陳述式。 這需要程序或陳述式包含驗證的資料結構和包裝所需的邏輯值。  
  
-   建立一系列個別的 SQL 陳述式會影響多個資料列的資料修改。 變更可以個別提交給伺服器，或它們批次處理成為群組。 不過，即使在包含多個陳述式的批次中提交，每個陳述式會分別在伺服器上執行。  
  
-   使用 bcp 公用程式或[SQLServerBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy(v=vs.110).aspx)来載入資料表中的許多資料列的物件。 雖然這項技術非常有效率，但是它不支援伺服器端處理，除非將資料載入暫存資料表或資料表變數。  
  
## <a name="creating-table-valued-parameter-types"></a>建立資料表值參數的型別  
 資料表值參數根據使用 TRANSACT-SQL CREATE TYPE 陳述式所定義的強型別資料表結構。 您必須建立資料表類型和 SQL Server 中定義的結構，才能在用戶端應用程式中使用資料表值參數。 如需有關建立資料表類型的詳細資訊，請參閱[使用者定義資料表類型](http://go.microsoft.com/fwlink/?LinkID=98364)SQL Server 線上叢書 》 中。  
  
```  
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```  
  
 建立資料表類型之後, 您可以宣告該類型為基礎的資料表值參數。 下列 TRANSACT-SQL 片段將示範如何宣告資料表值參數在預存程序定義中。 請注意，READONLY 關鍵字需要宣告資料表值參數。  
  
```  
CREATE PROCEDURE usp_UpdateCategories   
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```  
  
## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>修改資料與資料表值參數 (TRANSACT-SQL)  
 資料表值參數可以用於執行單一陳述式來影響多個資料列的集合為基礎的資料修改。 例如，您可以選取資料表值參數中的所有資料列，並將其插入至資料庫資料表時，或您可以建立的 update 陳述式資料表值參數加入您想要更新的資料表。  
  
 下列 TRANSACT-SQL UPDATE 陳述式示範如何使用資料表值參數聯結至 Categories 資料表。 當您使用具有在 FROM 子句中聯結的資料表值參數時，您必須也是別名，如下所示，其中資料表值參數的別名設定為"ec":  
  
```  
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```  
  
 此 TRANSACT-SQL 範例會示範如何從資料表值參數執行 INSERT，在單一集合式作業中選取資料列。  
  
```  
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```  
  
## <a name="limitations-of-table-valued-parameters"></a>資料表值參數的限制  
 有數個資料表值參數的限制：  
  
-   您無法將資料表值參數傳遞至使用者定義函式。  
  
-   資料表值參數僅支援 UNIQUE 或 PRIMARY KEY 條件約束的建立索引。 SQL Server 不會維護資料表值參數的統計資料。  
  
-   資料表值參數是唯讀的 TRANSACT-SQL 程式碼中。 您無法更新資料行中的值是資料表值參數的資料列，而且您無法插入或刪除資料列。 若要修改傳遞至預存程序或參數化陳述式資料表值參數中的資料，您必須插入資料至暫存資料表或資料表變數。  
  
-   您無法使用 ALTER TABLE 陳述式來修改資料表值參數的設計。
-   您可以串流處理大型資料表值參數中的物件。  
  
## <a name="configuring-a-table-valued-parameter"></a>設定資料表值參數  
 從 Microsoft JDBC Driver 6.0 for SQL Server，以參數化陳述式或參數化預存程序支援資料表值參數。 可以從 SQLServerDataTable，從結果集填入資料表值參數，或從使用者提供 ISQLServerDataRecord 介面的實作。 當設定備妥的查詢的資料表值參數時，您必須指定型別名稱必須符合先前在伺服器上建立相容的型別名稱。  
  
 下列兩個程式碼片段示範如何設定資料表值參數，SQLServerPreparedStatement 和 SQLServerCallableStatement 插入資料。 這裡 sourceTVPObject 可以 SQLServerDataTable，或結果集或 ISQLServerDataRecord 物件。 這些範例假設連接是使用中的連接物件。  
  
```  
// Using table-valued parameter with a SQLServerPreparedStatement.  
SQLServerPreparedStatement pStmt =   
    (SQLServerPreparedStatement) connection.prepareStatement(“INSERT INTO dbo.Categories SELECT * FROM ?”);  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);  
pStmt.execute();  
```  
  
```  
// Using table-valued parameter with a SQLServerCallableStatement.  
SQLServerCallableStatement pStmt =   
    (SQLServerCallableStatement) connection.prepareCall("exec usp_InsertCategories ?");       
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);;  
pStmt.execute();  
```  
  
> [!NOTE]  
>  請參閱 > 一節**JDBC 驅動程式的資料表值參數 API**下方的 Api 可讓您設定資料表值參數的完整清單。  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>將資料表值參數傳遞為 SQLServerDataTable 物件  
 從 Microsoft JDBC Driver 6.0 for SQL Server，SQLServerDataTable 類別代表記憶體中資料表的關聯式資料。 此範例示範如何從使用 SQLServerDataTable 物件的記憶體中資料的資料表值參數的建構。 程式碼第一次建立 SQLServerDataTable 物件、 定義其結構描述，並於其中填入資料的資料表。 然後，程式碼會設定 SQLServerPreparedStatement 會將此資料表做為資料表值參數傳遞給 SQL Server。  
  
```  
// Assumes connection is an active Connection object.  
  
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
>  請參閱 > 一節**JDBC 驅動程式的資料表值參數 API**下方的 Api 可讓您設定資料表值參數的完整清單。  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>將資料表值參數傳遞為結果集物件  
 此範例示範如何將串流處理的結果集的資料表值參數的資料列。 第一次從來源資料表中擷取資料的程式碼建立 SQLServerDataTable 物件，定義其結構描述並於其中填入資料的資料表。 然後，程式碼會設定 SQLServerPreparedStatement 會將此資料表做為資料表值參數傳遞給 SQL Server。  
  
```  
// Assumes connection is an active Connection object.  
  
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
>  請參閱 > 一節**JDBC 驅動程式的資料表值參數 API**下方的 Api 可讓您設定資料表值參數的完整清單。  
  
## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>將資料表值參數傳遞為 ISQLServerDataRecord 物件  
 從 Microsoft JDBC Driver 6.0 for SQL Server，新介面 ISQLServerDataRecord 是可用的資料流處理資料 （取決於使用者提供它的實作方式） 使用資料表值參數。 下列範例示範如何實作 ISQLServerDataRecord 介面以及如何將它當做資料表值參數傳遞。 為了簡單起見，下列範例會將包含硬式編碼值只在一個資料列傳遞至資料表值參數。 在理想情況下，使用者會實作這個介面的資料流的資料列從任何來源，例如，從文字檔案。  
  
```  
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
>  請參閱 > 一節**JDBC 驅動程式的資料表值參數 API**下方的 Api 可讓您設定資料表值參數的完整清單。  
    
## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>資料表值參數 API JDBC 驅動程式  
 **SQLServerMetaData**  
  
 此類別代表資料行中繼資料。 它用於 ISQLServerDataRecord 介面，以傳遞至資料表值參數資料行中繼資料。 此類別中的方法包括：  
  
|名稱|Description|  
|----------|-----------------|  
|公用 SQLServerMetaData （columnName 字串、 int sqlType、 int 有效位數、 int 規模、 布林 useServerDefault、 布林 isUniqueKey、 SQLServerSortOrder sortOrder、 int sortOrdinal）|初始化具有指定之資料行名稱、 sql 類型、 有效位數、 小數位數和伺服器預設的 SQLServerMetaData 的新執行個體。 這種形式的建構函式會藉由讓您可以指定資料行是否為資料表值參數、 資料行和排序資料行序數的排序次序中唯一支援資料表值參數。 <br><br>useServerDefault-指定是否此資料行應該使用預設的伺服器值。預設值為 false。<br>isUniqueKey-表示資料表值參數中的資料行是否為唯一的。預設值為 false。<br>sortOrder-指出資料行的排序次序預設值為 SQLServerSortOrder.Unspecified。<br>sortOrdinal-指定序數排序資料行;sortOrdinal 開始從 0;預設值為-1。|
|公用 SQLServerMetaData （columnName 字串、 int sqlType）|初始化 SQLServerMetaData 使用資料行名稱和 sql 類型的新執行個體。|  
|公用 SQLServerMetaData （字串 columnName int sqlType、 int、 整數位數 int 小數位數）|初始化 SQLServerMetaData 使用資料行名稱、 sql 類型、 有效位數和小數位數的新執行個體。|  
|公用 SQLServerMetaData (SQLServerMetaData sqlServerMetaData)|初始化新執行個體的 SQLServerMetaData 從另一個 SQLServerMetaData 物件。|  
|公開金鑰字串 getColumName()|擷取的資料行名稱。|  
|公用 int getSqlType()|擷取 java sql 類型。|  
|公用 int getPrecision()|擷取傳遞給資料行的類型的有效位數。|  
|公用 int getScale()|擷取的小數位數傳遞給資料行的類型。|  
|公用 SQLServerSortOrder getSortOrder()|擷取的排序次序。|
|公用 int getSortOrdinal()|擷取排序序數。|
|公用布林 isUniqueKey()|傳回資料行是否為唯一。|
|公用布林 useServerDefault()|傳回 wheher 資料行中，會使用預設伺服器值。|
  
 **SQLServerSortOrder**
 
 列舉，定義排序次序。 可能的值為遞增、 遞減以及未指定。 
  
 **SQLServerDataTable**  
  
 此類別代表記憶體中資料的資料表來搭配資料表值參數。 此類別中的方法包括：  
  
|名稱|Description|  
|----------|-----------------|  
|公用 SQLServerDataTable()|初始化 SQLServerDataTable 的新執行個體。|  
|公用的迭代器 < 項目\<整數，Object [] >> getIterator()|擷取迭代器上資料表的資料列。|  
|public void addColumnMetadata （columnName 字串、 int sqlType）|將指定之資料行的中繼資料。|  
|public void addColumnMetadata （SQLServerDataColumn 資料行）|將指定之資料行的中繼資料。|  
|public void addRow （物件...值）|將一個資料列加入至資料表。|  
|公用對應\<整數、 SQLServerDataColumn > getColumnMetadata()|擷取此資料表的資料行中繼資料。|
|public void clear （) |清除此資料表。 |  
  
 **SQLServerDataColumn**  
  
 此類別代表記憶體中資料表的 SQLServerDataTable 所代表的資料行。 此類別中的方法包括：  
  
|名稱|Description|  
|----------|-----------------|  
|公用 SQLServerDataColumn （columnName 字串、 int sqlType）|初始化具有資料行名稱和類型的 SQLServerDataColumn 的新執行個體。|  
|公開金鑰字串 getColumnName()|擷取的資料行名稱。|  
|公用 int getColumnType()|擷取的資料行類型。|  
  
 **ISQLServerDataRecord**  
  
 此類別代表使用者可以實作以資料表值參數的資料流資料的介面。 這個介面中的方法包括：  
  
|名稱|Description|  
|----------|-----------------|  
|公用 SQLServerMetaData getColumnMetaData （int 資料行）。|擷取給定的資料行索引的資料行中繼資料。|  
|公用 int getColumnCount();|擷取資料行的總數。|  
|[] getRowData() 公用物件;|擷取目前的資料列的資料當做物件的陣列。|  
|公用布林 next （);|移至下一個資料列。 如果移動成功，而且沒有下一個資料列，則為 false 的否則會傳回 True。|  
  
 **SQLServerPreparedStatement**  
  
 已加入下列方法加入這個類別支援將資料表值參數傳遞。  
  
|名稱|Description|  
|----------|-----------------|  
|公用最終的 void setStructured int parameterIndex、 字串 tvpName (SQLServerDataTable tvpDataTbale）|填入資料表值參數與日期資料表。 parameterIndex 是參數索引、 tvpName 是資料表值參數的名稱和 tvpDataTable 是來源資料的資料表物件。|  
|公用最終的 void setStructured int parameterIndex、 字串 tvpName (ResultSet tvpResultSet）|資料表值參數中填入從同一資料表中擷取結果集。 parameterIndex 是參數索引 tvpName 是資料表值參數的名稱，tvpResultSet 來源結果集物件。|  
|公用最終的 void setStructured int parameterIndex、 字串 tvpName (ISQLServerDataRecord tvpDataRecord）|填入資料表值參數與 ISQLServerDataRecord 物件。 ISQLServerDataRecord 用於串流資料，而使用者決定如何使用它。 parameterIndex 是參數索引 tvpName 是資料表值參數的名稱，tvpDataRecord ISQLServerDataRecord 物件。|  
  
 **SQLServerCallableStatement**  
  
 已加入下列方法加入這個類別支援將資料表值參數傳遞。  
  
|名稱|Description|  
|----------|-----------------|  
|公用最終的 void setStructured 字串 paratemeterName、 字串 tvpName (SQLServerDataTable tvpDataTable）|會填入資料表值參數傳遞至與日期資料表的預存程序。 paratemeterName 是參數的名稱、 tvpName 是 TVP，型別的名稱和 tvpDataTable 是資料的資料表物件。|  
|公用最終的 void setStructured 字串 paratemeterName、 字串 tvpName (ResultSet tvpResultSet）|會填入資料表值參數傳遞至預存程序，與另一個資料表中擷取結果集。 paratemeterName 是參數的名稱、 tvpName 是 TVP，型別的名稱和 tvpResultSet 是來源結果集物件。|  
|公用最終的 void setStructured 字串 paratemeterName、 字串 tvpName (ISQLServerDataRecord tvpDataRecord）|會填入資料表值參數傳遞至具有 ISQLServerDataRecord 物件的預存程序。 ISQLServerDataRecord 用於串流資料，而使用者決定如何使用它。 paratemeterName 是參數的名稱、 tvpName 是 TVP，型別的名稱和 tvpDataRecord 是 ISQLServerDataRecord 物件。|  
  
## <a name="see-also"></a>另請參閱  
 [JDBC 驅動程式概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

