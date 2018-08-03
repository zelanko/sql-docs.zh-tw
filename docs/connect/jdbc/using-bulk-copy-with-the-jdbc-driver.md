---
title: 使用 JDBC Driver 使用大量複製 |Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 21e19635-340d-49bb-b39d-4867102fb5df
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 310545ee532baa5d8d1bac3acb804637bd1f44ed
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/27/2018
ms.locfileid: "39279199"
---
# <a name="using-bulk-copy-with-the-jdbc-driver"></a>搭配 JDBC Driver 使用大量複製
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Microsoft SQL Server 包含名為 **bcp** 的常用命令列公用程式，用於將大型檔案快速大量複製到 SQL Server 資料庫中的資料表或檢視。 SQLServerBulkCopy 類別可讓您在提供類似功能的 Java 中撰寫程式碼方案。 還有其他方法可以將資料載入 SQL Server 資料表 (例如 INSERT 陳述式)，但 SQLServerBulkCopy 提供顯著超越其他方法的效能優勢。  
  
 SQLServerBulkCopy 類別只可以用來將資料寫入 SQL Server 資料表。 但資料來源不限於 SQL Server；任何資料來源皆可使用，只要該資料可以用結果集、資料列集或 ISQLServerBulkRecord 實作來讀取。  
  
 使用 SQLServerBulkCopy 類別時，您可以執行：  
  
-   單一大量複製作業  
  
-   多項大量複製作業  
  
-   交易的大量複製作業  
  
> [!NOTE]  
>  使用 Microsoft JDBC 驅動程式 4.1 for SQL Server 或更早版本 (其不支援 SQLServerBulkCopy 類別) 時，您可以改為執行 SQL Server Transact-SQL BULK INSERT 陳述式。  
  
## <a name="bulk-copy-example-setup"></a>大量複製範例設定  
 SQLServerBulkCopy 類別只可以用來將資料寫入 SQL Server 資料表。 此文章中所顯示的程式碼範例會使用 SQL Server 範例資料庫 AdventureWorks。 若要避免變更現有資料表的程式碼範例，請將資料寫入您必須先建立的資料表。  
  
 BulkCopyDemoMatchingColumns 和 BulkCopyDemoDifferentColumns 資料表都採用 AdventureWorks Production.Products 資料表。 在使用這些資料表的程式碼範例中，會將來自 Production.Products 資料表的資料加入其中一個範例資料表。 當此範例說明如何將來源資料的資料行對應至目的地資料表時，會使用 BulkCopyDemoDifferentColumns 資料表；BulkCopyDemoMatchingColumns 也適用於大部分其他範例。  
  
 幾個程式碼範例示範如何使用一個 SQLServerBulkCopy 類別來寫入多個資料表。 在這些範例中，BulkCopyDemoOrderHeader 和 BulkCopyDemoOrderDetail 資料表用來當做目的地資料表。 這些資料表以 AdventureWorks 中的 Sales.SalesOrderHeader 和 Sales.SalesOrderDetail 資料表為基礎。  
  
> [!NOTE]  
>  提供的 SQLServerBulkCopy 程式碼範例，只是用來示範使用 SQLServerBulkCopy 的語法。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL INSERT … SELECT 陳述式來複製資料會更方便且更快速。  
  
###  <a name="BKMK_TableSetup"></a> 資料表設定  
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
>  當錯誤發生時，如果您需要復原全部或部分大量複製，您可以使用 SQLServerBulkCopy 受管理的交易，或執行現有交易中的大量複製作業。  
>   
>  如需詳細資訊，請參閱[異動和大量複製作業](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TransactionBulk)  
  
 執行大量複製作業的一般步驟如下：  
  
1.  連接到來源伺服器，並取得要複製的資料。 如果資料可從結果集物件或 ISQLServerBulkRecord 實作中擷取，則該資料也可以來自其他來源。  
  
2.  連線到目的地伺服器 (除非您想要 **SQLServerBulkCopy** 為您建立連線)。  
  
3.  建立 SQLServerBulkCopy 物件，透過 **setBulkCopyOptions** 設定所有必要的屬性。  
  
4.  呼叫 **setDestinationTableName** 方法，以表示大量插入作業的目標資料表。  
  
5.  呼叫其中一種 **writeToServer** 方法。  
  
6.  (選擇性) 透過 **setBulkCopyOptions** 更新屬性，並視需要再次呼叫 **writeToServer**。  
  
7.  呼叫 **close**，或將該大量複製作業包裝在 try-with-resources 陳述式之內。  
  
> [!CAUTION]  
>  我們建議來源和目標資料行的資料類型必須相符。 如果此資料類型不相符，SQLServerBulkCopy 便會嘗試將每個來源值轉換成目標資料類型。 轉換可能會影響效能，並也可能會導致未預期的錯誤。 例如，double 資料類型大多可以轉換成 decimal 資料類型，但並非總是如此。  
  
### <a name="example"></a>範例  
 下列應用程式示範如何使用 SQLServerBulkCopy 類別載入資料。 在此範例中，將使用一個結果集將資料從 SQL Server AdventureWorks 資料庫的 Production.Product 資料表複製到相同資料庫中的類似資料表。  
  
> [!IMPORTANT]  
>  除非您已如[資料表設定](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup) 中所述建立工作資料表，否則此範例不會執行。 本程式碼只是提供用來示範使用 SQLServerBulkCopy 的語法。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL INSERT … SELECT 陳述式來複製資料會更方便且更快速。  
  
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
 以下範例將示範如何使用 executeUpdate 方法來執行 BULK INSERT 陳述式。  
  
> [!NOTE]  
>  資料來源的檔案路徑是與伺服器相對的。 伺服器處理序必須存取該路徑，藉此順利完成大量複製作業。  
  
```java
try (Connection con = DriverManager.getConnection(connectionUrl);
        Statement stmt = con.createStatement()) {
    // Perform the BULK INSERT
    stmt.executeUpdate(
            "BULK INSERT Northwind.dbo.[Order Details] " + "FROM 'f:\\mydata\\data.tbl' " + "WITH ( FORMATFILE='f:\\mydata\\data.fmt' )");
}
```  
  
## <a name="multiple-bulk-copy-operations"></a>多項大量複製作業  
 您可以使用 SQLServerBulkCopy 類別的單一執行個體，執行多項大量複製作業。 如果複製作業在參數 (例如目的地資料表名稱) 之間變更，您必須在後續呼叫任何 writeToServer 方法之前更新它們，如下列範例所示。 除非已明確地變更，所有屬性值與之前指定執行個體上的大量複製作業維持相同。  
  
> [!NOTE]  
>  比起對每項作業使用個別的執行個體，使用 SQLServerBulkCopy 的相同執行個體來執行多項大量複製作業通常更有效率。  
  
 如果您使用相同的 SQLServerBulkCopy 物件執行數項大量複製作業時，並無限制來源或目標資訊在每項作業中是否相等或不同。 不過，當您每次寫入到伺服器時，必須確定資料行關聯資訊已正確設定。  
  
> [!IMPORTANT]  
>  除非您已如[資料表設定](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup) 中所述建立工作資料表，否則此範例不會執行。 本程式碼只是提供用來示範使用 SQLServerBulkCopy 的語法。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL INSERT … SELECT 陳述式來複製資料會更方便且更快速。  
  
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
  
##  <a name="BKMK_TransactionBulk"></a> 交易和大量複製作業  
 大量複製作業可以做為隔離作業或做為多步驟交易的一部分執行。 這第二個選項可讓您執行相同交易內的多項大量複製作業，以及執行其他資料庫作業 (例如插入、更新和刪除)，同時仍然能夠認可或回復整個交易。  
  
 根據預設，大量複製作業會做為隔離作業執行。 該複製作業會以非交易的方式進行，且沒有機會復原。 當錯誤發生時，如果您需要復原全部或部分大量複製，您可以使用 SQLServerBulkCopy 受管理的交易，或執行現有交易中的大量複製作業。  
  
### <a name="performing-a-non-transacted-bulk-copy-operation"></a>執行非交易大量複製作業  
 對於非交易大量複製作業在作業過程遭遇錯誤時的狀況，下列應用程式顯示此時會發生什麼事。  
  
 在該範例中，來源資料表及目的地資料表各自包含識別欄位，其名為 **ProductID**。 程式碼會先準備目的地資料表，方法是刪除所有資料列，然後插入單一資料列，且其 **ProductID** 已知存在於來源資料表中。 根據預設，在目的地資料表中，身分識別欄位的新值會針對每個加入的資料列產生。 在此範例中，當此連接開啟時，且其強制大量載入處理序改為使用來源資料表中的識別值時，就會設定某個選項。  
  
 此大量複製作業執行時的 **BatchSize** 屬性設定為 10。 當此作業遇到無效的資料列時，就會擲回例外狀況。 在第一個範例中，大量複製作業會為非交易作業。 發生錯誤前複製的所有批次均已認可；包含重複索引鍵的批次已回復，而且大量複製作業會在處理任何其他批次之前暫止。  
  
> [!NOTE]  
>  除非您已如[資料表設定](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup) 中所述建立工作資料表，否則此範例不會執行。 本程式碼只是提供用來示範使用 SQLServerBulkCopy 的語法。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL INSERT … SELECT 陳述式來複製資料會更方便且更快速。  
  
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
  
### <a name="performing-a-dedicated-build-copy-operation-in-a-transaction"></a>在交易中執行專屬的大量複製作業  
 根據預設，大量複製作業為其自己的交易。 當您想要執行專屬的大量複製作業時，請使用連接字串建立 SQLServerBulkCopy 的新執行個體。 在此案例中，大量複製作業會先建立，然後再認可或回復此交易。 您可以明確指定 **SQLServerBulkCopyOptions** 的 **UseInternalTransaction** 選項，以便明確地讓大量複製作業在自己的交易中執行，使得大量複製作業的每個批次在個別的交易內執行。  
  
> [!NOTE]  
>  由於不同的批次在不同交易中執行，如果大量複製作業期間發生錯誤時，目前的批次中的所有資料列將會回復，但是先前批次的資料列將保留在資料庫中。  
  
 當您指定**UseInternalTransaction**選項**BulkCopyNonTransacted**，大量複製作業包含在較大的外部交易。 當發生主要索引鍵違規錯誤時，整個交易便會回復，並且沒有任何資料列會加入目的地資料表。
 
```java
SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
copyOptions.setKeepIdentity(true);
copyOptions.setBatchSize(10);
copyOptions.setUseInternalTransaction(true);
```
  
### <a name="using-existing-transactions"></a>使用現有的交易  
 您可以傳遞交易已做為 SQLServerBulkCopy 建構函式之參數啟用的連接物件。 在此情況下，大量複製作業會在現有的交易中執行，而且不會變更交易狀態 (也就是它尚未認可或中止)。 這可讓應用程式在其他資料庫作業的交易中包含大量複製作業。 如果因為發生錯誤，或大量複製應該要以可回復的較大程序之一部分執行，使得您需要復原整個大量複製作業，則您可以在大量複製作業之後的任何時間點，執行連接物件中的回復。  
  
 下列應用程式與 **BulkCopyNonTransacted** 類似，但有一個例外：在此範例中，大量複製作業包含在較大的外部交易中。 當發生主要索引鍵違規錯誤時，整個交易便會回復，並且沒有任何資料列會加入目的地資料表。
  
> [!NOTE]  
>  除非您已如[資料表設定](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#BKMK_TableSetup) 中所述建立工作資料表，否則此範例不會執行。 本程式碼只是提供用來示範使用 SQLServerBulkCopy 的語法。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL INSERT … SELECT 陳述式來複製資料會更方便且更快速。  
  
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
  
### <a name="bulk-copy-from-a-csv-file"></a>CSV 檔案中的大量複製  
 下列應用程式示範如何使用 SQLServerBulkCopy 類別載入資料。 在此範例中，將使用一個 CSV 檔案將從 SQL Server AdventureWorks 資料庫的 Production.Product 資料表匯出的資料複製到該資料庫中的類似資料表。  
  
> [!IMPORTANT]  
>  除非您已如[資料表設定](../../ssms/download-sql-server-management-studio-ssms.md) 中所述建立工作資料表來取得它，否則此範例不會執行。  
  
1.  開啟 **SQL Server Management Studio**，並連線到具有 AdventureWorks 資料庫的 SQL Server。  
  
2.  展開此資料庫，以滑鼠右鍵按一下 AdventureWorks 資料庫，選取 [工作] 和 [匯出資料]…  
  
3.  針對該 [資料來源]，請選取 [資料來源]，這可讓您連線到 SQL Server (例如 SQL Server Native Client 11.0)，然後檢查設定並按一下 [下一步]  
  
4.  針對該 [目的地]，請選取 [一般檔案目的地]，然後輸入 [檔案名稱] 為目的地，例如 C:\Test\TestBulkCSVExample.csv。 請檢查 [格式] 為 [分隔]，且 [文字限定詞] 為 [無]，並啟用 [第一個資料列的資料行名稱]，然後選取 [下一步]  
  
5.  選取 [寫入查詢來指定要傳送的資料]，然後按一下 [下一步]。  輸入 [SQL 陳述式] 如：SELECT ProductID, Name, ProductNumber FROM Production.Product，然後按一下 [下一步]  
  
6.  檢查設定：您可以將資料列分隔符號保留為 {CR}{LF}，並將資料行分隔符號保留為逗號 {,}。  選取 [編輯對應]… 然後檢查資料 [類型] 對於每個資料行是否都正確 (例如檢查 ProductID 是否為整數，以及檢查其他資料行是否為 Unicode 字串)。  
  
7.  直接跳到 [完成] 並執行匯出。  
  
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
  
### <a name="bulk-copy-with-always-encrypted-columns"></a>使用 Always Encrypted 資料行的大量複製  
 從 Microsoft JDBC Driver 6.0 for SQL Server，大量複製支援 Always Encrypted 資料行。  
  
 根據大量複製選項，以及加密 JDBC 驅動程式可能會以透明的方式解密和加密的資料，或它的來源和目的地資料表的型別可能會傳送加密的資料現狀。 比方說，當大量資料複製到未加密的資料行的加密資料行，驅動程式以透明的方式解密資料傳送到 SQL Server 之前。 同樣地複製大量資料時未加密的資料行 （或從 CSV 檔案） 來加密資料行，驅動程式以透明方式加密資料傳送到 SQL Server 之前。 如果同時在來源和目的地會加密，然後視**allowEncryptedValueModifications**大量複製選項，為是或會解密資料，然後將它加密再傳送到 SQL Server 驅動程式會傳送資料。  
  
 如需詳細資訊，請參閱 < **allowEncryptedValueModifications**大量複製選項，以及[JDBC 驅動程式搭配使用 Always Encrypted](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。  
  
> [!IMPORTANT]  
>  Microsoft JDBC Driver 6.0 for SQL Server 大量複製資料從 CSV 檔案，來加密資料行時的限制：  
>   
>  日期和時間類型支援只有 TRANSACT-SQL 預設字串常值格式  
>   
>  DATETIME 和 SMALLDATETIME 資料型別不支援  
  
## <a name="bulk-copy-api-for-jdbc-driver"></a>適用於 JDBC 驅動程式的大量複製 API  
  
### <a name="sqlserverbulkcopy"></a>SQLServerBulkCopy  
 讓您有效率地將其他來源的資料大量載入 SQL Server 資料表。  
  
 Microsoft SQL Server 包含名為 bcp 的常用命令提示字元公用程式，不管是在單一伺服器上或伺服器之間，都可用於將資料從一個資料表移動到另一個。 SQLServerBulkCopy 類別可讓您在提供類似功能的 Java 中撰寫程式碼方案。 還有其他方法可以將資料載入 SQL Server 資料表 (例如 INSERT 陳述式)，但 SQLServerBulkCopy 提供顯著超越其他方法的效能優勢。  
  
 SQLServerBulkCopy 類別只可以用來將資料寫入 SQL Server 資料表。 不過，資料來源不限於 SQL Server；任何資料來源皆可使用，只要該資料可以用結果集執行實體或 ISQLServerBulkRecord 實作來讀取。  
  
|建構函式|Description|  
|-----------------|-----------------|  
|SQLServerBulkCopy(Connection)|使用指定的 SQLServerConnection 開啟執行個體，以初始化 SQLServerBulkCopy 類別的新執行個體。 如果此連接已啟用交易，將會在該交易內執行複製作業。|  
|SQLServerBulkCopy (字串 connectionURL)|初始化並根據提供的 connectionURL 開啟 SQLServerConnection 的新執行個體。 此建構函式會使用 SQLServerConnection 初始化 SQLServerBulkCopy 類別的新執行個體。|  
  
|屬性|Description|  
|--------------|-----------------|  
|字串 DestinationTableName|該伺服器的目的地資料表名稱。<br /><br /> 如果呼叫 writeToServer 時尚未設定 DestinationTableName，便會擲回 SQLServerException。<br /><br /> DestinationTableName 名稱有三個部分 (\<資料庫>.\<主控結構描述 >.\<名稱>)。 如果您要加以選擇，則可以用該資料表的資料庫和主控結構描述來限定該資料表名稱。 不過，如果該資料表名稱使用底線 ("_") 或任何其他特殊字元，您就必須使用括起來的括號逸出該名稱。 如需詳細資訊，請參閱《SQL Server 線上叢書》中的＜識別碼＞。|  
|ColumnMappings|在資料來源的資料行和目的地的資料行之間，資料行對應可定義其關聯性。<br /><br /> 如果未定義對應，則該資料行會根據位置順序隱含地對應。 若要執行這項操作，則來源和目標結構描述必須相符。 如果不相符，將會擲回例外狀況。<br /><br /> 如果此對應不是空的，就不必指定存在於該資料來源的每個資料行。 會忽略未對應的部分。<br /><br /> 您可以依名稱或序數找到來源和目標資料行。|  
  
|方法|Description|  
|------------|-----------------|  
|Void addColumnMapping （int sourceColumn (int destinationColumn）|加入新的資料行對應，用來指定來源和目的地資料行的序數。|  
|Void addColumnMapping （int sourceColumn (字串 destinationColumn）|加入新的資料行對應，方法是使用來源資料行的序數和目的地資料行的資料行名稱。|  
|Void addColumnMapping （字串 sourceColumn (int destinationColumn）|加入新的資料行對應，方法是使用資料行名稱來描述來源資料行與序數，以指定此目的地資料行。|  
|Void addColumnMapping （字串 sourceColumn，字串 destinationColumn）|加入新的資料行對應，方法是使用資料行名稱來指定來源和目的地資料行。|  
|Void clearColumnMappings()|清除此資料行對應的內容。|  
|Void 的 close （)|關閉 SQLServerBulkCopy 執行個體。|  
|SQLServerBulkCopyOptions getBulkCopyOptions()|擷取 SQLServerBulkCopyOptions 的目前集合。|  
|String getDestinationTableName()|擷取目的地資料表的目前名稱。|  
|Void setBulkCopyOptions(SQLServerBulkCopyOptions copyOptions)|根據提供的選項，更新 SQLServerBulkCopy 執行個體的行為。|  
|Void setDestinationTableName(String tableName)|設定目的地資料表的名稱。|  
|Void writeToServer(ResultSet sourceData)|將提供之結果集的所有資料列複製到 SQLServerBulkCopy 物件的 DestinationTableName 屬性所指定的目的地資料表。|  
|Void writeToServer(RowSet sourceData)|將提供的資料列集之所有資料列複製到 SQLServerBulkCopy 物件的 DestinationTableName 屬性所指定的目的地資料表。|  
|Void writeToServer(ISQLServerBulkRecord sourceData)|將提供之 ISQLServerBulkRecord 實作的所有資料列複製到 SQLServerBulkCopy 物件的 DestinationTableName 屬性所指定的目的地資料表。|  
  
### <a name="sqlserverbulkcopyoptions"></a>SQLServerBulkCopyOptions  
 控制 writeToServer 方法在 SQLServerBulkCopy 執行個體中的行為模式的設定集合物件。  
  
|建構函式|Description|  
|-----------------|-----------------|  
|SQLServerBulkCopyOptions()|使用所有設定的預設值，初始化 SQLServerBulkCopyOptions 類別的新執行個體。|  
  
 Getter 和 Setter 主要用於下列選項：  
  
|選項|Description|預設|  
|------------|-----------------|-------------|  
|布林 CheckConstraints|在插入資料時檢查條件約束。|False-不檢查條件約束|  
|布林 FireTriggers|若已指定，則會導致此伺服器對於正在插入至此資料庫的資料列，引發插入觸發程序。|False - 不引發任何觸發程序。|  
|布林 KeepIdentity|保留來源識別值。|False - 由目的地指派的識別值。|  
|布林 KeepNulls|不論預設值的設定為何，均保留目的地資料表中的 null 值。|False - 在適用的情況下，以預設值取代 null 值。|  
|布林 TableLock|在大量複製作業期間，取得大量更新鎖定。|False - 使用資料列鎖定。|  
|布林 UseInternalTransaction|若已指定，則大量複製作業的每個批次將在交易內發生。 如果 SQLServerBulkCopy 使用現有的連接 (如建構函式所指定)，將會發生 SQLServerException。  如果 SQLServerBulkCopy 建立了專用的連接，將會啟用交易。|False - 無交易|  
|Int BatchSize|每個批次中的資料列數。 在每個批次的結尾，會將該批次中的資料列傳送到伺服器。<br /><br /> 當 BatchSize 資料列都已處理，或沒有更多資料列要傳送至目的地資料來源時，就會完成批次。  如果 SQLServerBulkCopy 執行個體在 UseInternalTransaction 選項未作用中的狀態下即已宣告，則資料列會一次傳送至該伺服器 BatchSize 資料列，但不採取任何交易相關的動作。 如果 UseInternalTransaction 處於作用中時，則每個資料列批次都是以個別的交易插入。|0 - 表示每個 writeToServer 作業是單一批次。|  
|Int BulkCopyTimeout|該作業要在此秒數之前完成，之後即逾時。值為 0 表示沒有限制；大量複製則會無限期等候。|60 秒。|  
|布林 allowEncryptedValueModifications|此選項是使用 Microsoft JDBC Driver 6.0 （或更高版本） for SQL Server。<br /><br /> 指定時， **allowEncryptedValueModifications**可讓您無須解密資料大量複製的資料表或資料庫之間的加密資料。 一般而言，應用程式會選取從加密資料行從一個資料表的資料而不需解密 （應用程式會連接到資料庫資料行加密設定關鍵字設定為停用） 的資料，並接著會使用這個選項來大量插入資料，這仍屬於加密。 如需詳細資訊，請參閱[搭配使用 Always Encrypted 與 JDBC 驅動程式](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。<br /><br /> 指定 **allowEncryptedValueModifications** 時請小心，這可能會導致資料庫損毀，因為驅動程式不會檢查資料是否確實加密，或是否使用與目標資料行相同的加密類型、演算法和金鑰正確加密。||  
  
 Getter 和 setter:  
  
|方法|Description|  
|-------------|-----------------|  
|布林 isCheckConstraints()|指出是否要檢查在插入資料時的條件約束。|  
|Void setCheckConstraints(Boolean checkConstraints)|設定條件約束是否要檢查在插入資料時。|  
|布林 isFireTriggers()|指出伺服器是否應該引發要插入至資料庫的資料列的 insert 觸發程序。|  
|Void setFireTriggers(Boolean fireTriggers)|設定是否應該設定引發觸發程序的資料列插入資料庫的伺服器。|  
|布林 isKeepIdentity()|指出要保留的任何來源識別值。|  
|Void setKeepIdentity(Boolean keepIdentity)|設定要保留識別值。|  
|布林 isKeepNulls()|指出是否要保留的設定預設值，不論與目的地資料表中的 null 值，或如果他們應該取代的預設值 （如果適用的話）。|  
|Void setKeepNulls(Boolean keepNulls)|設定是否要保留的設定預設值，不論與目的地資料表中的 null 值，或如果他們應該取代的預設值 （如果適用的話）。|  
|布林 isTableLock()|指出 SQLServerBulkCopy 是否應該在大量複製作業期間取得大量更新鎖定。|  
|Void setTableLock(Boolean tableLock)|設定是否使用 SQLServerBulkCopy 應該在大量複製作業期間取得大量更新鎖定。|  
|布林 isUseInternalTransaction()|表示大量複製作業的每個批次是否將在交易內發生。|  
|Void setUseInternalTranscation(Boolean useInternalTransaction)|設定大量複製作業的每個批次是否將在交易內發生。|  
|Int getBatchSize()|取得每個批次的資料列數目。 在每個批次的結尾，會將該批次中的資料列傳送至伺服器|  
|Void setBatchSize(int batchSize)|取得每個批次的資料列數目。 在每個批次的結尾，會將該批次中的資料列傳送到伺服器。|  
|Int getBulkCopyTimeout()|取得該作業要在逾時之前完成的秒數。|  
|Void setBulkCopyTimeout(int timeout)|設定該作業要在逾時之前完成的秒數。|  
|布林 isAllowEncryptedValueModifications()|指出 allowEncryptedValueModifications 設定是否要啟用或停用。|  
|void setAllowEncryptedValueModifications(boolean allowEncryptedValueModifications)|設定 allowEncryptedValueModifications 用於使用 Always Encrypted 資料行的大量複製。|  
  
### <a name="isqlserverbulkrecord"></a>ISQLServerBulkRecord  
 ISQLServerBulkRecord 介面可用來建立類別，從任何來源 (例如檔案) 的資料中讀取，並允許 SQLServerBulkCopy 執行個體以該資料大量載入 SQL Server 資料表。  
  
|介面方法|Description|  
|-----------------------|-----------------|  
|設定\<整數 > getColumnOrdinals()|取得此資料記錄中呈現的每個資料行序數。|  
|字串 getColumnName(int column)|取得指定資料行的名稱。|  
|Int getColumnType （int 資料行）|取得指定資料行的 JDBC 資料類型。|  
|Int getPrecision （int 資料行）|取得指定資料行的有效位數。|  
|物件 [] getRowData()|取得目前資料列的資料當做物件的陣列。<br /><br /> 每個物件都必須符合 Java 語言類型，其用來表示指定資料行的指定 JDBC 資料類型。  如需詳細資訊，請參閱適當對應的《了解 JDBC Driver 資料類型》。|  
|Int getScale （int 資料行）|取得指定資料行的小數位數。|  
|布林 isAutoIncrement （int 資料行）|指出該資料行是否代表識別欄位。|  
|布林值的 next （)|前移到下一個資料列。|  
  
### <a name="sqlserverbulkcsvfilerecord"></a>SQLServerBulkCSVFileRecord  
 ISQLServerBulkRecord 介面的簡單實作，可用於從分隔的檔案中讀取基本 Java 資料類型，其中每一行代表一個資料列。  
  
 實作注意事項和限制：  
  
1.  在任何指定資料列中允許的資料最大數量，會受可用記憶體限制，因為此資料一次只讀取一行。  
  
2.  不支援大型資料類型的資料流，例如 varchar(max)、varbinary (max)、nvarchar (max)、sqlxml、ntext。  
  
3.  該 CSV 檔案指定的分隔符號不應該出現在資料中的任何地方，如果是 Java 規則運算式中的限制字元，也應該要妥善逸出。  
  
4.  在 CSV 檔案的實作中，雙引號內視為資料的一部分。 例如，如果分隔符號是逗號，則這一行：hello,”world”,”hello,world” 會被視為擁有四個資料行，其值為 hello、"world"、"hello 和 world"。  
  
5.  新行字元做為資料列結束字元使用，因此在資料的任何地方都不允許使用。  
  
|建構函式|Description|  
|-----------------|-----------------|  
|SQLServerBulkCSVFileRecord （字串 fileToParse，字串編碼，字串分隔符號，則為 True firstLineIsColumnNamesSQLServerBulkCSVFileRecord （字串、 字串、 字串、 布林值）|初始化 SQLServerBulkCSVFileRecord 類別的新執行個體，這會以提供的分隔符號和編碼，剖析 fileToParse 的每一行。 如果 firstLineIsColumnNames 設為 True 時，檔案中的第一行會剖析為資料行名稱。  如果編碼為 NULL，將會使用預設編碼方式。|  
|SQLServerBulkCSVFileRecord (字串 fileToParse，字串編碼，則為 True firstLineIsColumnNamesSQLServerBulkCSVFileRecord (String，String，boolean)|初始化 SQLServerBulkCSVFileRecord 類別的新執行個體，這會以逗點做為分隔符號和以提供的編碼，剖析 fileToParse 的每一行。 如果 firstLineIsColumnNames 設為 True 時，檔案中的第一行會剖析為資料行名稱。  如果編碼為 NULL，將會使用預設編碼方式。|  
|SQLServerBulkCSVFileRecord (字串 fileToParse，布林 firstLineIsColumnNamesSQLServerBulkCSVFileRecord （字串、 布林值）|初始化 SQLServerBulkCSVFileRecord 類別的新執行個體，這會以逗點做為分隔符號和以預設的編碼，剖析 fileToParse 的每一行。 如果 firstLineIsColumnNames 設為 True 時，檔案中的第一行會剖析為資料行名稱。|  
  
|方法|Description|  
|------------|-----------------|  
|Void addColumnMetadata （int positionInFile、 字串 columnName、 int jdbcType、 int 有效位數、 int 小數位數）|在該檔案中加入指定資料行的中繼資料。|  
|Void 的 close （)|釋放與檔案讀取器相關聯的任何資源。|  
|Void setTimestampWithTimezoneFormat (DateTim eFormatter dateTimeFormatter|設定將時間戳記資料從檔案剖析為 java.sql.Types.TIMESTAMP_WITH_TIMEZONE 的格式。|  
|Void setTimestampWithTimezoneFormat(String dateTimeFormat)setTimeWithTimezoneFormat(DateTimeFormatter)|設定將時間資料從檔案剖析為 java.sql.Types.TIME_WITH_TIMEZONE 的格式。|  
|Void setTimeWithTimezoneFormat (DateTimeForm 散佈 dateTimeFormatter)|設定將時間資料從檔案剖析為 java.sql.Types.TIME_WITH_TIMEZONE 的格式。|  
|Void setTimeWithTimezoneFormat(String timeFormat)|設定將時間資料從檔案剖析為 java.sql.Types.TIME_WITH_TIMEZONE 的格式。|  
  
## <a name="see-also"></a>另請參閱  
 [JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
