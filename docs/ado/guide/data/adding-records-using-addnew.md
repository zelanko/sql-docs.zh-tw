---
title: 使用 AddNew 加入記錄 |Microsoft Docs
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
ms.openlocfilehash: 36f6bad9a8f0d74a81d02ce64c78d7a91ddc0fa8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926287"
---
# <a name="adding-records-using-addnew-method"></a>使用 AddNew 方法加入記錄
這是**AddNew**方法的基本語法：

 *記錄集*。AddNew *FieldList*，*值*

 *FieldList*和*Values*引數是選擇性的。 *FieldList*可以是單一名稱，或是新記錄中欄位的名稱陣列或序數位置。

 *Values*引數可以是單一值或新記錄中欄位的值陣列。

 一般而言，當您想要加入單一記錄時，您會呼叫**AddNew**方法，而不需要任何引數。 具體來說，您會呼叫**AddNew**;設定新記錄中每個欄位的**值**;然後呼叫**Update**或**UpdateBatch**，或兩者。 您可以使用**支援**具有**adAddNew**列舉常數的屬性，確保**記錄集**支援加入新記錄。

 下列程式碼會使用這項技術，將新的貨主加入至範例**記錄集**。 SQL Server 會自動提供 ShipperID 域值。 因此，程式碼不會嘗試提供新記錄的域值。

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
 因為此程式碼會在批次模式中使用已中斷連接的**記錄集**與用戶端資料指標，所以您必須先使用新的**連接**物件，將**記錄集**重新連接至資料來源，然後才能呼叫**UpdateBatch**方法將變更公佈到資料庫。 您可以使用新的函式**GetNewConnection**輕鬆完成這項作業。
