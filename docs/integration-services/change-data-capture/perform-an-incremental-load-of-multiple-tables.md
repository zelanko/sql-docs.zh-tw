---
title: 執行多個資料表的累加式載入 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],multiple tables
ms.assetid: 39252dd5-09c3-46f9-a17b-15208cfd336d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fee01a2531ce405f212c2559d91ec0ea241b9784
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65728621"
---
# <a name="perform-an-incremental-load-of-multiple-tables"></a>執行多個資料表的累加式載入

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  在 [利用異動資料擷取改善累加式載入](../../integration-services/change-data-capture/change-data-capture-ssis.md)主題中，圖表會說明只在一個資料表上執行累加式載入的基本封裝。 不過，載入一個資料表不如必須執行多個資料表的累加式載入那麼常見。  
  
 執行多個資料表的累加式載入時，會針對所有資料表執行一次某些步驟，而且必須針對每個來源資料表重複其他步驟。 您在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中實作這些步驟時有一個以上的選擇。  
  
-   使用父封裝和子封裝。  
  
-   在單一封裝中使用多個資料流程工作。  
  
## <a name="loading-multiple-tables-by-using-a-parent-package-and-multiple-child-packages"></a>使用父封裝和多個子封裝載入多個資料表  
 您可以使用父封裝來執行僅需要執行一次的步驟。 子封裝將會執行必須針對每個來源資料表執行的步驟。  
  
#### <a name="to-create-a-parent-package-that-performs-those-steps-that-only-have-to-be-done-once"></a>建立父封裝，執行僅需要執行一次的步驟  
  
1.  建立父封裝。  
  
2.  在控制流程中，使用「執行 SQL」工作或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 運算式來計算端點。  
  
     如需如何計算端點的範例，請參閱 [指定變更資料的間隔](../../integration-services/change-data-capture/specify-an-interval-of-change-data.md)。  
  
3.  如果需要，使用「For 迴圈」容器延遲執行，直到所選期間的變更資料就緒為止。  
  
     如需此類「For 迴圈」容器的範例，請參閱 [判斷變更資料是否就緒](../../integration-services/change-data-capture/determine-whether-the-change-data-is-ready.md)。  
  
4.  使用多個「執行封裝」工作，針對每個要載入的資料表執行子封裝。 使用「父封裝變數」組態，將父封裝中計算的端點傳遞到每個子封裝。  
  
     如需詳細資訊，請參閱 [執行封裝工作](../../integration-services/control-flow/execute-package-task.md) 和 [在子封裝中使用變數和參數的值](../../integration-services/packages/legacy-package-deployment-ssis.md#child)。  
  
#### <a name="to-create-child-packages-to-perform-those-steps-that-have-to-be-done-for-each-source-table"></a>建立子封裝來執行必須針對每個來源資料表執行的步驟  
  
1.  針對每個來源資料表建立子封裝。  
  
2.  在控制流程中，使用「指令碼」工作或「執行 SQL」工作來組合將用於查詢變更的 SQL 陳述式。  
  
     如需如何組合查詢的範例，請參閱 [準備查詢變更資料](../../integration-services/change-data-capture/prepare-to-query-for-the-change-data.md)。  
  
3.  使用每個子封裝中的單一「資料流程」工作來載入變更資料，並將其套用到目的地。 設定「資料流程」，如下列步驟所述：  
  
    1.  在資料流程中，使用來源元件來查詢所選端點內之變更的變更資料表。  
  
         如需如何查詢變更資料表的範例，請參閱 [擷取與了解變更資料](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md)。  
  
    2.  使用「條件式分割」轉換，將插入、更新與刪除導引到不同的輸出以便進行適當的處理。  
  
         如需如何設定此轉換來導向輸出的範例，請參閱 [處理插入、更新與刪除](../../integration-services/change-data-capture/process-inserts-updates-and-deletes.md)。  
  
    3.  使用目的地元件，將插入套用到目的地。 搭配參數化的 UPDATE 和 DELETE 陳述式使用「OLE DB 命令」轉換，將更新與刪除套用到目的地。  
  
         如需如何使用此轉換來套用更新與刪除的範例，請參閱 [將變更套用到目的地](../../integration-services/change-data-capture/apply-the-changes-to-the-destination.md)。  
  
## <a name="loading-multiple-tables-by-using-multiple-data-flow-tasks-in-a-single-package"></a>在單一封裝中使用多個資料流程工作來載入多個資料表  
 或者，您可以使用包含要載入的每個來源資料表之個別「資料流程」工作的單一封裝。  
  
#### <a name="to-load-multiple-tables-by-using-multiple-data-flow-tasks-in-a-single-package"></a>在單一封裝中使用多個資料流程工作載入多個資料表  
  
1.  建立單一封裝。  
  
2.  在控制流程中，使用「執行 SQL」工作或 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 運算式來計算端點。  
  
     如需如何計算端點的範例，請參閱 [指定變更資料的間隔](../../integration-services/change-data-capture/specify-an-interval-of-change-data.md)。  
  
3.  如果需要，使用「For 迴圈」容器延遲執行，直到所選間隔的變更資料就緒為止。  
  
     如需此類「For 迴圈」容器的範例，請參閱 [判斷變更資料是否就緒](../../integration-services/change-data-capture/determine-whether-the-change-data-is-ready.md)。  
  
4.  使用「指令碼」工作或「執行 SQL」工作來組合將用於查詢變更的 SQL 陳述式。  
  
     如需如何組合查詢的範例，請參閱 [準備查詢變更資料](../../integration-services/change-data-capture/prepare-to-query-for-the-change-data.md)。  
  
5.  使用多個「資料流程」工作，從每個來源資料表載入變更資料，並將其套用到目的地。 設定每個「資料流程」工作，如下列步驟所述。  
  
    1.  在每個資料流程中，使用來源元件來查詢所選端點內之變更的變更資料表。  
  
         如需如何查詢變更資料表的範例，請參閱 [擷取與了解變更資料](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md)。  
  
    2.  使用「條件式分割」轉換，將插入、更新與刪除導引到不同的輸出以便進行適當的處理。  
  
         如需如何設定此轉換來導向輸出的範例，請參閱 [處理插入、更新與刪除](../../integration-services/change-data-capture/process-inserts-updates-and-deletes.md)。  
  
    3.  使用目的地元件，將插入套用到目的地。 搭配參數化的 UPDATE 和 DELETE 陳述式使用「OLE DB 命令」轉換，將更新與刪除套用到目的地。  
  
         如需如何使用此轉換來套用更新與刪除的範例，請參閱 [將變更套用到目的地](../../integration-services/change-data-capture/apply-the-changes-to-the-destination.md)。  
  
  
