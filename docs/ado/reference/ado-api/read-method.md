---
title: Read 方法 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.component: reference
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords:
- Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 53e3f6c3b780d9d78697fb33dfea5574457a6b2c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="read-method"></a>Read 方法
從二進位檔中讀取指定的位元組數目[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>參數  
 *NumBytes*  
 選擇性。 A**長**值，指定要從檔案讀取的位元組數目或[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)值**adReadAll**，預設值。  
  
## <a name="return-value"></a>傳回值  
 **讀取**方法會讀取指定的數目的整個資料流或位元組**資料流**物件，並將產生的資料，以傳回**Variant**。  
  
## <a name="remarks"></a>備註  
 如果*NumBytes*個以上的位元組數目會留在**資料流**，僅將剩餘的位元組會傳回。 讀取的資料不會填補到符合所指定的長度*NumBytes*。 如果有任何剩餘要讀取的位元組，則會傳回具有 null 值的 variant。 **讀取**無法用來讀取回溯。  
  
> [!NOTE]
>  *NumBytes*一律會測量位元組。 文字**資料流**物件 ([類型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeText**)，使用[ReadText](../../../ado/reference/ado-api/readtext-method.md)。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ReadText 方法](../../../ado/reference/ado-api/readtext-method.md)
