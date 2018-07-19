---
title: Delete 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 30149ab2eacae34f3f90de68772821e5d2f0232c
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34574940"
---
# <a name="delete-element-xmla"></a>Delete 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  刪除 Analysis Services 執行個體上的物件。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Delete IgnoreFailures="boolean">  
      <Object>...</Object>  
   </Delete>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[物件](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|IgnoreFailures|選擇性 **Boolean** 屬性。 如果設定為 True， **Execute** 方法就會忽略網路失敗或與遠端資料分割相關的失敗。|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另請參閱
 [命令&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
