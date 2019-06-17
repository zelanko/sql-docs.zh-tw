---
title: 新增多個欄位 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], adding multiple fields
- editing data [ADO], AddNew method
ms.assetid: f3648ef4-9f36-4991-a868-83a617389844
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 90904154f324a86088fac0d637301193464feb2c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701239"
---
# <a name="adding-multiple-fields-and-values"></a>新增多個欄位和值
有時候，可能會將陣列的欄位和其對應的值，以更有效率**AddNew**方法，而不是設定**值**多次的每個新的欄位。 如果*FieldList*屬於陣列、*值*也必須是陣列具有相同成員數目，否則會發生錯誤。 欄位名稱的順序必須符合每個陣列中的欄位值的順序。 下列程式碼會將陣列的欄位和值的陣列傳遞**AddNew**方法。

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
