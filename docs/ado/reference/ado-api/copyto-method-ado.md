---
title: CopyTo 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_CopyTo
- _Stream::CopyTo
helpviewer_keywords:
- CopyTo method [ADO]
ms.assetid: b4aa5714-916b-48b8-8b09-cc2708379602
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01b2e7dc8b70c109fc6cf998cec2bbad1147692c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63308913"
---
# <a name="copyto-method-ado"></a>CopyTo 方法 (ADO)
複製指定的字元或位元組數 (取決於[型別](../../../ado/reference/ado-api/type-property-ado-stream.md)) 中[Stream](../../../ado/reference/ado-api/stream-object-ado.md)到另一個**Stream**物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>參數  
 *DestStream*  
 物件變數值，包含已開啟的參考**Stream**物件。 目前**Stream**複製到目的地**Stream**所指定*DestStream*。 目的地**Stream**必須已經開啟。 如果沒有，就會發生執行階段錯誤。  
  
> [!NOTE]
>  *DestStream*參數不可以是一個 proxy **Stream**物件，因為這需要私用介面的存取權**Stream**無法遠端處理到的物件用戶端。  
  
 *NumChars*  
 選擇性。 **整數**值，指定要從目前的位置，在來源中複製的字元或位元組數目**Stream**目的地**Stream**。 預設值為-1，指定複製所有的字元或位元組，從目前的位置向[EOS](../../../ado/reference/ado-api/eos-property.md)。  
  
## <a name="remarks"></a>備註  
 這個方法會複製指定的字元或位元組數，從所指定的目前位置開始[位置](../../../ado/reference/ado-api/position-property-ado.md)屬性。 如果指定的數目大於可用位元組之前的數目**EOS**，然後只字元或位元組從目前的位置向**EOS**複製。 如果值*NumChars*為-1，或省略，所有的字元或位元組從目前位置開始複製。  
  
 如果那里現有的字元或目的資料流中的位元組，超過時間點複本的結束位置的所有內容會保留，而不會被截斷。 **位置**變成緊接複製的最後一個位元組的位元組。 如果您想要截斷這些位元組，呼叫[SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 **CopyTo**應該用來將資料複製到目的地**Stream**做為來源相同型別的**Stream** (其**型別**屬性設定為這兩個**adTypeText**或兩者皆**adTypeBinary**)。 文字**Stream**物件，您可以變更[字元集](../../../ado/reference/ado-api/charset-property-ado.md)屬性設定為目的地**Stream**轉譯至另一個的字元集。 此外，文字**Stream**物件可以成功地複製到二進位**Stream**物件，而二進位**Stream**物件無法複製到文字**Stream**物件。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
