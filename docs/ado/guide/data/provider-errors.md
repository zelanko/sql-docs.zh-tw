---
title: 提供者錯誤，|Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- errors collection [ADO]
- provider errors [ADO]
- event-related errors [ADO]
- errors [ADO], provider
- Error object [ADO], provider errors
ms.assetid: cc7d6ff9-2034-45c6-9d61-90b177010054
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ddc3e887e15b856e0caddc9b97f4bb1e1f6078d1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="provider-errors"></a>提供者錯誤
發生提供者錯誤時，會傳回-2147467259 的執行階段錯誤。 當您收到這個錯誤時，請檢查**錯誤**作用中的集合**連接**物件，會包含一個或多個描述所發生的錯誤。  
  
## <a name="the-ado-errors-collection"></a>ADO 錯誤集合  
 因為特定的 ADO 作業可以產生多個提供者錯誤，ADO 會公開透過錯誤物件的集合**連接**物件。 此集合包含任何物件，如果作業成功地結束，包含一或多個**錯誤**物件，如果發生錯誤，提供者引發一個或多個錯誤。 檢查每個錯誤物件，以判斷錯誤的確切原因。  
  
 一旦您完成處理任何錯誤發生時，您可以藉由呼叫清除集合**清除**方法。 務必明確清除的**錯誤**集合才能呼叫**重新同步處理**， **UpdateBatch**，或**CancelBatch**方法**資料錄集**物件**開啟**方法上的**連接**物件，或設定**篩選**屬性**資料錄集**物件。 藉由明確清除集合，可以是特定的任何**錯誤**物件在集合中的沒有剩餘了前一項作業。  
  
 某些作業可能會產生錯誤加上的警告。 警告也都由**錯誤**中的物件**錯誤**集合。 當提供者會將警告加入至集合時，它不會產生執行階段錯誤。 請檢查**計數**屬性**錯誤**來決定是否產生警告的特定作業的集合。 如果計數為其中一個或更多，**錯誤**物件加入集合。 一旦您判斷出**錯誤**集合包含錯誤或警告，您可以逐一查看集合，並擷取每個資訊**錯誤**它所包含的物件。 下列簡短的 Visual Basic 範例為其示範：  
  
```  
' BeginErrorHandlingVB02  
Private Function DeleteCustomer(ByVal CompanyName As String) As Long  
    On Error GoTo DeleteCustomerError  
  
    rst.Find "CompanyName='" & CompanyName & "'"  
DeleteCustomerError:  
Dim objError As ADODB.Error  
Dim strError As String  
  
    If cnn.Errors.Count > 0 Then  
        For Each objError In cnn.Errors  
            strError = strError & "Error #" & objError.Number & _  
                " " & objError.Description & vbCrLf & _  
                "NativeError: " & objError.NativeError & vbCrLf & _  
                "SQLState: " & objError.SQLState & vbCrLf & _  
                "Reported by: " & objError.Source & vbCrLf & _  
                "Help file: " & objError.HelpFile & vbCrLf & _  
                "Help Context ID: " & objError.HelpContext  
        Next  
        MsgBox strError  
    End If  
End Function  
' EndErrorHandlingVB02  
```  
  
 錯誤處理常式包括**每個**會檢查每個物件中的迴圈**錯誤**集合。 在此範例中，它會顯示訊息。 在工作的程式中，您會撰寫程式碼以執行適當的工作，每個錯誤，例如關閉所有開啟的檔案和關閉程式，以正確順序的方式。  
  
## <a name="the-error-object"></a>Error 物件  
 藉由檢查**錯誤**物件，您可以決定發生的錯誤，而且更重要的是，哪些應用程式或哪些物件造成錯誤。 **錯誤**物件具有下列屬性：  
  
|屬性名稱|Description|  
|-------------------|-----------------|  
|**說明**|發生錯誤的文字描述。|  
|**HelpContext，說明檔**|指的說明主題，並說明檔案，含有發生之錯誤的描述。|  
|**NativeError**|提供者特定錯誤號碼。|  
|**數字**|長整數，表示數字 (列在**ErrorValueEnum**) 發生的錯誤。|  
|**Source**|表示產生錯誤的應用程式之物件的名稱。|  
|**SQLState**|提供者會傳回 SQL 陳述式的程序期間的五個字元的錯誤程式碼。|  
  
 ADO**錯誤**物件是非常類似於標準的 Visual Basic **Err**物件。 其屬性會描述所發生的錯誤。 除了發生的錯誤數目，您也會收到兩個相關的資訊片段。 **NativeError**屬性包含錯誤號碼您正在使用提供者特定的。 在上述範例中，提供者是 Microsoft OLE DB Provider for SQL Server，因此**NativeError**會包含 SQL Server 特定的錯誤。 **SQLState**屬性具有描述 SQL 陳述式中的發生錯誤的五個字母代碼。  
  
## <a name="event-related-errors"></a>與事件相關的錯誤  
 **錯誤**事件相關的錯誤發生時，也會使用物件。 您可以判斷是否藉由檢查引發 ADO 事件的處理序中發生錯誤**錯誤**做為事件參數傳遞的物件。  
  
 如果會造成事件的作業成功，卻*adStatus*事件處理常式的參數會設定為*adStatusOK*。 另一方面，如果引發事件的作業不成功， *adStatus*參數設定為*adStatusErrorsOccurred*。 在此情況下， *pError*參數會包含**錯誤**描述錯誤的物件。
