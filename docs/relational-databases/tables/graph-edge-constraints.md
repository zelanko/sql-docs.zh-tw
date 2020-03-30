---
title: 圖形邊緣條件約束 | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- edge constraints [SQL Server]
- CONNECTION constraints
- edge constraints [Azure SQL Database]
- graph edge constraints
- SQL Graph
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current||=azuresqldb-current'
ms.openlocfilehash: ae08d5baef685a0b338ad574357230f01d3814cf
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "70873878"
---
# <a name="edge-constraints"></a>邊緣條件約束

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

邊緣條件約束可以用來強制執行資料完整性以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 圖形資料庫邊緣資料表中的特定語意。

## <a name="edge-constraints"></a><a name="Connection"></a> 邊緣條件約束

在第一版的圖形功能中，邊緣資料表不會強制執行邊緣端點的任何項目。 亦即，圖形資料庫中的邊緣可以將任何節點連線至任何其他節點，不論類型為何。

此版本引進邊緣條件約束，讓使用者將條件約束新增至其邊緣資料表，藉此強制執行特定語意同時維護資料完整性。 使用邊緣條件約束將新的邊緣新增至邊緣資料表時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會強制邊緣所嘗試連線的節點存在於正確的節點資料表。 如果邊緣仍然參考節點，則也確保無法卸除節點。

### <a name="edge-constraint-clauses"></a>邊緣條件約束子句

每個邊緣條件約束都是由一或多個邊緣條件約束子句所組成。 邊緣條件約束子句是由一對 FROM 與指定邊緣可連線的 TO 節點所組成。

假設您的圖形中有 `Product` 和 `Customer` 節點，而且您使用 `Bought` 邊緣來連線這些節點。 邊緣條件約束子句指定 FROM 和 TO 節點配對以及邊緣方向。 在此情況下，邊緣條件約束子句會是 `Customer` TO `Product`。 亦即，允許插入從 `Bought` 流向 `Customer` 的 `Product`。 嘗試插入從 `Product` 流向 `Customer` 的邊緣失敗。

- 邊緣條件約束子句包含強制執行邊緣條件約束的一對 FROM 與 TO 節點資料表。
- 使用者可以為每個邊緣條件約束指定將套用為分離的多個邊緣條件約束子句。
- 如果在單一邊緣資料表上建立多個邊緣條件約束，則邊緣必須滿足允許的 ALL 條件約束。

### <a name="indexes-on-edge-constraints"></a>邊緣條件約束的索引

建立邊緣條件約束並不會自動在邊緣資料表的 `$from_id` 和 `$to_id` 資料行上建立對應的索引。 如果您有點查閱查詢或 OLTP 工作負載，則建議在 `$from_id` 和 `$to_id` 配對上手動建立索引。

### <a name="on-delete-referential-actions-on-edge-constraints"></a>邊緣條件約束的 ON DELETE 參考動作
邊緣條件約束串聯式動作可讓使用者定義當使用者刪除指定邊緣所連接節點時，資料庫引擎將採取的動作。 可以定義下列參考動作：  
*NO ACTION*   
當您嘗試刪除具有連接邊緣的節點時，資料庫引擎會引發錯誤。  

*CASCADE*   
從資料庫刪除節點時，將會刪除連接邊緣。  

## <a name="working-with-edge-constraints"></a>使用邊緣條件約束

您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中定義邊緣條件約束。 邊緣條件約束只能定義在圖形邊緣資料表上。 若要建立、刪除或修改邊緣條件約束，您必須擁有資料表的 **ALTER** 權限。

### <a name="create-edge-constraints"></a>建立邊緣條件約束

下列範例顯示如何在新的資料表或現有的資料表上建立邊緣條件約束

#### <a name="to-create-an-edge-constraint-on-a-new-edge-table"></a>在新的邊緣資料表上建立邊緣條件約束

下列範例會在 **bought** 邊緣資料表上建立邊緣條件約束。

```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      ,CustomerName VARCHAR(100)
   )
AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      ,ProductName VARCHAR(100)
   )
AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
         ,CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product) ON DELETE NO ACTION
   )
   AS EDGE;
   ```

#### <a name="defining-referential-actions-on-a-new-edge-table"></a>在新的邊緣資料表上定義參考動作 

下列範例會在 **bought** 邊緣資料表上建立邊緣條件約束，並定義 ON DELETE CASCADE 參考動作。 

```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      ,CustomerName VARCHAR(100)
   )
AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      ,ProductName VARCHAR(100)
   )
AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
         ,CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product) ON DELETE CASCADE
   )
   AS EDGE;
   ```

#### <a name="to-add-edge-constraint-to-an-existing-edge-table"></a>將邊緣條件約束新增至現有的邊緣資料表

下列範例使用 ALTER TABLE 將邊緣條件約束新增至 **bought** 邊緣資料表。

```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY,
      , CustomerName VARCHAR(100)
   )
   AS NODE;
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
   )
   AS EDGE;
GO
ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Customer TO Product);
```  

#### <a name="create-a-new-edge-constraint-on-existing-edge-table-with-additional-edge-constraint-clauses"></a>使用額外的邊緣條件約束子句，在現有的邊緣資料表上建立新的邊緣條件約束

下列範例會使用 `ALTER TABLE` 命令以使用額外的邊緣條件約束子句在 **bought** 邊緣資料表上新增邊緣條件約束。
  
```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      , CustomerName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Supplier
   (
      ID INTEGER PRIMARY KEY
      , SupplierName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
      , CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
   )
   AS EDGE;
-- Drop the existing edge constraint first and then create a new one.
ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT;
GO
-- User ALTER TABLE to create a new edge constraint.
ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Customer TO Product, Supplier TO Product);
```  

在上述範例中，*EC_BOUGHT1* 條件約束中有兩個邊緣條件約束子句：一個將 **Customer** 連結至 **Product**，另一個將 **Supplier** 連結至 **Product**。 這兩個子句都會套用至分離中。 亦即，指定邊緣必須滿足邊緣資料表中允許之這兩個子句的任一個。

#### <a name="creating-a-new-edge-constraint-on-existing-edge-table-with-new-edge-constraint-clause"></a>使用新的邊緣條件約束子句，在現有的邊緣資料表上建立新的邊緣條件約束

下列範例會使用 `ALTER TABLE` 命令以使用新的邊緣條件約束子句在 **bought** 邊緣資料表上新增邊緣條件約束。
  
 ```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      , CustomerName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Supplier
   (
      ID INTEGER PRIMARY KEY
      , SupplierName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT,
         CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
   )
   AS EDGE;
GO
ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT1 CONNECTION (Supplier TO Product);
 ```  

在上述範例中，我們已在 **bought** 邊緣資料表上建立兩個不同的邊緣條件約束：*EC_BOUGHT* 和 *EC_BOUGHT1*。 這兩個邊緣條件約束會有不同的邊緣條件約束子句。 如果邊緣資料表上有一個以上的邊緣條件約束，則指定的邊緣必須滿足邊緣資料表中允許的 **ALL** 邊緣條件約束。 因為沒有邊緣可以滿足這裡的 *EC_BOUGHT* 和 *EC_BOUGHT1*，所以 **bought** 邊緣資料表必須空白。

若要在此邊緣資料表中成功插入，必須卸除其中一個邊緣條件約束，或必須卸除其中兩者，而且應該建立具有兩個邊緣條件約束子句的新邊緣條件約束。

```sql
-- Drop the existing edge constraint first and then create a new one.
ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT;
GO
ALTER TABLE bought DROP CONSTRAINT EC_BOUGHT1;
GO
ALTER TABLE bought ADD CONSTRAINT EC_BOUGHT_NEW CONNECTION (Customer TO Product, Supplier TO Product);
GO
```  

針對 **bought** 邊緣中允許的指定邊緣，它必須滿足 *EC_BOUGHT_NEW* 條件約束中的任一邊緣條件約束子句。 因此，將允許嘗試將有效的 **Customer** 連線至 **Product** 或將 **Supplier** 連線至 **Product** 節點的任何邊緣。

### <a name="delete-edge-constraints"></a>刪除邊緣條件約束

下列範例會先識別邊緣條件約束的名稱，然後刪除條件約束。  
  
```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      , CustomerName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   ) AS NODE;
GO
CREATE TABLE bought
   (
      PurchaseCount INT
      , CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product)
    )
    AS EDGE;
GO
-- Return the name of edge constraint.
SELECT name  
   FROM sys.edge_constraints  
   WHERE type = 'EC' AND parent_object_id = OBJECT_ID('bought');  
GO  
-- Delete the primary key constraint.  
ALTER TABLE bought
DROP CONSTRAINT EC_BOUGHT;
```  

### <a name="modify-edge-constraints"></a>修改邊緣條件約束

若要使用 Transact-SQL 來修改邊緣條件約束，您必須先刪除現有的邊緣條件約束，然後使用新的定義來重新建立。


### <a name="view-edge-constraints"></a>檢視邊緣條件約束

[!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。

此範例會針對 tempdb 資料庫中的 `bought` 邊緣資料表傳回所有邊緣條件約束和其屬性。  

```sql
-- CREATE node and edge tables
CREATE TABLE Customer
   (
      ID INTEGER PRIMARY KEY
      , CustomerName VARCHAR(100)
   )
   AS NODE;
GO
CREATE TABLE Supplier
   (
      ID INTEGER PRIMARY KEY
      , SupplierName VARCHAR(100)
   )
   AS NODE;
   GO
CREATE TABLE Product
   (
      ID INTEGER PRIMARY KEY
      , ProductName VARCHAR(100)
   )
   AS NODE;

-- CREATE edge table with edge constraints.
CREATE TABLE bought
   (
      PurchaseCount INT
      , CONSTRAINT EC_BOUGHT CONNECTION (Customer TO Product, Supplier TO Product)
   )
   AS EDGE;

-- Query sys.edge_constraints and sys.edge_constraint_clauses to view
-- edge constraint properties.
SELECT
   EC.name AS edge_constraint_name
   , OBJECT_NAME(EC.parent_object_id) AS edge_table_name
   , OBJECT_NAME(ECC.from_object_id) AS from_node_table_name
   , OBJECT_NAME(ECC.to_object_id) AS to_node_table_name
   , is_disabled
   , is_not_trusted
FROM sys.edge_constraints EC
   INNER JOIN sys.edge_constraint_clauses ECC
   ON EC.object_id = ECC.object_id
WHERE EC.parent_object_id = object_id('bought');
```  

## <a name="related-tasks"></a>相關工作

[CREATE TABLE (SQL Graph)](../../t-sql/statements/create-table-sql-graph.md)  
[ALTER TABLE table_constraint](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)  

如需 SQL Server 中圖形技術的相關資訊，請參閱 [SQL Server 和 Azure SQL Database 的圖表處理](../graphs/sql-graph-overview.md?view=sql-server-2017)。

