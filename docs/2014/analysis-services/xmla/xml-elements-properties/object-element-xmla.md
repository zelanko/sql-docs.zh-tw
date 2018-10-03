---
title: 物件元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Object Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Object
- urn:schemas-microsoft-com:xml-analysis#Object
- microsoft.xml.analysis.object
helpviewer_keywords:
- Object element
ms.assetid: 99470537-2c4a-4072-9613-940c41c12487
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e4fb7e25b9e813487b612bbd6269c2f080d85f5e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178748"
---
# <a name="object-element-xmla"></a>Object 元素 (XMLA)
  包含父元素所使用的物件參考。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Alter> <!-- or any of the parent elements in the Element Relationships table -->  
...  
   <Object>  
      <!-- One or more object identifiers, depending on the parent element -->  
   </Object>  
...  
</Alter>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|上階或父系：[改變](../xml-elements-commands/create-element-xmla.md) &#124; 0-1： 只能出現一次一次的選擇性元素。<br /><br /> 上階或父系： 所有其他項目的&#124;1-1： 出現一次，一次的必要的元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Alter](../xml-elements-commands/alter-element-xmla.md)，[備份](../xml-elements-commands/backup-element-xmla.md)， [ClearCache](../xml-elements-commands/clearcache-element-xmla.md)，[刪除](../xml-elements-commands/delete-element-xmla.md)， [DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)，[鎖定](../xml-elements-commands/lock-element-xmla.md)， [NotifyTableChange](../xml-elements-commands/notifytablechange-element-xmla.md)，[處理程序](../xml-elements-commands/process-element-xmla.md)，[訂閱](../xml-elements-commands/subscribe-element-xmla.md)，[同步處理](../xml-elements-commands/synchronize-element-xmla.md)|  
|子元素|必要的「Analysis Services 指令碼語言」(ASSL) 元素。 透過列出物件及其上階 (不包括 `Server` 物件) 的識別碼元素指定。例如，下列 `Object` 元素會識別資料分割：<br /><br /> `<Object>`<br /><br /> `<DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>`<br /><br /> `<CubeID>Adventure Works</CubeID>`<br /><br /> `<MeasureGroupID>Internet Sales</MeasureGroupID>`<br /><br /> `<PartitionID>Inernet_Sales_2001</PartitionID>`<br /><br /> `</Object>`|  
  
## <a name="remarks"></a>備註  
 識別碼出現的順序並不重要。  
  
 針對`Alter`項目、 執行個體[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]如果當做預設物件`Object`未指定項目。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
