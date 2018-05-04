---
title: 重新同步處理命令屬性動態 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Resync Command property [ADO]
ms.assetid: 4e2bb601-0fe8-4d61-b00e-38341d85a6bb
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 240c4d6ce4aa392f01ebb27a4a52fd73c684b981
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="resync-command-property-dynamic-ado"></a>重新同步處理命令屬性動態 (ADO)
指定使用者提供的命令字串[重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法問題中名為資料表中的資料重新整理[唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)動態屬性。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值為命令字串。  
  
## <a name="remarks"></a>備註  
 [資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件是在多個基底資料表上執行聯結作業的結果。 取決於受影響的資料列*AffectRecords*參數[重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法。 標準**重新同步處理**方法，就會執行[唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)和**重新同步處理命令**未設定的屬性。  
  
 命令字串**重新同步處理命令**屬性參數化的命令或預存程序可唯一識別要重新整理的資料列，並傳回單一資料列的資料列包含相同的數目和資料行順序重新整理。 命令字串包含每個主索引鍵資料行中的參數**唯一資料表**，否則會傳回執行階段錯誤。 參數會自動填入從要重新整理的資料列的主索引鍵值。  
  
 以下是 SQL 為基礎的兩個範例：  
  
 1\) **資料錄集**定義的命令：  
  
```  
SELECT * FROM Customers JOIN Orders ON   
   Customers.CustomerID = Orders.CustomerID  
   WHERE city = 'Seattle'  
   ORDER BY CustomerID  
```  
  
 **重新同步處理命令**屬性設定為：  
  
```  
"SELECT * FROM   
   (SELECT * FROM Customers JOIN Orders   
   ON Customers.CustomerID = Orders.CustomerID  
   city = 'Seattle' ORDER BY CustomerID)  
WHERE Orders.OrderID = ?"  
```  
  
 **唯一資料表**是*訂單*和其主索引鍵， *OrderID*，參數化。 子 select 提供簡單的方式來以程式設計的方式確保傳回相同的數目和資料行的順序，為 「 依原始命令。  
  
 2\) **資料錄集**定義預存程序：  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 **重新同步處理**方法應該執行下列預存程序：  
  
```  
CREATE PROC CustordersResync @ordid int AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID  
WHERE Orders.ordid  = @ordid  
```  
  
 **重新同步處理命令**屬性設定為：  
  
```  
"{call CustordersResync (?)}"  
```  
  
 同樣地，**唯一資料表**是*訂單*和其主索引鍵， *OrderID*，參數化。  
  
 **重新同步處理命令**動態屬性附加至**資料錄集**物件[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合時[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
