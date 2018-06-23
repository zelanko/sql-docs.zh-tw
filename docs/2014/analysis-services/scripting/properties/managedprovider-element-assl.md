---
title: ManagedProvider 元素 (ASSL) |Microsoft 文件
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
- ManagedProvider Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- ManagedProvider element
ms.assetid: ed5a1077-20a4-40b9-b62d-0db0d53b9624
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fe2bb53abd8a528fa9ca5e1b685591bc57f162e1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032867"
---
# <a name="managedprovider-element-assl"></a>ManagedProvider 元素 (ASSL)
  包含衍生自項目所使用的 managed 提供者名稱[DataSource](../data-type/datasource-data-type-assl.md)資料型別。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataSource>  
   ...  
   <ManagedProvider>...</ManagedProvider>  
   ...  
</DataSource>  
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
|父元素|[DataSource](../data-type/datasource-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如果資料來源使用 Managed 提供者，`ManagedProvider` 元素就會包含 Managed 提供者的名稱。  
  
## <a name="see-also"></a>另請參閱  
 [名稱元素&#40;ASSL&#41;](name-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  