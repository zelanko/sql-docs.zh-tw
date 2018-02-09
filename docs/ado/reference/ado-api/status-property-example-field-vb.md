---
title: "狀態屬性範例 （欄位） (VB) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Status property [ADO Field], Visual Basic example
ms.assetid: fdd09b60-39c7-44be-8008-e891a031f80e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4ea3ebba271ebdc12802b31cc1f50cdd3befead0
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="status-property-example-field-vb"></a>狀態屬性範例 （欄位） (VB)
下列範例會從讀取/寫入資料夾，請使用開啟的文件[網際網路發行的提供者](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 [狀態](../../../ado/reference/ado-api/status-property-ado-field.md)屬性[欄位](../../../ado/reference/ado-api/field-object.md)物件[記錄](../../../ado/reference/ado-api/record-object-ado.md)先設為**adFieldPendingInsert**，然後更新至**adFieldOk**。  
  
```  
'BeginStatusFieldVB  
  
 ' to integrate this code replace the values in the source string  
  
Sub Main()  
  
   Dim File As ADODB.Record  
   Dim strFile As String  
   Dim Cnxn As ADODB.Connection  
   Dim strCnxn As String  
  
   Set Cnxn = New ADODB.Connection  
   strCnxn = "url=http://MyServer/"  
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
  
 下列範例會刪除已知**欄位**從**記錄**開啟文件中。 **狀態**屬性第一次將設定為**adFieldOK**，然後**adFieldPendingUnknown**。  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
 下列程式碼會刪除**欄位**從**記錄**上唯讀的文件開啟。 **狀態**會設定為**adFieldPendingDelete**。 在[更新](../../../ado/reference/ado-api/update-method.md)，則刪除作業將會失敗並**狀態**將**adFieldPendingDelete**加上**adFieldPermissionDenied**。 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)清除暫止**狀態**設定。  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
## <a name="see-also"></a>另請參閱  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)   
 [記錄物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Status 屬性 (ADO Field)](../../../ado/reference/ado-api/status-property-ado-field.md)
