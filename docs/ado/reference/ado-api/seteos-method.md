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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 027468926d444b25e60ede18bbfb26ff7cedf729
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711406"
---
# <a name="seteos-method"></a>SetEOS 方法
設定為資料流結尾的位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>備註  
 **SetEOS**的值更新[EOS](../../../ado/reference/ado-api/eos-property.md)屬性，藉由目前[位置](../../../ado/reference/ado-api/position-property-ado.md)資料流結尾。 任何位元組或字元之後的目前位置會被截斷。  
  
 因為[撰寫](../../../ado/reference/ado-api/write-method.md)， [WriteText](../../../ado/reference/ado-api/writetext-method.md)，並[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)不會截斷任何額外的值，在現有**Stream**物件時，您可以截斷這些藉由設定與新的資料流結尾位置的字元或位元組**SetEOS**。  
  
> [!CAUTION]
>  如果您設定**EOS**到實際的資料流結束前的位置，您將遺失所有資料之後的新**EOS**位置。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
