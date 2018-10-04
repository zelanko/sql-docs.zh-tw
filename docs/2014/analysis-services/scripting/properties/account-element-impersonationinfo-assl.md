---
title: 帳戶元素 (ImpersonationInfo) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Account Element (ImpersonationInfo)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Account element
ms.assetid: aa3a1281-e42a-4926-875b-e6b81f4599c3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f454e39a7c4ec4911f38ff070f94fcbe50a34c74
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48190368"
---
# <a name="account-element-impersonationinfo-assl"></a>Account 元素 (ImpersonationInfo) (ASSL)
  包含的使用者帳戶名稱[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)資料型別。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ImpersonationInfo  
   ...  
  <Account>...</Account>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ImpersonationInfo](../data-type/impersonationinfo-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 值`Account`項目，以及值[密碼](password-element-assl.md)項目，用於模擬用途，如果值[ImpersonationMode](impersonationmode-element-assl.md)之任何元素衍生自`ImpersonationInfo`資料類型設為*ImpersonateAccount*。  
  
## <a name="see-also"></a>另請參閱  
 [DataSourceImpersonationInfo 元素&#40;ASSL&#41;](impersonationinfo-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
