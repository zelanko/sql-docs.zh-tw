---
title: RequiresRestart 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 37199197b062930b96e9715aa6ed2f41348ea2f3
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="requiresrestart-element-assl"></a>RequiresRestart 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含相關聯的唯讀值[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)項目可決定是否變更伺服器屬性的值需要執行個體，重新啟動，變更才會生效。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ServerProperty>  
   ...  
   <RequiresRestart>...</RequiresRestart>  
   ...  
</ServerProperty>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目**RequiresRestart**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ServerProperty>。  
  
## <a name="see-also"></a>另請參閱  
 [ServerProperties 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)   
 [Server 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
