---
title: PermissionSet 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- PermissionSet Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PermissionSet
helpviewer_keywords:
- PermissionSet element
ms.assetid: da5a9175-48e4-4b5e-a780-3e0077939974
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 590dbc9ae62340fd3d4cf08d06f8a593bcf520f5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049301"
---
# <a name="permissionset-element-assl"></a>PermissionSet 元素 (ASSL)
  識別與相關聯的權限集合[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 組件。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ClrAssembly>  
   ...  
   <PermissionSet>...</PermissionSet>  
  
</ClrAssembly>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*安全*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ClrAssembly](../data-type/assembly-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*安全*|僅允許內部計算和本機資料存取。 *安全*是限制最嚴格的權限集合。 使用組件所執行的程式碼*安全*權限無法存取外部系統資源，例如檔案、 網路、 環境變數或登錄。|  
|*ExternalAccess*|*安全*，並附帶存取外部系統資源，例如檔案、 網路、 環境變數和登錄的能力。|  
|*不受限制*|Unrestricted 可讓組件無限制存取資源，內部和外部[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 從執行的程式碼*Unrestricted*組件可以呼叫 unmanaged 程式碼。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `PermissionSet` 允許值的列舉是 <xref:Microsoft.AnalysisServices.PermissionSet>。  
  
## <a name="see-also"></a>另請參閱  
 [ComAssembly 資料類型&#40;ASSL&#41;](../data-type/comassembly-data-type-assl.md)   
 [Assemblies 元素&#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [資料庫項目&#40;ASSL&#41;](../objects/database-element-assl.md)   
 [伺服器項目&#40;ASSL&#41;](../objects/server-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
