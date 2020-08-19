---
description: ConnectPromptEnum
title: ConnectPromptEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
author: rothja
ms.author: jroth
ms.openlocfilehash: 0ad8fe77bb3472931d3b16d5849b047001922c96
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444410"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
指定是否應顯示對話方塊，以在開啟與資料來源的連接時提示遺漏參數。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|一律提示。|  
|**adPromptComplete**|2|提示是否需要更多資訊。|  
|**adPromptCompleteRequired**|3|提示是否需要更多的資訊，但不允許選擇性參數。|  
|**adPromptNever**|4|永遠不會提示。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 相等  
 封裝： **.com. 資料**  
  
|常數|  
|--------------|  
|AdoEnums. ConnectPrompt. 一律|  
|AdoEnums. ConnectPrompt. 完成|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums. ConnectPrompt. 永不|  
  
## <a name="applies-to"></a>套用至  
 [Prompt 動態屬性 (ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)
