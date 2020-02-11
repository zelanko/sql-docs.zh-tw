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
ms.openlocfilehash: 4cc9de1481cc683bddafe2f92959977319600f6a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67928636"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
指定是否要將行分隔符號附加至寫入[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)物件的字串。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|預設。 將指定的文字字串（由*資料*參數指定）寫入**資料流程**物件。|  
|**adWriteLine**|1|將文字字串和行分隔符號寫入**資料流程**物件。 如果未定義[LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md)屬性，則這會傳回執行階段錯誤。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 這些常數沒有 ADO/WFC 對應項。  
  
## <a name="applies-to"></a>套用至  
 [WriteText 方法](../../../ado/reference/ado-api/writetext-method.md)
