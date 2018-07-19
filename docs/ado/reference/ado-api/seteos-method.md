---
title: SetEOS 方法 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SetEOS
- _Stream::SetEOS
helpviewer_keywords:
- SetEOS method [ADO]
ms.assetid: 707c18ca-6a56-4970-bbd6-ae1fb86a0b8a
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8821b58e5e111ad879c34f0d3d8177404945a72f
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35281607"
---
# <a name="seteos-method"></a>SetEOS 方法
設定為資料流結尾的位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>備註  
 **SetEOS**更新值[EOS](../../../ado/reference/ado-api/eos-property.md)屬性，藉由目前[位置](../../../ado/reference/ado-api/position-property-ado.md)資料流結尾。 任何位元組或字元目前位置會被截斷。  
  
 因為[寫入](../../../ado/reference/ado-api/write-method.md)， [WriteText](../../../ado/reference/ado-api/writetext-method.md)，和[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)不會截斷任何額外的值，在現有**資料流**物件，您也可以將這些截斷藉由設定與新的資料流結束位置的字元或位元組**SetEOS**。  
  
> [!CAUTION]
>  如果您設定**EOS**到實際的資料流結尾之前的位置，您將會遺失所有資料之後新**EOS**位置。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
