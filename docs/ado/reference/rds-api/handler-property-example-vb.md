---
description: Handler 屬性範例 (VB)
title: 處理常式屬性範例 (VB) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Handler property [ADO], Visual Basic example
ms.assetid: 9664f9a6-65fc-4e7f-be3d-3e4b501b558a
author: rothja
ms.author: jroth
ms.openlocfilehash: 925eafa58ced6d3bd4214616eac65fe5227c5ae8
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982099"
---
# <a name="handler-property-example-vb"></a>Handler 屬性範例 (VB)
> [!IMPORTANT]
>  從 Windows 8 和 Windows Server 2012 開始，Windows 作業系統中不再包含 RDS 伺服器元件 (如需詳細) 資訊，請參閱 Windows 8 和 [Windows server 2012 相容性操作手冊](https://www.microsoft.com/download/details.aspx?id=27416) 。 未來的 Windows 版本將移除 RDS 用戶端元件。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 使用 RDS 的應用程式應該遷移至 [WCF 資料服務](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 這個範例示範 [RDS DataControl](./datacontrol-object-rds.md) 物件 [處理常式](./handler-property-rds.md) 屬性。  (如需詳細資料，請參閱 [DataFactory 自訂](../../guide/remote-data-service/datafactory-customization.md) 。 )   
  
 假設參數檔中的下列區段（Msdfmap.ini）位於伺服器上：  
  
```  
[connect AuthorDataBase]  
Access=ReadWrite  
Connect="DSN=Pubs"  
[sql AuthorById]  
SQL="SELECT * FROM Authors WHERE au_id = ?"  
```  
  
 您的程式碼看起來如下所示。 指派給 [SQL](./sql-property.md) 屬性的命令將會符合 ***AuthorById*** 識別碼，並將會抓取作者 Michael O'Leary 的資料列。 將 **DataControl** 物件 **記錄集** 屬性指派給中斷連接的 [記錄集](../ado-api/recordset-object-ado.md) 物件，純粹是撰寫程式碼的便利性。  
  
```  
'BeginHandlerVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim dc As New DataControl  
    Dim rst As ADODB.Recordset  
  
    dc.Handler = "MSDFMAP.Handler"  
    dc.ExecuteOptions = 1  
    dc.FetchOptions = 1  
    dc.Server = "https://MyServer"  
    dc.Connect = "Data Source=AuthorDataBase"  
    dc.SQL = "AuthorById('267-41-2394')"  
    dc.Refresh                  'Retrieve the record  
    Set rst = dc.Recordset      'Use another Recordset as a convenience  
    Debug.Print "Author is '" & rst!au_fname & " " & rst!au_lname & "'"  
  
    ' clean up  
    If rst.State = adStateOpen Then rst.Close  
    Set rst = Nothing  
    Set dc = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rst Is Nothing Then  
        If rst.State = adStateOpen Then rst.Close  
    End If  
    Set rst = Nothing  
    Set dc = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndHandlerVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [DataControl 物件 (RDS) ](./datacontrol-object-rds.md)   
 [Handler 屬性 (RDS)](./handler-property-rds.md)