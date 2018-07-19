---
title: ConnectPromptEnum |Microsoft 文件
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
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62b1bb38789dcfb2fd15b80501315d9c1be38a66
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277237"
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
指定是否應該顯示的對話方塊開啟資料來源的連接時，遺漏的參數提示。  
  
|常數|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|@shouldalert|永遠會提示。|  
|**adPromptComplete**|2|如果您需要更多的資訊，會提示。|  
|**adPromptCompleteRequired**|3|如果您需要更多的資訊，但不是允許有選擇性參數，則會提示。|  
|**adPromptNever**|4|永遠不會提示。|  
  
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
