---
title: "對分析資料來源執行命令 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- AdomdCommand object
- commands [ADOMD.NET]
- ADOMD.NET, commands
ms.assetid: 1a958e5f-fc18-480b-9706-fc44e3b1d534
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 450d3553509ee3358711705bbc3f5e8a10874820
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
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
|傳回**XMLReader**物件，其中包含 XML for Analysis (XMLA) 相容的格式中的資料|<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteXmlReader%2A>|  
  
### <a name="example-of-running-a-command"></a>執行命令的範例  
 這個範例會使用<xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>執行 XMLA 命令，將會處理**Adventure Works DW**在本機伺服器上，而不傳回資料的 cube。  
  
 [!code-cs[Adomd.NetClient#ExecuteXMLAProcessCommand](../../analysis-services/multidimensional-models-adomd-net-client/codesnippet/csharp/executing-commands-again_1.cs)]  
  
  
