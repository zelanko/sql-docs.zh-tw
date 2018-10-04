---
title: 物件 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- objects [XML for Analysis]
- XML for Analysis, objects
- XMLA, objects
ms.assetid: 768188ef-85d4-432a-9390-be05c835137f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e60cc807677b563361dbeea06c2f6b45ab468049
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149368"
---
# <a name="objects-xmla"></a>物件 (XMLA)
  XML for Analysis (XMLA) 通訊協定會使用兩個方法：`Discover`並`Execute`，以提供標準的方式，讓應用程式存取的執行個體上的資訊[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 由於這些方法是使用簡易物件存取通訊協定 (SOAP) 通訊協定叫用的，因此它們會接受使用 XML 格式的輸入並以 XML 格式傳遞輸出。  
  
## <a name="in-this-section"></a>本節內容  
 下列主題將描述 [!INCLUDE[ssAS](../../includes/ssas-md.md)] 所實作的 XMLA 物件。  
  
|方法|描述|  
|------------|-----------------|  
|[DiscoverResponse 元素&#40;XMLA&#41;](xml-elements-objects-discoverresponse.md)|包含的執行個體所傳回的資訊[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]來回[Discover](xml-elements-methods-discover.md)方法呼叫。|  
|[ExecuteResponse 元素&#40;XMLA&#41;](xml-elements-objects-executeresponse.md)|包含的執行個體所傳回的資訊[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]來回[Execute](xml-elements-methods-execute.md)方法呼叫。|  
  
## <a name="see-also"></a>另請參閱  
 [XML 項目&#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [XML 資料型別&#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [XML 項目&#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)  
  
  
