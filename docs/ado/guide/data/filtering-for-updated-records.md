---
title: 篩選已更新的記錄 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- filtering for updated records [ADO]
ms.assetid: 4a798921-d7bb-47c9-a252-550fd9463ec9
author: rothja
ms.author: jroth
ms.openlocfilehash: 8dae572da8f87051a58415929657f77be6c91d14
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758264"
---
# <a name="filtering-for-updated-records"></a>篩選更新的記錄
在您呼叫 UpdateBatch 之前，您可以使用 [記錄集篩選] 屬性，只查看自從記錄集開啟或上次呼叫 UpdateBatch 之後已經變更的記錄。 若要這麼做，請將 Filter 設定為等於 adFilterPendingRecords，以判斷將更新多少記錄，如下一節的程式碼範例所示。  
  
## <a name="remarks"></a>備註  
 這個範例會擴充先前的 UpdateBatch 範例，其方式是在呼叫 UpdateBatch 之前篩選記錄集，並向使用者顯示哪些記錄將會變更，並允許她取消更新（使用 CancelBatch 方法）。  
  
```  
'BeginFilterPend  
    '...  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
  
    ' Change value of Phone field for first record in Recordset, saving value  
    ' for later restoration.  
    intId = objRs1("ShipperId")  
    sPhone = objRs1("Phone")  
  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Add two new records  
    For i = 0 To 1  
        objRs1.AddNew  
        objRs1(1) = "New Shipper #" & CStr((i + 1))  
        objRs1(2) = "(nnn) 555-" & i & i & i & i  
    Next i  
  
    objRs1.Filter = adFilterPendingRecords  
  
    MsgBox "There are " & objRs1.RecordCount & " records pending.", _  
            , "Filter Pending"  
  
    ' Cancel the updates  
    objRs1.CancelBatch  
'EndFilterPend  
```  
  
## <a name="see-also"></a>另請參閱  
 [批次模式](../../../ado/guide/data/batch-mode.md)
