---
title: ADO 事件具現化： ADO 和 WFC |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 9ee4be21-657b-407a-afa4-0b27a6b096ce
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 753deabf2c8ae69c535b60f5c43dca20b002ed63
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811986"
---
# <a name="ado-event-instantiation-ado-and-wfc"></a>ADO 事件具現化：ADO 和 WFC
ADO 的 Windows Foundation Classes (ADO/WFC) 為基礎的 ADO 事件模型，並提供簡化的應用程式開發介面。 一般情況下，ADO/WFC 攔截 ADO 事件、 將事件參數合併成單一的事件類別，然後再呼叫事件處理常式。  
  
### <a name="to-use-ado-events-in-adowfc"></a>ADO 事件用於 ADO/WFC  
  
1.  定義您自己的事件處理常式，來處理事件。 例如，如果您想要處理**ConnectComplete**中的事件**ConnectionEvent**系列，您可以使用此程式碼：  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    {  
        System.out.println("onConnectComplete:" + e);  
    }  
    ```  
  
2.  定義處理常式物件來代表您的事件處理常式。 事件處理常式物件應該是資料型別**ConnectEventHandler**之事件的型別**ConnectionEvent**，或資料型別**RecordsetEventHandler**之事件的型別**RecordsetEvent**。 例如，程式碼的下列事項您**ConnectComplete**事件處理常式：  
  
    ```  
    ConnectionEventHandler handler =   
        new ConnectionEventHandler(this, "onConnectComplete");  
    ```  
  
     第一個引數**ConnectionEventHandler**建構函式是類別，其中包含名為第二個引數中的事件處理常式的參考。  
  
3.  指定用來處理特定類型的事件處理常式的清單中加入事件處理常式。 使用此方法的名稱，例如 **addOn** *EventName*(*處理常式*)。  
  
4.  ADO/WFC 在內部實作所有 ADO 事件處理常式。 因此，事件會因**連接**或是**資料錄集**ADO/WFC 事件處理常式攔截作業。  
  
     ADO/WFC 事件處理常式會將傳遞的 ADO **ConnectionEvent** ADO/WFC 的執行個體中的參數**ConnectionEvent**類別或 ADO **RecordsetEvent**中的參數執行個體的 ADO/WFC **RecordsetEvent**類別。 這些 ADO/WFC 類別合併 ADO 事件參數;也就是每一個 ADO/WFC 類別包含一個資料成員的每個唯一的參數，在所有 ADO **ConnectionEvent**或是**RecordsetEvent**方法。  
  
5.  ADO/WFC 接著會呼叫事件處理常式與 ADO/WFC 事件物件。 例如，您**onConnectComplete**處理常式有簽章，就像這樣：  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     第一個引數會傳送事件的物件類型 ([連接](../../../ado/reference/ado-api/connection-object-ado.md)或是[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md))，第二個引數是 ADO/WFC 事件物件 (**ConnectionEvent**或**RecordsetEvent**)。  
  
     您的事件處理常式的簽章會比使用 ADO 事件。 不過，您仍然必須瞭解 ADO 事件模型，知道參數套用至事件，以及如何回應。  
  
6.  從您的事件處理常式返回 ADO 事件的 ADO/WFC 處理常式。 ADO/WFC 回到 ADO 事件參數中，複製相關的 ADO/WFC 事件資料成員，並傳回 ADO 事件處理常式。  
  
7.  當您已完成處理，從 ADO/WFC 事件處理常式的清單中移除您的處理常式。 使用此方法的名稱，例如 **removeOn** *EventName*(*處理常式*)。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO-WFC 語法索引](../../../ado/reference/ado-api/ado-wfc-syntax-index.md)   
 [事件參數](../../../ado/guide/data/event-parameters.md)   
 [事件處理常式如何一起運作](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [事件的類型](../../../ado/guide/data/types-of-events.md)
