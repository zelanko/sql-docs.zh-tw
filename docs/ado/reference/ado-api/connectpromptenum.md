---
title: ConnectPromptEnum | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 40ce74748e15a2715de26e813007e00be0c33729
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698601"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
指定是否應該顯示對話方塊中開啟資料來源的連接時，遺漏的參數提示。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|一律提示。|  
|**adPromptComplete**|2|如果需要更多的資訊，提示。|  
|**adPromptCompleteRequired**|3|如果您需要更多的資訊，但不是允許使用選擇性的參數會提示。|  
|**adPromptNever**|4|永遠不會出現提示。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 封裝： **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.ConnectPrompt.ALWAYS|  
|AdoEnums.ConnectPrompt.COMPLETE|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums.ConnectPrompt.NEVER|  
  
## <a name="applies-to"></a>適用於  
 [Prompt 動態屬性 (ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)
