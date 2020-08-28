---
description: ADO 事件具現化：ADO 和 WFC
title: ADO 事件具現化： ADO 和 WFC |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 9ee4be21-657b-407a-afa4-0b27a6b096ce
author: rothja
ms.author: jroth
ms.openlocfilehash: 906f895eade7120b57d401851a0e19203f943980
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991709"
---
# <a name="ado-event-instantiation-ado-and-wfc"></a>ADO 事件具現化：ADO 和 WFC
ADO for Windows Foundation 類別 (ADO/WFC) 建基於 ADO 事件模型，並提供簡化的應用程式設計介面。 一般情況下，ADO/WFC 會攔截 ADO 事件、將事件參數合併為單一事件類別，然後呼叫您的事件處理常式。  
  
### <a name="to-use-ado-events-in-adowfc"></a>若要在 ADO/WFC 中使用 ADO 事件  
  
1.  定義您自己的事件處理常式來處理事件。 例如，如果您想要處理**ConnectionEvent**系列中的**ConnectComplete**事件，您可以使用下列程式碼：  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    {  
        System.out.println("onConnectComplete:" + e);  
    }  
    ```  
  
2.  定義代表事件處理常式的處理常式物件。 處理常式物件應該是**ConnectionEvent**類型事件的資料類型**ConnectEventHandler** ，或**RecordsetEvent**類型事件的資料類型**RecordsetEventHandler** 。 例如，針對您的 **ConnectComplete** 事件處理常式撰寫下列程式碼：  
  
    ```  
    ConnectionEventHandler handler =   
        new ConnectionEventHandler(this, "onConnectComplete");  
    ```  
  
     **ConnectionEventHandler**函式的第一個引數是類別的參考，其中包含第二個引數中所指定的事件處理常式。  
  
3.  將事件處理常式加入至指定用來處理特定事件種類的處理常式清單。 使用具有名稱的方法 **，例如附加**_項 (_ *處理常式*) 。  
  
4.  ADO/WFC 會在內部執行所有 ADO 事件處理常式。 因此，由 ADO.NET/WFC 事件處理常式攔截 **連接** 或 **記錄集** 作業所造成的事件。  
  
     ADO/WFC 事件處理常式會在 ADO/WFC **ConnectionEvent**類別的實例中傳遞 ado **ConnectionEvent**參數，或在 ado/wfc **RecordsetEvent**類別的實例中傳遞 ado **RecordsetEvent**參數。 這些 ADO/WFC 類別會合並 ADO 事件參數;也就是說，每個 ADO/WFC 類別都包含所有 ADO **ConnectionEvent** 或 **RecordsetEvent** 方法中每一個唯一參數的一個資料成員。  
  
5.  ADO/WFC 接著會使用 ADO/WFC 事件物件來呼叫您的事件處理常式。 例如，您的 **onConnectComplete** 處理常式具有如下的簽章：  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     第一個引數是傳送事件 ([連接](../../reference/ado-api/connection-object-ado.md) 或 [記錄集](../../reference/ado-api/recordset-object-ado.md)) 的物件類型，而第二個引數是 ADO/WFC 事件物件 (**ConnectionEvent** 或 **RecordsetEvent**) 。  
  
     事件處理常式的簽章比 ADO 事件簡單得多。 不過，您仍然必須瞭解 ADO 事件模型，才能知道哪些參數適用于事件，以及如何回應。  
  
6.  從事件處理常式返回 ADO 事件的 ADO/WFC 處理常式。 ADO/WFC 會將相關的 ADO/WFC 事件資料成員複製回 ADO 事件參數，然後 ADO 事件處理常式會傳回。  
  
7.  當您完成處理之後，請從 ADO/WFC 事件處理常式清單中移除處理常式。 使用具有名稱的方法，例如 **removeOn**_事件_ 名稱 (*處理常式*) 。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](./ado-event-handler-summary.md)   
 [ADO-WFC 語法索引](../../reference/ado-api/ado-wfc-syntax-index.md)   
 [事件參數](./event-parameters.md)   
 [事件處理常式如何一起運作](./how-event-handlers-work-together.md)   
 [事件的類型](./types-of-events.md)