---
title: 移轉觸發程序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ad5385c5-5a50-40ca-a319-97d5606b8511
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7df393f26523991abafded74ded242390cb0e3b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63071466"
---
# <a name="migrating-triggers"></a>移轉觸發程序
  本主題討論 DDL 和 DML 觸發程序以及記憶體最佳化的資料表。  
  
 LOGON 觸發程序是定義成發生 LOGON 事件時引發。 LOGON 觸發程序不會影響記憶體最佳化的資料表。  
  
## <a name="ddl-triggers"></a>DDL 觸發程序  
 DDL 觸發程序是定義成對其定義所在的資料庫或伺服器執行 CREATE、ALTER、DROP、GRANT、DENY、REVOKE 或 UPDATE STATISTICS 陳述式時引發的觸發程序。  
  
 如果資料庫或伺服器有一個或多個 DDL 觸發程序定義於 CREATE_TABLE 或包含該等觸發程序的任何事件群組，您便無法建立記憶體最佳化的資料表。 如果資料庫或伺服器有一個或多個 DDL 觸發程序定義於 DROP_TABLE 或包含該等觸發程序的任何事件群組，您便無法卸除記憶體最佳化的資料表。  
  
 如果有一個或多個 DDL 觸發程序位於 CREATE_PROCEDURE、DROP_PROCEDURE 或包含這些事件的任何事件群組，您便無法建立原生編譯預存程序。  
  
## <a name="dml-triggers"></a>DML 觸發程序  
 記憶體最佳化的資料表不能定義 DML 觸發程序。 不過，如果您明確地使用預存程序插入、更新或刪除資料，記憶體中的 OLTP 便能讓您達到類似於 DML 觸發程序的效果。 若您的系統包含特定查詢，請將其轉換為改用這些預存程序來模擬 DML 觸發程序的效果。  
  
 視觸發程序事件 (FOR/AFTER 或 INSTEAD OF) 而定，您也許可將觸發程序的內容納入到對該資料表執行 INSERT、UPDATE 或 DELETE 的適當預存程序。 例如，在移轉 AFTER INSERT 觸發程序時，您可以將此觸發程序的內容納入到適當的 INSERT 陳述式後面，藉此更改執行插入作業的預存程序。  
  
 您可以使用解譯的預存程序或原生編譯預存程序。 解譯的預存程序中大多數的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 建構皆可對記憶體最佳化的資料表執行。 不過，原生編譯預存程序僅支援 [!INCLUDE[tsql](../../includes/tsql-md.md)] 建構的子集。 如需記憶體[!INCLUDE[tsql](../../includes/tsql-md.md)]優化資料表支援的詳細資訊，請參閱[使用已解讀的 Transact-sql 存取記憶體優化資料表](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)。 如需原[!INCLUDE[tsql](../../includes/tsql-md.md)]生編譯預存程式中支援的詳細資訊，請參閱[記憶體內部 OLTP 不支援的 transact-sql 結構](transact-sql-constructs-not-supported-by-in-memory-oltp.md)。  
  
 以下是針對記憶體最佳化的資料表模擬 DML 觸發程序行為的簡單範例。  
  
 資料庫包含下列物件，編寫成 CREATE TABLE、CREATE TRIGGER 和 CREATE PROCEDURE 陳述式：  
  
```sql  
CREATE TABLE OrderDetails  
(  
   OrderId int not null primary key,  
   ProductId int not null,  
   SalePrice money not null,  
   Quantity int not null,  
   Total money not null,  
   IsDeleted bit not null DEFAULT (0)  
)  
GO  
  
CREATE TRIGGER tr_order_details_insteadof_insert  
ON OrderDetails  
INSTEAD OF INSERT AS  
BEGIN  
   DECLARE @pid int, @qty_buy int, @qty_remain int  
   SELECT @pid = ProductId, @qty_buy = Quantity FROM inserted  
   SELECT @qty_remain = Quantity FROM Inventory WHERE ProductId = @pid  
   IF (@qty_remain <= @qty_buy)  
      THROW 51000, N'Insufficient inventory!', 1  
   ELSE  
   BEGIN  
      INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)   
      SELECT OrderId, ProductId, SalePrice, Quantity, Total FROM inserted  
      UPDATE Inventory SET Quantity = Quantity - @qty_buy WHERE ProductId = @pid  
   END  
END  
GO  
  
CREATE TRIGGER tr_order_details_after_update  
ON OrderDetails  
AFTER UPDATE AS  
BEGIN  
   INSERT INTO UpdateNotifications (OrderId, UpdateTime) SELECT OrderId, GETDATE() FROM inserted     
END  
GO  
  
CREATE PROCEDURE sp_insert_order_details   
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @total money  
AS BEGIN  
   INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)  
   VALUES (@OrderId, @ProductId, @SalePrice, @Quantity, @total)  
END  
GO  
  
CREATE PROCEDURE sp_update_order_details_by_id  
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @Total money  
AS BEGIN  
   UPDATE dbo.OrderDetails   
   SET ProductId = @ProductId, SalePrice = @SalePrice, Quantity = @Quantity, Total = @total  
   WHERE OrderId = @OrderId  
END  
GO  
```  
  
 下列物件的功能等同於移轉之前的狀態：  
  
```sql  
CREATE TABLE OrderDetails  
(  
   OrderId int not null PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 1048576),  
   ProductId int not null,  
   SalePrice money not null,  
   Quantity int not null,  
   Total money not null,  
   IsDeleted bit not null DEFAULT (0)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
GO  
  
CREATE TABLE Inventory  
(  
   ProductId int not null PRIMARY KEY NONCLUSTERED,  
   Quantity int not null  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
GO  
  
CREATE TABLE UpdateNotifications  
(  
   OrderId int not null,  
   UpdateTime datetime2 not null  
   CONSTRAINT pk_updateNotifications PRIMARY KEY NONCLUSTERED (OrderId, UpdateTime)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
GO  
  
CREATE PROCEDURE sp_insert_order_details   
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @total money  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'English')  
   DECLARE @qty_remain int  
   SELECT @qty_remain = Quantity FROM dbo.Inventory WHERE ProductId = @ProductId  
   IF (@qty_remain <= @Quantity)  
      THROW 51000, N'Insufficient inventory!', 1  
   ELSE  
   BEGIN  
      INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)   
      VALUES (@OrderId, @ProductId, @SalePrice, @Quantity, @total)  
      UPDATE dbo.Inventory SET Quantity = Quantity - @Quantity WHERE ProductId = @ProductId  
   END  
END  
GO  
  
CREATE PROCEDURE sp_update_order_details_by_id  
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @Total money  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'English')  
   UPDATE dbo.OrderDetails   
   SET ProductId = @ProductId, SalePrice = @SalePrice, Quantity = @Quantity, Total = @total  
   WHERE OrderId = @OrderId  
   INSERT INTO dbo.UpdateNotifications (OrderId, UpdateTime) VALUES (@OrderId, GETDATE())  
END  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [移轉至 In-Memory OLTP](migrating-to-in-memory-oltp.md)  
  
  
