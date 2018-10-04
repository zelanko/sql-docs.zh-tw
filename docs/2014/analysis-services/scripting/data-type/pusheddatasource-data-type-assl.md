---
title: PushedDataSource 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- PushedDataSource Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PushedDataSource
helpviewer_keywords:
- PushedDataSource data type
ms.assetid: b319ee87-7c0a-41ec-a8af-cc7089aeb6ad
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ec01d8795e9ba5212dd8bfbd30186bbf648a8726
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169837"
---
# <a name="pusheddatasource-data-type-assl"></a>PushedDataSource 資料類型 (ASSL)
  定義代表資料來源的基本資料類型 (例如[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]封裝) 用於 「 推送 」 資料[Cube](../objects/cube-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<PushedDataSource>  
   <Root>...</Root>  
   <EndOfData>...</EndOfData>  
</PushedDataSource>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|None|  
|衍生資料類型|None|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[EndOfData](../objects/data-element-assl.md)，[根](../properties/root-element-assl.md)|  
|衍生的元素|None|  
  
## <a name="remarks"></a>備註  
 `PushedDataSource` 只能在處理命令中當做非正規 (out-of-line) 資料來源使用。 保存的資料來源絕對不會屬於這種類型。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
