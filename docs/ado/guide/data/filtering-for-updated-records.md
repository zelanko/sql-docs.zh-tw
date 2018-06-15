---
title: 篩選更新記錄 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- filtering for updated records [ADO]
ms.assetid: 4a798921-d7bb-47c9-a252-550fd9463ec9
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 529845297ff3c4264cc152c652b31c0bd12f5441
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270877"
---
# <a name="filtering-for-updated-records"></a>篩選的更新記錄
在呼叫 UpdateBatch 之前，您可以使用資料錄集的篩選條件屬性，以檢視這些資料錄集開啟之後已經變更的記錄或 UpdateBatch 在上次呼叫。 若要這樣做，請設定篩選等於 adFilterPendingRecords 來判斷將更新的多少筆記錄，請在下一節中的程式碼範例所示。  
  
## <a name="remarks"></a>備註  
 此範例擴充 UpdateBatch 上例透過篩選資料錄集，它會呼叫 UpdateBatch 之前，顯示使用者的記錄將會變更並讓她可以取消更新 （使用 CancelBatch 方法）。  
  
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
