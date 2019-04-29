---
title: 提供者錯誤 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors collection [ADO]
- provider errors [ADO]
- event-related errors [ADO]
- errors [ADO], provider
- Error object [ADO], provider errors
ms.assetid: cc7d6ff9-2034-45c6-9d61-90b177010054
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18370885fedb106f02c9b404ea946680aa048b8b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62911367"
---
# <a name="provider-errors"></a>提供者錯誤
發生提供者錯誤時，會傳回-2147467259 的執行階段錯誤。 當您收到此錯誤時，請檢查**錯誤**作用中的集合**連線**物件，其中會包含描述所發生的一或多個錯誤。  
  
## <a name="the-ado-errors-collection"></a>ADO 錯誤集合  
 因為特定的 ADO 作業可能會產生多個提供者錯誤，ADO 會公開透過錯誤物件的集合**連線**物件。 此集合包含任何物件，如果作業成功結束，而且包含一或多個**錯誤**物件如果發生錯誤，而且提供者會引發一或多個錯誤。 檢查每個錯誤物件，以判斷錯誤的確切原因。  
  
 當您完成處理所發生的任何錯誤時，您可以清除集合，藉由呼叫**清除**方法。 它是特別重要，若要明確地清除**錯誤**集合，然後再呼叫**重新同步處理**， **UpdateBatch**，或**CancelBatch**上的方法**資料錄集**物件**開啟**方法**連線**物件，或設定**篩選**屬性**資料錄集**物件。 藉由明確地清除集合，可以是特定的任何**錯誤**集合中沒有剩餘物件先前的作業。  
  
 某些作業可能會產生除了錯誤的警告。 警告也都由**錯誤**中的物件**錯誤**集合。 當提供者會將警告加入至集合時，它不會產生執行階段錯誤。 請檢查**計數**屬性**錯誤**來決定是否產生警告的特定作業的集合。 如果計數為一個以上時，**錯誤**物件加入集合。 一旦您判斷出**錯誤**集合包含錯誤或警告，您可以逐一查看集合，並擷取每個資訊**錯誤**它所包含的物件。 下列簡短的 Visual Basic 範例示範：  
  
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
  
 包含錯誤處理常式**針對每個**會檢查每個物件中的迴圈**錯誤**集合。 在此範例中，它會一直累積顯示的訊息。 可運作的程式，在中，您會撰寫程式碼來執行適當的工作，針對每個錯誤，例如關閉所有開啟的檔案，並關閉程式，以進行有條理的方式。  
  
## <a name="the-error-object"></a>Error 物件  
 藉由檢查**錯誤**物件，您可以決定發生哪些錯誤，而且更重要的是，哪些應用程式或哪些物件造成錯誤。 **錯誤**物件具有下列屬性：  
  
|屬性名稱|描述|  
|-------------------|-----------------|  
|**說明**|發生錯誤的文字描述。|  
|**HelpContext、 HelpFile**|是指包含所發生的錯誤描述的說明主題，並說明檔案。|  
|**NativeError**|提供者特有的錯誤數目。|  
|**數字**|長整數，表示數字 (列入**ErrorValueEnum**) 發生的錯誤。|  
|**Source**|表示產生錯誤的應用程式之物件的名稱。|  
|**SQLState**|提供者會傳回 SQL 陳述式的過程中五個字元的錯誤程式碼。|  
  
 ADO**錯誤**物件是非常類似於標準的 Visual Basic **Err**物件。 其屬性會描述所發生的錯誤。 除了錯誤數目，您也會收到兩個相關的資訊片段。 **NativeError**屬性包含錯誤號碼您正在使用提供者特定的。 在上述範例中，提供者是 Microsoft OLE DB Provider for SQL Server，因此**NativeError**會包含 SQL Server 特有的錯誤。 **SQLState**屬性具有描述 SQL 陳述式中的發生錯誤的五個字母代碼。  
  
## <a name="event-related-errors"></a>與事件相關的錯誤  
 **錯誤**事件相關的錯誤發生時，也會使用物件。 您可以判斷是否藉由檢查引發 ADO 事件的處理序中發生的錯誤**錯誤**做為事件參數傳遞的物件。  
  
 如果引發事件的作業成功，結束*adStatus*事件處理常式的參數會設定為*adStatusOK*。 另一方面，如果不成功，引發事件的作業*adStatus*參數設為*adStatusErrorsOccurred*。 在此情況下， *pError*參數會包含**錯誤**描述錯誤的物件。
