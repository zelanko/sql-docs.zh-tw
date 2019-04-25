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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3b50db388151de1f5b99d8d9a3f48904e6d7c2c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642958"
---
# <a name="writetext-method"></a>WriteText 方法
將指定的文字字串來寫入[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>參數  
 *資料*  
 A**字串**值，其中包含以字元為單位來寫入的文字。  
  
 *選項。*  
 選擇性。 A [StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)值，指定是否必須在指定的字串結尾處寫入行分隔符號字元。  
  
## <a name="remarks"></a>備註  
 指定的字串會寫入**Stream**物件不含任何中間的空格或每個字串之間的字元。  
  
 目前[位置](../../../ado/reference/ado-api/position-property-ado.md)設為之後寫入的資料的字元。 **WriteText**方法不會截斷的資料流中的其餘部分。 如果您想要截斷這些字元，呼叫[SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 如果您寫入超過目前[EOS](../../../ado/reference/ado-api/eos-property.md)位置[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)的**Stream**就會增加以包含任何新的字元，以及**EOS**將移至新的最後一個位元組，在**Stream**。  
  
> [!NOTE]
>  **WriteText**方法搭配文字資料流 ([型別](../../../ado/reference/ado-api/type-property-ado-stream.md)會**adTypeText**)。 二進位資料流 (**型別**是**adTypeBinary**)，使用[撰寫](../../../ado/reference/ado-api/write-method.md)。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Write 方法](../../../ado/reference/ado-api/write-method.md)
