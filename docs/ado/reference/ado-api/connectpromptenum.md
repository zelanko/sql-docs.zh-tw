---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: afd5d9ca0de6b8d2ffba75f862e6ca0afb594848
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919448"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
指定在開啟資料來源的連接時，是否應該顯示對話方塊，以提示遺漏參數。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|一律會出現提示。|  
|**adPromptComplete**|2|如果需要詳細資訊，則提示。|  
|**adPromptCompleteRequired**|3|如果需要更多資訊，但不允許選擇性參數，則會提示。|  
|**adPromptNever**|4|永遠不會提示。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等  
 Package： **.com. wfc. 資料**  
  
|持續性|  
|--------------|  
|AdoEnums. ConnectPrompt. ALWAYS|  
|AdoEnums. ConnectPrompt. COMPLETE|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums. ConnectPrompt. NEVER|  
  
## <a name="applies-to"></a>套用至  
 [Prompt 動態屬性 (ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)
