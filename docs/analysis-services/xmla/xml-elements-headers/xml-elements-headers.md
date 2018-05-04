---
title: 標頭 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XMLA, headers
- SOAP headers [XML for Analysis]
- XML for Analysis, headers
- headers [XML for Analysis]
ms.assetid: 36407b5c-d98d-47e4-8d36-d8896e15a748
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0fd680e1fe5df195752e1618fe23551f4c10f2a2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="xml-elements---headers"></a>XML 項目-標頭
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  XML for Analysis (XMLA) 通訊協定會在 SOAP 標頭內部使用 XML 元素來管理通訊協定層級的功能，例如工作階段支援和支援功能的交涉。  
  
## <a name="in-this-section"></a>本節內容  
 下列主題將描述所實作的 XMLA 標頭元素[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
|方法|Description|  
|------------|-----------------|  
|[BeginSession 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/beginsession-element-xmla.md)|在 SOAP 要求訊息中使用 SOAP 標頭，以便在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上啟動新的工作階段。|  
|[EndSession 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/endsession-element-xmla.md)|在 SOAP 要求訊息中使用 SOAP 標頭，以便在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上結束現有的工作階段。|  
|[Session 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/session-element-xmla.md)|在 SOAP 要求訊息中使用 SOAP 標頭，以便在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體上識別現有的明確工作階段。|  
|[ProtocolCapabilities 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-headers/protocolcapabilities-element-xmla.md)|在 SOAP 要求訊息中使用 SOAP 標頭，以便識別 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體與用戶端應用程式之間的通訊協定功能。|  
  
## <a name="see-also"></a>另請參閱  
 [XML 項目 & #40;XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML 資料類型 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [XML 項目 & #40;XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
