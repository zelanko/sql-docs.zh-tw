---
description: SetEOS 方法
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
ms.openlocfilehash: fd1d0418fe0c6a0a475594605acc6f28851a777e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442120"
---
# <a name="seteos-method"></a>SetEOS 方法
設定資料流程結尾的位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>備註  
 **SetEOS**會將目前[位置](../../../ado/reference/ado-api/position-property-ado.md)設為數據流的結尾，藉以更新[EOS](../../../ado/reference/ado-api/eos-property.md)屬性的值。 目前位置之後的任何位元組或字元都會被截斷。  
  
 因為 [Write](../../../ado/reference/ado-api/write-method.md)、 [WriteText](../../../ado/reference/ado-api/writetext-method.md)和 [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) 不會截斷現有 **資料流程** 物件中的任何額外值，所以您可以使用 **SetEOS**來設定新的資料流程結尾位置，以截斷這些位元組或字元。  
  
> [!CAUTION]
>  如果您將 **EOS** 設定為數據流實際結束之前的位置，則會遺失新的 **EOS** 位置之後的所有資料。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
