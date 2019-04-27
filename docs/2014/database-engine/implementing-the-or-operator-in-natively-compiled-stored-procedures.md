---
title: 實作 OR 運算子，原生編譯的預存程序 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f2528e74-2b1c-48cb-861b-c4e57b51ac35
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 64de082cd12c967f3f3c90ca3cb99c51985ed41a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62778909"
---
# <a name="implementing-the-or-operator-in-natively-compiled-stored-procedures"></a>在原生編譯的預存程序中實作 OR 運算子
  原生編譯預存程序內部的查詢述詞中不支援 OR 運算子。 由於原生編譯預存程序內部的查詢述詞中也不支援 NOT 運算子，所以無法透過單獨使用同等的邏輯運算子來模擬 OR 運算子的效果。 不過，OR 運算子的效果可透過記憶體最佳化資料表變數加以模擬。  
  
## <a name="or-operator-in-where-clause"></a>WHERE 子句中的 OR 運算子  
 如果您在 WHERE 子句中有 OR 運算子，您可以使用下列方法模擬其行為：  
  
1.  使用適當的結構描述建立記憶體最佳化資料表變數。 這需要預先定義的記憶體最佳化資料表類型。  
  
2.  從最上層 OR 運算子開始，根據 OR 運算子所聯結的述詞將 WHERE 子句分成兩部分。 如果您在 WHERE 子句中有一個以上的 OR 運算子，您可能必須多次執行這項處理。 重複這個步驟，直到沒有留下任何 OR 運算子為止。 例如，如果您有以下述詞：  
  
    ```  
    pred1 OR (pred2 AND (pred3 OR pred4)) OR (pred5 AND pred6)  
    ```  
  
     在這個步驟之後，您應該有下列述詞：  
  
    ```  
    pred1  
    pred5 AND pred6  
    pred2 AND pred3  
    pred2 AND pred4  
    ```  
  
3.  使用步驟 2 中找到之兩個部分的每一部分當做述詞來執行查詢。 將每個查詢的結果插入步驟 1 所建立的記憶體最佳化資料表變數中。  
  
4.  必要時，從記憶體最佳化資料表變數中移除重複項。  
  
5.  使用記憶體最佳化資料表變數的內容當做查詢的結果。  
  
 下列範例使用 AdventureWorks2012 資料庫中為 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 更新的資料表。 若要下載此範例中，移至的檔案[AdventureWorks 資料庫-2012、 2008 r2 和 2008年](http://msftdbprodsamples.codeplex.com/releases/view/93587)。 若要套用[!INCLUDE[hek_2](../includes/hek-2-md.md)]程式碼 AdventureWorks2012 的範例，請前往[SQL Server 2014 記憶體中 OLTP 範例](https://msftdbprodsamples.codeplex.com/releases/view/114491)。  
  
 將下列預存程序加入至資料庫。 我們將會轉換這個預存程序來使用原生編譯。  
  
```  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesOrderDetail_ondisk  
  @SalesOrderId int = 0, @SalesOrderDetailId int = 0,   
  @CarrierTrackingNumber nvarchar(25) = N'', @ProductId int = 0,   
  @minUnitPrice money = 0, @maxUnitPrice money = 0  
AS BEGIN  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_ondisk s  
  WHERE  s.SalesOrderId = @SalesOrderId  
      OR s.SalesOrderDetailId = @SalesOrderDetailId  
      OR s.CarrierTrackingNumber = @CarrierTrackingNumber  
      OR s.ProductID = @ProductId  
      OR (s.UnitPrice > @minUnitPrice AND s.UnitPrice < @maxUnitPrice)  
END  
GO  
```  
  
 在轉換後，資料表和預存程序的結構描述如下所示：  
  
```  
CREATE TYPE Sales.fuzzySearchSalesOrderDetailType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  ModifiedDate datetime2(7) not null  
  INDEX ix_fuzzySearchSalesOrderDetailType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE TYPE Sales.fuzzySearchSalesOrderDetailTempType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  recordcount int not null  
  INDEX ix_fuzzySearchSalesOrderDetailTempType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesOrderDetail_inmem  
  @SalesOrderId int = 0, @SalesOrderDetailId int = 0,   
  @CarrierTrackingNumber nvarchar(25) = N'', @ProductId int = 0,   
  @minUnitPrice money = 0, @maxUnitPrice money = 0  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'ENGLISH')  
  
  DECLARE @retValue Sales.fuzzySearchSalesOrderDetailType  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.SalesOrderId = @SalesOrderId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.SalesOrderDetailId = @SalesOrderDetailId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.CarrierTrackingNumber COLLATE Latin1_General_BIN2 = @CarrierTrackingNumber COLLATE Latin1_General_BIN2   
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.ProductID = @ProductId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE (s.UnitPrice > @minUnitPrice AND s.UnitPrice < @maxUnitPrice)  
  
  -- After the above statements, there will be duplicates inside @retValue  
  -- Delete the duplicates from @retValue  
  DECLARE @duplicates Sales.fuzzySearchSalesOrderDetailTempType  
  
  INSERT INTO @duplicates (SalesOrderId, SalesOrderDetailId, recordcount)   
  SELECT SalesOrderId, SalesOrderDetailId, COUNT(*) AS recordCount  
  FROM @retValue  
  GROUP BY SalesOrderId, SalesOrderDetailId  
  
  -- Now we have one row per pair  
  -- clear and rebuild the result set  
  DELETE FROM @retValue  
  
  INSERT INTO @retValue  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN @duplicates d ON s.SalesOrderId = d.SalesOrderId AND s.SalesOrderDetailId = d.SalesOrderDetailId  
  
  -- After this every pair of (SalesOrderId, SalesOrderDetailId) in @retValue should be unique.  
  SELECT SalesorderId, SalesOrderDetailId, ModifiedDate FROM @retValue  
END  
GO  
```  
  
## <a name="or-operator-in-join-condition"></a>JOIN 條件中的 OR 運算子  
 如果您在 SELECT 陳述式的 JOIN 條件中有 OR 運算子，您可以使用下列方法模擬其行為。 如果您在 JOIN 條件中有多個 OR 運算子，或者您在 OR 運算子中有多個 JOIN 條件，您可能必須多次執行這項處理。  
  
 如果您有 OUTER JOIN 條件，您可以將這個因應措施與 OUTER JOIN 條件的因應措施結合在一起。  
  
1.  使用適當的結構描述建立記憶體最佳化資料表變數。 這需要預先定義的記憶體最佳化資料表類型。  
  
2.  根據 OR 運算子所聯結的述詞，將 JOIN 條件中的述詞分成兩部分。 如果您有多個 JOIN 條件，您可能必須針對每個 JOIN 條件進行這項處理，然後建立一組結果片段的組合。 例如，如果您有三個 JOIN 條件，每個 JOIN 條件中都有一個 OR 運算子，您可能會有 2x2x2=8 個述詞。  
  
3.  針對步驟 2 所產生的每個述詞建立一個查詢，將其結果插入步驟 1 所建立的記憶體最佳化資料表變數中。  
  
4.  必要時，從記憶體最佳化資料表變數中移除重複項。  
  
5.  使用記憶體最佳化資料表變數的內容當做查詢的結果。  
  
 下列範例使用 AdventureWorks2012 資料庫中為 [!INCLUDE[hek_2](../includes/hek-2-md.md)] 更新的資料表。 若要下載此範例中，移至的檔案[AdventureWorks 資料庫-2012、 2008 r2 和 2008年](http://msftdbprodsamples.codeplex.com/releases/view/93587)。 若要套用[!INCLUDE[hek_2](../includes/hek-2-md.md)]程式碼 AdventureWorks2012 的範例，請前往[SQL Server 2014 記憶體中 OLTP 範例](https://msftdbprodsamples.codeplex.com/releases/view/114491)。  
  
 將下列預存程序加入至資料庫。 我們將會轉換這個預存程序來使用原生編譯。 此範例使用 INNER JOIN 條件。  
  
```  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesSpecialOffers_ondisk  
  @SpecialOfferId int  
AS BEGIN  
  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_ondisk s  
  JOIN Sales.SpecialOffer_onDisk offer   
    ON s.SpecialOfferID = offer.SpecialOfferID   
    OR s.ProductID IN (SELECT ProductId FROM Sales.SpecialOfferProduct sop WHERE sop.SpecialOfferID = @SpecialOfferId)  
END  
```  
  
 在轉換後，資料表和預存程序的結構描述如下所示：  
  
```  
CREATE TYPE Sales.fuzzySearchSalesSpecialOffers_Type AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  SpecialOfferId int not null,  
  ModifiedDate datetime2(7) not null  
  INDEX ix_fuzzySearchSalesSpecialOffers_Type NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE TYPE Sales.fuzzySearchSalesSpecialOffers_TempType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  SpecialOfferId int not null,  
  recordcount int null  
  INDEX ix_fuzzySearchSalesSpecialOffers_TempType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesSpecialOffers_inmem  
  @SpecialOfferId int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'ENGLISH')  
  
  DECLARE @retValue Sales.FuzzySearchSalesSpecialOffers_Type  
  
  -- Find all special offers matching the conditions  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, SpecialOfferid, ModifiedDate)  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN Sales.SpecialOffer_inmem offer   
    ON s.SpecialOfferID = offer.SpecialOfferID  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, SpecialOfferid, ModifiedDate)  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN Sales.SpecialOfferProduct_inmem sop   
    ON sop.SpecialOfferId = @SpecialOfferId AND s.ProductID = sop.ProductId  
  
  -- Now we need to remove the duplicates from @matchingSpecialOffers  
  DECLARE @duplicates Sales.fuzzySearchSalesSpecialOffers_TempType  
  
  INSERT INTO @duplicates (SalesOrderId, SalesOrderDetailId, SpecialOfferid, recordcount)  
  SELECT SalesOrderId, SalesOrderDetailId, SpecialOfferId, COUNT(*)   
  FROM @retValue  
  GROUP BY SalesOrderId, SalesOrderDetailId, SpecialOfferId  
  
  -- now there should be no duplicates within @duplicate  
  -- use @duplicate for join.  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN @duplicates offer   
    ON    s.SalesOrderId = offer.SalesOrderId   
      AND s.SalesOrderDetailId = offer.SalesOrderDetailID   
      AND s.SpecialOfferId = offer.SpecialOfferId  
END  
GO  
```  
  
## <a name="side-effects"></a>副作用  
 如果您在 WHERE 子句或 JOIN 條件中有多個 OR 運算子，模擬此行為所必須執行的查詢數目可能會以指數方式遞增。 這樣可能會降低查詢效能，也可能會增加記憶體使用量，因為必須使用記憶體最佳化資料表變數。  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯預存程序的移轉問題](../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)  
  
  
