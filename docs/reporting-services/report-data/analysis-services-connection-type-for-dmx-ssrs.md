---
title: "Analysis Services DMX (SSRS) 的連線類型 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameters [Reporting Services], DMX
- Data Mining Prediction [Reporting Services]
- query view [Reporting Services]
- DMX [Reporting Services]
- design view [Reporting Services]
- data mining [Reporting Services]
- passing parameters [Reporting Services]
ms.assetid: 2de825e9-6d8a-4128-add0-da15dc6cea3e
caps.latest.revision: 64
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e4cb050e8f838eaab2bc215005b167c0dea258fc
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="analysis-services-connection-type-for-dmx-ssrs"></a>Analysis Services Connection Type for DMX (SSRS)
  當您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源建立資料集時，報表設計師會在偵測到有效的 Cube 時顯示多維度運算式 (MDX) 查詢設計工具。 如果未偵測到任何 Cube，但是有提供資料採礦模型，報表設計師會顯示資料採礦延伸模組 (DMX) 查詢設計工具。 若要在 MDX 與 DMX 設計工具之間切換，請按一下**命令類型 DMX** (![變更為 DMX 查詢語言檢視](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.gif "變更為 DMX 查詢語言檢視")) 在工具列上的按鈕。 使用 DMX 查詢設計工具，透過圖形元素以互動方式建立 DMX 查詢。 若要使用 DMX 查詢設計工具，您指定的資料來源必須已經具有提供資料的資料採礦模型。 查詢結果會轉換成扁平化的資料列集，以提供報表使用。  
  
> [!NOTE]  
>  設計報表之前，您必須先培訓模型。 如需詳細資訊，請參閱 [資料採礦方案](../../analysis-services/data-mining/data-mining-solutions.md)。  
  
## <a name="design-mode"></a>設計模式  
 DMX 查詢設計工具會在設計模式中開啟。 設計模式包含一個用來選取單一資料採礦模型和輸入資料表的圖形設計介面，以及一個用來指定預測查詢的方格。 DMX 查詢設計工具中有另外兩種模式：查詢模式和結果模式。 在查詢模式中，會以 [查詢] 窗格取代設計模式中的方格，您可以利用這個窗格來輸入 DMX 查詢。 在 [結果] 模式中，查詢傳回的結果集會出現在資料方格中。  
  
 若要變更 DMX 查詢設計工具模式，以滑鼠右鍵按一下查詢設計介面，然後選取**設計**，**查詢**，或**結果**。 如需詳細資訊，請參閱[Analysis Services DMX Query Designer User Interface](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)和[從資料採礦模型 &#40; DMX &#41; &#40; 擷取資料SSRS &#41;](../../reporting-services/report-data/retrieve-data-from-a-data-mining-model-dmx-ssrs.md).  
  
## <a name="designing-a-prediction-query"></a>設計預測查詢  
 設計模式的 [查詢設計] 窗格包含兩個視窗： **[採礦模型]** 和 **[選取輸入資料表]**。 使用 **[採礦模型]** 視窗，即可選取要在查詢中使用的採礦模型。 使用 **[選取輸入資料表]** 視窗，即可選取要做為預測基礎的資料表。 如果您想要使用單一查詢，而不是輸入資料表，以滑鼠右鍵按一下查詢設計 窗格中，然後選取**單一查詢**。 就會將 **[選取輸入資料表]** 視窗取代成 **[單一查詢輸入]** 視窗。  
  
 在設計模式中，將 **[採礦模型]** 和 **[選取輸入資料表]** 視窗中的欄位拖曳至 [方格] 窗格中的 **[欄位]** 資料行。 您也可以填入其餘資料行，以便指定別名、在結果中顯示欄位、將欄位群組在一起，以及指定運算子來將欄位值限制為給定的準則或引數。 如果您在 [查詢] 模式中，請將欄位拖曳到 [查詢] 窗格來建立 DMX 查詢。  
  
## <a name="using-parameters"></a>使用參數  
 您可以將報表參數傳遞至 DMX 查詢參數。 若要這樣做，您必須將參數加入您的 DMX 查詢中，在 **[查詢參數]** 對話方塊中定義查詢參數，然後修改相關聯的報表參數。 若要定義查詢參數，請按一下**查詢參數**(![查詢參數 對話方塊的圖示](../../reporting-services/report-data/media/iconqueryparameter.gif "查詢參數 對話方塊的圖示")) 在工具列上的按鈕。 若要檢視 DMX 查詢中定義參數的相關指示，請參閱[在 Analysis Services 的 MDX 查詢設計工具中定義參數 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/define-parameters-in-the-mdx-query-designer-for-analysis-services.md)。  
  
 如需如何管理報表參數與查詢參數之間的關聯性的詳細資訊，請參閱[將查詢參數與報表參數 &#40; 產生關聯報表產生器及 SSRS &#41;](../../reporting-services/report-data/associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs.md). 如需參數的詳細資訊，請參閱[報表參數 &#40;報表產生器和報表設計工具 &#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦方案](../../analysis-services/data-mining/data-mining-solutions.md)   
 [查詢設計工具 &#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md)   
 [資料連接、資料來源及連接字串 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  

