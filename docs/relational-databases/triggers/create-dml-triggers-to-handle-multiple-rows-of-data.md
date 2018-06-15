---
title: 建立 DML 觸發程序以處理多重資料列 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: triggers
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-dml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- multiple row DML triggers
- UPDATE statement [SQL Server], DML triggers
- DELETE statement [SQL Server], DML triggers
- multirow DML triggers [SQL Server]
- INSERT statement [SQL Server], DML triggers
- DML triggers, multirow
ms.assetid: d476c124-596b-4b27-a883-812b6b50a735
caps.latest.revision: 25
author: rothja
ms.author: jroth
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a7309d66c4fdc154ca30707133145e94dbf62f86
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33012016"
---
# <a name="create-dml-triggers-to-handle-multiple-rows-of-data"></a>建立 DML 觸發程序以處理多重資料列
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  撰寫 DML 觸發程序的程式碼時，請將造成觸發程序引發的陳述式，視為可影響多個資料列而非只影響單一資料列的單一陳述式。 此行為對 UPDATE 與 DELETE 觸發程序是常見的，因為這些陳述式經常會影響多個資料列。 然而該行為對 INSERT 觸發程序較不常見，因為基本 INSERT 陳述式僅會加入單一資料列。 不過，由於 INSERT 觸發程序可以由 INSERT INTO (*table_name*) SELECT 陳述式引發，所以插入多個資料列也許會造成單一觸發程序引動過程。  
  
 當 DML 觸發程序執行自動重新計算來自資料表的摘要值，並將計算結果存至另一資料表的功能時，考慮多重資料列所造成的影響就顯得特別地重要。  
  
> [!NOTE]  
>  我們不建議在觸發程序中使用資料指標，因為這樣可能會減低效能。 若要設計出可影響多個資料列的觸發程序，請使用資料列集邏輯而非資料指標。  
  
## <a name="examples"></a>範例  
 在以下範例中，DML 觸發程序是用來將資料行的累計值儲存到 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫中的另一個資料表。  
  
### <a name="a-storing-a-running-total-for-a-single-row-insert"></a>A. 儲存單一資料列插入的累加值  
 當一個資料列載入至 `PurchaseOrderDetail` 資料表時，第一種 DML 觸發程序版本非常適用於單一資料列插入。 INSERT 陳述式引發 DML 觸發程序，而且在此觸發程序的執行期間，會將新的資料列載入到 **inserted** 資料表。 `UPDATE` 陳述式為資料列讀取 `LineTotal` 資料行的值，並將此值與 `SubTotal` 資料表中 `PurchaseOrderHeader` 資料行中的現有值加以累計。 `WHERE` 子句確定 `PurchaseOrderDetail` 資料表中已更新的資料列與 `PurchaseOrderID` inserted **資料表中資料列的** 相符。  
  
```  
-- Trigger is valid for single-row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail  
ON Purchasing.PurchaseOrderDetail  
AFTER INSERT AS  
   UPDATE PurchaseOrderHeader  
   SET SubTotal = SubTotal + LineTotal  
   FROM inserted  
   WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID ;  
```  
  
### <a name="b-storing-a-running-total-for-a-multirow-or-single-row-insert"></a>B. 儲存多資料列或單一資料列插入的累加值  
 若範例 A 中的 DML 觸發程序執行多資料列的插入動作時，極有可能會發生錯誤；在 UPDATE 陳述式中，指派運算式右邊的運算式 (`SubTotal` + `LineTotal`) 只能是單一數值，而不能是一串數值。 因此，觸發程序的作用是擷取 **inserted** 資料表中任意單一資料列中的值，並針對特定 `SubTotal` 值，將擷取的值與 `PurchaseOrderHeader` 資料表中現有的 `PurchaseOrderID` 值加以累計。 如果 `PurchaseOrderID` inserted **資料表中出現多次** 值，則此計算結果可能不是我們所要的。  
  
 若要正確更新 `PurchaseOrderHeader` 資料表，觸發程序必須允許 **inserted** 資料表中可以有多個資料列。 只要使用 `SUM` 函數，針對每個 `LineTotal` ，計算出 **inserted** 資料表中一組資料列的 `PurchaseOrderID`總數，就可以完成這個目標。 `SUM` 函數包含於相互關聯的子查詢中 (括號內的 `SELECT` 陳述式)。 如果 `PurchaseOrderID` inserted **資料表中每個** 與 `PurchaseOrderID` 資料表中的 `PurchaseOrderHeader` 相符或相互關聯，則此子查詢會為每個相符的項目傳回單一值。  
  
```  
-- Trigger is valid for multirow and single-row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail2  
ON Purchasing.PurchaseOrderDetail  
AFTER INSERT AS  
   UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal +   
      (SELECT SUM(LineTotal)  
      FROM inserted  
      WHERE PurchaseOrderHeader.PurchaseOrderID  
       = inserted.PurchaseOrderID)  
   WHERE PurchaseOrderHeader.PurchaseOrderID IN  
      (SELECT PurchaseOrderID FROM inserted);  
```  
  
 此觸發程序在單一資料列插入中也適用； `LineTotal` 值資料行的總和即單一資料列的總和。 不過，由於此觸發程序， `IN` 子句運算子中使用的相互關聯子查詢與 `WHERE` 運算子需要從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]進行額外的處理。 這個動作對單一資料列插入是不必要的。  
  
### <a name="c-storing-a-running-total-based-on-the-type-of-insert"></a>C. 根據插入類型儲存累加值  
 您可以變更觸發程序，使用最適於多個資料列的方法。 例如， `@@ROWCOUNT` 函數可以在觸發程序邏輯中使用，以區別單一資料列插入及多資料列插入。  
  
```  
-- Trigger valid for multirow and single row inserts  
-- and optimal for single row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail3  
ON Purchasing.PurchaseOrderDetail  
FOR INSERT AS  
IF @@ROWCOUNT = 1  
BEGIN  
   UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal + LineTotal  
   FROM inserted  
   WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
END  
ELSE  
BEGIN  
      UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal +   
      (SELECT SUM(LineTotal)  
      FROM inserted  
      WHERE PurchaseOrderHeader.PurchaseOrderID  
       = inserted.PurchaseOrderID)  
   WHERE PurchaseOrderHeader.PurchaseOrderID IN  
      (SELECT PurchaseOrderID FROM inserted)  
END;  
```  
  
## <a name="see-also"></a>另請參閱  
 [DML 觸發程序](../../relational-databases/triggers/dml-triggers.md)  
  
  
