---
title: PermissionSet 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2299f76822ae24eb2fee1085fc49836704ba275a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34038832"
---
# <a name="permissionset-element-assl"></a>PermissionSet 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  識別相關聯的權限集合[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 組件。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ClrAssembly>  
   ...  
   <PermissionSet>...</PermissionSet>  
  
</ClrAssembly>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*Safe*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*Safe*|僅允許內部計算和本機資料存取。 *安全*是限制最嚴格的權限集合。 與組件所執行的程式碼*安全*權限無法存取外部系統資源，例如檔案、 網路、 環境變數或登錄。|  
|*ExternalAccess*|*安全*，其他能夠存取外部系統資源，例如檔案、 網路、 環境變數和登錄。|  
|*不受限制*|不受限制允許內部和外部的資源組件無限制存取[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 從執行的程式碼*Unrestricted*組件可以呼叫 unmanaged 程式碼。|  
  
 列舉型別對應至允許的值**PermissionSet**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.PermissionSet>。  
  
## <a name="see-also"></a>另請參閱  
 [ComAssembly 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)   
 [Assemblies 元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [Database 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Server 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
