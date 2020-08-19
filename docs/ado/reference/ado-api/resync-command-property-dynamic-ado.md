---
description: Resync Command 動態屬性 (ADO)
title: Resync 命令屬性-Dynamic (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Resync Command property [ADO]
ms.assetid: 4e2bb601-0fe8-4d61-b00e-38341d85a6bb
author: rothja
ms.author: jroth
ms.openlocfilehash: a7a350540d94ea0379f7829fa004d98ce691f1e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442300"
---
# <a name="resync-command-property-dynamic-ado"></a>Resync Command 動態屬性 (ADO)
指定使用者提供的命令字串，重新 [同步](../../../ado/reference/ado-api/resync-method.md) 處理方法會發出重新整理，以重新整理 [Unique table](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 動態屬性中所指定資料表中的資料。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **字串** 值，此為命令字串。  
  
## <a name="remarks"></a>備註  
 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件是在多個基表上執行聯結作業的結果。 受影響的資料列取決於[Resync](../../../ado/reference/ado-api/resync-method.md)方法的*AffectRecords*參數。 如果未設定[Unique Table](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)和**Resync 命令**屬性，則會執行標準重新**同步**處理方法。  
  
 **Resync 命令**屬性的命令字串是參數化的命令或預存程式，可唯一識別正在重新整理的資料列，並傳回單一資料列，其中包含與要重新整理的資料列相同的資料行數目和順序。 命令字串包含 **唯一資料表**中每個主鍵資料行的參數;否則，會傳回執行階段錯誤。 系統會自動填入這些參數，其中包含要重新整理之資料列的主鍵值。  
  
 以下是以 SQL 為基礎的兩個範例：  
  
 1 \) **記錄集** 是由命令所定義：  
  
```  
SELECT * FROM Customers JOIN Orders ON   
   Customers.CustomerID = Orders.CustomerID  
   WHERE city = 'Seattle'  
   ORDER BY CustomerID  
```  
  
 **Resync 命令**屬性會設定為：  
  
```  
"SELECT * FROM   
   (SELECT * FROM Customers JOIN Orders   
   ON Customers.CustomerID = Orders.CustomerID  
   city = 'Seattle' ORDER BY CustomerID)  
WHERE Orders.OrderID = ?"  
```  
  
 **唯一資料表**是 Orders，而其 primary *key （* *Orders* ）已參數化。 子選取提供簡單的方法，讓您以程式設計的方式確保相同的資料行數目和順序會以原始命令傳回。  
  
 2 \) **記錄集** 是由預存程式所定義：  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 **Resync**方法應該執行下列預存程式：  
  
```  
CREATE PROC CustordersResync @ordid int AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID  
WHERE Orders.ordid  = @ordid  
```  
  
 **Resync 命令**屬性會設定為：  
  
```  
"{call CustordersResync (?)}"  
```  
  
 同樣地， **唯一的資料表** 是 *Orders* ，而其 primary key *（* Orders）已參數化。  
  
 當[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**時，重新**同步命令**是附加到**記錄集**物件[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合的動態屬性。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
