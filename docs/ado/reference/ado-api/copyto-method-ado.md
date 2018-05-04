---
title: CopyTo 方法 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_CopyTo
- _Stream::CopyTo
helpviewer_keywords:
- CopyTo method [ADO]
ms.assetid: b4aa5714-916b-48b8-8b09-cc2708379602
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 368385864bf9cb5e0497e9acd3bf40e6e468b8bc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="copyto-method-ado"></a>CopyTo 方法 (ADO)
複製指定的字元或位元組數 (取決於[類型](../../../ado/reference/ado-api/type-property-ado-stream.md)) 中[資料流](../../../ado/reference/ado-api/stream-object-ado.md)到另一個**資料流**物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>參數  
 *DestStream*  
 物件變數值，其中包含開放參考**資料流**物件。 目前**資料流**複製到目的地**資料流**所指定*DestStream*。 目的地**資料流**必須已經開啟。 如果沒有，就會發生執行階段錯誤。  
  
> [!NOTE]
>  *DestStream*參數不可以是一個 proxy**資料流**物件，因為這需要存取私用介面上**資料流**無法遠端處理到的物件用戶端。  
  
 *NumChars*  
 選擇性。 **整數**值，指定要從目前的位置，在來源中複製的字元或位元組數**資料流**目的地**資料流**。 預設值為 – 1，指定所有的字元或位元組從目前的位置，以便複製[EOS](../../../ado/reference/ado-api/eos-property.md)。  
  
## <a name="remarks"></a>備註  
 這個方法會複製指定的字元或位元組數，從所指定的目前位置開始[位置](../../../ado/reference/ado-api/position-property-ado.md)屬性。 如果指定的數目超過可用的位元組直到**EOS**，則只有字元或位元組從目前的位置，以便**EOS**複製。 如果值*NumChars*為 – 1，或省略，則所有的字元或位元組從目前位置開始複製。  
  
 如果那里現有字元或位元組目的地資料流中的，複製結束處的點以外的所有內容會保留，而不會被截斷。 **位置**變成緊接複製的最後一個位元組的位元組。 如果您想要截斷這些位元組，呼叫[SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 **CopyTo**應該用來將資料複製到目的地**資料流**與來源相同型別的**資料流**(其**類型**屬性設定為這兩個**adTypeText**或兩者都**adTypeBinary**)。 文字**資料流**物件，您可以變更[Charset](../../../ado/reference/ado-api/charset-property-ado.md)屬性設定為目的地**資料流**轉譯至另一個的字元集。 此外，文字**資料流**物件可以成功地複製到二進位**資料流**物件，而二進位**資料流**物件不能複製到文字**資料流**物件。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
