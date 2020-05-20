---
title: Stream 物件（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a9812344008bc066b18328036cf36fe106e8845a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759654"
---
# <a name="stream-object-ado"></a>Stream 物件 (ADO)
表示二進位資料或文字的資料流程。  
  
 在樹狀結構（例如檔案系統或電子郵件系統）中，[記錄](../../../ado/reference/ado-api/record-object-ado.md)可能會有與它相關聯的預設二進位資料流程，其中包含檔案或電子郵件的內容。 **資料流程**物件可以用來操作包含這些資料資料流程的欄位或記錄。 **串流**物件可以透過下列方式取得：  
  
-   從指向物件（通常是檔案）並包含二進位或文字資料的 URL。 這個物件可以是簡單的檔、代表結構化檔的**記錄**物件，或資料夾。  
  
-   開啟與**記錄**物件相關聯的預設**資料流程**物件。 開啟**記錄**時，您可以取得與**記錄**物件相關聯的預設資料流程，以排除只開啟資料流程的來回行程。  
  
-   藉由具現化**資料流程**物件。 這些**資料流程**物件可以用來儲存應用程式用途的資料。 不同于與 URL 相關聯的**資料流程**，或**記錄**的預設**資料流程**，具現化的**資料流程**預設不會與基礎來源建立關聯。  
  
 使用**資料流程**物件的方法和屬性，您可以執行下列動作：  
  
-   使用[open](../../../ado/reference/ado-api/open-method-ado-stream.md)方法，從**記錄**或 URL 開啟**資料流程**物件。  
  
-   使用[close](../../../ado/reference/ado-api/close-method-ado.md)方法關閉**資料流程**。  
  
-   使用[Write](../../../ado/reference/ado-api/write-method.md)和[WriteText](../../../ado/reference/ado-api/writetext-method.md)方法將位元組或文字輸入**資料流程**。  
  
-   使用[read](../../../ado/reference/ado-api/read-method.md)和[ReadText](../../../ado/reference/ado-api/readtext-method.md)方法，從**資料流程**讀取位元組。  
  
-   使用[Flush](../../../ado/reference/ado-api/flush-method-ado.md)方法，將任何仍在 ADO 緩衝區中的**資料流程**資料寫入基礎物件。  
  
-   使用[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)方法將**資料流程**的內容複寫到另一個**資料流程**。  
  
-   使用[SkipLine](../../../ado/reference/ado-api/skipline-method.md)方法和[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)屬性，控制從來源檔案讀取行的方式。  
  
-   使用[EOS](../../../ado/reference/ado-api/eos-property.md)屬性和[SetEOS](../../../ado/reference/ado-api/seteos-method.md)方法，判斷資料流程位置的結尾。  
  
-   使用[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)和[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)方法，儲存和還原檔案中的資料。  
  
-   指定用來儲存含有[字元集](../../../ado/reference/ado-api/charset-property-ado.md)屬性之**資料流程**的字元集。  
  
-   使用[Cancel](../../../ado/reference/ado-api/cancel-method-ado.md)方法來中止非同步**資料流程**作業。  
  
-   使用[Size](../../../ado/reference/ado-api/size-property-ado-stream.md)屬性來決定**資料流程**中的位元組數目。  
  
-   使用[position](../../../ado/reference/ado-api/position-property-ado.md)屬性來控制**資料流程**內的目前位置。  
  
-   使用[type](../../../ado/reference/ado-api/type-property-ado-stream.md)屬性判斷**資料流程**中的資料類型。  
  
-   使用[state](../../../ado/reference/ado-api/state-property-ado.md)屬性來判斷**資料流程**的目前狀態（封閉式、open 或執行中）。  
  
-   使用[mode](../../../ado/reference/ado-api/mode-property-ado.md)屬性指定**資料流程**的存取模式。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用[Microsoft OLE DB 提供者以進行網際網路發佈](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱[絕對和相對 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
 **資料流程**物件可安全地進行腳本處理。  
  
 此章節包含下列主題。  
  
-   [Stream 物件屬性、方法和事件](../../../ado/reference/ado-api/stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [記錄和資料流](../../../ado/guide/data/records-and-streams.md)
