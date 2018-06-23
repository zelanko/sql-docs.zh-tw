---
title: 標頭 (XMLA) |Microsoft 文件
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
topic_type:
- apiref
- apinav
helpviewer_keywords:
- XMLA, headers
- SOAP headers [XML for Analysis]
- XML for Analysis, headers
- headers [XML for Analysis]
ms.assetid: 36407b5c-d98d-47e4-8d36-d8896e15a748
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: bb2cff2e70ccd1ac0cf391f7832db4978a415f56
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134796"
---
# <a name="headers-xmla"></a>標頭 (XMLA)
  XML for Analysis (XMLA) 通訊協定會在 SOAP 標頭內部使用 XML 元素來管理通訊協定層級的功能，例如工作階段支援和支援功能的交涉。  
  
## <a name="in-this-section"></a>本節內容  
 下列主題將描述所實作的 XMLA 標頭元素[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
|方法|描述|  
|------------|-----------------|  
|[BeginSession 元素&#40;XMLA&#41;](session-element-xmla.md)|在 SOAP 要求訊息中使用 SOAP 標頭，以便在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上啟動新的工作階段。|  
|[EndSession 元素&#40;XMLA&#41;](endsession-element-xmla.md)|在 SOAP 要求訊息中使用 SOAP 標頭，以便在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上結束現有的工作階段。|  
|[工作階段項目&#40;XMLA&#41;](session-element-xmla.md)|在 SOAP 要求訊息中使用 SOAP 標頭，以便在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上識別現有的明確工作階段。|  
|[ProtocolCapabilities 元素&#40;XMLA&#41;](protocolcapabilities-element-xmla.md)|在 SOAP 要求訊息中使用 SOAP 標頭，以便識別 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體與用戶端應用程式之間的通訊協定功能。|  
  
## <a name="see-also"></a>另請參閱  
 [XML 項目&#40;XMLA&#41;](../../dev-guide/xml-elements-xmla.md)   
 [XML 資料型別&#40;XMLA&#41;](../xml-data-types/xml-data-types-xmla.md)   
 [XML 項目&#40;XMLA&#41;](../../dev-guide/xml-elements-xmla.md)  
  
  