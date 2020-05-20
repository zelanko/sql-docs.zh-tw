---
title: WriteText 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_WriteText
- _Stream::WriteText
helpviewer_keywords:
- WriteText method [ADO]
ms.assetid: 7a669048-13f4-4574-a2b1-985e089729d5
author: rothja
ms.author: jroth
ms.openlocfilehash: 3ee7f4b99b40b6aec3e384f9f5739f8f5d2280f4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764409"
---
# <a name="writetext-method"></a>WriteText 方法
將指定的文字字串寫入[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>參數  
 *Data*  
 **字串**值，包含要寫入之字元中的文字。  
  
 *選項*  
 選擇性。 [StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)值，指定是否必須在指定字串的結尾寫入行分隔符號。  
  
## <a name="remarks"></a>備註  
 指定的字串會寫入**資料流程**物件中，而且每個字串之間不會有任何中間的空格或字元。  
  
 目前的[位置](../../../ado/reference/ado-api/position-property-ado.md)會設定為寫入資料之後的字元。 **WriteText**方法不會截斷資料流程中的其餘資料。 如果您想要截斷這些字元，請呼叫[SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 如果您寫出目前的[EOS](../../../ado/reference/ado-api/eos-property.md)位置，**資料流程**的[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)將會增加以包含任何新的字元，而**EOS**則會移至**資料流程**中的新最後一個位元組。  
  
> [!NOTE]
>  **WriteText**方法用於文字資料流程（[類型](../../../ado/reference/ado-api/type-property-ado-stream.md)為**adTypeText**）。 若為二進位資料流程（**類型**為**adTypeBinary**），請使用[Write](../../../ado/reference/ado-api/write-method.md)。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Write 方法](../../../ado/reference/ado-api/write-method.md)
