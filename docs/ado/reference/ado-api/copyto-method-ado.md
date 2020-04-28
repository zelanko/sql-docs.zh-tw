---
title: CopyTo 方法（ADO） |Microsoft Docs
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
ms.openlocfilehash: 25d57116e1fa24658d62a0c9083e00a3e320d2a8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67933376"
---
# <a name="copyto-method-ado"></a>CopyTo 方法 (ADO)
將[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)中指定的字元或位元組數（視[類型](../../../ado/reference/ado-api/type-property-ado-stream.md)而定）複製到另一個**資料流程**物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>參數  
 *DestStream*  
 物件變數值，其中包含開放式**資料流程**物件的參考。 目前的**資料流程**會複製到*DestStream*所指定的目的地**資料流程**。 目的地**資料流程**必須已經開啟。 如果不是，就會發生執行階段錯誤。  
  
> [!NOTE]
>  *DestStream*參數可能不是**stream**物件的 proxy，因為這需要存取**資料流程**物件上無法遠端處理至用戶端的私用介面。  
  
 *NumChars*  
 選擇性。 **整數**值，指定要從來源**資料流程**中的目前位置複製到目的地**資料流程**的位元組或字元數。 預設值為-1，指定將所有字元或位元組從目前的位置複製到[EOS](../../../ado/reference/ado-api/eos-property.md)。  
  
## <a name="remarks"></a>備註  
 這個方法會從[position](../../../ado/reference/ado-api/position-property-ado.md)屬性所指定的目前位置開始，複製指定的字元數或位元組數。 如果指定的數位在**EOS**之前超過可用的位元組數目，則只會複製目前位置到**eos**的字元或位元組。 如果*NumChars*的值為-1，或省略，則會複製從目前位置開始的所有字元或位元組。  
  
 如果目的地資料流程中有現有的字元或位元組，則複本結束的位置以外的所有內容都會保留下來，而且不會被截斷。 **Position**會成為複製最後一個位元組之後的位元組。 如果您想要截斷這些位元組，請呼叫[SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 **CopyTo**應該用來將資料複製到與來源**資料流程**相同類型的目的地**資料流程**（其**類型**屬性設定同時為**adTypeText**或兩個**adTypeBinary**）。 對於文字**資料流程**物件，您可以變更目的地**資料流程**的 [[字元集](../../../ado/reference/ado-api/charset-property-ado.md)] 屬性設定，以從一個字元集轉譯成另一個字元集。 此外，文字**資料流程**物件也可以成功複製到二進位**資料流程**物件中，但無法將二進位**資料流程**物件複製到文字**資料流程**物件中。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
