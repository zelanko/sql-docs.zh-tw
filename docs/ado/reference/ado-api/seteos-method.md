---
title: SetEOS 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SetEOS
- _Stream::SetEOS
helpviewer_keywords:
- SetEOS method [ADO]
ms.assetid: 707c18ca-6a56-4970-bbd6-ae1fb86a0b8a
author: rothja
ms.author: jroth
ms.openlocfilehash: 9dbe2846674d760163fa9eb3ab78e07e68b80d0e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759894"
---
# <a name="seteos-method"></a>SetEOS 方法
設定為數據流結尾的位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>備註  
 **SetEOS**會藉由將目前[位置](../../../ado/reference/ado-api/position-property-ado.md)設為數據流的結尾，來更新[EOS](../../../ado/reference/ado-api/eos-property.md)屬性的值。 在目前位置之後的任何位元組或字元都會被截斷。  
  
 由於[Write](../../../ado/reference/ado-api/write-method.md)、 [WriteText](../../../ado/reference/ado-api/writetext-method.md)和[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)不會截斷現有**資料流程**物件中的任何額外值，因此您可以藉由設定新的資料流程結束位置與**SetEOS**來截斷這些位元組或字元。  
  
> [!CAUTION]
>  如果您將**EOS**設定為數據流的實際結尾之前的位置，您將會遺失新的**EOS**位置之後的所有資料。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
