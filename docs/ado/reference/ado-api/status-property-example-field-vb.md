---
title: Status 屬性範例（Field）（VB） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Status property [ADO Field], Visual Basic example
ms.assetid: fdd09b60-39c7-44be-8008-e891a031f80e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c28a0b615a9f250c8539e87abf9fefbc11f513ee
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67916821"
---
# <a name="status-property-example-field-vb"></a>Status 屬性範例 (Field) (VB)
下列範例會使用[網際網路發行提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)，從讀取/寫入資料夾中開啟檔。 [記錄](../../../ado/reference/ado-api/record-object-ado.md)之[欄位](../../../ado/reference/ado-api/field-object.md)物件的[Status](../../../ado/reference/ado-api/status-property-ado-field.md)屬性會先設定為**adFieldPendingInsert**，然後更新為**adFieldOk**。  
  
```  
'BeginStatusFieldVB  
  
 ' to integrate this code replace the values in the source string  
  
Sub Main()  
  
   Dim File As ADODB.Record  
   Dim strFile As String  
   Dim Cnxn As ADODB.Connection  
   Dim strCnxn As String  
  
   Set Cnxn = New ADODB.Connection  
   strCnxn = "url=https://MyServer/"  
   Cnxn.Open strCnxn  
  
   Set File = New ADODB.Record  
   strFile = "Folder/FileName"  
   ' Open a read/write document  
   File.Source = strFile  
   File.ActiveConnection = Cnxn  
   File.Mode = adModeReadWrite  
   File.Open  
  
   Debug.Print "Append a couple of fields"  
  
   File.Fields.Append "chektest:fld1", adWChar, 42, adFldUpdatable, "fld1"  
   File.Fields.Append "chektest:fld2", adWChar, 42, adFldUpdatable, "fld2"  
  
   Debug.Print "status for the fields"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert  
  
    'turn off error-handling to verify field status  
   On Error Resume Next  
  
   File.Fields.Update  
  
   Debug.Print "Update succeeds"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert + adFieldUnavailable  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert + adFieldUnavailable  
  
    ' resume default error-handling  
   On Error GoTo 0  
  
     ' clean up  
    File.Close  
    Cnxn.Close  
    Set File = Nothing  
    Set Cnxn = Nothing  
  
End Sub  
'EndStatusFieldVB  
```  
  
 下列範例會從檔中開啟的**記錄**，刪除已知的**欄位**。 **Status**屬性會先設定為**AdFieldOK**，然後**adFieldPendingUnknown**。  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
 下列程式碼會從唯讀檔案上開啟的**記錄**中刪除**欄位**。 **狀態**會設定為**adFieldPendingDelete**。 在[更新](../../../ado/reference/ado-api/update-method.md)時，刪除將會失敗，且**狀態**會是**adFieldPendingDelete**加上**adFieldPermissionDenied**。 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)會清除擱置**狀態**設定。  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
## <a name="see-also"></a>另請參閱  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)   
 [Record 物件（ADO）](../../../ado/reference/ado-api/record-object-ado.md)   
 [Status 屬性 (ADO Field)](../../../ado/reference/ado-api/status-property-ado-field.md)
