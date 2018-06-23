---
title: NotifyTableChange 元素 (XMLA) |Microsoft 文件
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
- NotifyTableChange Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#NotifyTableChange
- http://schemas.microsoft.com/analysisservices/2003/engine#NotifyTableChange
- microsoft.xml.analysis.notifytablechange
helpviewer_keywords:
- NotifyTableChange command
ms.assetid: b76898eb-20d3-48c8-9eb8-1fd5df638bcc
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 64779ceab6d83365755ed212a93685ee3f31837f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134246"
---
# <a name="notifytablechange-element-xmla"></a>NotifyTableChange 元素 (XMLA)
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[物件](../xml-elements-properties/object-element-xmla.md)， [TableNotifications](../xml-elements-properties/tablenotifications-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `NotifyTableChange` 命令允許用戶端應用程式明確通知 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體，表示資料來源中包含的一個或多個資料表已經變更。 若為主動式快取，這個通知會指出以這些資料表為基礎的關聯式 OLAP (ROLAP) 物件應該進行檢閱和更新。  
  
 這種通知方法最適合用於以資料來源檢視中定義之檢視或具名查詢為基礎的 ROLAP 物件，因為這些物件的變更可能難以偵測和追蹤。  
  
 `Object` 元素必須參考 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 資料庫中的資料來源。 如果 `Object` 元素參考資料來源以外的物件，就會發生錯誤。  
  
 如需主動式快取的詳細資訊，請參閱[主動式快取 &#40;資料分割&#41;](../../multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。  
  
## <a name="see-also"></a>另請參閱  
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  