---
description: 重新成形
title: 重新整形 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 04c43b9fcca56959aec242f344da6ec81a825030
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979769"
---
# <a name="reshaping"></a>重新成形
Shape 命令的子句所建立的 **記錄集** 可能會被指派 *別名* 名稱， (通常使用 AS 關鍵字) 。 您可以在完全不同的命令中參考成形 **記錄集** 的別名。 也就是說，您可以在新的圖形命令中重複使用或 *調整*先前成形的 **記錄集** 。 為了支援這項功能，ADO 提供了一個屬性，它會 [改變名稱](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)。  
  
 整形有兩個主要功能。 第一個是將現有的 **記錄集** 與新的父 **記錄集**建立關聯。  
  
## <a name="example"></a>範例  
  
```  
rs1.Open "SHAPE {select * from Customers} " & _  
         "APPEND ({select * from Orders} AS chapOrders " & _  
         "RELATE CustomerID to CustomerID)", cn  
  
rs2.Open "SHAPE {select * from Employees} " & _  
         "APPEND (chapOrders RELATE EmployeeID to EmployeeID)", cn  
```  
  
 第二個函式是使用語法 "SHAPE" 來啟用對現有子 **記錄集** 物件的非章節式存取 \<recordset reshape name> 。  
  
> [!NOTE]
>  您無法將資料行附加至現有的**記錄集**、將參數化記錄集重新調整為任何仲介計運算元句中的參數化**記錄集**或**記錄集**物件，或對正在重設之**記錄集**的任何**記錄集**子系執行 要重做的 **記錄集** 和新的 shape 命令都必須使用相同的 [連接](../../../ado/reference/ado-api/connection-object-ado.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)
