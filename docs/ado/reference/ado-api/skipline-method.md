---
description: SkipLine 方法
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
ms.openlocfilehash: 463de3740ce29b859732c5ddb7ba69d58069f93f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442093"
---
# <a name="skipline-method"></a>SkipLine 方法
讀取文字 [資料流程](../../../ado/reference/ado-api/stream-object-ado.md)時，略過一行。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>備註  
 會略過所有字元（最多到和包含下一行分隔符號）。 依預設， [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) 為 **adCRLF**。 如果您嘗試跳過過去的 [eos](../../../ado/reference/ado-api/eos-property.md)，目前的位置將維持在 **eos**。  
  
 **SkipLine**方法搭配文字資料流程使用 ([類型](../../../ado/reference/ado-api/type-property-ado-stream.md)為**adTypeText**) 。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
