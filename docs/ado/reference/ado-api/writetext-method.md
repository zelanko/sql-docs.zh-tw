---
description: WriteText 方法
title: WriteText 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: d38d493fb57e8147f882056d07514ba9f405ecf9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987719"
---
# <a name="writetext-method"></a>WriteText 方法
將指定的文字字串寫入 [資料流程](./stream-object-ado.md) 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>參數  
 *Data*  
 **字串**值，包含要寫入的文字（以字元為單位）。  
  
 *選項*  
 選擇性。 [StreamWriteEnum](./streamwriteenum.md)值，這個值會指定是否必須在指定的字串結尾寫入行分隔字元。  
  
## <a name="remarks"></a>備註  
 指定的字串會寫入 **資料流程** 物件，且每個字串之間不會有任何中間的空格或字元。  
  
 目前的 [位置](./position-property-ado.md) 會設定為寫入資料之後的字元。 **WriteText**方法不會截斷資料流程中其餘的資料。 如果您想要截斷這些字元，請呼叫 [SetEOS](./seteos-method.md)。  
  
 如果您寫過目前的[EOS](./eos-property.md)位置，**資料流程**的[大小](./size-property-ado-stream.md)會增加以包含任何新的字元，而**EOS**將移至**資料流程**中的新最後一個位元組。  
  
> [!NOTE]
>  **WriteText**方法搭配文字資料流程使用 ([類型](./type-property-ado-stream.md)為**adTypeText**) 。 針對二進位資料流程 (**類型** 為 **adTypeBinary**) ，請使用 [Write](./write-method.md)。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Write 方法](./write-method.md)