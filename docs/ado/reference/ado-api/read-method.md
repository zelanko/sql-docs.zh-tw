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
ms.openlocfilehash: 7c2b2b1579beb967ec75b5a0b32532b846640b01
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88772717"
---
# <a name="read-method"></a>Read 方法
從二進位 [資料流程](./stream-object-ado.md) 物件讀取指定的位元組數目。  
  
## <a name="syntax"></a>語法  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>參數  
 *NumBytes*  
 選擇性。 **Long**值，指定要從檔案讀取的位元組數目或[StreamReadEnum](./streamreadenum.md)值**adReadAll**（預設值）。  
  
## <a name="return-value"></a>傳回值  
 **Read**方法會從**資料流程**物件中讀取指定的位元組數目或整個資料流程，並以**變異**數的形式傳回產生的資料。  
  
## <a name="remarks"></a>備註  
 如果 *NumBytes* 超過 **資料流程**中剩餘的位元組數，則只會傳回剩餘的位元組。 讀取的資料並未填補，以符合 *NumBytes*所指定的長度。 如果沒有剩餘的位元組可供讀取，則會傳回具有 null 值的變數。 無法使用**read**來向後讀取。  
  
> [!NOTE]
>  *NumBytes* 一律會測量位元組。 若為文字 **資料流程** 物件 ([類型](./type-property-ado-stream.md) 為 **AdTypeText**) ，請使用 [ReadText](./readtext-method.md)。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ReadText 方法](./readtext-method.md)