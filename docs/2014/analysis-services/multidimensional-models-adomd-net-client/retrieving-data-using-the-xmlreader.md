---
title: 使用 XmlReader 擷取資料 |Microsoft 文件
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
- retrieving data
- XmlReader object
- data retrieval [ADOMD.NET], XmlReader object
ms.assetid: 420ec40e-be2d-413a-b4b2-6d2b1756e270
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 257777c40c829921680b8fce333bd6e44f6f57fd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032891"
---
# <a name="retrieving-data-using-the-xmlreader"></a>使用 XmlReader 擷取資料
  屬於 Microsoft .NET Framework 類別庫的 `XmlReader` 命名空間的 `System.Xml` 類別，類似於 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 類別，因為 `XmlReader` 類別也可以用快速、非快取且順向的方式存取資料。 如果不需要使用 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 物件，對資料進行記憶體中的分析檢視，`XmlReader` 物件也非常適合用以擷取 XML 資料，特別是大量的資料。 因為 `XmlReader` 會串流資料，所以`XmlReader` 不必擷取和快取所有的資料，即可向呼叫端公開資料，如果 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 物件是用來將 XML for Analysis 回應轉換為分析物件模型表示，也是如此。  
  
 當呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> 物件的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 方法時，`XmlReader` 類別可以直接存取 ADOMD.NET 收到的 XML for Analysis 回應。 因為擷取的資料是原始 XML，所以您必須手動剖析資料與中繼資料。 在擷取資料之後，應該立即關閉 `XmlReader` 物件。  
  
## <a name="retrieving-data-and-metadata"></a>擷取資料和中繼資料  
 若要使用 `XmlReader` 類別擷取資料，請遵循以下步驟：  
  
1.  **建立物件的新執行個體。**  
  
     若要建立 `XmlReader` 類別的新執行個體，請呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 物件的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A> 或 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 方法。  
  
2.  **擷取資料。**  
  
     在命令執行查詢和傳回 `XmlReader` 之後，您必須剖析資料和中繼資料。 XML 資料與中繼資料會以 XML for Analysis 提供者所使用的原生格式呈現。 對於大部分的 XML for Analysis 提供者，原生格式是 `MDDataSet` 格式。 `MDDataSet` 格式以結構良好的格式提供資料格集的資料與中繼資料。 如需有關 `MDDataSet` 格式的詳細資訊，請參閱 XML for Analysis 規格。  
  
3.  **關閉讀取器。**  
  
     完成使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.Close%2A> 物件後，務必呼叫 `XmlReader` 方法。 當 `XmlReader` 處於開啟狀態時，該 `XmlReader` 對於用以執行命令的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件具有獨佔使用權。 在您關閉原始 `XmlReader` 之前，您將無法執行任何使用該 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 的命令，包括建立其他的 `XmlReader` 或 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>。  
  
### <a name="example-of-retrieving-data-from-the-xmlreader"></a>從 XmlReader 擷取資料的範例  
 下列範例會執行命令並將資料擷取成 `XmlReader`，以便將檔案內容輸出到主控台。  
  
 [!code-csharp[Adomd.NetClient#OutputDataWithXML](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#outputdatawithxml)]  
  
## <a name="see-also"></a>另請參閱  
 [從分析資料來源擷取資料](retrieving-data-from-an-analytical-data-source.md)   
 [使用資料格集擷取資料](retrieving-data-using-the-cellset.md)   
 [使用 AdomdDataReader 擷取資料](retrieving-data-using-the-adomddatareader.md)  
  
  