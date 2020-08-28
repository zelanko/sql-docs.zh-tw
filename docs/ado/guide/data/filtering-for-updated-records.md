---
description: 篩選更新的記錄
title: 篩選更新的記錄 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- filtering for updated records [ADO]
ms.assetid: 4a798921-d7bb-47c9-a252-550fd9463ec9
author: rothja
ms.author: jroth
ms.openlocfilehash: cd97232b83b355948f449fefb57aa748bbc2db40
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991249"
---
# <a name="filtering-for-updated-records"></a>篩選更新的記錄
在您呼叫 UpdateBatch 之前，您可以使用 [記錄集篩選] 屬性，只查看自記錄集開啟以來已變更的記錄，或上次呼叫 UpdateBatch 的記錄。 若要這樣做，請將 Filter 設定為等於 adFilterPendingRecords，以判斷將更新多少記錄，如下一節中的程式碼範例所示。  
  
## <a name="remarks"></a>備註  
 這個範例會先篩選記錄集，然後再呼叫 UpdateBatch 來擴充先前的 UpdateBatch 範例，顯示使用者記錄將會變更，並允許她使用 CancelBatch 方法) 來取消更新 (。  
  
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
 [批次模式](./batch-mode.md)