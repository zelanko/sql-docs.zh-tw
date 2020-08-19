---
description: StreamWriteEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 939de5306982ab2e369fce0648e477cac5f48cb8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441790"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
指定是否將行分隔符號附加至寫入 [資料流程](../../../ado/reference/ado-api/stream-object-ado.md) 物件的字串。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|預設值。 將 *資料* 參數) 指定的指定文字字串 (寫入 **資料流程** 物件。|  
|**adWriteLine**|1|將文字字串和行分隔字元寫入 **資料流程** 物件。 如果未定義 [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) 屬性，則會傳回執行階段錯誤。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 這些常數沒有 ADO/WFC 對等專案。  
  
## <a name="applies-to"></a>套用至  
 [WriteText 方法](../../../ado/reference/ado-api/writetext-method.md)
