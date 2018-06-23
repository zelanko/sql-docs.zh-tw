---
title: PermissionSet 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a6246058af826a73b589f1854b0236de946a4d65
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133550"
---
# <a name="permissionset-element-assl"></a>PermissionSet 元素 (ASSL)
  識別相關聯的權限集合[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 組件。  
  
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
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*安全*|僅允許內部計算和本機資料存取。 *安全*是限制最嚴格的權限集合。 與組件所執行的程式碼*安全*權限無法存取外部系統資源，例如檔案、 網路、 環境變數或登錄。|  
|*ExternalAccess*|*安全*，其他能夠存取外部系統資源，例如檔案、 網路、 環境變數和登錄。|  
|*不受限制*|不受限制允許內部和外部的資源組件無限制存取[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 從執行的程式碼*Unrestricted*組件可以呼叫 unmanaged 程式碼。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `PermissionSet` 允許值的列舉是 <xref:Microsoft.AnalysisServices.PermissionSet>。  
  
## <a name="see-also"></a>另請參閱  
 [ComAssembly 資料類型&#40;ASSL&#41;](../data-type/comassembly-data-type-assl.md)   
 [Assemblies 元素&#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [Database 元素&#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Server 元素&#40;ASSL&#41;](../objects/server-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  