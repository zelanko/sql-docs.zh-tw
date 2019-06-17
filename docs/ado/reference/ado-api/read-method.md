---
title: Read 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords:
- Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f4594e4b85ad66b1ab11a2966bc7a0d79815db09
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702979"
---
# <a name="read-method"></a>Read 方法
讀取指定的位元組數目從二進位[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>參數  
 *NumBytes*  
 選擇性。 A**長**值，指定要從檔案讀取的位元組數目或[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)值**adReadAll**，這是預設值。  
  
## <a name="return-value"></a>傳回值  
 **讀取**方法會讀取指定的數目的整個資料流或位元組**Stream**物件，並將產生的資料，以傳回**Variant**。  
  
## <a name="remarks"></a>備註  
 如果*NumBytes*個以上的位元組數目會留在**Stream**，僅將剩餘的位元組會傳回。 讀取的資料不會填補到符合所指定的長度*NumBytes*。 如果不有任何供讀取的位元組，則會傳回具有 null 值的 variant。 **讀取**無法用來讀取回溯。  
  
> [!NOTE]
>  *NumBytes*一律量值的位元組。 文字**Stream**物件 ([型別](../../../ado/reference/ado-api/type-property-ado-stream.md)會**adTypeText**)，使用[ReadText](../../../ado/reference/ado-api/readtext-method.md)。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ReadText 方法](../../../ado/reference/ado-api/readtext-method.md)
