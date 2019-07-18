---
title: ADO 事件具現化：Visual Basic |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ead713a37d4ecf8bdfecd0d6c485684d1ad0777f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926073"
---
# <a name="ado-event-instantiation-visual-basic"></a>ADO 事件具現化：Visual Basic
若要處理 ADO 事件，在 Microsoft® Visual Basic® 中的，您必須宣告模組層級變數 using **WithEvents**關鍵字。 變數可以宣告只為一部分的類別模組，而且必須在模組層級宣告。 這是不一樣嚴格，因為看似，不過，因為 Visual Basic**表單**物件也是類別。 最簡單的方式來處理 ADO 事件是要宣告使用變數**WithEvents**。 下列範例會處理**ConnectComplete**事件**連線**物件：  
  
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
  
 **連接**物件在宣告**表單**層級使用**WithEvents**關鍵字來啟用事件處理。 實際指派新建立物件的 Form_Load 事件處理常式**連接**物件*connEvent* ，然後開啟 連線。 當然，實際的應用程式一樣 Form_Load 事件處理常式比此處顯示更多的處理。
