---
description: StreamWriteEnum
title: StreamWriteEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c09a15f5c5aba9d36f038304b68cc1e64112ade3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988439"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
指定是否將行分隔符號附加至寫入 [資料流程](./stream-object-ado.md) 物件的字串。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|預設值。 將 *資料* 參數) 指定的指定文字字串 (寫入 **資料流程** 物件。|  
|**adWriteLine**|1|將文字字串和行分隔字元寫入 **資料流程** 物件。 如果未定義 [LineSeparator](./lineseparator-property-ado.md) 屬性，則會傳回執行階段錯誤。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 這些常數沒有 ADO/WFC 對等專案。  
  
## <a name="applies-to"></a>套用至  
 [WriteText 方法](./writetext-method.md)