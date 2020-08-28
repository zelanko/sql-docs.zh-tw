---
description: 提供者錯誤
title: 提供者錯誤 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b31f530bafd69d59c98893cc2ead29039372dea9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979979"
---
# <a name="provider-errors"></a>提供者錯誤
當提供者錯誤發生時，會傳回-2147467259 的執行階段錯誤。 當您收到此錯誤時，請檢查作用中**連接**物件的 [**錯誤**] 集合，它會包含一或多個描述發生問題的錯誤。  
  
## <a name="the-ado-errors-collection"></a>ADO Errors 集合  
 由於特定的 ADO 作業可能會產生多個提供者錯誤，因此 ADO 會透過 **連接** 物件公開錯誤物件的集合。 如果作業成功完成，且包含一個或多個 **錯誤** 物件（如果發生錯誤，而且提供者引發一或多個錯誤），此集合就不會包含任何物件。 檢查每個錯誤物件，以判斷錯誤的確切原因。  
  
 當您完成處理任何發生的錯誤之後，就可以藉由呼叫 **clear** 方法來清除集合。 在您呼叫**記錄集**物件上的**Resync**、 **UpdateBatch**或**CancelBatch**方法、**連接**物件上的**Open**方法或設定**記錄集**物件的**Filter**屬性之前，明確地清除**錯誤**集合特別重要。 明確清除集合之後，您就可以確定集合中的任何 **錯誤** 物件都不會離開先前的作業。  
  
 某些作業除了錯誤外，還會產生警告。 錯誤物件也會以**錯誤物件**表示警告**Errors** 。 當提供者將警告新增至集合時，不會產生執行階段錯誤。 檢查**錯誤**集合的**Count**屬性，以判斷是否有特定作業產生警告。 如果計數為一或更高，則會將 **錯誤** 物件加入至集合。 一旦您判斷出 **錯誤** 集合中包含錯誤或警告，您可以逐一查看集合，並取得其所包含的每個 **錯誤** 物件的相關資訊。 下列簡短的 Visual Basic 範例會示範這一點：  
  
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
  
 錯誤處理常式包含一個 **For each** 迴圈，可檢查 **錯誤** 集合中的每個物件。 在此範例中，它會累積訊息以供顯示。 在工作程式中，您會撰寫程式碼以針對每個錯誤執行適當的工作，例如關閉所有開啟的檔案，並以合理的方式關閉程式。  
  
## <a name="the-error-object"></a>Error 物件  
 藉由檢查 **error** 物件，您就可以判斷發生了哪些錯誤，以及更重要的是哪個應用程式或哪個物件造成錯誤。 **Error**物件具有下列屬性：  
  
|屬性名稱|描述|  
|-------------------|-----------------|  
|**說明**|所發生錯誤的文字描述。|  
|**HelpCoNtext，説明**|指的是包含所發生錯誤之描述的說明主題和說明檔。|  
|**NativeError**|提供者特定的錯誤號碼。|  
|**Number**|長整數，表示所發生錯誤的 **ErrorValueEnum**) 中所列的 (數目。|  
|**Source**|表示產生錯誤的物件或應用程式的名稱。|  
|**SQLState**|提供者在 SQL 語句的過程中傳回的五個字元的錯誤碼。|  
  
 ADO **Error** 物件與標準 Visual Basic **Err** 物件非常類似。 其屬性描述發生的錯誤。 除了錯誤的數目之外，您也會收到兩個相關的資訊片段。 **NativeError**屬性包含您所使用之提供者特定的錯誤號碼。 在上述範例中，提供者是適用于 SQL Server 的 Microsoft OLE DB 提供者，因此 **NativeError** 將包含 SQL Server 特定的錯誤。 **SQLState**屬性具有五個字母的代碼，描述 SQL 語句中的錯誤。  
  
## <a name="event-related-errors"></a>事件相關的錯誤  
 發生事件相關的錯誤時，也會使用 **Error** 物件。 您可以藉由檢查傳遞做為事件參數的 **錯誤** 物件，判斷引發 ADO 事件的進程中是否發生錯誤。  
  
 如果導致事件的作業成功結束，則事件處理常式的 *adStatus* 參數會設定為 *adStatusOK*。 另一方面，如果引發事件的作業不成功，則 *adStatus* 參數會設定為 *adStatusErrorsOccurred*。 在此情況下， *pError* 參數會包含描述錯誤的 **錯誤** 物件。
