---
title: Password 元素 (ASSL) |Microsoft Docs
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 99d7eabdd66e6c7f036389b4825c5926873367b2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37197738"
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
 值`Password`項目，以及值[帳號](account-element-impersonationinfo-assl.md)項目，用於模擬用途，如果的值[ImpersonationMode](impersonationmode-element-assl.md)之任何元素衍生自`ImpersonationInfo`資料類型設為*ImpersonateAccount*。  
  
 只有 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體之伺服器管理員角色的成員可以針對 `Password` 元素提供空白值。  
  
## <a name="see-also"></a>另請參閱  
 [DataSourceImpersonationInfo 元素&#40;ASSL&#41;](impersonationinfo-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
