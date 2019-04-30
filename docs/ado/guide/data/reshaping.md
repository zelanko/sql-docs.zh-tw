---
title: 重整 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- reshaping previously shaped Recordset [ADO]
- data shaping [ADO], reshaping
ms.assetid: b1c965b7-3dad-4de6-9e0e-502ca8785be3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 324801cbfc97db4e2a1137fa04df0c74dc1897a1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280398"
---
# <a name="reshaping"></a>重新成形
A **Recordset**建立命令可能會指派圖案的子句*別名*名稱 （通常是使用 AS 關鍵字）。 形狀的別名**資料錄集**可以完全不同的命令中參考。 也就是說，您可以重複使用，或*重塑*，先前形狀**資料錄集**在新的圖形命令。 若要支援這項功能，ADO 會提供屬性[調整形狀名稱](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)。  
  
 重整有兩個主要的功能。 第一個步驟是建立關聯的現有**Recordset**使用新的父**資料錄集**。  
  
## <a name="example"></a>範例  
  
```  
rs1.Open "SHAPE {select * from Customers} " & _  
         "APPEND ({select * from Orders} AS chapOrders " & _  
         "RELATE CustomerID to CustomerID)", cn  
  
rs2.Open "SHAPE {select * from Employees} " & _  
         "APPEND (chapOrders RELATE EmployeeID to EmployeeID)", cn  
```  
  
 第二個函式會以非編製章節存取現有的子系**資料錄集**物件，使用語法 「 圖形\<資料錄集調整形狀名稱 >"。  
  
> [!NOTE]
>  您無法將資料行附加至現有**資料錄集**，調整參數化**資料錄集**或**資料錄集**任何中介 COMPUTE 子句中的物件，或執行彙總任何作業**Recordset**從子系**資料錄集**正在重繪。 **Recordset**正在調整形狀和新的形狀命令都必須使用相同[連線](../../../ado/reference/ado-api/connection-object-ado.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)
