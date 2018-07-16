---
title: 針對分析資料來源執行命令 |Microsoft Docs
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
- AdomdCommand object
- commands [ADOMD.NET]
- ADOMD.NET, commands
ms.assetid: 1a958e5f-fc18-480b-9706-fc44e3b1d534
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 36d94ba3ae75f2b3d59e0fb159ee639a5f2edb43
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202018"
---
# <a name="executing-commands-against-an-analytical-data-source"></a>針對分析資料來源執行命令
  建立分析資料來源的連接後，您可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 物件，針對該資料來源執行命令並從中傳回結果。 這些命令可以透過使用多維度運算式 (MDX)、資料採礦延伸模組 (DMX) 甚或是有限的 SQL 語法，來擷取資料。 此外，您可以使用 Analysis Services 指令碼語言 (ASSL) 命令修改基礎資料庫。  
  
## <a name="creating-a-command"></a>建立命令  
 在執行命令之前，您必須先建立它。 您可以使用以下兩種方法之一來建立命令：  
  
-   第一個方法是使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 建構函式，它會接受要在資料來源執行的命令以及執行命令所在的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 物件做為參數。  
  
-   第二個方法是使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.CreateCommand%2A> 物件的 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> 方法。  
  
 可以使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.CommandText%2A> 屬性來查詢和修改要執行的命令文字。 您建立的命令不必在執行之後傳回資料。  
  
## <a name="running-a-command"></a>執行命令  
 在建立 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 物件之後，您的命令可以使用數種 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> 方法以執行各種動作。 下表列出其中一些動作。  
  
|若要|使用這個方法|  
|--------|---------------------|  
|傳回結果做為資料流|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteReader%2A> 會傳回 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> 物件|  
|傳回 <xref:Microsoft.AnalysisServices.AdomdClient.CellSet> 物件|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteCellSet%2A>|  
|執行不會傳回資料列的命令|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteNonQuery%2A>|  
|傳回 `XMLReader` 物件，這個物件包含 XML for Analysis (XMLA) 相容格式的資料|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A>|  
  
### <a name="example-of-running-a-command"></a>執行命令的範例  
 此範例使用 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand> 執行 XMLA 命令，這個命令將會處理在本機伺服器上的 `Adventure Works DW` Cube，而不會傳回資料。  
  
 [!code-csharp[Adomd.NetClient#ExecuteXMLAProcessCommand](../../snippets/csharp/SQL14/adomd.net/adomd.netclient/cs/adomdexample.cs#executexmlaprocesscommand)]  
  
  
