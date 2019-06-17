---
title: 傳送更新：UpdateBatch 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 87123797-831f-48e0-94b5-f669f9ca194a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6759f007e652a6a52a1633b021553faa2978f6b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66706644"
---
# <a name="sending-the-updates-updatebatch-method"></a>傳送更新：UpdateBatch 方法
下列程式碼藉由 LockType 屬性設定為 Adlockpessimistic 和以 adUseClient CursorLocation 批次模式中開啟資料錄集。 它將加入兩筆新記錄和變更在現有的記錄儲存到原始值欄位的值，然後呼叫 UpdateBatch 傳送回資料來源所做的變更。  
  
## <a name="remarks"></a>備註  
  
```  
'BeginBatchUpdate  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT ShipperId, CompanyName, Phone FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
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
  
    ' Send the updates  
    objRs1.UpdateBatch  
'EndBatchUpdate  
```  
  
 如果您正在編輯目前的記錄，或當您呼叫 UpdateBatch 方法時，請新增新的記錄，ADO 會自動呼叫 Update 方法，再傳輸到提供者的批次的變更時，將任何暫止的變更儲存至目前的記錄。  
  
## <a name="see-also"></a>另請參閱  
 [批次模式](../../../ado/guide/data/batch-mode.md)
