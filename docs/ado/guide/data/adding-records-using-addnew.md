---
title: 加入資料錄使用 AddNew |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- AddNew method [ADO]
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: cab4adff-f22f-4fb1-9217-f8138c795268
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ba15d68b5fbaa749e00987b1fbfef73887dc377
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="adding-records-using-addnew-method"></a>加入資料錄使用 AddNew 方法
這是基本語法**AddNew**方法：

 *資料錄集*。AddNew *FieldList*，*值*

 *FieldList*和*值*引數是選擇性。 *FieldList*單一名稱或名稱的陣列或欄位的新記錄中的序數位置。

 *值*引數是單一值或新記錄中的欄位值的陣列。

 一般而言，當您想要新增一筆記錄，您會呼叫**AddNew**沒有任何引數的方法。 具體來說，您會呼叫**AddNew**; 設定**值**每個新的記錄; 中的欄位，然後呼叫**更新**或**UpdateBatch**，或兩者。 您可以確定您**資料錄集**支援透過加入新資料錄**支援**屬性**adAddNew**列舉的常數。

 下列程式碼會使用這項技術範例中加入新的託運商**資料錄集**。 SQL Server 都會自動提供即貨運公司編號欄位值。 因此，程式碼不會嘗試提供新的記錄欄位的值。

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
 因為此程式碼會使用已中斷連線**資料錄集**與批次模式是用戶端資料指標，您必須重新連線**資料錄集**新的資料來源**連接**物件之前，您可以呼叫**UpdateBatch**張貼到資料庫變更的方法。 這輕鬆地透過新的函式**GetNewConnection**。
