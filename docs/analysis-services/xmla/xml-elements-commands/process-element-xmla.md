---
title: 處理元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 10e5fbdf4e5b701342cf98bb1f04212e89b65cab
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="process-element-xmla"></a>Process 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  在處理物件[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Process>  
      <Type>...</Type>  
      <Object>...</Object>  
      <Bindings>...</Bindings>  
      <DataSource>...</DataSource>  
      <DataSourceView>...</DataSourceView>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <WriteBackTableCreation>...</WriteBackTableCreation>  
   </Process>  
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
|子元素|[繫結](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md)， [DataSource](../../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md)， [DataSourceView](../../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md)， [ErrorConfiguration](../../../analysis-services/xmla/xml-elements-properties/errorconfiguration-element-xmla.md)，[物件](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)，[類型項目&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/type-element-xmla.md)， [WriteBackTableCreation](../../../analysis-services/xmla/xml-elements-properties/writebacktablecreation-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 如需有關處理物件的詳細資訊，請參閱[處理物件&#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md)。  
  
## <a name="see-also"></a>另請參閱  
 [命令 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
