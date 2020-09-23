---
title: 搭配 JDBC 驅動程式使用大量複製
description: SQLServerBulkCopy 類別讓您能夠在 Java 中撰寫資料載入解決方案，透過標準 JDBC API 提供顯著的效能優勢。
ms.custom: ''
ms.date: 08/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 21e19635-340d-49bb-b39d-4867102fb5df
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69379b9af3dc126713cb2bbd3172003692a7d4de
ms.sourcegitcommit: 9be0047805ff14e26710cfbc6e10d6d6809e8b2c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "89042211"
---
# <a name="using-bulk-copy-with-the-jdbc-driver"></a>搭配 JDBC 驅動程式使用大量複製

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft SQL Server 包含名為 `bcp` 的常用命令列公用程式，其用於將大型檔案快速大量複製到 SQL Server 資料庫中的資料表或檢視表。 `SQLServerBulkCopy` 類別可供在 Java 中撰寫程式碼解決方案來提供類似的功能。 還有其他方法可以將資料載入 SQL Server 資料表 (例如 INSERT 陳述式)，但 `SQLServerBulkCopy` 提供顯著超越其他方法的效能優勢。  
  
`SQLServerBulkCopy` 類別只能用來將資料寫入到 SQL Server 資料表。 但資料來源不限於 SQL Server；任何資料來源皆可使用，只要該資料可以用 `ResultSet`、`RowSet` 或 `ISQLServerBulkRecord` 實作來讀取。  
  
使用 `SQLServerBulkCopy` 類別，您可以執行：  
  
- 單一大量複製作業  
  
- 多項大量複製作業  
  
- 交易的大量複製作業  
  
> [!NOTE]  
> 使用 Microsoft JDBC 驅動程式 4.1 for SQL Server 或更早版本 (其不支援 SQLServerBulkCopy 類別) 時，您可以改為執行 SQL Server Transact-SQL BULK INSERT 陳述式。  
  
## <a name="bulk-copy-example-setup"></a>大量複製範例設定  

`SQLServerBulkCopy` 類別只能用來將資料寫入到 SQL Server 資料表。 本文中所顯示的程式碼範例會使用 SQL Server 範例資料庫 [AdventureWorks](../../samples/adventureworks-install-configure.md)。 為了避免改變程式碼範例中的現有資料表，請將資料寫入先建立的資料表中。  
  
`BulkCopyDemoMatchingColumns` 和 `BulkCopyDemoDifferentColumns` 資料表都是以 AdventureWorks `Production.Products` 資料表為依據。 在使用這些資料表的程式碼範例中，會將來自 `Production.Products` 資料表的資料新增至其中一個範例資料表。 當此範例說明如何將來源資料的資料行對應至目的地資料表時，會使用 `BulkCopyDemoDifferentColumns` 資料表；針對大部分其他範例，則會使用 `BulkCopyDemoMatchingColumns`。  
  
幾個程式碼範例示範如何使用一個 `SQLServerBulkCopy` 類別來寫入多個資料表。 針對這些範例，會使用 `BulkCopyDemoOrderHeader` 和 `BulkCopyDemoOrderDetail` 資料表作為目的地資料表。 這些資料表是以 AdventureWorks 中的 `Sales.SalesOrderHeader` 和 `Sales.SalesOrderDetail` 資料表為依據。  
  
> [!NOTE]  
> `SQLServerBulkCopy` 程式碼範例僅提供用於 示範使用 `SQLServerBulkCopy` 的語法。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL INSERT ...SELECT 陳述式以複製資料。  

### <a name="table-setup"></a>資料表設定  

若要建立程式碼範例正確執行所需的資料表，您必須在 SQL Server 資料庫中執行下列 Transact-SQL 陳述式。  

```sql
USE AdventureWorks  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoMatchingColumns]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoMatchingColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoMatchingColumns]([ProductID] [int] IDENTITY(1,1) NOT NULL,  
    [Name] [nvarchar](50) NOT NULL,  
    [ProductNumber] [nvarchar](25) NOT NULL,  
 CONSTRAINT [PK_ProductID] PRIMARY KEY CLUSTERED
(  
    [ProductID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoDifferentColumns]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoDifferentColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoDifferentColumns]([ProdID] [int] IDENTITY(1,1) NOT NULL,  
    [ProdNum] [nvarchar](25) NOT NULL,  
    [ProdName] [nvarchar](50) NOT NULL,  
 CONSTRAINT [PK_ProdID] PRIMARY KEY CLUSTERED
(  
    [ProdID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderHeader]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderHeader]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderHeader]([SalesOrderID] [int] IDENTITY(1,1) NOT NULL,  
    [OrderDate] [datetime] NOT NULL,  
    [AccountNumber] [nvarchar](15) NULL,  
 CONSTRAINT [PK_SalesOrderID] PRIMARY KEY CLUSTERED
(  
    [SalesOrderID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderDetail]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderDetail]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderDetail]([SalesOrderID] [int] NOT NULL,  
    [SalesOrderDetailID] [int] NOT NULL,  
    [OrderQty] [smallint] NOT NULL,  
    [ProductID] [int] NOT NULL,  
    [UnitPrice] [money] NOT NULL,  
 CONSTRAINT [PK_LineNumber] PRIMARY KEY CLUSTERED
(  
    [SalesOrderID] ASC,  
    [SalesOrderDetailID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
```

## <a name="single-bulk-copy-operations"></a>單一大量複製作業

執行 SQL Server 大量複製作業最簡單的方式為執行對資料庫的單一作業。 根據預設，大量複製作業會做為隔離作業執行：該複製作業會以非交易的方式進行，且沒有機會復原。  
  
> [!NOTE]  
> 當錯誤發生時，如果您需要復原全部或部分大量複製，您可以使用 `SQLServerBulkCopy` 受管理的交易，或執行現有交易中的大量複製作業。  
> 如需詳細資訊，請參閱[交易和大量複製作業](#transaction-and-bulk-copy-operations)  
  
 執行大量複製作業的一般步驟如下：  
  
1. 連接到來源伺服器，並取得要複製的資料。 如果可從 `ResultSet` 物件或 `ISQLServerBulkRecord` 實作中擷取資料，則資料也可來自其他來源。  
  
2. 連線到目的地伺服器 (除非想要 `SQLServerBulkCopy` 建立連線)。  
  
3. 建立 `SQLServerBulkCopy` 物件，並透過 `setBulkCopyOptions` 來設定任何必要的屬性。  
  
4. 呼叫 `setDestinationTableName` 方法，以指出大量插入作業的目標資料表。  
  
5. 呼叫其中一個 `writeToServer` 方法。  
  
6. (選擇性) 透過 `setBulkCopyOptions` 更新屬性，並視需要再次呼叫 `writeToServer`。  
  
7. 呼叫 `close`，或將該大量複製作業包裝在 try-with-resources 陳述式之內。  
  
> [!CAUTION]  
> 我們建議來源和目標資料行的資料類型必須相符。 如果此資料類型不相符，`SQLServerBulkCopy`即會嘗試將每個來源值轉換成目標資料類型。 轉換可能會影響效能，並也可能會導致未預期的錯誤。 例如，double 資料類型大多可以轉換成 decimal 資料類型，但並非總是如此。  
  
### <a name="example"></a>範例

下列應用程式示範如何使用 `SQLServerBulkCopy` 類別來載入資料。 在這個範例中，`ResultSet` 用於從 SQL Server AdventureWorks 資料庫的 Production.Product 資料表，將資料複製到同一資料庫中的類似資料表中。  
  
> [!IMPORTANT]  
> 除非您已如[資料表設定](#table-setup) 中所述建立工作資料表，否則此範例不會執行。 這個程式碼僅提供用於示範使用 `SQLServerBulkCopy` 的語法。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL INSERT ...SELECT 陳述式以複製資料。  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;

public class BulkCopySingle {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection)) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // In real world applications you would
            // not use SQLServerBulkCopy to move data from one table to the other
            // in the same database. This is for demonstration purposes only.

            // Set up the bulk copy object.
            // Note that the column positions in the source
            // table match the column positions in
            // the destination table so there is no need to
            // map columns.
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            bulkCopy.writeToServer(rsSourceData);

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="performing-a-bulk-copy-operation-using-transact-sql"></a>使用 Transact-SQL 執行大量複製作業

以下範例將示範如何使用 `executeUpdate` 方法來執行 BULK INSERT 陳述式。  
  
> [!NOTE]  
> 資料來源的檔案路徑是與伺服器相對的。 伺服器處理序必須存取該路徑，藉此順利完成大量複製作業。  

```java
try (Connection con = DriverManager.getConnection(connectionUrl);
        Statement stmt = con.createStatement()) {
    // Perform the BULK INSERT
    stmt.executeUpdate(
            "BULK INSERT Northwind.dbo.[Order Details] " + "FROM 'f:\\mydata\\data.tbl' " + "WITH ( FORMATFILE='f:\\mydata\\data.fmt' )");
}
```  

## <a name="multiple-bulk-copy-operations"></a>多項大量複製作業  

您可以使用 `SQLServerBulkCopy` 類別的單一執行個體，執行多項大量複製作業。 如果此作業在複本 (例如目的地資料表的名稱) 之間變更，則必須在後續呼叫任何 `writeToServer` 方法之前加以更新，如下列範例所示。 除非已明確地變更，所有屬性值與之前指定執行個體上的大量複製作業維持相同。  

> [!NOTE]  
> 比起對每項作業使用個別的執行個體，使用 `SQLServerBulkCopy` 的相同執行個體來執行多項大量複製作業通常更有效率。  
  
如果您使用相同的 `SQLServerBulkCopy` 物件執行數項大量複製作業，並未限制來源或目標資訊在每項作業中是否相等或不同。 不過，當您每次寫入到伺服器時，必須確定資料行關聯資訊已正確設定。  
  
> [!IMPORTANT]  
> 除非您已如[資料表設定](#table-setup) 中所述建立工作資料表，否則此範例不會執行。 這個程式碼僅提供用於示範使用 `SQLServerBulkCopy` 的語法。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL INSERT ...SELECT 陳述式以複製資料。  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyMultiple {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationHeaderTable = "dbo.BulkCopyDemoOrderHeader";
        String destinationDetailTable = "dbo.BulkCopyDemoOrderDetail";
        int countHeaderBefore, countDetailBefore, countHeaderAfter, countDetailAfter;
        ResultSet rsHeader, rsDetail;

        try (Connection sourceConnection1 = DriverManager.getConnection(connectionUrl);
                Connection sourceConnection2 = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection1.createStatement();
                PreparedStatement preparedStmt1 = sourceConnection1.prepareStatement(
                        "SELECT [SalesOrderID], [OrderDate], [AccountNumber] FROM [Sales].[SalesOrderHeader] WHERE [AccountNumber] = ?;");
                PreparedStatement preparedStmt2 = sourceConnection2.prepareStatement(
                        "SELECT [Sales].[SalesOrderDetail].[SalesOrderID], [SalesOrderDetailID], [OrderQty], [ProductID], [UnitPrice] FROM "
                                + "[Sales].[SalesOrderDetail] INNER JOIN [Sales].[SalesOrderHeader] ON "
                                + "[Sales].[SalesOrderDetail].[SalesOrderID] = [Sales].[SalesOrderHeader].[SalesOrderID] WHERE [AccountNumber] = ?;");
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(connectionUrl);) {

            // Empty the destination tables.
            stmt.executeUpdate("DELETE FROM " + destinationHeaderTable);
            stmt.executeUpdate("DELETE FROM " + destinationDetailTable);

            // Perform an initial count on the destination
            // table with matching columns.
            countHeaderBefore = getRowCount(stmt, destinationHeaderTable);

            // Perform an initial count on the destination
            // table with different column positions.
            countDetailBefore = getRowCount(stmt, destinationDetailTable);

            // Get data from the source table as a ResultSet.
            // The Sales.SalesOrderHeader and Sales.SalesOrderDetail
            // tables are quite large and could easily cause a timeout
            // if all data from the tables is added to the destination.
            // To keep the example simple and quick, a parameter is
            // used to select only orders for a particular account
            // as the source for the bulk insert.
            preparedStmt1.setString(1, "10-4020-000034");
            rsHeader = preparedStmt1.executeQuery();

            // Get the Detail data in a separate connection.
            preparedStmt2.setString(1, "10-4020-000034");
            rsDetail = preparedStmt2.executeQuery();

            // Create the SQLServerBulkCopySQLServerBulkCopy object.
            SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setBulkCopyTimeout(100);
            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationHeaderTable);

            // Guarantee that columns are mapped correctly by
            // defining the column mappings for the order.
            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");
            bulkCopy.addColumnMapping("OrderDate", "OrderDate");
            bulkCopy.addColumnMapping("AccountNumber", "AccountNumber");

            // Write rsHeader to the destination.
            bulkCopy.writeToServer(rsHeader);

            // Set up the order details destination.
            bulkCopy.setDestinationTableName(destinationDetailTable);

            // Clear the existing column mappings
            bulkCopy.clearColumnMappings();

            // Add order detail column mappings.
            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");
            bulkCopy.addColumnMapping("SalesOrderDetailID", "SalesOrderDetailID");
            bulkCopy.addColumnMapping("OrderQty", "OrderQty");
            bulkCopy.addColumnMapping("ProductID", "ProductID");
            bulkCopy.addColumnMapping("UnitPrice", "UnitPrice");

            // Write rsDetail to the destination.
            bulkCopy.writeToServer(rsDetail);

            // Perform a final count on the destination
            // tables to see how many rows were added.
            countHeaderAfter = getRowCount(stmt, destinationHeaderTable);
            countDetailAfter = getRowCount(stmt, destinationDetailTable);

            System.out.println((countHeaderAfter - countHeaderBefore) + " rows were added to the Header table.");
            System.out.println((countDetailAfter - countDetailBefore) + " rows were added to the Detail table.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

## <a name="transaction-and-bulk-copy-operations"></a>交易和大量複製作業

 大量複製作業可以做為隔離作業或做為多步驟交易的一部分執行。 這第二個選項可讓您執行相同交易內的多項大量複製作業，以及執行其他資料庫作業 (例如插入、更新和刪除)，同時仍然能夠認可或回復整個交易。  
  
 根據預設，大量複製作業會做為隔離作業執行。 該複製作業會以非交易的方式進行，且沒有機會復原。 如果需要在發生錯誤時回復全部或部分大量複製，則可使用由 `SQLServerBulkCopy` 管理的交易，或在現有的交易內執行大量複製作業。  

## <a name="extended-bulk-copy-for-azure-data-warehouse"></a>適用於 Azure 資料倉儲的延伸大量複製

驅動程式 v8.4.1 版加入一個新的連線屬性 `sendTemporalDataTypesAsStringForBulkCopy`。 此布林值屬性預設為 `true`。

當這個連線屬性設定為 `false` 時，將會傳送 **DATE**、**DATETIME**、**DATIMETIME2**、**DATETIMEOFFSET**、**SMALLDATETIME** 和 **TIME** 資料類型作為其各自的類型，而不是以字串的形式傳送。

將時態性資料類型作為其各自的類型傳送，可讓使用者針對 Azure Synapse Analytics (SQL DW) 將資料傳送到那些資料行中；這在之前並不可能達成，因為驅動程式會將資料轉換成字串。 將字串資料傳送到時態性資料行適用於 SQL Server，因為 SQL Server 會為我們執行隱含轉換，但其與 Azure Synapse Analytics (SQL DW) 並不相同。

此外，即使不將此連接字串設定為 'false'，從 **v8.4.1** 和更新版本開始，**MONEY** 和 **SMALLMONEY** 資料類型將會以 **MONEY** / **SMALLMONEY** 資料類型 (而不是 **DECIMAL**) 的形式傳送，這也會允許將那些資料類型大量複製到 Azure Synapse Analytics (SQL DW)。

### <a name="extended-bulk-copy-for-azure-data-warehouse-limitations"></a>適用於 Azure 資料倉儲的延伸大量複製限制

目前有兩個限制：

1. 當此連線屬性設定為 `false` 時，驅動程式只會接受每個時態性資料類型的預設字串常值格式，例如：

    `DATE: YYYY-MM-DD`

    `DATETIME: YYYY-MM-DD hh:mm:ss[.nnn]`

    `DATETIME2: YYYY-MM-DD hh:mm:ss[.nnnnnnn]`

    `DATETIMEOFFSET: YYYY-MM-DD hh:mm:ss[.nnnnnnn] [{+/-}hh:mm]`

    `SMALLDATETIME:YYYY-MM-DD hh:mm:ss`

    `TIME: hh:mm:ss[.nnnnnnn]`

2. 當此連線屬性設定為 `false` 時，針對大量複製所指定的資料行類型必須遵循[這裡](../../connect/jdbc/using-basic-data-types.md)的資料類型對應圖表。 例如，使用者先前可以指定 `java.sql.Types.TIMESTAMP`，以將資料大量複製到 `DATE` 資料行中，但在啟用此功能之後，必須指定 `java.sql.Types.DATE` 才能執行相同的工作。
  
### <a name="performing-a-non-transacted-bulk-copy-operation"></a>執行非交易大量複製作業

對於非交易大量複製作業在作業過程遭遇錯誤時的狀況，下列應用程式顯示此時會發生什麼事。  
  
在範例中，來源資料表及目的地資料表都包含名為 `ProductID` 的識別欄位。 程式碼會先準備目的地資料表，方法是刪除所有資料列，然後插入單一資料列，且其 `ProductID` 已知存在於來源資料表中。 根據預設，在目的地資料表中，身分識別欄位的新值會針對每個加入的資料列產生。 在此範例中，會在開啟連線時設定選項，以強制大量載入處理序改為使用來源資料表中的識別值。  
  
此大量複製作業執行時的 `BatchSize` 屬性設定為 10。 當此作業遇到無效的資料列時，就會擲回例外狀況。 在第一個範例中，大量複製作業會為非交易作業。 發生錯誤前複製的所有批次均已認可；包含重複索引鍵的批次已回復，而且大量複製作業會在處理任何其他批次之前暫止。  
  
> [!NOTE]  
> 除非您已如[資料表設定](#table-setup) 中所述建立工作資料表，否則此範例不會執行。 這個程式碼僅提供用於示範使用 `SQLServerBulkCopy` 的語法。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL INSERT ...SELECT 陳述式以複製資料。  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyNonTransacted {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(connectionUrl)) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Add a single row that will result in duplicate key
            // when all rows from source are bulk copied.
            // Note that this technique will only be successful in
            // illustrating the point if a row with ProductID = 446
            // exists in the AdventureWorks Production.Products table.
            // If you have made changes to the data in this table, change
            // the SQL statement in the code to add a ProductID that
            // does exist in your version of the Production.Products
            // table. Choose any ProductID in the middle of the table
            // (not first or last row) to best illustrate the result.
            stmt.executeUpdate("SET IDENTITY_INSERT " + destinationTable + " ON;" + "INSERT INTO " + destinationTable
                    + "([ProductID], [Name] ,[ProductNumber]) VALUES(446, 'Lock Nut 23','LN-3416'); SET IDENTITY_INSERT " + destinationTable
                    + " OFF");

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // Set up the bulk copy object using the KeepIdentity option and BatchSize = 10.
            SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setKeepIdentity(true);
            copyOptions.setBatchSize(10);

            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            // This should fail with a duplicate key error
            // after some of the batches have been copied.
            try {
                bulkCopy.writeToServer(rsSourceData);
            }
            catch (SQLException e) {
                e.printStackTrace();
            }

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="performing-a-dedicated-bulk-copy-operation-in-a-transaction"></a>在交易中執行專用大量複製作業

根據預設，大量複製作業不會自行建立交易。 當想要執行專用大量複製作業時，請使用連接字串來建立 `SQLServerBulkCopy` 的新執行個體。 在此案例中，大量複製作業的每個批次都會由資料庫以隱含方式認可。 您可以在 `SQLServerBulkCopyOptions` 中將 `UseInternalTransaction` 選項設定為 `true`，讓大量複製作業建立交易，並在大量複製作業的每個批次之後執行認可。
  
```java
SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
copyOptions.setKeepIdentity(true);
copyOptions.setBatchSize(10);
copyOptions.setUseInternalTransaction(true);
```

### <a name="using-existing-transactions"></a>使用現有的交易

您可傳遞已啟用交易的 `Connection` 物件，其作為 `SQLServerBulkCopy` 建構函式的參數。 在此情況下，大量複製作業會在現有的交易中執行，且不會變更交易狀態 (也就是其尚未認可或中止)。 這可讓應用程式在其他資料庫作業的交易中包含大量複製作業。 如果因為發生錯誤而需要回復整個大量複製作業，或如果大量複製應該作為可回復的更大型處理序一部分來執行，則可在大量複製作業之後的任何時間點，在 `Connection` 物件上執行回復。  
  
下列應用程式與 `BulkCopyNonTransacted` 類似，但有一個例外：在此範例中，大量複製作業包含在較大的外部交易中。 當發生主要索引鍵違規錯誤時，整個交易便會回復，並且沒有任何資料列會加入目的地資料表。

> [!NOTE]  
> 除非您已如[資料表設定](#table-setup) 中所述建立工作資料表，否則此範例不會執行。 這個程式碼僅提供用於示範使用 `SQLServerBulkCopy` 的語法。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL INSERT ...SELECT 陳述式以複製資料。  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyExistingTransactions {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;
        SQLServerBulkCopyOptions copyOptions;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection);) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Add a single row that will result in duplicate key
            // when all rows from source are bulk copied.
            // Note that this technique will only be successful in
            // illustrating the point if a row with ProductID = 446
            // exists in the AdventureWorks Production.Products table.
            // If you have made changes to the data in this table, change
            // the SQL statement in the code to add a ProductID that
            // does exist in your version of the Production.Products
            // table. Choose any ProductID in the middle of the table
            // (not first or last row) to best illustrate the result.
            stmt.executeUpdate("SET IDENTITY_INSERT " + destinationTable + " ON;" + "INSERT INTO " + destinationTable
                    + "([ProductID], [Name] ,[ProductNumber]) VALUES(446, 'Lock Nut 23','LN-3416'); SET IDENTITY_INSERT " + destinationTable
                    + " OFF");

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // Set up the bulk copy object inside the transaction.
            destinationConnection.setAutoCommit(false);

            copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setKeepIdentity(true);
            copyOptions.setBatchSize(10);

            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            // This should fail with a duplicate key error.
            try {
                bulkCopy.writeToServer(rsSourceData);
                destinationConnection.commit();
            }
            catch (SQLException e) {
                e.printStackTrace();
                destinationConnection.rollback();
            }

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        catch (Exception e) {
            // Handle any errors that may have occurred.
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="bulk-copy-from-a-csv-file"></a>從 CSV 檔案進行大量複製  

 下列應用程式示範如何使用 `SQLServerBulkCopy` 類別來載入資料。 在此範例中，將使用一個 CSV 檔案將從 SQL Server AdventureWorks 資料庫的 Production.Product 資料表匯出的資料複製到該資料庫中的類似資料表。  
  
> [!IMPORTANT]  
> 除非您已如[資料表設定](#table-setup) 中所述建立工作資料表來取得它，否則此範例不會執行。  
  
1. 開啟 **SQL Server Management Studio**，並連線到具有 AdventureWorks 資料庫的 SQL Server。  
  
2. 展開此資料庫，以滑鼠右鍵按一下 AdventureWorks 資料庫，選取 [工作]  和 [匯出資料]  …  
  
3. 針對 [資料來源]，選取 [資料來源]，這可供連線到 SQL Server (例如 SQL Server Native Client 11.0)，檢查設定，然後按一下 [下一步]  
  
4. 針對 [目的地]，選取 [一般檔案目的地]，然後輸入目的地的 [檔案名稱]，例如 `C:\Test\TestBulkCSVExample.csv`。 請檢查 [格式]  為 [分隔]，且 [文字限定詞]  為 [無]，並啟用 [第一個資料列的資料行名稱]  ，然後選取 [下一步]   
  
5. 選取 [寫入查詢來指定要傳送的資料]  ，然後按一下 [下一步]  。  輸入 [SQL 陳述式] `SELECT ProductID, Name, ProductNumber FROM Production.Product`，然後按一下 [下一步]  
  
6. 檢查設定：您可將資料列分隔符號保留為 `{CR}{LF}`，並將資料行分隔符號保留為逗號 `{,}`。  選取 [編輯對應]，然後檢查資料 [類型] 對於每個資料行是否都正確 (例如檢查 `ProductID` 是否為整數，以及檢查其他資料行是否為 Unicode 字串)。  
  
7. 直接跳到 [完成]  並執行匯出。  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCSVFileRecord;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;

public class BulkCopyCSV {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;

        // Get data from the source file by loading it into a class that implements ISQLServerBulkRecord.
        // Here we are using the SQLServerBulkCSVFileRecord implementation to import the example CSV file.
        try (Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = destinationConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection);
                SQLServerBulkCSVFileRecord fileRecord = new SQLServerBulkCSVFileRecord("C:\\Test\\TestBulkCSVExample.csv", true);) {

            // Set the metadata for each column to be copied.
            fileRecord.addColumnMetadata(1, null, java.sql.Types.INTEGER, 0, 0);
            fileRecord.addColumnMetadata(2, null, java.sql.Types.NVARCHAR, 50, 0);
            fileRecord.addColumnMetadata(3, null, java.sql.Types.NVARCHAR, 25, 0);

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Set up the bulk copy object.
            // Note that the column positions in the source
            // data reader match the column positions in
            // the destination table so there is no need to
            // map columns.
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            bulkCopy.writeToServer(fileRecord);

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```  

### <a name="bulk-copy-with-delimiters-as-data-in-csv-file"></a>以分隔符號作為 CSV 檔案中的資料進行大量複製

驅動程式 8.4.1 版會新增新的 API `SQLServerBulkCSVFileRecord.setEscapeColumnDelimitersCSV(boolean)`。 當設定為 true 時，將會套用下列規則：

- 每個欄位可以也可以不以雙引號括住。
- 如果欄位不以雙引號括住，雙引號便不可以出現在欄位內。
- 包含雙引號和分隔符號的欄位應該以雙引號括住。
- 如果使用雙引號來括住欄位，則針對出現在欄位內的雙引號，必須在其前方加上另一個雙引號來加以逸出。

### <a name="bulk-copy-with-always-encrypted-columns"></a>Always Encrypted 資料行的大量複製  

自 Microsoft JDBC Driver 6.0 for SQL Server 6.0 起，Always Encrypted 資料行支援大量複製。  
  
根據大量複製選項，以及來源和目的地資料表的加密類型，JDBC 驅動程式可能會以透明的方式解密然後加密資料，或是它可能會依現狀傳送加密的資料。 例如，當從加密資料行將資料大量複製到未加密的資料行時，驅動程式會先以透明的方式解密資料，然後才傳送到 SQL Server。 同樣地，當從未加密資料行 (或從 CSV 檔案) 將資料大量複製到加密資料行時，驅動程式會先以透明的方式加密資料，然後才傳送到 SQL Server。 如果來源和目的地都已加密，則視 `allowEncryptedValueModifications` 大量複製選項而定，驅動程式會依現狀傳送資料，或是先解密資料再將它加密，然後才傳送到 SQL Server。  
  
如需詳細資訊，請參閱底下的 `allowEncryptedValueModifications` 大量複製選項，以及[搭配使用 Always Encrypted 與 JDBC 驅動程式](using-always-encrypted-with-the-jdbc-driver.md)。  
  
> [!IMPORTANT]  
> Microsoft JDBC Driver 6.0 for SQL Server 在從 CSV 檔案大量複製資料到加密資料行時的限制：  
>
> 針對日期和時間類型，只支援 Transact-SQL 預設字串常值格式  
>
> 不支援 DATETIME 和 SMALLDATETIME 資料類型  
  
## <a name="bulk-copy-api-for-jdbc-driver"></a>適用於 JDBC 驅動程式的大量複製 API  
  
### <a name="sqlserverbulkcopy"></a>SQLServerBulkCopy

讓您有效率地將其他來源的資料大量載入 SQL Server 資料表。  
  
Microsoft SQL Server 包含名為 bcp 的常用命令提示字元公用程式，不管是在單一伺服器上或伺服器之間，都可用於將資料從一個資料表移動到另一個。 `SQLServerBulkCopy` 類別可供在 Java 中撰寫程式碼解決方案來提供類似的功能。 還有其他方法可將資料載入 SQL Server 資料表 (例如 INSERT 陳述式) 中，但 `SQLServerBulkCopy` 提供顯著超越其他方法的效能優勢。  
  
`SQLServerBulkCopy` 類別只能用來將資料寫入到 SQL Server 資料表。 不過，資料來源不限於 SQL Server；任何資料來源皆可使用，只要該資料可以用 `ResultSet` 執行個體或 `ISQLServerBulkRecord` 實作來讀取。  
  
| 建構函式 | 描述 |
| ----------- | ----------- |
| `SQLServerBulkCopy(Connection connection)` | 使用 `SQLServerConnection` 的指定開放執行個體，以初始化 `SQLServerBulkCopy` 類別的新執行個體。 如果 `Connection` 已啟用交易，則會在該交易內執行複製作業。 |
| `SQLServerBulkCopy(String connectionURL)` | 根據所提供的 `connectionURL` 來初始化並開啟 `SQLServerConnection` 的新執行個體。 這個建構函式會使用 `SQLServerConnection` 來初始化 `SQLServerBulkCopy` 類別的新執行個體。 |
  
| 屬性 | 說明 |
| -------- | ----------- |
| `String DestinationTableName` | 該伺服器的目的地資料表名稱。<br /><br /> 如果呼叫 `writeToServer` 時尚未設定 `DestinationTableName`，則會擲回 `SQLServerException`。<br /><br /> `DestinationTableName` 是三部分名稱 (`<database>.<owningschema>.<name>`)。 如果您要加以選擇，則可以用該資料表的資料庫和主控結構描述來限定該資料表名稱。 不過，如果該資料表名稱使用底線 ("_") 或任何其他特殊字元，您就必須使用括起來的括號逸出該名稱。 如需詳細資訊，請參閱＜ [Database Identifiers](../../relational-databases/databases/database-identifiers.md)＞。 |
| `ColumnMappings` | 在資料來源的資料行和目的地的資料行之間，資料行對應可定義其關聯性。<br /><br /> 如果未定義對應，則該資料行會根據位置順序隱含地對應。 若要執行這項操作，則來源和目標結構描述必須相符。 如果不相符，將會擲回例外狀況。<br /><br /> 如果此對應不是空的，就不必指定存在於該資料來源的每個資料行。 會忽略未對應的部分。<br /><br /> 您可以依名稱或序數找到來源和目標資料行。 |
  
| 方法 | 說明 |
| ------ | ----------- |
| `void addColumnMapping(int sourceColumn, int destinationColumn)` | 加入新的資料行對應，用來指定來源和目的地資料行的序數。 |
| `void addColumnMapping (int sourceColumn, String destinationColumn)` | 加入新的資料行對應，方法是使用來源資料行的序數和目的地資料行的資料行名稱。 |
| `void addColumnMapping (String sourceColumn, int destinationColumn)` | 加入新的資料行對應，方法是使用資料行名稱來描述來源資料行與序數，以指定此目的地資料行。 |
| `void addColumnMapping (String sourceColumn, String destinationColumn)` | 加入新的資料行對應，方法是使用資料行名稱來指定來源和目的地資料行。 |
| `void clearColumnMappings()` | 清除此資料行對應的內容。 |
| `void close()` | 關閉 `SQLServerBulkCopy` 執行個體。 |
| `SQLServerBulkCopyOptions getBulkCopyOptions()` | 擷取 `SQLServerBulkCopyOptions` 的目前集合。 |
| `String getDestinationTableName()` | 擷取目的地資料表的目前名稱。 |
| `void setBulkCopyOptions(SQLServerBulkCopyOptions copyOptions)` | 根據提供的選項，更新 `SQLServerBulkCopy` 執行個體的行為。 |
| `void setDestinationTableName(String tableName)` | 設定目的地資料表的名稱。 |
| `void writeToServer(ResultSet sourceData)` | 將所提供 `ResultSet` 中的所有資料列複製到 `SQLServerBulkCopy` 物件 `DestinationTableName` 屬性所指定目的地資料表。 |
| `void writeToServer(RowSet sourceData)` | 將所提供 `RowSet` 中的所有資料列複製到 `SQLServerBulkCopy` 物件 `DestinationTableName` 屬性所指定目的地資料表。 |
| `void writeToServer(ISQLServerBulkRecord sourceData)` | 將所提供 `ISQLServerBulkRecord` 實作中的所有資料列複製到 `SQLServerBulkCopy` 物件 `DestinationTableName` 屬性所指定目的地資料表。 |
  
### <a name="sqlserverbulkcopyoptions"></a>SQLServerBulkCopyOptions  

 控制 `writeToServer` 方法在 `SQLServerBulkCopy` 執行個體中運作方式的設定集合。  
  
| 建構函式 | 描述 |
| ----------- | ----------- |
| `SQLServerBulkCopyOptions()` | 使用所有設定的預設值，以初始化 `SQLServerBulkCopyOptions` 類別的新執行個體。 |
  
 Getter 和 Setter 主要用於下列選項：  
  
| 選項 | 描述 | 預設 |
| ------ | ----------- | ------- |
| `boolean CheckConstraints` | 在插入資料時檢查條件約束。 | False - 不會檢查條件約束 |
| `boolean FireTriggers` | 導致伺服器引發插入觸發程序，以將資料列插入資料庫中。 | False - 不引發任何觸發程序。 |
| `boolean KeepIdentity` | 保留來源識別值。 | False - 由目的地指派的識別值。 |
| `boolean KeepNulls` | 不論預設值的設定為何，均保留目的地資料表中的 null 值。 | False - 在適用的情況下，以預設值取代 null 值。 |
| `boolean TableLock` | 在大量複製作業期間，取得大量更新鎖定。 | False - 使用資料列鎖定。 |
| `boolean UseInternalTransaction` | 當設定為 `true` 時，大量複製作業的每個批次會在交易內發生。 如果 `SQLServerBulkCopy` 使用現有的連線 (如建構函式所指定)，則會發生 `SQLServerException`。  如果 `SQLServerBulkCopy` 建立了專用連線，則會為每個批次建立和認可交易。 | False - 無交易 |
| `int BatchSize` | 每個批次中的資料列數。 在每個批次的結尾，會將該批次中的資料列傳送到伺服器。<br /><br /> 當 `BatchSize` 資料列都已處理，或沒有更多資料列要傳送至目的地資料來源時，就會完成批次。  如果 `SQLServerBulkCopy` 執行個體在 `UseInternalTransaction` 選項設定為 `false` 的狀態下即已宣告，則資料列會一次傳送至該伺服器的 `BatchSize` 個資料列，但不採取任何交易相關的動作。 如果 `UseInternalTransaction` 設定為 `true`，則會在明確交易內執行資料列的每個批次。 | 0 - 表示每個 `writeToServer` 作業是單一批次 |
| `int BulkCopyTimeout` | 作業要在此秒數之前完成，之後即逾時。值為 0 表示沒有限制；大量複製則會無限期等候。 | 60 秒。 |
| `boolean allowEncryptedValueModifications` | 此選項是 Microsoft JDBC Driver 6.0 for SQL Server (或更高版本) 的功能。<br /><br /> 當設定為 `true` 時，`allowEncryptedValueModifications` 可供在資料表或資料庫之間大量複製加密資料，而不需要解密資料。 一般而言，應用程式會從一個資料表的加密資料行選取資料而不會解密資料 (應用程式會連線到資料庫，並將資料行加密設定關鍵字設定為停用)，接著會使用這個選項來大量插入資料，資料仍然加密。 如需詳細資訊，請參閱[搭配使用 Always Encrypted 與 JDBC 驅動程式](using-always-encrypted-with-the-jdbc-driver.md)。<br /><br /> 將 `allowEncryptedValueModifications` 設定為 `true` 時請小心，這可能會導致資料庫損毀，因為驅動程式不會檢查資料是否確實加密，或其是否使用與目標資料行相同的加密類型、演算法和金鑰正確加密。 |
  
 Getter 和 setter：  
  
| 方法 | 描述 |
| ------- | ----------- |
| `boolean isCheckConstraints()` | 指出在插入資料時是否要檢查條件約束。 |
| `void setCheckConstraints(boolean checkConstraints)` | 設定在插入資料時是否要檢查條件約束。 |
| `boolean isFireTriggers()` | 指出伺服器對於正在插入至此資料庫的資料列，是否應該引發插入觸發程序。 |
| `void setFireTriggers(boolean fireTriggers)` | 設定伺服器對於正在插入至此資料庫的資料列，是否應該設定為引發觸發程序。 |
| `boolean isKeepIdentity()` | 指出是否保留任何來源識別值。 |
| `void setKeepIdentity(boolean keepIdentity)` | 設定是否保留識別值。 |
| `boolean isKeepNulls()` | 指出是否保留目的地資料表中的 null 值，而不管預設值的設定為何，或是否應該取代為預設值 (如果適用的話)。 |
| `void setKeepNulls(boolean keepNulls)` | 設定是否保留目的地資料表中的 null 值，而不管預設值的設定為何，或是否應該取代為預設值 (如果適用的話)。 |
| `boolean isTableLock()` | 指出在大量複製作業期間，`SQLServerBulkCopy` 是否應該取得大量更新鎖定。 |
| `void setTableLock(boolean tableLock)` | 設定在大量複製作業期間，`SQLServerBulkCopy` 是否應該取得大量更新鎖定。 |
| `boolean isUseInternalTransaction()` | 表示大量複製作業的每個批次是否將在交易內發生。 |
| `void setUseInternalTranscation(boolean useInternalTransaction)` | 設定大量複製作業的每個批次是否將在交易內發生。 |
| `int getBatchSize()` | 取得每個批次的資料列數目。 在每個批次的結尾，會將該批次中的資料列傳送到伺服器。 |
| `void setBatchSize(int batchSize)` | 取得每個批次的資料列數目。 在每個批次的結尾，會將該批次中的資料列傳送到伺服器。 |
| `int getBulkCopyTimeout()` | 取得該作業要在逾時之前完成的秒數。 |
| `void  setBulkCopyTimeout(int timeout)` | 設定該作業要在逾時之前完成的秒數。 |
| `boolean isAllowEncryptedValueModifications()` | 指出 `allowEncryptedValueModifications` 設定已啟用或停用。 |
| `void setAllowEncryptedValueModifications(boolean allowEncryptedValueModifications)` | 設定用於 Always Encrypted 資料行大量複製的 `allowEncryptedValueModifications` 設定。 |
  
### <a name="isqlserverbulkrecord"></a>ISQLServerBulkRecord  

 `ISQLServerBulkRecord` 介面可用來建立類別，以從任何來源 (例如檔案) 讀入資料，並允許 `SQLServerBulkCopy` 執行個體使用該資料來大量載入 SQL Server 資料表。  
  
| 介面方法 | 描述 |
| ----------------- | ----------- |
| `set<Integer> getColumnOrdinals()` | 取得此資料記錄中呈現的每個資料行序數。 |
| `String getColumnName(int column)` | 取得指定資料行的名稱。 |
| `int getColumnType(int column)` | 取得指定資料行的 JDBC 資料類型。 |
| `int getPrecision(int column)`  | 取得指定資料行的有效位數。 |
| `object[] getRowData()` | 取得目前資料列的資料當做物件的陣列。<br /><br /> 每個物件都必須符合 Java 語言類型，其用來表示指定資料行的指定 JDBC 資料類型。  如需詳細資訊，請參閱[了解 JDBC 驅動程式資料類型](understanding-the-jdbc-driver-data-types.md)以取得適當對應。 |
| `int getScale(int column)` | 取得指定資料行的小數位數。 |
| `boolean isAutoIncrement(int column)` | 指出該資料行是否代表識別欄位。 |
| `boolean next()` | 前移到下一個資料列。 |
  
### <a name="sqlserverbulkcsvfilerecord"></a>SQLServerBulkCSVFileRecord  

`ISQLServerBulkRecord` 介面的簡單實作，其可用於從分隔的檔案中讀入基本 Java 資料類型，其中每一行代表一個資料列。  
  
實作注意事項和限制：  
  
1. 在任何指定資料列中允許的資料最大數量，會受可用記憶體限制，因為此資料一次只讀取一行。  
  
2. 不支援大型資料類型的資料流，例如 `varchar(max)`、`varbinary(max)`、`nvarchar(max)`、`sqlxml` 和 `ntext`。  
  
3. 該 CSV 檔案指定的分隔符號不應該出現在資料中的任何地方，如果是 Java 規則運算式中的限制字元，也應該要妥善逸出。  
  
4. 在 CSV 檔案的實作中，雙引號內視為資料的一部分。 例如，如果分隔符號是逗號，則 `hello,"world","hello,world"` 一行會視為具有四個值為 `hello`、`"world"`、`"hello` 和 `world"` 的資料行。  
  
5. 新行字元做為資料列結束字元使用，因此在資料的任何地方都不允許使用。  
  
| 建構函式 | 描述 |
| ----------- | ----------- |
| `SQLServerBulkCSVFileRecord(String fileToParse, String encoding, String delimiter, boolean firstLineIsColumnNames)` | 初始化 `SQLServerBulkCSVFileRecord` 類別的新執行個體，這會所提供分隔符號和編碼來剖析 `fileToParse` 的每一行。 如果 `firstLineIsColumnNames` 設定為 True，則檔案中的第一行會剖析為資料行名稱。  如果編碼為 NULL，將會使用預設編碼方式。 |
| `SQLServerBulkCSVFileRecord(String fileToParse, String encoding, boolean firstLineIsColumnNames)` | 初始化 `SQLServerBulkCSVFileRecord` 類別的新執行個體，這會以逗號作為分隔符號並以所提供編碼來剖析 `fileToParse` 的每一行。 如果 `firstLineIsColumnNames` 設定為 True，則檔案中的第一行會剖析為資料行名稱。  如果編碼為 NULL，將會使用預設編碼方式。 |
| `SQLServerBulkCSVFileRecord(String fileToParse, boolean firstLineIsColumnNames` | 初始化 `SQLServerBulkCSVFileRecord` 類別的新執行個體，這會以逗號作為分隔符號並以預設編碼來剖析 `fileToParse` 的每一行。 如果 `firstLineIsColumnNames` 設定為 True，則檔案中的第一行會剖析為資料行名稱。 |
  
| 方法 | 說明 |
| ------ | ----------- |
| `void addColumnMetadata(int positionInFile, String columnName, int jdbcType, int precision, int scale)` | 在該檔案中加入指定資料行的中繼資料。 |
| `void close()` | 釋放與檔案讀取器相關聯的任何資源。 |
| `void setTimestampWithTimezoneFormat(DateTimeFormatter dateTimeFormatter)` | 設定將時間戳記資料從檔案剖析為 `java.sql.Types.TIMESTAMP_WITH_TIMEZONE` 的格式。 |
| `void setTimestampWithTimezoneFormat(String dateTimeFormat)` | 設定將時間戳記資料從檔案剖析為 `java.sql.Types.TIME_WITH_TIMEZONE` 的格式。 |
| `void setTimeWithTimezoneFormat(DateTimeFormatter dateTimeFormatter)` | 設定將時間戳記資料從檔案剖析為 `java.sql.Types.TIME_WITH_TIMEZONE` 的格式。 |
| `void setTimeWithTimezoneFormat(String timeFormat)` | 設定將時間戳記資料從檔案剖析為 `java.sql.Types.TIME_WITH_TIMEZONE` 的格式。 |
  
## <a name="see-also"></a>另請參閱  

[JDBC 驅動程式概觀](overview-of-the-jdbc-driver.md)  
