---
title: "才可遏制 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reshaping previously shaped Recordset [ADO]
- data shaping [ADO], reshaping
ms.assetid: b1c965b7-3dad-4de6-9e0e-502ca8785be3
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d5264de973e4ed36cc24eb5c535576bdfa0a7228
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="reshaping"></a>才可遏制
A**資料錄集**建立命令可能會指派 」 圖形的子句*別名*名稱 （通常是使用 AS 關鍵字）。 形狀的別名**資料錄集**可以完全不同的命令中參考。 也就是說，您可以重複使用，或*重繪*，先前形狀**資料錄集**中新的圖形命令。 若要支援這項功能，ADO 提供屬性，[重繪名稱](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)。  
  
 才可遏制有兩個主要的功能。 第一個是相關聯的現有**資料錄集**與新的父**資料錄集**。  
  
## <a name="example"></a>範例  
  
```  
rs1.Open "SHAPE {select * from Customers} " & _  
         "APPEND ({select * from Orders} AS chapOrders " & _  
         "RELATE CustomerID to CustomerID)", cn  
  
rs2.Open "SHAPE {select * from Employees} " & _  
         "APPEND (chapOrders RELATE EmployeeID to EmployeeID)", cn  
```  
  
 第二個函式是以非分段存取現有的子系**資料錄集**物件使用的語法 」 圖形\<資料錄集重新塑造名稱 >"。  
  
> [!NOTE]
>  您無法將資料行附加至現有**資料錄集**，調整參數化**資料錄集**或**資料錄集**任何中介的 COMPUTE 子句中的物件或執行彙總作業上任何**資料錄集**從**資料錄集**正在重繪。 **資料錄集**正在重繪和新的形狀命令都必須使用相同[連接](../../../ado/reference/ado-api/connection-object-ado.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)
