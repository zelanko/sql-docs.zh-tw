---
title: 重新整形 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e0328b7a09f18cde0043cfbcc21d2dceb4893442
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760934"
---
# <a name="reshaping"></a>重新成形
Shape 命令的子句所建立的**記錄集**可能會被指派*別名*名稱（通常使用 AS 關鍵字）。 在完全不同的命令中，可以參考形狀**記錄集**的別名。 也就是說，您可以在新的圖形命令中重複使用或*改變*先前成形的**記錄集**。 為了支援這項功能，ADO 提供屬性，並重新[調整名稱](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)。  
  
 重新整形有兩個主要功能。 第一種方式是將現有的**記錄集**與新的父**記錄集**產生關聯。  
  
## <a name="example"></a>範例  
  
```  
rs1.Open "SHAPE {select * from Customers} " & _  
         "APPEND ({select * from Orders} AS chapOrders " & _  
         "RELATE CustomerID to CustomerID)", cn  
  
rs2.Open "SHAPE {select * from Employees} " & _  
         "APPEND (chapOrders RELATE EmployeeID to EmployeeID)", cn  
```  
  
 第二個函式是使用「圖形記錄集重新塑造名稱>」語法，啟用對現有子**記錄集**物件的非章節式存取 \< 。  
  
> [!NOTE]
>  您不能將資料行附加至現有的**記錄集**、將參數化**記錄集**或任何中間計運算元句中的**記錄集**物件重新整形，或在要重新整形的**記錄****集上**執行匯總作業。 正在重做的**記錄集**，而新的圖形命令必須同時使用相同的[連接](../../../ado/reference/ado-api/connection-object-ado.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)
