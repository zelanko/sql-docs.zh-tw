---
title: StreamWriteEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d0f42561d7b324a13068c14d0fc7971d3d46d83b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633486"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
指定寫入的字串是否有附加行分隔符號[Stream](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|預設值。 寫入指定的文字字串 (所指定*資料*參數) 來**Stream**物件。|  
|**adWriteLine**|1|將文字字串和要行分隔符號字元寫入**Stream**物件。 如果[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)未定義屬性，則這會傳回執行階段錯誤。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 這些常數不需要 ADO/WFC 對等項目。  
  
## <a name="applies-to"></a>適用於  
 [WriteText 方法](../../../ado/reference/ado-api/writetext-method.md)
