---
title: NotifyTableChange 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6b379fde8b0561af0af41cabcef1b91adf459a26
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="notifytablechange-element-xmla"></a>NotifyTableChange 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  通知的執行個體[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ，已經變更指定的資料來源中的資料表。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <NotifyTableChange>  
      <Object>...</Object>  
      <TableNotifications>...</TableNotifications>  
   </NotifyTableChange>  
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
|子元素|[物件](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)， [TableNotifications](../../../analysis-services/xmla/xml-elements-properties/tablenotifications-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 **NotifyTableChange**命令可讓用戶端應用程式明確通知[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]執行個體，一部或多個資料來源中所包含的資料表已變更。 若為主動式快取，這個通知會指出以這些資料表為基礎的關聯式 OLAP (ROLAP) 物件應該進行檢閱和更新。  
  
 這種通知方法最適合用於以資料來源檢視中定義之檢視或具名查詢為基礎的 ROLAP 物件，因為這些物件的變更可能難以偵測和追蹤。  
  
 **物件**元素必須參考中的資料來源[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫。 如果**物件**項目參考資料來源以外的物件就會發生錯誤。  
  
 如需主動式快取的詳細資訊，請參閱[主動式快取 &#40;資料分割&#41;](../../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。  
  
## <a name="see-also"></a>另請參閱  
 [命令 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
