---
title: ServerProperty 元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 78ee20a793b17fe9c646057a2d0861fe32d7cf67
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34036169"
---
# <a name="serverproperty-element-assl"></a>ServerProperty 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義相關聯的伺服器屬性[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ServerProperties>  
   <ServerProperty>  
      <Name>...</Name>  
      <Value>...</Value>  
            <RequiresRestart>...</RequiresRestart>  
            <PendingValue>...</PendingValue>  
      <DefaultValue>...</DefaultValue>  
      <DisplayFlag>...</DisplayFlag>  
   </ServerProperty>  
</ServerProperties>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ServerProperties](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)|  
|子元素|[DefaultValue](../../../analysis-services/scripting/properties/defaultvalue-element-assl.md)， [DisplayFlag](../../../analysis-services/scripting/properties/displayflag-element-assl.md)，[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)， [PendingValue](../../../analysis-services/scripting/properties/pendingvalue-element-assl.md)， [RequiresRestart](../../../analysis-services/scripting/properties/requiresrestart-element-assl.md)，[值](../../../analysis-services/scripting/properties/value-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 **ServerProperty**元素描述的資料和中繼資料的執行個體相關聯之伺服器屬性[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 不同於其他集合中 Analysis Services 指令碼語言 (ASSL)，所包含的項目**ServerProperty**項目使用而明確命名的項目不是名稱/值組，來描述伺服器屬性。 名稱/值組可提供彈性和擴充性。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.ServerProperty>。  
  
## <a name="see-also"></a>另請參閱  
 [Server 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [物件 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
