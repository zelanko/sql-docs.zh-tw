---
title: "資料流物件 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Stream
helpviewer_keywords:
- Stream object [ADO]
ms.assetid: 0514531f-009d-4519-abc3-d727014a39f1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b074a26bdd82bd4356620dbd0b12dc0b7f1c75c7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="stream-object-ado"></a>資料流物件 (ADO)
表示二進位資料或文字資料流。  
  
 在樹狀結構階層中的檔案系統或電子郵件系統，例如[記錄](../../../ado/reference/ado-api/record-object-ado.md)可能會有預設的二進位資料流與它相關聯的位元，其中包含的檔案或電子郵件的內容。 A**資料流**物件可以用來操作欄位或記錄包含這些資料流的資料。 A**資料流**物件可透過下列方式：  
  
-   從指向包含二進位或文字資料的物件 （通常檔案） 的 URL。 這個物件可以是簡單的文件，**記錄**物件，代表結構化文件或資料夾。  
  
-   開啟預設**資料流**物件相關聯**記錄**物件。 您可以取得相關聯的預設資料流**記錄**物件時**記錄**開啟時，若要消除往返只開啟資料流。  
  
-   藉由執行個體化**資料流**物件。 這些**資料流**物件可以用來儲存資料的應用程式的用途。 不同於**資料流**URL 或預設值相關聯**資料流**的**記錄**，具現化**資料流**與沒有關聯預設的基礎來源。  
  
 使用的方法和屬性的**資料流**物件，您可以執行下列：  
  
-   開啟**資料流**物件從**記錄**或 URL 與[開啟](../../../ado/reference/ado-api/open-method-ado-stream.md)方法。  
  
-   關閉**資料流**與[關閉](../../../ado/reference/ado-api/close-method-ado.md)方法。  
  
-   輸入文字或位元組**資料流**與[寫入](../../../ado/reference/ado-api/write-method.md)和[WriteText](../../../ado/reference/ado-api/writetext-method.md)方法。  
  
-   讀取位元組從**資料流**與[讀取](../../../ado/reference/ado-api/read-method.md)和[ReadText](../../../ado/reference/ado-api/readtext-method.md)方法。  
  
-   寫入任何**資料流**仍在 ADO 中的資料緩衝區的基礎物件[排清](../../../ado/reference/ado-api/flush-method-ado.md)方法。  
  
-   複製的內容**資料流**到另一個**資料流**與[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)方法。  
  
-   控制讀取方式的幾行的原始程式檔從[SkipLine](../../../ado/reference/ado-api/skipline-method.md)方法和[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)屬性。  
  
-   判斷使用的資料流位置的結尾[EOS](../../../ado/reference/ado-api/eos-property.md)屬性和[SetEOS](../../../ado/reference/ado-api/seteos-method.md)方法。  
  
-   儲存和還原的檔案中的資料[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)和[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)方法。  
  
-   指定用來儲存的字元集**資料流**與[Charset](../../../ado/reference/ado-api/charset-property-ado.md)屬性。  
  
-   暫止的非同步**資料流**操作[取消](../../../ado/reference/ado-api/cancel-method-ado.md)方法。  
  
-   判斷位元組數**資料流**與[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)屬性。  
  
-   控制項中目前的位置**資料流**與[位置](../../../ado/reference/ado-api/position-property-ado.md)屬性。  
  
-   判斷中的資料型別**資料流**與[類型](../../../ado/reference/ado-api/type-property-ado-stream.md)屬性。  
  
-   判斷目前的狀態**資料流**（關閉，開啟，或執行） 與[狀態](../../../ado/reference/ado-api/state-property-ado.md)屬性。  
  
-   指定的存取模式**資料流**與[模式](../../../ado/reference/ado-api/mode-property-ado.md)屬性。  
  
> [!NOTE]
>  使用 http 配置 Url 將會自動叫用[Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 **資料流**物件而言是安全的指令碼。  
  
 此章節包含下列主題。  
  
-   [資料流物件屬性、 方法和事件](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [記錄和資料流](../../../ado/guide/data/records-and-streams.md)

