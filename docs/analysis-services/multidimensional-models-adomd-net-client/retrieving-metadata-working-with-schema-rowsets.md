---
title: Working with Schema Rowsets in ADOMD.NET |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bf3cc03d9f3b1fba2a88e7bdf3468bc0314dd9fd
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="retrieving-metadata---working-with-schema-rowsets"></a>擷取中繼資料-使用 結構描述資料列集
  當您需要的中繼資料比 ADOMD.NET 物件模型所提供的還要多時，ADOMD.NET 提供的功能，可擷取完整範圍的 XML for Analysis (XMLA)、OLE DB、OLE DB for OLAP 以及 OLE DB for Data Mining 結構描述資料列集：  
  
 **XML for Analysis 中繼資料**  
 XML for Analysis 結構描述資料列集提供擷取有關伺服器低階資訊的方法。 可用的資訊包括伺服器上可用的資料來源、提供者保留的關鍵字、提供者支援的常值等等。 您甚至可以使用 XML for Analysis 結構描述資料列集，以探索提供者支援的所有結構描述資料列集。  
  
 如需詳細資訊： [XML for Analysis 結構描述資料列集](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
 **OLE DB 中繼資料**  
 OLE DB 結構描述資料列集提供業界標準方法，可從各種提供者擷取資訊。  
  
 如需詳細資訊： [OLE DB 結構描述資料列集](../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
 **OLAP 中繼資料**  
 提供給分析資料來源的結構描述資訊，包括分析資料來源中可用的資料庫或是目錄、在資料庫中的 Cube 與採礦模型、在資料來源的 Cube 所存在的角色等等。  
  
 如需詳細資訊： [OLE DB for OLAP 結構描述資料列集](../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
 **資料採礦中繼資料**  
 除了 OLAP 中繼資料之外，還可以使用結構描述資料列集來擷取資料採礦中繼資料。 可用的資料列集會公開資料庫中可用的資料採礦模型、可用的採礦演算法、演算法所需的參數、採礦結構等相關資訊。  
  
 如需詳細資訊：[資料採礦結構描述資料列集](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
 對於這些不同的結構描述資料列集，您可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A> 物件的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 方法傳遞 GUID 或 XMLA 名稱，以從資料列集擷取中繼資料。  
  
## <a name="retrieving-metadata-by-passing-guids"></a>透過傳遞 GUID 擷取中繼資料  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid> 類別包含的欄位清單，代表提供者與分析資料來源最常支援的結構描述資料列集。 若要從提供者或分析資料來源擷取一般和提供者特定的中繼資料，可以透過下列其中一個方法，來使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdSchemaGuid> 物件中所含的 GUID：  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
> [!NOTE]  
>  ADOMD.NET 資料提供者透過特定提供者與分析資料來源所提供的功能，來公開結構描述資訊。 每個提供者與資料來源可能會提供不同的中繼資料。  
  
## <a name="retrieving-metadata-by-passing-xmla-names"></a>透過傳遞 XMLA 名稱以擷取中繼資料  
 下列方法將 XMLA 結構描述名稱當成引數，該名稱識別要傳回的結構描述資訊以及對那些傳回之資料行的限制陣列。  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
-   <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
 每一種方法傳回的執行個體**資料集**結構描述資訊擴展的物件。 **資料集**物件是來自**System.Data** Microsoft.NET Framework 類別庫的命名空間。  
  
## <a name="example"></a>範例  
 在下列範例中，GetActions 函數會採用連接、 cube 名稱、 座標和座標類型，會擷取[MDSCHEMA_ACTIONS 資料列集](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-actions-rowset.md)，並傳回選取座標上可用的動作。  
  
 [!code-cs[Adomd.NetClient#GetActions](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-metadata-work_0_1.cs)]  
  
## <a name="see-also"></a>另請參閱  
 [從分析資料來源擷取中繼資料](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
  
