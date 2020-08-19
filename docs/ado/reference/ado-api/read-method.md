---
description: Read 方法
title: Read 方法 |Microsoft Docs
ms.prod: sql
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6600c02af5c24fc1ce27a04422678f8a3f40a179
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442550"
---
# <a name="read-method"></a>Read 方法
從二進位 [資料流程](../../../ado/reference/ado-api/stream-object-ado.md) 物件讀取指定的位元組數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>參數  
 *NumBytes*  
 選擇性。 **Long**值，指定要從檔案讀取的位元組數目或[StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md)值**adReadAll**（預設值）。  
  
## <a name="return-value"></a>傳回值  
 **Read**方法會從**資料流程**物件中讀取指定的位元組數目或整個資料流程，並以**變異**數的形式傳回產生的資料。  
  
## <a name="remarks"></a>備註  
 如果 *NumBytes* 超過 **資料流程**中剩餘的位元組數，則只會傳回剩餘的位元組。 讀取的資料並未填補，以符合 *NumBytes*所指定的長度。 如果沒有剩餘的位元組可供讀取，則會傳回具有 null 值的變數。 無法使用**read**來向後讀取。  
  
> [!NOTE]
>  *NumBytes* 一律會測量位元組。 若為文字 **資料流程** 物件 ([類型](../../../ado/reference/ado-api/type-property-ado-stream.md) 為 **AdTypeText**) ，請使用 [ReadText](../../../ado/reference/ado-api/readtext-method.md)。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ReadText 方法](../../../ado/reference/ado-api/readtext-method.md)
