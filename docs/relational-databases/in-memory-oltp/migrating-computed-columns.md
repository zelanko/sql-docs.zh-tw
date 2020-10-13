---
title: 移轉計算資料行 | Microsoft Docs
description: 了解如何模擬記憶體最佳化資料表中的計算資料行。 評估移轉之後是否需要計算資料行功能。
ms.custom: ''
ms.date: 12/17/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 64a9eade-22c3-4a9d-ab50-956219e08df1
author: MightyPen
ms.author: genemi
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 1ff95c2fad217e0592e82c6e7bf034813931e758
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91863840"
---
# <a name="migrating-computed-columns"></a>移轉計算資料行

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

記憶體最佳化資料表中不支援計算資料行。 但是，您可以模擬計算資料行。

從 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 開始，經記憶體最佳化的資料表和索引支援計算資料行。

當您將以磁碟為基礎的資料表移轉至記憶體最佳化資料表時，必須考慮保存計算資料行的需求。 記憶體最佳化資料表和原生編譯預存程序之間的不同效能特性可能會消除保存資料行的需求。  
  
## <a name="non-persisted-computed-columns"></a>非保存計算資料行  
 若要模擬非保存計算資料行的影響，請在記憶體最佳化的資料表上建立檢視表。 在定義檢視的 SELECT 陳述式中，將計算資料行定義加入檢視。 除了在原生編譯預存程序中，使用源自這個計算資料行的值所進行的查詢必須從檢視讀取。 在原生編譯預存程序中，您應該依據計算資料行的定義更新任何 SELECT、UPDATE 或 DELETE 陳述式。  
  
```sql  
-- Schema for the table dbo.OrderDetails:  
-- OrderId int not null primary key,  
-- ProductId int not null,  
-- SalePrice money not null,  
-- Quantity int not null,  
-- Total money not null  
--  
-- Total is computed as SalePrice * Quantity and is not persisted.  
CREATE VIEW dbo.v_order_details AS  
   SELECT  
      OrderId,  
      ProductId,  
      SalePrice,  
      Quantity,  
      Quantity * SalePrice AS Total  
   FROM dbo.order_details  
```  
  
## <a name="persisted-computed-columns"></a>保存計算資料行  
 若要模擬保存計算資料行的影響，請建立預存程序以插入資料表，再建立另一個預存程序以更新資料表。 在插入或更新資料表時，請叫用這些預存程序以執行這些工作。 在預存程序中，可根據輸入計算位於計算欄位中的值，這與計算資料行在原始以磁碟為基礎之資料表的定義十分類似。 然後，插入或更新預存程序內所需的資料表。  
  
```sql  
-- Schema for the table dbo.OrderDetails:  
-- OrderId int not null primary key,  
-- ProductId int not null,  
-- SalePrice money not null,  
-- Quantity int not null,  
-- Total money not null  
--  
-- Total is computed as SalePrice * Quantity and is persisted.  
-- we need to create insert and update procedures to calculate Total.  

CREATE PROCEDURE sp_insert_order_details   
@OrderId int, @ProductId int, @SalePrice money, @Quantity int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (LANGUAGE = N'english', TRANSACTION ISOLATION LEVEL = SNAPSHOT)  

-- compute the value here.   
-- this stored procedure works with single rows only.  
-- for bulk inserts, accept a table-valued parameter into the stored procedure  
-- and use an INSERT INTO SELECT statement.  

DECLARE @total money = @SalePrice * @Quantity  
INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)  
VALUES (@OrderId, @ProductId, @SalePrice, @Quantity, @total)  
END  
GO  
  
CREATE PROCEDURE sp_update_order_details_by_id  
@OrderId int, @ProductId int, @SalePrice money, @Quantity int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (LANGUAGE = N'english', TRANSACTION ISOLATION LEVEL = SNAPSHOT)  

-- compute the value here.   
-- this stored procedure works with single rows only.  

DECLARE @total money = @SalePrice * @Quantity  
UPDATE dbo.OrderDetails   
SET ProductId = @ProductId, SalePrice = @SalePrice, Quantity = @Quantity, Total = @total  
WHERE OrderId = @OrderId  
END  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [移轉至 In-Memory OLTP](./plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)  
  
