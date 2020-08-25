---
description: SaveToFile 方法
title: SaveToFile 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SaveToFile
- _Stream::SaveToFile
helpviewer_keywords:
- SaveToFile method [ADO]
ms.assetid: 8a8594f2-422b-4d2e-94f8-7fe337445900
author: rothja
ms.author: jroth
ms.openlocfilehash: a1f6890d25922789a4b3656429582e4e8a60efc1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777547"
---
# <a name="savetofile-method"></a>SaveToFile 方法
將 [資料流程](./stream-object-ado.md) 的二進位內容儲存至檔案。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>參數  
 *FileName*  
 **字串**值，包含將用來儲存**資料流程**內容之檔案的完整名稱。 您可以儲存至任何有效的本機位置，或您可以透過 UNC 值存取的任何位置。  
  
 *System.xml.linq.saveoptions>*  
 [SaveOptionsEnum](./saveoptionsenum.md)值，指定是否要由**SaveToFile**建立新檔案（如果不存在的話）。 預設值為 **adSaveCreateNotExists**。 您可以使用這些選項來指定如果指定的檔案不存在，就會發生錯誤。 您也可以指定 **SaveToFile** 覆寫現有檔案的目前內容。  
  
> [!NOTE]
>  如果您覆寫現有的檔案 (當 **adSaveCreateOverwrite** 設定為) 時， **SaveToFile** 會從原始的現有檔案中截斷任何符合新的 [EOS](./eos-property.md)的位元組。  
  
## <a name="remarks"></a>備註  
 **SaveToFile** 可用來將 **資料流程** 物件的內容複寫到本機檔案。 **資料流程**物件的內容或屬性不會有任何變更。 在呼叫**SaveToFile**之前，必須先開啟**資料流程**物件。  
  
 這個方法不會變更 **資料流程** 物件與其基礎來源的關聯。 **資料流程**物件仍會與開啟時來源的原始 URL 或**記錄**相關聯。  
  
 在 **SaveToFile** 作業之後，資料流程中 ([位置](./position-property-ado.md)) 的目前位置會設定為數據流的開頭 (0) 。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO Stream 的 Open 方法) ](./open-method-ado-stream.md)   
 [Save 方法](./save-method.md)