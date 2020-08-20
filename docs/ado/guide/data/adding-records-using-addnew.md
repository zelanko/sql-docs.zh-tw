---
description: 使用 AddNew 方法加入記錄
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 27b42b9d65a4c00d4786ed900ad35ce00ef4b8f1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453870"
---
# <a name="adding-records-using-addnew-method"></a>使用 AddNew 方法加入記錄
這是 **AddNew** 方法的基本語法：

 *記錄集*。AddNew *FieldList*， *值*

 *FieldList*和*Values*引數是選擇性的。 *FieldList* 可以是單一名稱，或是新記錄中欄位的名稱或序數位置陣列。

 *Values*引數是新記錄中欄位的單一值或值陣列。

 一般來說，當您想要新增單一記錄時，將會呼叫 **AddNew** 方法，而不需要任何引數。 具體來說，您將會呼叫 **AddNew**;設定新記錄中每個欄位的 **值** 。然後呼叫 **Update** 或 **UpdateBatch**，或兩者。 您可以使用**支援**屬性搭配**adAddNew**列舉常數，以確定您的**記錄集**支援加入新的記錄。

 下列程式碼會使用這項技術，將新的貨主新增至範例 **記錄集**。 SQL Server 會自動提供 ShipperID 域值。 因此，程式碼不會嘗試提供新記錄的域值。

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
 因為此程式碼會在批次模式中使用具有用戶端資料指標的中斷連接**記錄集**，所以您必須使用新的**連接**物件，將**記錄集**重新連接到資料來源，然後才能呼叫**UpdateBatch**方法將變更張貼到資料庫。 您可以使用 [新增函式 **GetNewConnection**] 輕鬆完成這項工作。
