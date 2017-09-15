---
title: "撰寫方法 |Microsoft 文件"
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
- _Stream::raw_Write
- _Stream::Write
helpviewer_keywords:
- Write method [ADO]
ms.assetid: 02982e6a-ac5f-4af2-b82e-ce12534b84b2
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6adf96fa3fd1135727a55a8c7e26351942f886c4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="write-method"></a>Write 方法
將二進位資料寫入[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>參數  
 *緩衝區*  
 A **Variant** ，其中包含要寫入的位元組陣列。  
  
## <a name="remarks"></a>備註  
 指定的位元組寫入**資料流**不含任何中間的空格，每個位元組之間的物件。  
  
 目前[位置](../../../ado/reference/ado-api/position-property-ado.md)設為下列寫入的資料的位元組。 **寫入**方法不會截斷的資料流中的其餘部分。 如果您想要截斷這些位元組，呼叫[SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 如果您寫入超過目前[EOS](../../../ado/reference/ado-api/eos-property.md)位置[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)的**資料流**就會增加以包含任何新的位元組和**EOS**會移動在新的最後一個位元組**資料流**。  
  
> [!NOTE]
>  **寫入**方法搭配二進位資料流 ([類型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeBinary**)。 文字資料流 (**類型**是**adTypeText**)，使用[WriteText](../../../ado/reference/ado-api/writetext-method.md)。  
  
## <a name="applies-to"></a>適用於  
 [資料流物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [WriteText 方法](../../../ado/reference/ado-api/writetext-method.md)
