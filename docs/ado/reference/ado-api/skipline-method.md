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
ms.openlocfilehash: c0897d90ffeccabbce57525f268214577a523d92
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777467"
---
# <a name="skipline-method"></a>SkipLine 方法
讀取文字 [資料流程](./stream-object-ado.md)時，略過一行。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>備註  
 會略過所有字元（最多到和包含下一行分隔符號）。 依預設， [LineSeparator](./lineseparator-property-ado.md) 為 **adCRLF**。 如果您嘗試跳過過去的 [eos](./eos-property.md)，目前的位置將維持在 **eos**。  
  
 **SkipLine**方法搭配文字資料流程使用 ([類型](./type-property-ado-stream.md)為**adTypeText**) 。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](./stream-object-ado.md)