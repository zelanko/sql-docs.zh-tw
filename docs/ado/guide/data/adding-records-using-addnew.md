---
title: 使用 AddNew 新增記錄 |Microsoft Docs
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
- editing data [ADO], AddNew method
ms.assetid: cab4adff-f22f-4fb1-9217-f8138c795268
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0be4014809500c4d83b2019dc16bd083b8ed6452
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701198"
---
# <a name="adding-records-using-addnew-method"></a>新增記錄使用 AddNew 方法
這是基本語法**AddNew**方法：

 *資料錄集*。AddNew *FieldList*，*值*

 *FieldList*並*值*引數是選擇性。 *FieldList*單一名稱或名稱的陣列或欄位的新記錄中的序數位置。

 *值*引數是單一值或陣列的新記錄中欄位的值。

 一般而言，當您想要新增單一記錄，您會呼叫**AddNew**不含任何引數的方法。 具體來說，您會呼叫**AddNew**; set**值**每個新的記錄; 中的欄位，然後再呼叫**Update**或是**UpdateBatch**，或兩者。 您可以確定您**Recordset**支援使用加入新的記錄**支援**屬性**adAddNew**列舉的常數。

 下列程式碼會使用這項技術範例新增新的託運商**資料錄集**。 SQL Server 會自動提供即貨運公司編號欄位值。 因此，程式碼不會嘗試提供新的資料錄的欄位值。

```
'BeginAddNew1.1
If objRs.Supports(adAddNew) Then
    With objRs
        .AddNew
        .Fields("CompanyName") = "Sample Shipper"
        .Fields("Phone") = "(931) 555-6334"
        .Update
    End With
End If
'EndAddNew1.1
```

## <a name="remarks"></a>備註
 因為此程式碼會使用已中斷連接**資料錄集**與 批次模式中建立用戶端資料指標，您必須重新連線**資料錄集**與新的資料來源**連接**物件，您可以呼叫才能**UpdateBatch**方法，以變更公佈到資料庫。 這會輕鬆地透過新的函式**GetNewConnection**。
