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
ms.openlocfilehash: 7dbbbf92c751093d2a7333b7ac1f76888d41d345
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212337"
---
# <a name="ado-event-instantiation-ado-and-wfc"></a>ADO 事件具現化：ADO 和 WFC
ADO for Windows Foundation 類別（ADO/WFC）是以 ADO 事件模型為基礎，並提供簡化的應用程式開發介面。 一般來說，ADO/WFC 會攔截 ADO 事件、將事件參數合併成單一事件類別，然後再呼叫您的事件處理常式。  
  
### <a name="to-use-ado-events-in-adowfc"></a>使用 ADO/WFC 中的 ADO 事件  
  
1.  定義您自己的事件處理常式來處理事件。 例如，如果您想要處理**ConnectionEvent**系列中的**ConnectComplete**事件，您可以使用下列程式碼：  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    {  
        System.out.println("onConnectComplete:" + e);  
    }  
    ```  
  
2.  定義處理常式物件，以代表您的事件處理常式。 對於**ConnectionEvent**類型的事件，處理常式物件應該是**ConnectEventHandler**的資料類型，或**RecordsetEvent**類型的事件的資料類型**RecordsetEventHandler** 。 例如，針對您的**ConnectComplete**事件處理常式撰寫下列程式碼：  
  
    ```  
    ConnectionEventHandler handler =   
        new ConnectionEventHandler(this, "onConnectComplete");  
    ```  
  
     **ConnectionEventHandler**函數的第一個引數是類別的參考，其中包含第二個引數中名為的事件處理常式。  
  
3.  將事件處理常式新增至指定用來處理特定類型事件的處理常式清單。 搭配使用方法與名稱 **，例如附加**項_事件_（*處理常式*）。  
  
4.  ADO/WFC 內部會執行所有 ADO 事件處理常式。 因此，ADO/WFC 事件處理常式會攔截**連接**或**記錄集**作業所造成的事件。  
  
     ADO/WFC 事件處理常式會在 ADO/WFC **ConnectionEvent**類別的實例中傳遞 ado **ConnectionEvent**參數，或在 ado/wfc **RecordsetEvent**類別的實例中傳遞 ado **RecordsetEvent**參數。 這些 ADO/WFC 類別會合並 ADO 事件參數;也就是說，每個 ADO/WFC 類別都會針對所有 ADO **ConnectionEvent**或**RecordsetEvent**方法中的每個唯一參數，各包含一個資料成員。  
  
5.  ADO/WFC 接著會使用 ADO/WFC 事件物件來呼叫您的事件處理常式。 例如，您的**onConnectComplete**處理常式具有如下的簽章：  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     第一個引數是傳送事件的物件類型（[連接](../../../ado/reference/ado-api/connection-object-ado.md)或[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)），而第二個引數是 ADO/WFC 事件物件（**ConnectionEvent**或**RecordsetEvent**）。  
  
     事件處理常式的簽章比 ADO 事件簡單。 不過，您仍然必須瞭解 ADO 事件模型，以知道哪些參數適用于事件，以及如何回應。  
  
6.  從您的事件處理常式返回 ADO 事件的 ADO/WFC 處理常式。 ADO/WFC 會將相關的 ADO/WFC 事件資料成員複製回 ADO 事件參數，然後 ADO 事件處理常式會傳回。  
  
7.  當您完成處理時，請從 ADO/WFC 事件處理常式清單中移除您的處理常式。 使用方法搭配名稱，例如**removeOn**_事件_（*處理常式*）。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO-WFC 語法索引](../../../ado/reference/ado-api/ado-wfc-syntax-index.md)   
 [事件參數](../../../ado/guide/data/event-parameters.md)   
 [事件處理常式如何搭配使用](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [事件的類型](../../../ado/guide/data/types-of-events.md)
