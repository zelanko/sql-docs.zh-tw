---
title: 加入多個欄位 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: cd5999d62056582d5739f50f415680b9b0dc8a3f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761414"
---
# <a name="adding-multiple-fields-and-values"></a>新增多個欄位和值
有時候，將欄位的陣列及其對應的值傳入**AddNew**方法可能會更有效率，而不是針對每個新的欄位設定多次的**值**。 如果*FieldList*是陣列，*值*也必須是具有相同成員數目的陣列;否則，就會發生錯誤。 功能變數名稱的順序必須符合每個陣列中域值的順序。 下列程式碼會將欄位陣列和值陣列傳遞給**AddNew**方法。

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
