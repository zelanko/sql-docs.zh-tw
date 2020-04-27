---
title: Resync 命令屬性-Dynamic （ADO） |Microsoft Docs
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
ms.openlocfilehash: e81fa9ffb28ba31f50d77cacf372bc24d09787ba
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917140"
---
# <a name="resync-command-property-dynamic-ado"></a>Resync Command 動態屬性 (ADO)
指定使用者提供的命令字串，重新[同步](../../../ado/reference/ado-api/resync-method.md)處理方法會發出此錯誤，以重新整理[唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)動態屬性中名為的資料表中的資料。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值，這是命令字串。  
  
## <a name="remarks"></a>備註  
 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件是在多個基表上執行聯結作業的結果。 受影響的資料列取決於[Resync](../../../ado/reference/ado-api/resync-method.md)方法的*AffectRecords*參數。 如果未設定[唯一的資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)和重新**同步命令**屬性，則會執行標準重新**同步**處理方法。  
  
 [重新**同步命令**] 屬性的命令字串是參數化命令或預存程式，可唯一識別要重新整理的資料列，並傳回包含與要重新整理之資料行相同的資料行數目和順序的單一資料列。 命令字串包含**唯一資料表**中每個主鍵資料行的參數。否則，會傳回執行階段錯誤。 這些參數會自動填入要重新整理之資料列中的主鍵值。  
  
 以下是以 SQL 為基礎的兩個範例：  
  
 1\) **記錄集**是由命令定義的：  
  
```  
SELECT * FROM Customers JOIN Orders ON   
   Customers.CustomerID = Orders.CustomerID  
   WHERE city = 'Seattle'  
   ORDER BY CustomerID  
```  
  
 [重新**同步命令**] 屬性設定為：  
  
```  
"SELECT * FROM   
   (SELECT * FROM Customers JOIN Orders   
   ON Customers.CustomerID = Orders.CustomerID  
   city = 'Seattle' ORDER BY CustomerID)  
WHERE Orders.OrderID = ?"  
```  
  
 **唯一資料表**是*訂單*，而其主要*金鑰（即訂單）* 已參數化。 子選取提供簡單的方式，以程式設計方式確保相同的資料行數目和順序會由原始命令傳回。  
  
 2\) **記錄集**是由預存程式所定義：  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 重新**同步**處理方法應執行下列預存程式：  
  
```  
CREATE PROC CustordersResync @ordid int AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID  
WHERE Orders.ordid  = @ordid  
```  
  
 [重新**同步命令**] 屬性設定為：  
  
```  
"{call CustordersResync (?)}"  
```  
  
 同樣地，**唯一資料表**是*Orders* ，而它的主要索引*鍵，則*是參數化的。  
  
 當[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**AdUseClient**時， **Resync 命令**是附加至**記錄集**物件[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合的動態屬性。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
