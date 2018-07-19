---
title: Edition 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 466a597a94a61e30dbd819cb3a87747c42dec5a9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34036129"
---
# <a name="edition-element-assl"></a>Edition 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含執行個體的唯讀版本[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]由[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Server>  
      ...  
      <Edition>...</Edition>  
   ...  
</Server>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **Edition**元素描述哪個版本的[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]安裝。 這個元素的值限制為下表所列的其中一個字串。  
  
|Value|Description|  
|-----------|-----------------|  
|*Standard*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]適用於 32 位元處理器的 standard edition。|  
|*企業版*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]適用於 32 位元處理器的 Enterprise edition。|  
|*EnterpriseCore*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise edition： 核心授權適用於 32 位元處理器。|  
|*BusinessIntelligence*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]適用於 32 位元處理器的 business Intelligence edition。|  
|*開發人員*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]適用於 32 位元處理器的 developer edition|  
|*評估*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]適用於 64 位元處理器的 evaluation edition。|  
|*本機*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]適用於 32 位元處理器的 local edition。|  
|*Standard64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]適用於 64 位元處理器的 standard edition。|  
|*Enterprise64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]適用於 64 位元處理器的 Enterprise edition。|  
|*EnterpriseCore64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise edition： 核心授權適用於 64 位元處理器。|  
|*BusinessIntelligence64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]適用於 64 位元處理器的 business Intelligence edition。|  
|*Developer64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]適用於 64 位元處理器的 developer edition|  
|*Evaluation64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]適用於 64 位元處理器的 evaluation edition。|  
|*Local64*|[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]適用於 64 位元處理器的 local edition。|  
  
 列舉型別對應至允許的值**ServerEdition**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ServerEdition>。  
  
## <a name="see-also"></a>另請參閱  
 [Version 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/version-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
