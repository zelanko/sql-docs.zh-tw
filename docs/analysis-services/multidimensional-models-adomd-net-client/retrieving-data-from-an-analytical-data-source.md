---
title: "從分析資料來源擷取資料 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- data retrieval [ADOMD.NET]
- retrieving data
- ADOMD.NET, data retrieval
- data retrieval [ADOMD.NET], about retrieving data
ms.assetid: 88358189-28aa-4bc7-8dda-5a92e3a012b8
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 473813a85d925bc98f914293ae075a7254597b6d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="retrieving-data-from-an-analytical-data-source"></a>從分析資料來源擷取資料
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]一旦您建立連線，並建立查詢，您可以擷取任何資料。 在 ADOMD.NET 中，您可以擷取使用三個不同物件的資料 (<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>， <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>，和<xref:System.Xml.XmlReader>) 透過呼叫其中一個**Execute**方法<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>物件。  
  
 在這三個物件中，每個都可以平衡互動性和負擔：  
  
-   *互動功能*指的使用性和可透過物件模型的資訊數量。  
  
-   *額外負荷*參考的物件模型會透過網路連線到伺服器時，物件模型中，以及與物件模型擷取資料的速度所需的記憶體數量產生的流量。  
  
 為了協助您選取最符合應用程式需求的資料擷取物件，下表會強調每個物件在互動性與負擔之間的差異。  
  
|Object|互動性|負擔|保留維度性|使用方式資訊|  
|------------|-------------------|--------------|----------------------------|-----------------------|  
|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>|最高|中度高，也就導致資料擷取的速度變成最慢|是|[使用 CellSet 擷取資料](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-cellset.md)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter>|中度|中度|否|[填入資料集從配接器](http://go.microsoft.com/fwlink/?LinkId=70016)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>|中度|中度|否|[使用 AdomdDataReader 擷取資料](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-adomddatareader.md)|  
|<xref:System.Xml.XmlReader>|最低|最低，也就導致資料擷取的速度變成最快|是|[使用 XmlReader 擷取資料](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-xmlreader.md)|  
  
## <a name="see-also"></a>請參閱  
 [ADOMD.NET 用戶端程式設計](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
