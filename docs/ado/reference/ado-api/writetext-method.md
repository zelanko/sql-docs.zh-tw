---
title: WriteText 方法 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_WriteText
- _Stream::WriteText
helpviewer_keywords:
- WriteText method [ADO]
ms.assetid: 7a669048-13f4-4574-a2b1-985e089729d5
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dda7b8a8aa215f43cadfc080a1d0df24b7c94e0d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="writetext-method"></a>WriteText 方法
將指定的文字字串至[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>參數  
 *資料*  
 A**字串**包含以字元為單位來寫入的文字值。  
  
 *選項。*  
 選擇性。 A [StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md)值，指定是否必須在指定的字串結尾處寫入行分隔符號字元。  
  
## <a name="remarks"></a>備註  
 指定的字串寫入**資料流**物件不含任何中間的空格或每個字串之間的字元。  
  
 目前[位置](../../../ado/reference/ado-api/position-property-ado.md)設為下列寫入的資料的字元。 **WriteText**方法不會截斷的資料流中的其餘部分。 如果您想要截斷這些字元，呼叫[SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
 如果您寫入超過目前[EOS](../../../ado/reference/ado-api/eos-property.md)位置[大小](../../../ado/reference/ado-api/size-property-ado-stream.md)的**資料流**包含任何新的字元，就會增加和**EOS**將會移到新的最後一個位元組中**資料流**。  
  
> [!NOTE]
>  **WriteText**方法配合文字資料流 ([類型](../../../ado/reference/ado-api/type-property-ado-stream.md)是**adTypeText**)。 二進位資料流 (**類型**是**adTypeBinary**)，使用[寫入](../../../ado/reference/ado-api/write-method.md)。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Write 方法](../../../ado/reference/ado-api/write-method.md)
