---
description: ADO 事件具現化：Visual Basic
title: ADO 事件具現化： Visual Basic |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
ms.assetid: dce0a2a3-326f-4aaf-a822-6c5549833afa
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ea53b5d48c0eb72fe91ebeda2d2612437cf4c36
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453790"
---
# <a name="ado-event-instantiation-visual-basic"></a>ADO 事件具現化：Visual Basic
為了處理 Microsoft® Visual Basic®中的 ADO 事件，您必須使用 **WithEvents** 關鍵字宣告模組層級變數。 變數只能宣告為類別模組的一部分，而且必須在模組層級宣告。 不過，這並不像它的限制，因為 Visual Basic **Form** 物件也是類別。 處理 ADO 事件最簡單的方式，就是使用 **WithEvents**宣告變數。 下列範例會處理**連接**物件的**ConnectComplete**事件：  
  
```  
' BeginEventExampleVB02  
Dim WithEvents connEvent As Connection  
Attribute connEvent.VB_VarHelpID = -1  
  
Private Sub Form_Load()  
Dim strConn As String  
  
   ' Create a new object with event  
   ' handling enabled.  
   strConn = "Provider=sqloledb;" & _  
      "Data Source=MyServer;" & _  
      "Initial Catalog=Northwind;" & _  
      "Integrated Security=SSPI;"  
   Set connEvent = New ADODB.Connection  
   connEvent.Open strConn  
End Sub  
  
Private Sub connEvent_ConnectComplete(ByVal pError As ADODB.Error, _  
    adStatus As ADODB.EventStatusEnum, _  
    ByVal pConnection As ADODB.Connection)  
Dim strMsg As String  
  
   If adStatus = adStatusErrorsOccurred Then  
      Select Case pError.Number  
         Case adErrOperationCancelled  
            ' The operation was cancelled in the  
            ' Will event. Notify the user and exit.  
            strMsg = "I'm sorry you can't connect right now." & vbCrLf  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
         Case Else  
            strMsg = "Error " & Format(pError.Number) & vbCrLf  
            strMsg = strMsg & pError.Description  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
      End Select  
   End If  
   frmWait.btnOK.Enabled = True  
End Sub  
' EndEventExampleVB02  
```  
  
 **連接**物件是在**表單**層級使用**WithEvents**關鍵字宣告來啟用事件處理。 Form_Load 的事件處理常式會藉由將新的 **連接** 物件指派給 *connEvent* ，然後開啟連接，來實際建立物件。 當然，實際的應用程式會在 Form_Load 的事件處理常式中進行更多處理，而不是此處所示。
