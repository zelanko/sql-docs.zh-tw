---
description: SetEOS 方法
title: SetEOS 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 3ebf47bdae6a879a3afe699be36081eb136b700e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989129"
---
# <a name="seteos-method"></a>SetEOS 方法
設定資料流程結尾的位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>備註  
 **SetEOS**會將目前[位置](./position-property-ado.md)設為數據流的結尾，藉以更新[EOS](./eos-property.md)屬性的值。 目前位置之後的任何位元組或字元都會被截斷。  
  
 因為 [Write](./write-method.md)、 [WriteText](./writetext-method.md)和 [CopyTo](./copyto-method-ado.md) 不會截斷現有 **資料流程** 物件中的任何額外值，所以您可以使用 **SetEOS**來設定新的資料流程結尾位置，以截斷這些位元組或字元。  
  
> [!CAUTION]
>  如果您將 **EOS** 設定為數據流實際結束之前的位置，則會遺失新的 **EOS** 位置之後的所有資料。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](./stream-object-ado.md)