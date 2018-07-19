---
title: ProductName 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 724f62e041c43aa2fb51070f1e130a8bbabfe855
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34038412"
---
# <a name="productname-element-assl"></a>ProductName 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含執行個體的唯讀產品名稱[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]相關聯[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Server>  
      ...  
      <ProductName>...</ProductName>  
   ...  
</Server>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[[伺服器]](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **ProductName**項目會提供唯讀存取的執行個體相關聯的產品名稱[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 對應目的父代的項目**ProductName**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Server>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
