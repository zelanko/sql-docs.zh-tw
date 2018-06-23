---
title: 使用資料格集擷取資料 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- CellSet object
- retrieving data
- data retrieval [ADOMD.NET], CellSet object
ms.assetid: 77e4ee58-882d-4012-91a3-0565f18a4882
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cda35dc6151d17e1dad2d341337d67ef39d9f839
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035101"
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
 下列範例會建立本機伺服器的連接，然後在該連接上執行命令。 範例會使用 `CellSet` 物件模型來剖析結果：從第一個軸擷取資料行標題 (中繼資料)、從第二個軸擷取每個資料列的標題 (中繼資料)，並使用 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.Cells%2A> 集合擷取交叉資料。  
  
 [!code-csharp[Adomd.NetClient#ReturnCommandUsingCellSet](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#returncommandusingcellset)]  
  
## <a name="retrieving-data-in-a-disconnected-state"></a>在中斷連接狀態下擷取資料  
 透過載入從上一個查詢傳回的 XML，您可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 物件，提供瀏覽分析資料的完整方法，而不需要使用中的連接。  
  
> [!NOTE]  
>  並非 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 物件提供的所有物件屬性，都可以在中斷連接的狀態下使用。 如需詳細資訊，請參閱<xref:Microsoft.AnalysisServices.AdomdClient.CellSet.LoadXml%2A>。  
  
### <a name="example-of-retrieving-data-in-a-disconnected-state"></a>在中斷連接狀態下擷取資料的範例  
 下列範例類似於本主題稍早所示範的中繼資料與資料範例。 不過，下列範例中的命令在執行時會呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A>，而且結果會以 `System.Xml.XmlReader` 傳回。 此範例接著會使用這個 `System.Xml.XmlReader` 加上 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 方法來擴展 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet.LoadXml%2A> 物件。 雖然這個範例會立即載入 `System.Xml.XmlReader`，不過，您可以將讀取器所含的 XML 快取到硬碟，或是在將資料載入到資料格集之前，先透過任何方式將該資料傳輸到不同的應用程式。  
  
 [!code-csharp[Adomd.NetClient#DemonstrateDisconnectedCellset](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#demonstratedisconnectedcellset)]  
  
## <a name="see-also"></a>另請參閱  
 [從分析資料來源擷取資料](retrieving-data-from-an-analytical-data-source.md)   
 [使用 AdomdDataReader 擷取資料](retrieving-data-using-the-adomddatareader.md)   
 [使用 XmlReader 擷取資料](retrieving-data-using-the-xmlreader.md)  
  
  