---
description: Write 方法
title: Write 方法 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b43e0f505a3c4455768c32abd93dbc89afe04a82
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441460"
---
# <a name="write-method"></a>Write 方法
將二進位資料寫入 [資料流程](../../../ado/reference/ado-api/stream-object-ado.md) 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>參數  
 *Buffer*  
 包含要寫入位元組陣列的 **Variant** 。  
  
## <a name="remarks"></a>備註  
 指定的位元組會寫入 **資料流程** 物件，且每個位元組之間不會有任何中間的空格。  
  
 目前的 [位置](../../../ado/reference/ado-api/position-property-ado.md) 會設定為寫入的資料之後的位元組。 **Write**方法不會截斷資料流程中其餘的資料。 如果您想要截斷這些位元組，請呼叫 [SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 如果您寫過目前的[EOS](../../../ado/reference/ado-api/eos-property.md)位置，**資料流程**的[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)會增加以包含任何新的位元組，而**EOS**將移至**資料流程**中的新最後一個位元組。  
  
> [!NOTE]
>  **Write**方法可搭配二進位資料流程使用， ([類型](../../../ado/reference/ado-api/type-property-ado-stream.md)為**adTypeBinary**) 。 若為文字資料流程 (**類型** 為 **adTypeText**) ，請使用 [WriteText](../../../ado/reference/ado-api/writetext-method.md)。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [WriteText 方法](../../../ado/reference/ado-api/writetext-method.md)
