---
title: Password 元素 (ASSL) |Microsoft 文件
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
- Password Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Password element
ms.assetid: ee756b01-fb08-4a9a-8c2a-7c04af0f8658
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e702e7307e11c506652e91ca4cdc8f02ca06318d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022711"
---
# <a name="password-element-assl"></a>Password 元素 (ASSL)
  包含的使用者帳戶的密碼[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Password>...</Password>  
   ...  
</ImpersonationInfo>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值`Password`項目，以及值[帳戶](account-element-impersonationinfo-assl.md)項目，用於模擬用途，如果值[ImpersonationMode](impersonationmode-element-assl.md)之任何元素衍生自`ImpersonationInfo`資料類型設為*ImpersonateAccount*。  
  
 只有 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體之伺服器管理員角色的成員可以針對 `Password` 元素提供空白值。  
  
## <a name="see-also"></a>另請參閱  
 [DataSourceImpersonationInfo 元素&#40;ASSL&#41;](impersonationinfo-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  