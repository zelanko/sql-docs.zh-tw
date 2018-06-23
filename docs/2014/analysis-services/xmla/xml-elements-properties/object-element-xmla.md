---
title: 物件元素 (XMLA) |Microsoft 文件
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
caps.latest.revision: 16
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 02d27280ab74e907558c07ece457d114f8dcbd1b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145228"
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
|資料類型和長度|無|  
|預設值|無|  
|基數|上階或父系： [Alter](../xml-elements-commands/create-element-xmla.md) &#124; 0-1： 只能出現一次只能出現一次的選擇性項目。<br /><br /> 上階或父系： 其他所有項目&#124;1-1： 出現一次的必要項目。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Alter](../xml-elements-commands/alter-element-xmla.md)，[備份](../xml-elements-commands/backup-element-xmla.md)， [ClearCache](../xml-elements-commands/clearcache-element-xmla.md)，[刪除](../xml-elements-commands/delete-element-xmla.md)， [DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md)，[鎖定](../xml-elements-commands/lock-element-xmla.md)， [NotifyTableChange](../xml-elements-commands/notifytablechange-element-xmla.md)，[程序](../xml-elements-commands/process-element-xmla.md)，[訂閱](../xml-elements-commands/subscribe-element-xmla.md)，[同步處理](../xml-elements-commands/synchronize-element-xmla.md)|  
|子元素|必要的「Analysis Services 指令碼語言」(ASSL) 元素。 透過列出物件及其上階 (不包括 `Server` 物件) 的識別碼元素指定。例如，下列 `Object` 元素會識別資料分割：<br /><br /> `<Object>`<br /><br /> `<DatabaseID>Adventure Works DW Multidimensional 2012</DatabaseID>`<br /><br /> `<CubeID>Adventure Works</CubeID>`<br /><br /> `<MeasureGroupID>Internet Sales</MeasureGroupID>`<br /><br /> `<PartitionID>Inernet_Sales_2001</PartitionID>`<br /><br /> `</Object>`|  
  
## <a name="remarks"></a>備註  
 識別碼出現的順序並不重要。  
  
 如`Alter`項目、 執行個體[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]如果當做預設物件`Object`未指定項目。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  