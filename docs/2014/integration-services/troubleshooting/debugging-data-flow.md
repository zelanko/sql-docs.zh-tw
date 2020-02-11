---
title: 偵錯資料流程 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- progress reporting [Integration Services]
- data viewers [Integration Services]
- data flow [Integration Services], debugging
- debugging [Integration Services], data flow
- counting rows
ms.assetid: 1c574f1b-54f7-4c05-8e42-8620e2c1df0f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fdfaeeb9e8dafe82a1312593df2dd128635b8365
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62766191"
---
# <a name="debugging-data-flow"></a>偵錯資料流程
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]而[!INCLUDE[ssIS](../../includes/ssis-md.md)]設計工具組含的功能和工具，可讓您用來疑難排解[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]封裝中的資料流程。  
  
-   
  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」會提供資料檢視器。  
  
-   
  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 轉換會提供資料列計數。  
  
-   
  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」提供執行階段的進度報表。  
  
## <a name="data-viewers"></a>資料檢視器  
 資料檢視器可以顯示資料流程中兩個元件之間的資料。 從資料來源擷取資料或資料第一次進入資料流程時、在轉換更新資料之前和之後，以及在資料載入其目的地之前，可以透過資料檢視器來顯示資料。  
  
 若要檢視資料，請將資料檢視器附加至連接兩個資料流程元件的路徑。 具有在不同資料流程元件之間檢視資料的能力，可讓您更容易識別非預期的資料值、檢視轉換變更資料行值的方式，以及探索轉換失敗的原因。 例如，如果您發現參考資料表中的查閱失敗，為了修正此問題，您可能希望加入為空白資料行提供預設資料的轉換。  
  
 資料檢視器可以在方格中顯示資料。 使用方格時，您需要選取要顯示的資料行。 選定資料行的值會以表格格式顯示。  
  
 您也可以在路徑上加入多個資料檢視器， 並以不同格式顯示相同資料，例如，建立資料的圖表檢視與方格檢視，或是為不同資料行建立不同的資料檢視器。  
  
 當您將資料檢視器加入至路徑時，「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」會在 **[資料流程]** 索引標籤之設計介面上的路徑旁邊，加入資料檢視器圖示。 具備多個輸出的轉換 (例如「條件式分割」轉換) 可以在每個路徑上加入資料檢視器。  
  
 在執行階段， **[資料檢視器]** 視窗會開啟，並顯示以資料檢視器格式所指定的資訊。 例如，使用方格格式的資料檢視器會顯示選定資料行的資料、傳遞至資料流程元件的輸出資料列數目，以及顯示的資料列數目。 資訊會以逐一緩衝區的方式顯示，且根據資料流程中的資料列寬度而定，緩衝區可能包含一或多個資料列。  
  
 在 **[資料檢視器]** 對話方塊中，您可以將資料複製到剪貼簿、從資料表清除所有資料、重新設定資料檢視器、繼續資料流程，以及卸離或附加資料檢視器。  
  
#### <a name="to-add-a-data-viewer"></a>若要加入資料檢視器  
  
-   [將資料檢視器加入資料流程](../add-a-data-viewer-to-a-data-flow.md)  
  
## <a name="row-counts"></a>資料列計數  
 經過某個路徑傳送的資料列數目，會顯示在「 **設計師」中** [資料流程] [!INCLUDE[ssIS](../../includes/ssis-md.md)] 索引標籤之設計介面上的該路徑旁邊。 隨著資料不斷經由路徑移動，該數目會定期更新。  
  
 您也可以將「資料列計數」轉換加入資料流程，以擷取變數中的最後資料列計數。 如需詳細資訊，請參閱 [Row Count Transformation](../data-flow/transformations/row-count-transformation.md)。  
  
## <a name="progress-reporting"></a>進度報表  
 當您執行封裝時，「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」會在 **[資料流程]** 索引標籤的設計介面上，使用指示狀態的色彩顯示每個資料流程元件，以描述進度。 當每個元件開始執行其工作時，會從無色彩變更為黃色，並在成功完成時變更為綠色， 紅色則表示該元件已失敗。  
  
 下表描述色彩編碼。  
  
|Color|描述|  
|-----------|-----------------|  
|無色彩|正在等候由資料流程引擎呼叫。|  
|黃色|正在執行轉換、擷取資料或載入資料。|  
|綠色|已成功執行。|  
|紅色|已執行但發生錯誤。|  
  
## <a name="see-also"></a>另請參閱  
 [套件開發的疑難排解工具](troubleshooting-tools-for-package-development.md)  
  
  
