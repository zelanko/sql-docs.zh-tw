---
title: "使用 ADOMD.NET 物件模型 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
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
- metadata [ADOMD.NET]
- object model (client) [ADOMD.NET]
- retrieving metadata
ms.assetid: 0183dcdc-f2ea-4246-ad00-6e8ccc9d8217
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 81a9272284e662eb7f5f47e464e85e324b92a39d
ms.contentlocale: zh-tw
ms.lasthandoff: 10/24/2017

---
# <a name="retrieving-metadata---working-with-adomdnet-object-model"></a>擷取中繼資料-使用 ADOMD.NET 物件模型
  ADOMD.NET 提供的物件模型，可檢視分析資料來源所包含的 Cube 與從屬物件。 不過，並非指定的分析資料來源之所有中繼資料，都可透過物件模型取得。 物件模型只能存取對用戶端應用程式而言最為實用並加以顯示的資訊，以允許使用者以互動方式建構命令。 因為要顯示的中繼資料之複雜性已降低，所以 ADOMD.NET 物件模型使用起來較容易。  
  
 在 ADOMD.NET 物件模型中，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件可存取定義在分析資料來源中的線上分析處理 (OLAP) Cube 與採礦模型的相關資訊，以及維度、命名集和採礦演算法等相關物件。  
  
## <a name="retrieving-olap-metadata"></a>擷取 OLAP 中繼資料  
 每個 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件都有 <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> 物件的集合，代表可供使用者或應用程式使用的 Cube。 <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> 物件會公開有關 Cube 的資訊，以及各種與 Cube 相關的物件，例如維度、關鍵效能指標、量值、命名集等等。  
  
 對於一般的中繼資料顯示與存取目的而言，或是在支援多個 OLAP 伺服器的用戶端應用程式中，您應該盡可能地使用 <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> 物件來代表其中的中繼資料。  
  
> [!NOTE]  
>  對於提供者特定的中繼資料，或是詳細的中繼資料顯示與存取，請使用結構描述資料列集來擷取中繼資料。 如需詳細資訊，請參閱 [Working with Schema Rowsets in ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下列範例使用 <xref:Microsoft.AnalysisServices.AdomdClient.CubeDef> 物件從本機伺服器擷取可見的 Cube 及其維度：  
  
 [!code-cs[Adomd.NetClient#RetrieveCubesAndDimensions](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-metadata-work_1_1.cs)]  
  
## <a name="retrieving-data-mining-metadata"></a>擷取資料採礦中繼資料  
 每個 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件都有數個集合，以提供資料來源的資料採礦功能之相關資訊：  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelCollection> 包含資料來源中所有採礦模型的清單。  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningServiceCollection> 會提供可用之採礦演算法的相關資訊。  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.MiningStructureCollection> 會公開伺服器上採礦結構的相關資訊。  
  
 若要判斷如何針對伺服器上的採礦模型進行查詢，請在 <xref:Microsoft.AnalysisServices.AdomdServer.MiningModel.Columns%2A> 集合中反覆運算。 每個 <xref:Microsoft.AnalysisServices.AdomdClient.MiningModelColumn> 物件會公開下列特性：  
  
-   物件是否為輸入資料行 (<xref:Microsoft.AnalysisServices.AdomdClient.MiningModelColumn.IsInput%2A>)。  
  
-   物件是否為預測資料行 (<xref:Microsoft.AnalysisServices.AdomdClient.MiningModelColumn.IsPredictable%2A>)。  
  
-   與離散資料行關聯的值 (<xref:Microsoft.AnalysisServices.AdomdClient.MiningModelColumn.Values%2A>)。  
  
-   資料行中的資料類型 (<xref:Microsoft.AnalysisServices.AdomdClient.MiningModelColumn.Type%2A>)。  
  
## <a name="see-also"></a>另請參閱  
 [從分析資料來源擷取中繼資料](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
  

