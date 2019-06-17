---
title: Stream 物件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream
helpviewer_keywords:
- Stream object [ADO]
ms.assetid: 0514531f-009d-4519-abc3-d727014a39f1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 509f91b3e19b8e1215919ce89a98c6ac1c8fc74f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710752"
---
# <a name="stream-object-ado"></a>Stream 物件 (ADO)
表示二進位資料或文字資料流。  
  
 在樹狀結構階層中的檔案系統或電子郵件系統，例如[記錄](../../../ado/reference/ado-api/record-object-ado.md)可能會有預設二進位資料流與它相關聯的位元，其中包含檔案或電子郵件的內容。 A **Stream**物件可用來操作欄位或記錄，其中包含這些資料流的資料。 A **Stream**物件可以透過下列方式取得：  
  
-   從 URL，指向包含二進位或文字資料的物件 （通常是檔案）。 這個物件可以是簡單的文件中，**記錄**物件，表示結構化文件或資料夾。  
  
-   預設值 %installationdirectory **Stream**相關聯的物件**記錄**物件。 您可以取得相關聯的預設資料流**記錄**物件時**記錄**開啟時，若要消除往返只開啟資料流。  
  
-   藉由執行個體化**Stream**物件。 這些**Stream**物件可以用來儲存資料，您的應用程式的目的。 不同於**Stream** URL 或預設值相關聯**Stream**的**記錄**，具現化**Stream**沒有與相關聯預設的基礎來源。  
  
 使用的方法和屬性的**Stream**物件時，您可以執行下列動作：  
  
-   開啟**Stream**物件**記錄**或 URL[開啟](../../../ado/reference/ado-api/open-method-ado-stream.md)方法。  
  
-   關閉**Stream**具有[關閉](../../../ado/reference/ado-api/close-method-ado.md)方法。  
  
-   輸入位元組或文字**Stream**具有[撰寫](../../../ado/reference/ado-api/write-method.md)並[WriteText](../../../ado/reference/ado-api/writetext-method.md)方法。  
  
-   讀取位元組**Stream**具有[讀取](../../../ado/reference/ado-api/read-method.md)並[ReadText](../../../ado/reference/ado-api/readtext-method.md)方法。  
  
-   撰寫任何**Stream**仍在 ADO 中的資料緩衝至基礎物件，但[排清](../../../ado/reference/ado-api/flush-method-ado.md)方法。  
  
-   複製的內容**Stream**到另一個**Stream**具有[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)方法。  
  
-   控制如何從具有原始程式檔讀取行[SkipLine](../../../ado/reference/ado-api/skipline-method.md)方法並[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)屬性。  
  
-   判斷使用的資料流位置的結尾[EOS](../../../ado/reference/ado-api/eos-property.md)屬性並[SetEOS](../../../ado/reference/ado-api/seteos-method.md)方法。  
  
-   儲存和還原的檔案中的資料[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)並[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)方法。  
  
-   指定用於儲存字元集**Stream**具有[字元集](../../../ado/reference/ado-api/charset-property-ado.md)屬性。  
  
-   暫止的非同步**Stream**操作[取消](../../../ado/reference/ado-api/cancel-method-ado.md)方法。  
  
-   判斷位元組數目**Stream**具有[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)屬性。  
  
-   控制項中目前的位置**Stream**具有[位置](../../../ado/reference/ado-api/position-property-ado.md)屬性。  
  
-   判斷資料中的型別**Stream**具有[型別](../../../ado/reference/ado-api/type-property-ado-stream.md)屬性。  
  
-   判斷目前的狀態**Stream** （已關閉，開啟，或執行） 與[狀態](../../../ado/reference/ado-api/state-property-ado.md)屬性。  
  
-   指定的存取模式**Stream**具有[模式](../../../ado/reference/ado-api/mode-property-ado.md)屬性。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 <<c0> [ 絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 **Stream**物件而言是安全的指令碼。  
  
 此章節包含下列主題。  
  
-   [Stream 物件屬性、 方法和事件](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [記錄和資料流](../../../ado/guide/data/records-and-streams.md)
