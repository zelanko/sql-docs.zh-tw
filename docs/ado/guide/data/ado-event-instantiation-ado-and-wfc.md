---
title: "ADO 事件具現化： ADO 和 WFC |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9ee4be21-657b-407a-afa4-0b27a6b096ce
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4d46ec3bdad80879ddc4a931d8668a5298972e58
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="ado-event-instantiation-ado-and-wfc"></a>ADO 事件具現化： ADO 和 WFC
ADO 的 Windows Foundation 類別 (ADO/WFC) ADO 事件模型為基礎，提供簡化的應用程式開發介面。 一般情況下，ADO/WFC 攔截 ADO 事件、 將事件參數合併成單一事件類別，然後再呼叫事件處理常式。  
  
### <a name="to-use-ado-events-in-adowfc"></a>若要使用 ADO/WFC 使用 ADO 的事件  
  
1.  定義您自己的事件處理常式來處理事件。 例如，如果您想要處理**ConnectComplete**中的事件**ConnectionEvent**系列，您可能會使用此程式碼：  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    {  
        System.out.println("onConnectComplete:" + e);  
    }  
    ```  
  
2.  定義處理常式物件來代表您的事件處理常式。 事件處理常式物件的資料類型應為**ConnectEventHandler**型別的事件**ConnectionEvent**，或資料類型**RecordsetEventHandler** 類型的事件**RecordsetEvent**。 例如，程式碼的下列您**ConnectComplete**事件處理常式：  
  
    ```  
    ConnectionEventHandler handler =   
        new ConnectionEventHandler(this, "onConnectComplete");  
    ```  
  
     第一個引數**ConnectionEventHandler**建構函式是包含名為第二個引數中的事件處理常式的類別的參考。  
  
3.  將事件處理常式加入指定用來處理特定類型的事件處理常式的清單。 使用此方法的名稱，例如**addOn***EventName*(*處理常式*)。  
  
4.  ADO/WFC 在內部實作所有 ADO 事件處理常式。 因此，事件的原因**連接**或**資料錄集**ADO/WFC 事件處理常式攔截作業。  
  
     ADO/WFC 事件處理常式會傳遞 ADO **ConnectionEvent**參數執行個體中的 ADO/WFC **ConnectionEvent**類別或 ADO **RecordsetEvent**中的參數執行個體的 ADO/WFC **RecordsetEvent**類別。 這些 ADO/WFC 類別合併 ADO 事件參數;也就是說，每個 ADO/WFC 類別包含一個資料成員中每個唯一參數所有 ADO **ConnectionEvent**或**RecordsetEvent**方法。  
  
5.  ADO/WFC 接著會呼叫事件處理常式與 ADO/WFC 事件物件。 例如，您**onConnectComplete**處理常式的簽章如下：  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     第一個引數會傳送事件的物件類型 ([連接](../../../ado/reference/ado-api/connection-object-ado.md)或[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md))，第二個引數是 ADO/WFC 事件物件 (**ConnectionEvent**或**RecordsetEvent**)。  
  
     事件處理常式的簽章會比 ADO 事件。 不過，您仍然必須瞭解知道參數套用至事件，以及如何回應的 ADO 事件模型。  
  
6.  從您的事件處理常式返回 ADO 事件的 ADO/WFC 處理常式。 ADO/WFC 複製回 ADO 事件參數，ADO/WFC 相關的事件資料成員，然後 ADO 事件處理常式傳回。  
  
7.  當您準備完成處理，從 ADO/WFC 事件處理常式的清單中移除您的處理常式。 使用此方法的名稱，例如**removeOn***EventName*(*處理常式*)。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO-WFC 語法索引](../../../ado/reference/ado-api/ado-wfc-syntax-index.md)   
 [事件參數](../../../ado/guide/data/event-parameters.md)   
 [事件處理常式一起運作的方式](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [事件類型](../../../ado/guide/data/types-of-events.md)

