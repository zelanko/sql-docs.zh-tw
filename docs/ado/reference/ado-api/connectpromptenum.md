---
title: ConnectPromptEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4761b8375e78c10556d3c9f414e3558cb59a4e21
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="connectpromptenum"></a>ConnectPromptEnum
指定是否應該顯示的對話方塊開啟資料來源的連接時，遺漏的參數提示。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|永遠會提示。|  
|**adPromptComplete**|2|如果您需要更多的資訊，會提示。|  
|**adPromptCompleteRequired**|3|如果您需要更多的資訊，但不是允許有選擇性參數，則會提示。|  
|**adPromptNever**|4|永遠不會提示。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 Package: **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.ConnectPrompt.ALWAYS|  
|AdoEnums.ConnectPrompt.COMPLETE|  
|AdoEnums.ConnectPrompt.COMPLETEREQUIRED|  
|AdoEnums.ConnectPrompt.NEVER|  
  
## <a name="applies-to"></a>適用於  
 [Prompt 動態屬性 (ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)
