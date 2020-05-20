---
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
ms.openlocfilehash: dba3be9c80160dca2773c63b2ed7f7c706678625
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761314"
---
# <a name="ado-event-instantiation-visual-basic"></a>ADO 事件具現化：Visual Basic
為了處理 Microsoft® Visual Basic®中的 ADO 事件，您必須使用**WithEvents**關鍵字來宣告模組層級變數。 變數只能宣告為類別模組的一部分，而且必須在模組層級宣告。 但這並不嚴格，因為 Visual Basic **Form**物件也是類別。 處理 ADO 事件最簡單的方式，就是使用**WithEvents**宣告變數。 下列範例會處理**連接**物件的**ConnectComplete**事件：  
  
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
  
 **連接**物件是在**表單**層級使用**WithEvents**關鍵字來進行宣告，以啟用事件處理。 Form_Load 事件處理常式實際上會建立物件，方法是將新的**連接**物件指派給*connEvent* ，然後開啟連接。 當然，實際的應用程式會在 Form_Load 事件處理常式中執行比此處顯示更多的處理。
