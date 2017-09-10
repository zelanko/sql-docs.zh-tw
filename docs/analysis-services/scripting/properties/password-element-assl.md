---
title: "Password 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Password Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Password element
ms.assetid: ee756b01-fb08-4a9a-8c2a-7c04af0f8658
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d83c0cccfaf1c4a50b2c10efead1f923012e6e0d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="password-element-assl"></a>Password 元素 (ASSL)
  包含的使用者帳戶的密碼[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Password>...</Password>  
   ...  
</ImpersonationInfo>  
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
|父元素|[ImpersonationInfo](../../../analysis-services/scripting/data-type/impersonationinfo-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 值**密碼**項目，以及值[帳戶](../../../analysis-services/scripting/properties/account-element-impersonationinfo-assl.md)項目，用於模擬用途，如果值[ImpersonationMode](../../../analysis-services/scripting/properties/impersonationmode-element-assl.md)項目任何項目衍生自**ImpersonationInfo**資料類型設為*ImpersonateAccount*。  
  
 只有伺服器管理員角色的成員[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體可以提供空白值**密碼**項目  
  
## <a name="see-also"></a>另請參閱  
 [DataSourceImpersonationInfo 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/datasourceimpersonationinfo-element-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
