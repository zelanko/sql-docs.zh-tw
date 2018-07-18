---
title: Statement 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 49238b50457a586bbf23cc75ee454003c57ac04e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979160"
---
# <a name="statement-element-xmla"></a>Statement 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含查詢或陳述式來傳送使用**Execute** Analysis Services 執行個體的方法。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Statement>...</Statement>  
</Command>  
```  
  
## <a name="element-characteristics"></a>項目特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>項目關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **陳述式**命令上執行的查詢或陳述式[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支援下列語言：  
  
-   多維度運算式 (MDX)  
  
-   資料採礦延伸模組 (MDX)  
  
-   結構化查詢語言 (SQL) 的子集  
  
## <a name="see-also"></a>另請參閱
 [命令&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
