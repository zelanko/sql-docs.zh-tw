---
title: 互動式排序 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 00cafed5-1a3c-4ce0-a1fb-ff1e2613f495
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5c62d4244b025ab987100a58aef1b2a10a7efa17
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59966824"
---
# <a name="interactive-sort-report-builder-and-ssrs"></a>互動式排序 (報表產生器及 SSRS)
  您可以加入互動式排序按鈕，讓使用者在資料表中切換資料列的遞增和遞減順序，或在矩陣中切換資料列及資料行的遞增和遞減順序。 互動式排序的常見用法為，將排序按鈕加入到每個資料行標頭。 接著，使用者可以選擇排序所依據的資料行。  
  
 不過，您可以將互動式排序按鈕加入到任何文字方塊，而不只是資料行標頭。 例如，對於資料列群組外之資料列中的文字方塊，您可以針對父群組資料列或資料行、子群組資料列或資料行，或詳細資料列或資料行指定排序。 也可以將欄位結合成一個單一的群組運算式，然後依多個欄位進行排序。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 當您加入互動式排序時，必須指定下列項目：  
  
-   **要排序的項目：** 資料列或資料行？  
  
-   **排序依據的項目：** 顯示在資料表資料行中的欄位？ 未顯示的欄位？  
  
-   **要排序的內容：** 例如，您可以針對下列項目進行排序：與資料列群組建立關聯的資料列、與資料行群組建立關聯的資料行、詳細資料列、父群組內的子群組，或是父群組和子群組一起。  
  
-   **要新增排序按鈕的文字方塊：** 在資料行標頭或群組資料列標頭中？  
  
-   **是否要同步處理多個資料區的排序：** 您可以設計一份報表，讓使用者切換排序次序時，也排序具有相同上階的其他資料區。  
  
 如需逐步指示，請參閱 [將互動式排序加入至資料表或矩陣 &#40;報表產生器及 SSRS&#41;](add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)(將互動式排序加入資料表或矩陣 (報表產生器及 SSRS))。  
  
 下表摘要說明您可以使用互動式排序按鈕達到的效果。  
  
|動作|要排序的項目|要加入排序按鈕的位置|排序依據的項目|排序範圍|  
|------------|------------------|----------------------------------|---------------------|----------------|  
|排序沒有群組之資料表的詳細資料列|詳細資料|資料行標頭|繫結至此資料行的資料集欄位|資料區域|  
|排序矩陣的最上層群組執行個體|群組|資料行標頭|父群組的群組運算式|資料區域|  
|排序資料表中子群組的詳細資料列|詳細資料|子群組標題資料列|排序依據的資料集欄位|子群組|  
|排序資料表中多個資料列群組和詳細資料列的資料列|群組，但是您必須重新定義群組運算式|資料行標頭|排序依據之資料集欄位的彙總|資料區域|  
|同步處理多個資料區域的排序次序|群組|通常是資料行標頭|群組運算式|資料集|  
  
 報表處理器會在套用所有資料區域和群組排序運算式之後，套用互動式排序。 如需詳細資訊，請參閱 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)(將互動式排序加入資料表或矩陣 (報表產生器及 SSRS))。  
  
## <a name="adding-interactive-sort-for-multiple-groups"></a>加入多個群組的互動式排序  
 在每個以單一資料集欄位為基礎之巢狀資料列群組的資料表中，您可以加入互動式排序按鈕，排序父群組值、子群組值或詳細資料列。 不過，您可能想要讓使用者能夠同時依父群組值和子群組值排序資料表，而不必按滑鼠多次。  
  
 若要這樣做，您必須重新設計資料表，以便針對結合多個欄位的運算式分組。 例如，對於包含存貨計數的資料集，如果原始資料表先依大小，然後依色彩分組，您可以利用結合大小和色彩的群組運算式指定單一群組。 如需詳細資訊，請參閱 [將互動式排序加入至資料表或矩陣 &#40;報表產生器及 SSRS&#41;](add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)(將互動式排序加入資料表或矩陣 (報表產生器及 SSRS))。  
  
## <a name="see-also"></a>另請參閱  
 [在資料區中排序資料 &#40;報表產生器及 SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [將互動式排序加入至資料表或矩陣 &#40;報表產生器及 SSRS&#41;](add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)  
  
  
