---
title: "將多個欄位加入 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], adding multiple fields
- editing data [ADO], AddNew method
ms.assetid: f3648ef4-9f36-4991-a868-83a617389844
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 61f6d3c21d4260126f67511c31bbcc680a2da6fa
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="adding-multiple-fields-and-values"></a>加入多個欄位和值
有時候，可能會將陣列中的欄位和其相對應的值，以更有效率**AddNew**方法，而非設定**值**多次的每個新的欄位。 如果*FieldList*屬於陣列、*值*也必須是陣列具有相同數目的成員; 否則就會發生錯誤。 欄位名稱的順序必須符合的每個陣列中的欄位值的順序。 下列程式碼會將欄位的陣列和值的陣列傳遞**AddNew**方法。

```
'BeginAddNew2
    Dim avarFldNames As Variant
    Dim avarFldValues As Variant

    avarFldNames = Array("CompanyName", "Phone")
    avarFldValues = Array("Sample Shipper 2", "(931) 555-6334")

    If objRs1.Supports(adAddNew) Then
        objRs1.AddNew avarFldNames, avarFldValues
    End If

    'Re-establish a Connection and update
    Set objRs1.ActiveConnection = GetNewConnection
    objRs1.UpdateBatch
'EndAddNew2
```

