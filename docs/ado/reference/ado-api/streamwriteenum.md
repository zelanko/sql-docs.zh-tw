---
title: StreamWriteEnum |Microsoft 文件
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
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62b5718d87d9c5117d10ad4ba55cdc783948778a
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282708"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
指定是否要將分行符號附加至字串寫入[資料流](../../../ado/reference/ado-api/stream-object-ado.md)物件。  
  
|常數|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|預設值。 寫入指定的文字字串 (所指定*資料*參數) 來**資料流**物件。|  
|**adWriteLine**|@shouldalert|寫入的文字字串，並以行分隔字元**資料流**物件。 如果[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)未定義屬性，則這會傳回執行階段錯誤。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 這些常數沒有 ADO/WFC 對等項目。  
  
## <a name="applies-to"></a>適用於  
 [WriteText 方法](../../../ado/reference/ado-api/writetext-method.md)
