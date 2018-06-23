---
title: 處理元素 (XMLA) |Microsoft 文件
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
- Process Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Process
- http://schemas.microsoft.com/analysisservices/2003/engine#Process
- microsoft.xml.analysis.process
helpviewer_keywords:
- Process command
ms.assetid: 886fd480-c0e6-4c9b-b65e-da47f874d938
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 4e90cbb8d18cdba034019e74b7b9d0b00966ee7f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135477"
---
# <a name="process-element-xmla"></a>Process 元素 (XMLA)
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[繫結](../xml-elements-properties/bindings-element-xmla.md)， [DataSource](../xml-elements-properties/source-element-xmla.md)， [DataSourceView](../xml-elements-properties/datasourceview-element-xmla.md)， [ErrorConfiguration](../xml-elements-properties/errorconfiguration-element-xmla.md)，[物件](../xml-elements-properties/object-element-xmla.md)，[類型項目&#40;XMLA&#41;](../xml-elements-properties/type-element-xmla.md)， [WriteBackTableCreation](../xml-elements-properties/writebacktablecreation-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 如需有關處理物件的詳細資訊，請參閱[處理物件&#40;XMLA&#41;](../xml-elements-objects.md)。  
  
## <a name="see-also"></a>另請參閱  
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  