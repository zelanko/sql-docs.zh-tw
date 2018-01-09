---
title: "程式設計 AMO 資料採礦物件 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- programming [AMO]
- data mining [AMO]
- AMO, data mining
- Analysis Management Objects, data mining
ms.assetid: d27f58b9-91be-449c-8403-439aa6dd1ff9
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 19f72f294bc06ecec0e38be763afb656f7ebcc67
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="programming-amo-data-mining-objects"></a>設計 AMO 資料採礦物件的程式
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]藉由使用 AMO 設計資料採礦物件既簡單又直接。 第一個步驟是建立資料結構模型以支援採礦專案。 接著建立足以支援您要使用之採礦演算法的資料採礦模型，這是為了預測或是尋找隱藏在資料之下無法察覺的關係。 採礦專案建立完成後 (包括結構與演算法)，您就可以處理採礦模型並取得定型模型，以便稍後在從用戶端應用程式查詢和預測時可以使用。  
  
 有一件事請記住，AMO 並不是用於查詢，而是用於管理您的採礦結構與模型。 若要查詢您的資料，請使用[使用 ADOMD.NET 來開發](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md)。  
  
 本主題包含下列幾節：  
  
-   [MiningStructure 物件](#MiningStructure)  
  
-   [MiningModel 物件](#MiningModel)  
  
##  <a name="MiningStructure"></a>MiningStructure 物件  
 採礦結構是用以建立所有採礦模型的資料結構定義。 採礦結構包含在資料庫中定義的資料來源檢視繫結，並且包含所有參與採礦模型的資料行定義。 一個採礦結構可以包含一個以上的採礦模型。  
  
 建立 <xref:Microsoft.AnalysisServices.MiningStructure> 物件需要下列步驟：  
  
1.  建立 <xref:Microsoft.AnalysisServices.MiningStructure> 物件並擴展基本屬性。 基本屬性包括物件名稱、物件識別碼 (內部識別碼) 以及資料來源繫結。  
  
2.  建立模型的資料行。 資料行可以是純量或資料表定義。  
  
     每個資料行都需要名稱與內部識別碼、類型、內容定義以及繫結。  
  
3.  透過使用物件的 Update 方法，將 <xref:Microsoft.AnalysisServices.MiningStructure> 物件更新到伺服器。  
  
     採礦結構可加以處理，而且在處理採礦結構時，也會處理或是重塑其子系採礦模型。  
  
 下列範例程式碼會建立採礦結構以預測時間序列中的銷售額。 在執行之前的範例程式碼，請確定資料庫*db*，做為參數傳遞`CreateSalesForecastingMiningStructure`，包含在`db.DataSourceViews[0]`檢視的參照*dbo.vTimeSeries*中[!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)]範例資料庫。  
  
```  
public static MiningStructure CreateSalesForecastingMiningStructure(Database db)  
{  
    MiningStructure ms = db.MiningStructures.FindByName("Forecasting Sales Structure");  
    if (ms != null)  
        ms.Drop();  
    ms = db.MiningStructures.Add("Forecasting Sales Structure", "Forecasting Sales Structure");  
    ms.Source = new DataSourceViewBinding(db.DataSourceViews[0].ID);  
  
    ScalarMiningStructureColumn amount = ms.Columns.Add("Amount", "Amount");  
    amount.Type = MiningStructureColumnTypes.Double;  
    amount.Content = MiningStructureColumnContents.Continuous;  
    amount.KeyColumns.Add("vTimeSeries", "Amount", OleDbType.Currency);  
  
    ScalarMiningStructureColumn modelRegion = ms.Columns.Add("Model Region", "Model Region");  
    modelRegion.IsKey = true;  
    modelRegion.Type = MiningStructureColumnTypes.Text;  
    modelRegion.Content = MiningStructureColumnContents.Key;  
    modelRegion.KeyColumns.Add("vTimeSeries", "ModelRegion", OleDbType.WChar, 56);  
  
    ScalarMiningStructureColumn qty = ms.Columns.Add("Quantity", "Quantity");  
    qty.Type = MiningStructureColumnTypes.Long;  
    qty.Content = MiningStructureColumnContents.Continuous;  
    qty.KeyColumns.Add("vTimeSeries", "Quantity", OleDbType.Integer);  
  
    ScalarMiningStructureColumn timeIndex = ms.Columns.Add("TimeIndex", "TimeIndex");  
    timeIndex.IsKey = true;  
    timeIndex.Type = MiningStructureColumnTypes.Long;  
    timeIndex.Content = MiningStructureColumnContents.KeyTime;  
    timeIndex.KeyColumns.Add("vTimeSeries", "TimeIndex", OleDbType.Integer);  
  
    ms.Update();  
    return ms;  
}  
```  
  
##  <a name="MiningModel"></a>MiningModel 物件  
 採礦模式是一個儲存機制，其中包含所有資料行以及將用於採礦演算法中的資料行定義。  
  
 建立 <xref:Microsoft.AnalysisServices.MiningModel> 物件需要下列步驟：  
  
1.  建立 <xref:Microsoft.AnalysisServices.MiningModel> 物件並擴展基本屬性。  
  
     基本屬性包括物件名稱、物件識別碼 (內部識別碼) 以及採礦演算法規格。  
  
2.  加入採礦模型的資料行。 必須將其中一個資料行定義為案例索引鍵。  
  
3.  透過使用物件的 Update 方法，將 <xref:Microsoft.AnalysisServices.MiningModel> 物件更新到伺服器。  
  
     <xref:Microsoft.AnalysisServices.MiningModel> 物件可以獨立於父 <xref:Microsoft.AnalysisServices.MiningStructure> 中的其他模型，單獨進行處理。  
  
 下列範例程式碼會根據 "Forecasting Sales Structure" 採礦結構來建立 Microsoft 時間序列預測模型。  
  
```  
public static MiningModel CreateSalesForecastingMiningModel(MiningStructure ms)  
{  
    if (ms.MiningModels.ContainsName("Sales Forecasting Model"))  
    {  
        ms.MiningModels["Sales Forecasting Model"].Drop();  
    }  
    MiningModel mm = ms.CreateMiningModel(true, "Sales Forecasting Model");  
    mm.Algorithm = MiningModelAlgorithms.MicrosoftTimeSeries;  
    mm.AlgorithmParameters.Add("PERIODICITY_HINT", "{12}");  
  
    MiningModelColumn amount = new MiningModelColumn();  
    amount.SourceColumnID = "Amount";  
    amount.Usage = MiningModelColumnUsages.Predict;  
  
    MiningModelColumn modelRegion = new MiningModelColumn();  
    modelRegion.SourceColumnID = "Model Region";  
    modelRegion.Usage = MiningModelColumnUsages.Key;  
  
    MiningModelColumn qty = new MiningModelColumn();  
    qty.SourceColumnID = "Quantity";  
    qty.Usage = MiningModelColumnUsages.Predict;  
  
    MiningModelColumn ti = new MiningModelColumn();  
    ti.SourceColumnID = "TimeIndex";  
    ti.Usage = MiningModelColumnUsages.Key;  
  
    mm.Update();  
    mm.Process(ProcessType.ProcessFull);  
    return mm;  
}  
```  
  
## <a name="see-also"></a>請參閱  
 <xref:Microsoft.AnalysisServices>   
 [AMO 基礎類別](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)   
 [AMO 類別簡介](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [AMO 資料採礦類別](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-data-mining-classes.md)   
 [邏輯架構 &#40;Analysis Services-多維度資料 &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [資料庫物件 &#40;Analysis Services-多維度資料 &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
