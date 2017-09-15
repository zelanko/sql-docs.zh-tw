---
title: "ConnectPromptEnum |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ConnectPromptEnum
helpviewer_keywords:
- ConnectPromptEnum enumeration [ADO]
ms.assetid: 21026e24-62b7-4cc9-8aef-62c1fc6cba75
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8ae0c2179e321e521a86fdc76e5f8978ab4ab747
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="connectpromptenum"></a>ConnectPromptEnum
指定是否應該顯示的對話方塊開啟資料來源的連接時，遺漏的參數提示。  
  
|常數|值|Description|  
|--------------|-----------|-----------------|  
|**adPromptAlways**|1|永遠會提示。|  
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
 [提示屬性動態 (ADO)](../../../ado/reference/ado-api/prompt-property-dynamic-ado.md)
