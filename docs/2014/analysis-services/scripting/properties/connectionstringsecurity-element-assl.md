---
title: ConnectionStringSecurity 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ConnectionStringSecurity Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ConnectionStringSecurity
helpviewer_keywords:
- ConnectionStringSecurity element
ms.assetid: f25c4448-bb0d-4945-bc84-9c015eefa0eb
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9479865bd2e3f10570418ee33064bc30f4b7b786
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37300868"
---
# <a name="connectionstringsecurity-element-assl"></a>ConnectionStringSecurity 元素 (ASSL)
  指定是否要針對安全性目的從資料來源連接字串中移除使用者密碼。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataSource>  
   ...  
   <ConnectionStringSecurity>...</ConnectionStringSecurity>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DataSource](../objects/datasource-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*PasswordRemoved*|已經從連接字串中移除密碼。|  
|*未變更*|尚未修改連接字串。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `ConnectionStringSecurity` 允許值的列舉是 <xref:Microsoft.AnalysisServices.ConnectionStringSecurity>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
