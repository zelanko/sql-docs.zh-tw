---
description: Stream 物件 (ADO)
title: " (ADO) 的資料流程物件 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 619d9d307e26829ffa74a24c6904fa84889f476f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988589"
---
# <a name="stream-object-ado"></a>Stream 物件 (ADO)
代表二進位資料或文字的資料流程。  
  
 在樹狀結構階層架構（例如檔案系統或電子郵件系統）中， [記錄](./record-object-ado.md) 可能會有與其相關聯的預設二進位資料流程，其中包含檔案的內容或電子郵件。 **資料流程**物件可以用來操作包含這些資料資料流程的欄位或記錄。 您可以透過下列方式取得 **資料流程** 物件：  
  
-   從指向物件的 URL (通常是包含二進位或文字資料的檔案) 。 這個物件可以是簡單的檔、代表結構化檔的 **記錄** 物件或資料夾。  
  
-   開啟與**記錄**物件相關聯的預設**資料流程**物件。 當**記錄**開啟時，您可以取得與**記錄**物件相關聯的預設資料流程，以消除只是開啟資料流程的來回行程。  
  
-   藉由具現化 **資料流程** 物件。 這些 **資料流程** 物件可用來儲存資料，以供您的應用程式之用。 不同于與 URL 相關聯的**資料流程**或**記錄**的預設**資料流程**，具現化的**資料流程**預設不會與基礎來源建立關聯。  
  
 使用 **資料流程** 物件的方法和屬性，您可以執行下列動作：  
  
-   使用[open](./open-method-ado-stream.md)方法，從**記錄**或 URL 開啟**資料流程**物件。  
  
-   使用[close](./close-method-ado.md)方法關閉**資料流程**。  
  
-   使用[寫入](./write-method.md)和[WriteText](./writetext-method.md)方法輸入**資料流程**的位元組或文字。  
  
-   使用[read](./read-method.md)和[ReadText](./readtext-method.md)方法從**資料流程**讀取位元組。  
  
-   使用[Flush](./flush-method-ado.md)方法將仍在 ADO 緩衝區中的任何**資料流程**資料寫入基礎物件。  
  
-   使用[CopyTo](./copyto-method-ado.md)方法將**資料流程**的內容複寫到另一個**資料流程**。  
  
-   使用 [SkipLine](./skipline-method.md)方法和 [LineSeparator](./lineseparator-property-ado.md) 屬性，控制如何從原始程式檔讀取行。  
  
-   使用 [EOS](./eos-property.md)屬性和 [SetEOS](./seteos-method.md) 方法判斷資料流程位置的結尾。  
  
-   使用 [SaveToFile](./savetofile-method.md)和 [LoadFromFile](./loadfromfile-method-ado.md) 方法儲存和還原檔案中的資料。  
  
-   指定用來儲存 **資料流程** 與 [字元集](./charset-property-ado.md) 屬性的字元集。  
  
-   使用[Cancel](./cancel-method-ado.md)方法來中止非同步**資料流程**作業。  
  
-   使用[Size](./size-property-ado-stream.md)屬性來判斷**資料流程**中的位元組數目。  
  
-   使用[position](./position-property-ado.md)屬性控制**資料流程**中的目前位置。  
  
-   使用[type](./type-property-ado-stream.md)屬性判斷**資料流程**中的資料類型。  
  
-   使用[state](./state-property-ado.md)屬性來判斷**資料流程**的目前狀態 (關閉、開啟或執行) 。  
  
-   使用[mode](./mode-property-ado.md)屬性指定**資料流程**的存取模式。  
  
> [!NOTE]
>  使用 HTTP 配置的 Url 會自動叫用 [Microsoft OLE DB 提供者進行網際網路發佈](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 如需詳細資訊，請參閱 [絕對和相對 url](../../guide/data/absolute-and-relative-urls.md)。  
  
 **資料流程**物件可以安全地進行腳本處理。  
  
 此章節包含下列主題。  
  
-   [Stream 物件屬性、方法和事件](./stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [記錄和資料流](../../guide/data/records-and-streams.md)