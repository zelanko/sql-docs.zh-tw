---
title: 重新同步命令動態屬性 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5567bf3cc460aac6abfc2979a14e124bfd9d4cac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061932"
---
# <a name="resync-command-property-dynamic-ado"></a>Resync Command 動態屬性 (ADO)
指定使用者所提供的命令字串[Resync](../../../ado/reference/ado-api/resync-method.md)方法來重新整理中所命名的資料表中資料的問題[唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)動態屬性。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**命令字串的值。  
  
## <a name="remarks"></a>備註  
 [資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件是在多個基底資料表上執行聯結作業的結果。 受影響的資料列相依於*AffectRecords*的參數[重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法。 標準**重新同步處理**方法，就會執行[唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)並**重新同步處理命令**沒有設定的屬性。  
  
 命令字串**重新同步處理命令**屬性參數化的命令或預存程序，可唯一識別正在重新整理的資料列，並傳回單一資料列做為資料列包含相同數目和資料行順序重新整理。 命令字串包含每個主要的索引鍵資料行中的參數**唯一資料表**，否則會傳回執行階段錯誤。 參數會自動填入從重新整理的資料列的主索引鍵值。  
  
 以下是 SQL 為基礎的兩個範例：  
  
 1\) **資料錄集**命令所定義：  
  
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
  
 **唯一資料表**是*訂單*及其主要的索引鍵*OrderID*，參數化。 子 select 提供簡單的方法，以程式設計的方式確保傳回相同的數目和資料行的順序，藉由原始命令。  
  
 2\) **資料錄集**定義預存程序：  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 **Resync**方法應該執行下列預存程序：  
  
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
  
 同樣地，**唯一資料表**是*訂單*及其主要的索引鍵*OrderID*，參數化。  
  
 **重新同步處理命令**動態屬性附加至**Recordset**物件[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合時[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
