---
title: "Read 方法 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords: Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ad739a0d3aded4b0bf0458803d9fcdba5b388272
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
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
  
## <a name="see-also"></a>請參閱  
 [ReadText 方法](../../../ado/reference/ado-api/readtext-method.md)
