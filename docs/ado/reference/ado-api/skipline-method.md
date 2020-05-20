---
title: SkipLine 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SkipLine
- _Stream::SkipLine
helpviewer_keywords:
- Skipline method [ADO]
ms.assetid: 0abc00fe-ee09-4c8e-b1f2-48ee9c5f3329
author: rothja
ms.author: jroth
ms.openlocfilehash: f983646fd87be27fe9861f3a37b0e852a05ba06b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759874"
---
# <a name="skipline-method"></a>SkipLine 方法
讀取文字[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)時，略過一行整行。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>備註  
 會略過直到下一行分隔符號為止的所有字元。 根據預設， [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)為**adCRLF**。 如果您嘗試跳過過去的[EOS](../../../ado/reference/ado-api/eos-property.md)，目前的位置將維持在**eos**。  
  
 **SkipLine**方法用於文字資料流程（[類型](../../../ado/reference/ado-api/type-property-ado-stream.md)為**adTypeText**）。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
