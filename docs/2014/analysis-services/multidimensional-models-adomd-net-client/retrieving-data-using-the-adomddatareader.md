---
title: 使用 AdomdDataReader 擷取資料 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
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
- AdomdDataReader object
- data retrieval [ADOMD.NET], AdomdDataReader object
ms.assetid: 8ed7ea26-b5f8-4852-80fc-75dd62df5b3a
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5631238b78804bb593e8db90f910aec0ddebb933
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321228"
---
# <a name="retrieving-data-using-the-adomddatareader"></a>使用 AdomdDataReader 擷取資料
  擷取分析資料時，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 物件可提供負擔與互動性的良好平衡。 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 物件會從分析資料來源擷取唯讀、順向且扁平化的資料流。 這個未緩衝的資料流可讓程序邏輯有效且循序地處理來自分析資料來源的結果。 當擷取大量資料以供顯示之用時，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 是不錯的選擇，因為資料不會快取至記憶體。  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 也可以增加應用程式效能，方法是一旦資料變成可用時便擷取它，而不是等待傳回查詢的完整結果。 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 也可降低系統負擔，因為依預設，這個讀取器在記憶體中一次只會儲存一個資料列。  
  
 最佳化效能的權衡取捨在於 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 物件所提供的擷取資料資訊比其他資料擷取方法少。 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 物件並不支援代表資料或是中繼資料的大型物件模型，這個物件模型也不允許像資料格回寫等較複雜的分析功能。 不過，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 物件確實提供一組強型別方法以擷取資料格集資料，以及一個擷取表格式格式之資料格集中繼資料的方法。 此外，<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>會實作**IDbDataReader**介面，可以支援資料繫結，以及使用擷取的資料`SelectCommand`方法，從**System.Data**的命名空間Microsoft.NET Framework 類別庫。  
  
## <a name="retrieving-data-from-the-adomddatareader"></a>從 AdomdDataReader 擷取資料  
 若要使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 物件擷取資料，請遵循以下步驟：  
  
1.  **建立物件的新執行個體。**  
  
     若要建立 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 類別的新執行個體，請呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 物件的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteReader%2A> 或 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 方法。  
  
2.  **擷取資料。**  
  
     在命令執行查詢時，ADOMD.NET 會傳回 `Resultset` 格式的結果，這是 XML for Analysis 規格中所述的表格式格式，用以扁平化 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 物件的資料。 就分析資料中的可變維度性而論，表格式格式並不常見於查詢分析資料。  
  
     除非您使用下列其中一個方法來要求這些表格式結果，否則 ADOMD.NET 會將它們一直儲存在用戶端的網路緩衝區中：  
  
    -   呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.Read%2A> 物件的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 方法。  
  
         <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.Read%2A> 方法可從查詢結果取得資料列。 您可以將資料行的名稱或序數參考傳遞給 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.Item%2A> 屬性，以存取傳回之資料列的每個資料行。 例如，在目前資料列中的第一個資料行名為 ColumnName。 然後 `reader[0].ToString()` 或 `reader["ColumnName"].ToString()` 將傳回目前資料列中第一個資料行的內容。  
  
    -   呼叫其中一個類型存取子方法。  
  
         <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 提供一系列類型存取子方法，這些方法可讓您存取其原生資料類型的資料行值。 當您知道資料行值的基礎資料類型時，類型存取子方法可減少擷取資料行值時所需的類型轉換量，也因此可提供最高的效能。  
  
         有些可用的類型存取子方法包括 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetDateTime%2A>、<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetDouble%2A> 和 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetInt32%2A>。 如需類型存取子方法的完整清單，請參閱＜<xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>＞。  
  
3.  **關閉讀取器。**  
  
     完成使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.Close%2A> 物件後，務必呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 方法。 當 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 物件的執行個體處於開啟狀態，該 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 會以獨佔方式使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>。 您將無法在 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 的執行個體上執行任何命令，包括建立其他的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 或是 `System.Xml.XmlReader`，除非您關閉原始 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>。  
  
### <a name="example-of-retrieving-data-from-the-adomddatareader"></a>從 AdomdDataReader 擷取資料的範例  
 下列程式碼範例會在 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 物件中反覆運算，並從每個資料列傳回前兩個字串值。  
  
```vb  
If Reader.HasRows Then  
    Do While objReader.Read()  
        Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _  
            objReader.GetString(0), objReader.GetString(1))  
    Loop  
Else  
  Console.WriteLine("No rows returned.")  
End If  
  
objReader.Close()  
```  
  
```csharp  
if (objReader.HasRows)  
  while (objReader.Read())  
    Console.WriteLine("\t{0}\t{1}", _  
        objReader.GetString(0), objReader.GetString(1));  
else  
  Console.WriteLine("No rows returned.");  
  
objReader.Close();  
```  
  
## <a name="retrieving-metadata-from-the-adomddatareader"></a>從 AdomdDataReader 擷取中繼資料  
 當 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 物件的執行個體處於開啟狀態時，您可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetSchemaTable%2A> 方法擷取有關目前資料錄集的結構描述資訊或中繼資料。 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetSchemaTable%2A>傳回`DataTable`會填入目前資料錄集的結構描述資訊的物件。 `DataTable` 將會為資料錄集的每個資料行包含一個資料列。 結構描述資料表資料列的每個資料行會對應至資料格集內所傳回的資料行屬性，其中 `ColumnName` 是屬性名稱，而資料行值就是屬性的值。  
  
### <a name="example-of-retrieving-metadata-from-the-adomddatareader"></a>從 AdomdDataReader 擷取中繼資料的範例  
 下列程式碼範例會寫出 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 物件的結構描述資訊。  
  
```vb  
Dim schemaTable As DataTable = objReader.GetSchemaTable()  
  
Dim objRow As DataRow  
Dim objColumn As DataColumn  
  
For Each objRow In schemaTable.Rows  
  For Each objColumn In schemaTable.Columns  
    Console.WriteLine(objColumn.ColumnName & " = " & objRow(objColumn).ToString())  
  Next  
  Console.WriteLine()  
Next  
DataTable schemaTable = objReader.GetSchemaTable();  
```  
  
```csharp  
foreach (DataRow objRow in schemaTable.Rows)  
{  
  foreach (DataColumn objColumn in schemaTable.Columns)  
    Console.WriteLine(objColumn.ColumnName + " = " + objRow[objColumn]);  
  Console.WriteLine();  
}  
```  
  
## <a name="retrieving-multiple-result-sets"></a>擷取多個結果集  
 資料採礦支援巢狀資料表的概念，ADOMD.NET 會公開成巢狀資料列集。 若要擷取與每個資料列關聯的巢狀資料列集，可以呼叫 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetDataReader%2A> 方法。  
  
## <a name="see-also"></a>另請參閱  
 [從分析資料來源擷取資料](retrieving-data-from-an-analytical-data-source.md)   
 [使用 CellSet 擷取資料](retrieving-data-using-the-cellset.md)   
 [使用 XmlReader 擷取資料](retrieving-data-using-the-xmlreader.md)  
  
  
