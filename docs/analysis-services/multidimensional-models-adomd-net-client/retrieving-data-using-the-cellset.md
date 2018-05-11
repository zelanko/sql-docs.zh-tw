---
title: 使用資料格集擷取資料 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9954141f2f4c69d42be879960ea183fc11d4e162
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="retrieving-data-using-the-cellset"></a>使用 CellSet 擷取資料
  當擷取分析資料時，<xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 物件可提供最大的互動性和彈性。 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 物件是階層式資料和中繼資料的記憶體中快取，其中保留了資料的原始維度性。 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 物件也可能以連接或中斷連接的狀態來周遊。 因為這個中斷連接的能力，<xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 物件可用來以任何順序檢視資料和中繼資料，並為資料擷取提供最完整的物件模型。 這個中斷連接的功能也會造成 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 物件有最大的負擔，並成為擴展最慢的 ADOMD.NET 資料擷取物件模型。  
  
## <a name="retrieving-data-in-a-connected-state"></a>在連接狀態下擷取資料  
 若要使用 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 物件擷取資料，請遵循以下步驟：  
  
1.  **建立物件的新執行個體。**  
  
     若要建立 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 物件的新執行個體，請呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 物件的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A> 或 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 方法。  
  
2.  **識別中繼資料。**  
  
     除了擷取資料之外，ADOMD.NET 也會為資料格集擷取中繼資料。 只要該命令已執行查詢且傳回 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>，您可以透過各種物件來擷取中繼資料。 當用戶端應用程式要顯示資料格集資料並與其互動時，就需要這個中繼資料。 例如，許多用戶端應用程式提供向下鑽研的功能，或是以階層方式顯示資料格集中指定位置的子系位置之功能。  
  
     在 ADOMD.NET 中，<xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Axes%2A> 物件的 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.FilterAxis%2A> 與 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 屬性，在傳回的資料格集中分別代表查詢與 Slicer 軸的中繼資料。 兩個屬性都會傳回 <xref:Microsoft.AnalysisServices.AdomdClient.Axis> 物件的參考，依序包含在每個軸上所代表的位置。  
  
     每個 <xref:Microsoft.AnalysisServices.AdomdClient.Axis> 物件都包含代表該軸可用 Tuple 集合的 <xref:Microsoft.AnalysisServices.AdomdClient.Position> 物件集合。 每個 <xref:Microsoft.AnalysisServices.AdomdClient.Position> 物件都代表單一 Tuple，其中包含一或多個由 <xref:Microsoft.AnalysisServices.AdomdClient.Member> 物件的集合所代表的成員。  
  
3.  **從資料格集集合中擷取資料。**  
  
     除了擷取中繼資料之外，ADOMD.NET 也會為資料格集擷取資料。 只要該命令已執行查詢並且傳回 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet>，您可以透過使用 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Cells%2A> 的 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 集合來擷取資料。 這個集合包含為查詢中所有軸的交集所計算的值。 因此，有幾個存取每個交集或是資料格的索引子。 如需索引子的清單，請參閱＜<xref:Microsoft.AnalysisServices.AdomdClient.CellCollection.Item%2A>＞。  
  
### <a name="example-of-retrieving-data-in-a-connected-state"></a>在連接狀態下擷取資料的範例  
 下列範例會建立本機伺服器的連接，然後在該連接上執行命令。 此範例會使用剖析結果**資料格集**物件模型： 第一個軸中，從擷取的資料行的標題 （中繼資料），並從第二個軸擷取每個資料列的標題 （中繼資料） 和交集的資料擷取使用<xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Cells%2A>集合。  
  
 [!code-cs[Adomd.NetClient#ReturnCommandUsingCellSet](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-data-using-th_0_1.cs)]  
  
## <a name="retrieving-data-in-a-disconnected-state"></a>在中斷連接狀態下擷取資料  
 透過載入從上一個查詢傳回的 XML，您可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 物件，提供瀏覽分析資料的完整方法，而不需要使用中的連接。  
  
> [!NOTE]  
>  並非 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 物件提供的所有物件屬性，都可以在中斷連接的狀態下使用。 如需詳細資訊，請參閱<xref:Microsoft.AnalysisServices.AdomdClient.CellSet.LoadXml%2A>。  
  
### <a name="example-of-retrieving-data-in-a-disconnected-state"></a>在中斷連接狀態下擷取資料的範例  
 下列範例類似於本主題稍早所示範的中繼資料與資料範例。 不過，在下列範例命令會執行呼叫<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A>，而且結果會當做傳回**System.Xml.XmlReader**。 此範例接著會填入<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>使用此物件**System.Xml.XmlReader**與<xref:Microsoft.AnalysisServices.AdomdClient.CellSet.LoadXml%2A>方法。 雖然這個範例會載入**System.Xml.XmlReader**立即，您可以快取的 XML 包含硬碟的讀取器，或該資料傳輸到不同的應用程式，透過任何方式載入資料之前資料格集。  
  
 [!code-cs[Adomd.NetClient#DemonstrateDisconnectedCellset](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-data-using-th_0_2.cs)]  
  
## <a name="see-also"></a>另請參閱  
 [從分析資料來源擷取資料](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)   
 [使用 AdomdDataReader 擷取資料](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-adomddatareader.md)   
 [使用 XmlReader 擷取資料](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-xmlreader.md)  
  
  
