---
title: "ADOMD.NET 用戶端功能 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- functionality [ADOMD.NET]
- ADOMD.NET, functionality
ms.assetid: 0f5e16a1-dc2d-4c87-8551-985921bf069b
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8010335c897b279ead050e34a25b2f2833d63021
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="adomdnet-client-functionality"></a>ADOMD.NET 用戶端功能
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]ADOMD.NET 中，如同其他[!INCLUDE[msCoName](../../includes/msconame-md.md)].NET Framework 資料提供者，可做為應用程式與資料來源之間的橋樑。 不過，ADOMD.NET 與其他 .NET Framework 資料提供者不同的是，ADOMD.NET 可處理分析資料。 為了處理分析資料，ADOMD.NET 支援與其他 .NET Framework 資料提供者非常不一樣的功能。 ADOMD.NET 不僅可讓您擷取資料，還可以擷取中繼資料並變更分析資料存放區的結構：  
  
 **擷取中繼資料**  
 應用程式可以進一步了解使用結構描述資料列集或是物件模型，透過中繼資料擷取從資料來源擷取的資料。 每個可用的關鍵效能指標 (KPI) 類型、在 Cube 中的維度以及採礦模型所需的參數等資訊全部都是可探索的。 中繼資料，是最重要*動態*需要使用者輸入，以決定要擷取類型、 深度和資料範圍的應用程式。 範例包括 Query Analyzer、Microsoft Excel 及其他查詢工具。 中繼資料是較不重要*靜態*執行一組預先定義的動作的應用程式。  
  
 如需詳細資訊：[從分析資料來源擷取的中繼資料](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)。  
  
 **擷取資料**  
 資料擷取是實際擷取儲存在資料來源中的資訊。 資料擷取是「靜態」應用程式的主要功能，這些應用程式知道資料來源的結構。 資料擷取也是「動態」應用程式的最終結果。 當天給定時間點上的 KPI 值、每家店前一個小時內所銷售的腳踏車數目，以及決定員工年度績效的因素，全部都是可以擷取的資料範例。 擷取資料對於任何查詢應用程式都是非常重要的。  
  
 如需詳細資訊：[從分析資料來源擷取的資料](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)。  
  
 **變更分析資料的結構**  
 ADOMD.NET 也可用以實際變更分析資料存放區的結構。 雖然這通常是透過「分析管理物件」(AMO) 物件模型來完成，不過，您可以使用 ADOMD.NET 傳送「Analysis Services 指令碼語言」(ASSL) 命令，來建立、修改或是刪除伺服器上的物件。  
  
 如需詳細資訊：[執行命令對分析資料來源](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md)，[使用分析管理物件 &#40; 開發AMO &#41;](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)， [analysis Services 指令碼語言 &#40;ASSL XMLA &#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)  
  
 擷取中繼資料、擷取資料以及變更資料結構，每個都發生在一般 ADOMD.NET 應用程式工作流程中的某個特定點。  
  
## <a name="typical-process-flow"></a>一般處理流程  
 傳統的 ADOMD.NET 應用程式通常會在處理分析資料庫時，遵循相同的工作流程。  
  
1.  首先，使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件，建立連至資料庫的連接。 當您開啟連接時，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件會公開您已連接之伺服器的中繼資料。 在動態應用程式中，通常會對使用者顯示這項資訊的某些部分，這樣使用者就可以做選擇，例如要查詢哪個 Cube。 應用程式可以多次重複使用在這個步驟期間建立的連接，以減少負擔。  
  
     如需詳細資訊： [Establishing Connections in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)  
  
2.  一旦建立連接，動態應用程式就會查詢伺服器，以取得更多特定的中繼資料。 若是靜態應用程式，程式設計人員會預先知道應用程式將查詢哪些物件，因此將不需要擷取此中繼資料。 應用程式與使用者可以在下一個步驟中使用已擷取的中繼資料。  
  
     如需詳細資訊：[從分析資料來源擷取的中繼資料](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
3.  應用程式接著會針對伺服器執行命令。 這個命令可能是為了擷取其他中繼資料、擷取資料或修改資料庫結構等目的。 對於這些工作的任何一個，應用程式都可以使用先前決定的查詢，或是利用新擷取的中繼資料以建立其他查詢。  
  
     如需詳細資訊：[從分析資料來源擷取的中繼資料](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)，[從分析資料來源擷取的資料](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)，[執行命令對分析資料來源](../../analysis-services/multidimensional-models-adomd-net-client/executing-commands-against-an-analytical-data-source.md)  
  
4.  一旦將命令傳送到伺服器，伺服器會開始將中繼資料或是資料傳回用戶端。 這項資訊可以使用檢視<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>物件<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>物件，或**System.XmlReader**物件。  
  
 為了說明這個傳統的工作流程，下列範例所含的方法會開啟資料庫的連接、針對已知的 Cube 執行命令，以及將結果擷取至資料格集。 資料格集接著會傳回含有資料行標頭、資料列標頭以及資料格資料的 Tab 鍵分隔字串。  
  
 [!code-cs[Adomd.NetClient#ReturnCommandUsingCellSet](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/adomd-net-client-functio_1.cs)]  
  
## <a name="see-also"></a>請參閱  
 [ADOMD.NET 用戶端程式設計](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
