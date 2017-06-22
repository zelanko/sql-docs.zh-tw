---
title: "Analysis Services DMX 查詢設計工具使用者介面 |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10012"
- sql13.rtp.rptdesigner.dataview.asquerydesigner.f1
helpviewer_keywords:
- Analysis Services [DMX]
- DMX [Analysis Services], user interface
- query designers [DMX]
ms.assetid: 5fd726a4-aed7-4e6c-9404-ccb2db66cf26
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8787272709b10a8b4d19105eb7560f1c82bd9b21
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="analysis-services-dmx-query-designer-user-interface"></a>Analysis Services DMX 查詢設計工具使用者介面
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 提供了圖形化查詢設計工具，可用來建立 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源的資料採礦運算式 (DMX) 查詢和多維度運算式 (MDX) 查詢。 此主題即描述 DMX 查詢設計工具。 如需 MDX 查詢設計工具的詳細資訊，請參閱 [Analysis Services MDX 查詢設計工具使用者介面](../../reporting-services/report-data/analysis-services-mdx-query-designer-user-interface.md)。  
  
 DMX 圖形化查詢設計工具有三種模式：「設計」、「查詢」和「結果」。 若要切換模式，請以滑鼠右鍵按一下 [查詢設計工具] 窗格並選取模式。 每一種模式都會提供 [中繼資料] 窗格，您可以在這個窗格中，從選取的 Cube 中拖曳成員，以建立 DMX 查詢，在處理報表時為資料集擷取資料。  
  
## <a name="graphical-dmx-query-designer-toolbar"></a>圖形化 DMX 查詢設計工具工具列  
 查詢設計工具工具列會提供按鈕，協助您使用圖形化介面設計 DMX 查詢。 下表描述這些按鈕及其功能。  
  
|按鈕|說明|  
|------------|-----------------|  
|**當成文字編輯**|這種資料來源類型已停用此選項。|  
|**匯入**|從檔案系統上的報表定義 (.rdl) 檔案匯入現有的查詢。 如需詳細資訊，請參閱 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。|  
|![變更為 MDX 查詢檢視](../../reporting-services/report-data/media/rsqdicon-commandtypemdx.gif "變更為 MDX 查詢檢視")|切換到 MDX 查詢設計工具模式。|  
|![變更為 DMX 查詢語言檢視](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.gif "變更為 DMX 查詢語言檢視")|切換到 DMX 查詢設計工具模式。|  
|![重新整理結果資料](../../reporting-services/report-data/media/rsqdicon-refresh.gif "重新整理結果資料")|重新整理資料來源中的中繼資料。|  
|![刪除](../../reporting-services/report-data/media/rsqdicon-delete.gif "刪除")|從查詢中刪除 [資料] 窗格中選取的資料行。|  
|![查詢參數 對話方塊的圖示](../../reporting-services/report-data/media/iconqueryparameter.gif "查詢參數 對話方塊的圖示")|顯示 **[查詢參數]** 對話方塊。 當您指派預設值給變數時，就會在您切換到 [報表設計師] 中的 [配置] 檢視時建立對應的報表參數。|  
|![執行查詢](../../reporting-services/report-data/media/rsqdicon-run.gif "執行查詢")|準備查詢。|  
|![切換到設計模式](../../reporting-services/media/rsqdicon-designmode.gif "切換到設計模式")|在「設計」模式與「查詢」模式之間切換。 若要變更為結果檢視，請以滑鼠右鍵按一下 [設計] 窗格並選擇 [結果]。|  
  
## <a name="graphical-dmx-query-designer-in-design-mode"></a>設計模式中的圖形化 DMX 查詢設計工具  
 當您編輯的資料集所使用的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源沒有有效的 Cube，但是具有有效的採礦模型時，圖形化查詢設計工具會在 [設計] 模式下開啟。 下圖會標示出設計模式的窗格。  
  
 ![Analysis Services DMX 查詢設計工具，設計檢視](../../reporting-services/report-data/media/rsqd-dsawas-dmx-designmode.gif "Analysis Services DMX 查詢設計工具，設計檢視")  
  
 下表會描述各個窗格的功能。  
  
|窗格|函數|  
|----------|--------------|  
|[查詢設計] 窗格|使用 [採礦模型] 及 [選取輸入資料表] 對話方塊建立 DMX 查詢。|  
|[方格] 窗格|針對方格中的每一個資料列，使用 [來源] 下拉式清單選取函數或運算式，並選擇要在 DMX 查詢中使用的欄位、群組和準則或引數。 若要查看依據選取項目所產生的 DMX 查詢文字，請按一下工具列上的 [設計模式] 按鈕。|  
  
 若要執行 DMX 查詢並將結果顯示在 [結果] 窗格中，請以滑鼠右鍵按一下 [查詢設計] 窗格並選取 [結果]。  
  
## <a name="graphical-dmx-query-designer-in-query-mode"></a>查詢模式中的圖形化 DMX 查詢設計工具  
 若要將圖形化查詢設計工具變更為「查詢」模式，請按一下工具列上的 [設計模式] 按鈕，或是以滑鼠右鍵按一下查詢設計介面並從捷徑功能表中選擇 [查詢]。 使用這種模式可直接在 [查詢] 窗格中輸入 DMX 文字。  
  
 下圖會標示出「查詢」模式中的窗格。  
  
 ![Analysis Services DMX 查詢設計工具，查詢檢視](../../reporting-services/report-data/media/rsqd-dsawas-dmx-querymode.gif "Analysis Services DMX 查詢設計工具，查詢檢視")  
  
 下表會描述各個窗格的功能。  
  
|窗格|函數|  
|----------|--------------|  
|[查詢設計] 窗格|使用 [採礦模型] 及 [選取輸入資料表] 對話方塊建立 DMX 查詢。|  
|[查詢] 窗格|直接在窗格中檢視或編輯 DMX 查詢文字。 如果變回 [設計] 模式，則無法保存 DMX 查詢文字的變更。|  
  
 若要執行 DMX 查詢並將結果顯示在 [結果] 窗格中，請以滑鼠右鍵按一下 [查詢設計] 窗格並選取 [結果]。  
  
## <a name="graphical-dmx-query-designer-in-result-mode"></a>結果模式中的圖形化 DMX 查詢設計工具  
 若要顯示「結果」模式，請以滑鼠右鍵按一下查詢設計介面並從捷徑功能表中選擇 [結果]。 當您切換到「結果」模式時，DMX 查詢便會自動執行。  
  
 下圖會顯示「結果」模式中的查詢設計工具。  
  
 ![Analysis Services DMX 查詢設計工具，結果檢視](../../reporting-services/report-data/media/rsqd-dsawas-dmx-resultmode.gif "Analysis Services DMX 查詢設計工具，結果檢視")  
  
 若要切換回「設計」模式或「查詢」模式，請以滑鼠右鍵按一下 [結果] 窗格並選取 [設計] 或 [查詢]。  
  
## <a name="see-also"></a>另請參閱  
 [在 Analysis Services 的 MDX 查詢設計工具中定義參數 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/define-parameters-in-the-mdx-query-designer-for-analysis-services.md)   
 [建立共用資料集或內嵌資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [DMX 的 Analysis Services 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)   
 [從資料採礦模型擷取資料 &#40;DMX&#41; &#40;SSRS&#41;](../../reporting-services/report-data/retrieve-data-from-a-data-mining-model-dmx-ssrs.md)   
 [RSReportDesigner 組態檔](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [MDX 的 Analysis Services 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)   
 [DMX 的 Analysis Services 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)  
  
  
