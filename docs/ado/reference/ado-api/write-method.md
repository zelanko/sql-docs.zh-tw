---
title: 撰寫方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_Write
- _Stream::Write
helpviewer_keywords:
- Write method [ADO]
ms.assetid: 02982e6a-ac5f-4af2-b82e-ce12534b84b2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 52561b6d240a58e59490d607c8729b5d878b96a7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772551"
---
# <a name="write-method"></a>Write 方法
將二進位資料寫入[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>參數  
 *Buffer*  
 A **Variant** ，其中包含要寫入的位元組陣列。  
  
## <a name="remarks"></a>備註  
 指定的位元組會寫入**Stream**不含任何中間的空格，每個位元組之間的物件。  
  
 目前[位置](../../../ado/reference/ado-api/position-property-ado.md)設為寫入的資料位元組。 **寫入**方法不會截斷的資料流中的其餘部分。 如果您想要截斷這些位元組，呼叫[SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 如果您寫入超過目前[EOS](../../../ado/reference/ado-api/eos-property.md)位置[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)的**Stream**就會增加以包含新的任何位元組，並**EOS**會移動在新的最後一個位元組**Stream**。  
  
> [!NOTE]
>  **撰寫**方法搭配二進位資料流 ([型別](../../../ado/reference/ado-api/type-property-ado-stream.md)會**adTypeBinary**)。 文字資料流 (**型別**是**adTypeText**)，使用[WriteText](../../../ado/reference/ado-api/writetext-method.md)。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [WriteText 方法](../../../ado/reference/ado-api/writetext-method.md)
