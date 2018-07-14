---
title: RemoteDatasourceID 元素 (ASSL) |Microsoft Docs
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
- RemoteDatasourceID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RemoteDatasourceID
helpviewer_keywords:
- RemoteDatasourceID element
ms.assetid: 2eaf0b9c-8c2d-4dc6-9bad-1db70a4b04b1
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 021b242c80aedbc23a5cf34b35b54714dd21e557
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37189105"
---
# <a name="remotedatasourceid-element-assl"></a>RemoteDatasourceID 元素 (ASSL)
  指定的識別碼 (ID)，指向 執行個體的 OLAP 資料來源[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]儲存遠端資料分割。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Partition>  
      ...  
   <RemoteDatasourceID>...</RemoteDatasourceID>  
   ...  
</Partition>  
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
|父元素|[資料分割](../objects/partition-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如果 `RemoteDatasourceID` 為 Null，就表示資料分割位於本機。  
  
 對應至父系的元素`RemoteDatasourceID`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
