---
description: 傳送更新：UpdateBatch 方法
title: 正在傳送更新： UpdateBatch 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 87123797-831f-48e0-94b5-f669f9ca194a
author: rothja
ms.author: jroth
ms.openlocfilehash: 6f4e6a94282687ed70f10552e2dedf9c9312433e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979709"
---
# <a name="sending-the-updates-updatebatch-method"></a>傳送更新：UpdateBatch 方法
下列程式碼會將 LockType 屬性設定為 adLockBatchOptimistic，並將 CursorLocation 設定為 adUseClient，以批次模式開啟記錄集。 它會加入兩筆新記錄，並變更現有記錄中的欄位值、儲存原始值，然後呼叫 UpdateBatch 將變更傳回資料來源。  
  
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
  
 如果您要編輯目前的記錄，或在呼叫 UpdateBatch 方法時加入新的記錄，ADO 會自動呼叫 Update 方法，在將批次變更傳送給提供者之前，先將任何暫止的變更儲存至目前的記錄。  
  
## <a name="see-also"></a>另請參閱  
 [批次模式](../../../ado/guide/data/batch-mode.md)
