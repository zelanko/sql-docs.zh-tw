---
title: 使用 XmlReader 擷取資料 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2c8f4392b3cd37abb57ef2b7294e4b1ed223b27a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="retrieving-data-using-the-xmlreader"></a>使用 XmlReader 擷取資料
  **XmlReader**類別，一部分**System.Xml** Microsoft.NET Framework 類別庫的命名空間是類似於<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>類別， **XmlReader**類別也提供快速、 非快取、 順向的資料存取。 如果不需要取得資料使用的記憶體中的分析檢視<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>物件**XmlReader**物件也非常適合用以擷取 XML 資料，特別是針對大量資料。 因為**XmlReader**串流資料， **XmlReader**不必擷取和之前公開給呼叫端的資料快取的所有資料，因為可以則<xref:Microsoft.AnalysisServices.AdomdClient.CellSet>物件用來轉換XML for Analysis 回應的分析物件模型表示法。  
  
 **XmlReader**類別可直接存取 XML for Analysis 回應 ADOMD.NET 收到時<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A>方法<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>稱為物件。 因為擷取的資料是原始 XML，所以您必須手動剖析資料與中繼資料。 已擷取的資料，如**XmlReader**物件應該關閉。  
  
## <a name="retrieving-data-and-metadata"></a>擷取資料和中繼資料  
 若要使用**XmlReader**類別來擷取資料，請遵循下列步驟：  
  
1.  **建立物件的新執行個體。**  
  
     若要建立的新執行個體**XmlReader**的類別，呼叫<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A>或<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A>方法<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>物件。  
  
2.  **擷取資料。**  
  
     此命令會執行查詢並傳回之後**XmlReader**，您必須剖析資料和中繼資料。 XML 資料與中繼資料會以 XML for Analysis 提供者所使用的原生格式呈現。 對於大部分的 XML for Analysis 提供者，原生格式是**MDDataSet**格式。 **MDDataSet**格式提供資料和中繼資料之資料格集結構完善的格式。 如需有關**MDDataSet**格式，請參閱 XML for Analysis 規格。  
  
3.  **關閉讀取器。**  
  
     您應該一律呼叫<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A>方法，當您完成使用**XmlReader**物件。 雖然**XmlReader**是開啟的**XmlReader**會獨佔使用<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>用來執行命令的物件。 您無法執行使用的任何命令<xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>，包括建立其他**XmlReader**或<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>，除非您關閉原始**XmlReader**。  
  
### <a name="example-of-retrieving-data-from-the-xmlreader"></a>從 XmlReader 擷取資料的範例  
 下列範例會執行命令，並擷取資料做為**XmlReader**，輸出到主控台檔案的內容。  
  
 [!code-cs[Adomd.NetClient#OutputDataWithXML](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/retrieving-data-using-th_1_1.cs)]  
  
## <a name="see-also"></a>另請參閱  
 [從分析資料來源擷取資料](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)   
 [使用資料格集擷取資料](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-cellset.md)   
 [使用 AdomdDataReader 擷取資料](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-adomddatareader.md)  
  
  
