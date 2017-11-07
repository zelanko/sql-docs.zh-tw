---
title: "Detach 元素 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Detach command
ms.assetid: adbc7920-2a4a-4842-9e6f-37006fa19ff8
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7ec8a5cfc27be9fbf9fcf4f5844cb0112ad437cd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="detach-element"></a>Detach 元素
  從目前的伺服器執行個體中卸離 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Detach>  
      <Object>...</Object>  
      <Password>...</Password>  
   </Detach>  
</Command>  
  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[物件](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)<br /><br /> [密碼](../../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md)|  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Attach 元素](../../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [附加和卸離 Analysis Services 資料庫](../../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [移動 Analysis Services 資料庫](../../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [資料庫 Readwritemode](../../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [切換 ReadOnly 和 ReadWrite 模式之間的 Analysis Services 資料庫](../../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)  
  
  

