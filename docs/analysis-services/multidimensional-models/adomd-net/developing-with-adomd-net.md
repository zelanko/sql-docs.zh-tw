---
title: "使用 ADOMD.NET 來開發 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ADOMD.NET
ms.assetid: abaf33aa-db55-43bf-8f30-15547559be1d
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9e0c9a2e2e2bc0b5900beeb65d4b80fdfc61fafb
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="developing-with-adomdnet"></a>使用 ADOMD.NET 來開發
  ADOMD.NET 是[!INCLUDE[msCoName](../../../includes/msconame-md.md)]設計來與通訊的.NET Framework 資料提供者[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 ADOMD.NET 使用 XML for Analysis 通訊協定，透過 TCP/IP 或 HTTP 連接傳輸和接收符合 XML for Analysis 規格的 SOAP 要求與回應，來和分析資料來源通訊。 命令可以用多維度運算式 (MDX)、資料採礦延伸模組 (MDX)、Analysis Services 指令碼語言 (ASSL)，或甚至是有限的 SQL 語法來傳送，而且可能不會傳回結果。 您可以透過使用 ADOMD.NET 物件模型來查詢和操作分析資料、關鍵效能指標 (KPI) 以及採礦模型。 透過使用 ADOMD.NET，您也可以擷取 OLE DB 符合的結構描述資料列集，或是使用 ADOMD.NET 物件模型，來檢視和使用中繼資料。  
  
 ADOMD.NET 資料提供者由**Microsoft.AnalysisServices.AdomdClient**命名空間。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|Description|  
|-----------|-----------------|  
|[ADOMD.NET 用戶端程式設計](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)|描述如何使用 ADOMD.NET 用戶端物件來從分析資料來源擷取資料和中繼資料。|  
|[ADOMD.NET 伺服器程式設計](../../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)|描述如何使用 ADOMD.NET 伺服器物件，建立預存程序及使用者定義函數。|  
|[轉散發 ADOMD.NET](../../../analysis-services/multidimensional-models/adomd-net/redistributing-adomd-net.md)|說明轉散發 ADOMD.NET 的程序。|  
|<xref:Microsoft.AnalysisServices.AdomdClient>|詳細資料中所包含的物件**Microsoft.AnalysisServices.AdomdClient**命名空間。|  
  
## <a name="see-also"></a>另請參閱  
 [多維度運算式 &#40;MDX &#41;參考](../../../mdx/multidimensional-expressions-mdx-reference.md)   
 [資料採礦延伸模組 &#40; DMX &#41;參考](../../../dmx/data-mining-extensions-dmx-reference.md)   
 [Analysis Services 結構描述資料列集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [開發使用 Analysis Services 指令碼語言 &#40;ASSL &#41;](../../../analysis-services/multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [多維度模型資料存取 &#40;Analysis Services-多維度資料 &#41;](../../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)  
  
  

