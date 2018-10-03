---
title: 從分析資料來源擷取資料 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- data retrieval [ADOMD.NET]
- retrieving data
- ADOMD.NET, data retrieval
- data retrieval [ADOMD.NET], about retrieving data
ms.assetid: 88358189-28aa-4bc7-8dda-5a92e3a012b8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0cfc0c783e8c61689d8f5b0ca3bab6ded39a57a4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48212378"
---
# <a name="retrieving-data-from-an-analytical-data-source"></a>從分析資料來源擷取資料
  一旦您建立連接和查詢，就可以擷取任何資料。 在 ADOMD.NET 中，您可以呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 物件的其中一個 `Execute` 方法，以使用三個不同的物件來擷取資料 (<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>、<xref:System.Xml.XmlReader> 和 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>)。  
  
 在這三個物件中，每個都可以平衡互動性和負擔：  
  
-   *互動性*指的是使用規定及透過物件模型提供的資訊數量。  
  
-   *額外負荷*參考的物件模型會透過網路連線到伺服器，也就是所需的物件模型中，以及與物件模型擷取資料的速度的記憶體數量產生的流量。  
  
 為了協助您選取最符合應用程式需求的資料擷取物件，下表會強調每個物件在互動性與負擔之間的差異。  
  
|Object|互動性|負擔|保留維度性|使用方式資訊|  
|------------|-------------------|--------------|----------------------------|-----------------------|  
|<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>|最高|中度高，也就導致資料擷取的速度變成最慢|是|[使用 CellSet 擷取資料](retrieving-data-using-the-cellset.md)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataAdapter>|中度|中度|否|[從 DataAdapter 填入 DataSet](http://go.microsoft.com/fwlink/?LinkId=70016)|  
|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>|中度|中度|否|[使用 AdomdDataReader 擷取資料](retrieving-data-using-the-adomddatareader.md)|  
|<xref:System.Xml.XmlReader>|最低|最低，也就導致資料擷取的速度變成最快|是|[使用 XmlReader 擷取資料](retrieving-data-using-the-xmlreader.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ADOMD.NET 用戶端程式設計](adomd-net-client-programming.md)  
  
  
