---
title: ImpersonationMode 元素 (ASSL) |Microsoft 文件
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
- ImpersonationMode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ImpersonateMode
helpviewer_keywords:
- ImpersonateMode element
ms.assetid: 160fdcb2-ac9f-4c5a-a0eb-a5f7669166b9
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e41e5b5fef7759f6ad310a7f04dc012a7b7cb54f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133322"
---
# <a name="impersonationmode-element-assl"></a>ImpersonationMode 元素 (ASSL)
  包含值，指出衍生自的元素的模擬方法[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)資料型別。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ImpersonationInfo>  
   ...  
   <ImpersonationMode>...</ImpersonationMode>  
  
</ImpersonationInfo>...  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*預設值*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*預設值*|父系會使用最適用於使用模擬之環境的模擬方法。|  
|*ImpersonateAccount*|父系會使用父元素中指定之使用者帳戶的認證。|  
|*ImpersonateAnonymous*|父系會使用匿名使用者的認證。|  
|*也就是 ImpersonateCurrentUser*|父系會使用目前使用者的認證。|  
|*ImpersonateServiceAccount*|父系會使用與執行個體相關聯的服務帳戶的認證[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `ImpersonationMode` 允許值的列舉是 <xref:Microsoft.AnalysisServices.ImpersonationLevel>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  