---
title: 鎖定元素 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Lock Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Lock
- microsoft.xml.analysis.lock
- http://schemas.microsoft.com/analysisservices/2003/engine#Lock
helpviewer_keywords:
- Lock command
ms.assetid: a819e805-4793-43bb-8af3-16a19f8bdab3
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 84211c6df5fc6e8efc97f4d81bc8890e4ab489d3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="lock-element-xmla"></a>Lock 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  鎖定指定的物件上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <Lock>  
      <ID>...</ID>  
      <Object>...</Object>  
      <Mode>...</Mode>  
   </Lock>  
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
|子元素|[ID](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md), [Mode](../../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md), [Object](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **鎖定**命令會鎖定物件，以便共用或獨佔使用，目前使用中交易內容中。 只有資料庫管理員或伺服器管理員可以明確發出**鎖定**命令。 鎖定物件會防止認可交易，直到移除鎖定為止。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支援兩種鎖定類型：共用鎖定和獨佔鎖定。 如需有關所支援的鎖定類型[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，請參閱[Mode 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md).  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 僅允許鎖定資料庫。 **物件**元素必須包含的物件參考[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫。 如果**物件**未指定項目或**物件**元素參考資料庫以外的物件發生錯誤。  
  
 其他命令會隱含地問題**鎖定**命令[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫。 讀取資料庫，例如任何資料或中繼資料的任何作業**探索**方法或**Execute**方法執行**陳述式**命令都會隱含地發出共用在資料庫上的鎖定。 在將資料或中繼資料的變更認可至物件的任何交易[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫，例如**Execute**方法執行**Alter**命令，以隱含方式上發出獨佔鎖定資料庫。  
  
 所有鎖定都會保存在目前交易的內容中。 當目前的交易經過認可或回復時，就會自動釋放在交易內部定義的所有鎖定。  
  
## <a name="see-also"></a>另請參閱  
 [解除鎖定元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)   
 [命令 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
