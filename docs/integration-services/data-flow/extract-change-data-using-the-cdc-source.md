---
title: 使用 CDC 來源擷取變更資料 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 604fbafb-15fa-4d11-8487-77d7b626eed8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 35e8d152cbffb5a5f34be4cda5c7e97fc8140d2d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292811"
---
# <a name="extract-change-data-using-the-cdc-source"></a>使用 CDC 來源擷取變更資料

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  若要加入及設定 CDC 來源，封裝至少必須包含一個資料流程工作及一個 CDC 控制工作。  
  
 如需 CDC 控制工作的詳細資訊，請參閱 [CDC 控制工作](../../integration-services/control-flow/cdc-control-task.md)。  
  
 如需 CDC 來源的詳細資訊，請參閱 [CDC 來源](../../integration-services/data-flow/cdc-source.md)。  
  
### <a name="to-extract-change-data-using-a-cdc-source"></a>若要使用 CDC 來源擷取變更資料  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝加以開啟。  
  
3.  按一下 [資料流程]  索引標籤，然後將 CDC 來源從 [工具箱]  拖曳至設計介面。  
  
4.  按兩下 CDC 來源。  
  
5.  在 [CDC 來源編輯器]  對話方塊中的 [連線管理員]  頁面上，從清單中選取現有的 ADO.NET 連線管理員，或按一下 [新增]  以建立新的連接。 連接應該指向包含要讀取之變更資料表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。  
  
6.  選取您要處理變更的 **CDC 資料表** 。  
  
7.  選取或輸入包含要讀取之 CDC 資料表的 **CDC 擷取執行個體** 名稱。  
  
     擷取的來源資料表可以具有一個或兩個擷取執行個體，以便透過結構描述變更處理資料表定義的流暢轉換。 如果針對所擷取的來源資料表定義了多個擷取執行個體，請在此選取您想要使用的擷取執行個體。 [schema].[table] 資料表的預設擷取執行個體名稱是 \<結構描述>_\<資料表>，但是使用中的實際擷取執行個體名稱可能有所不同。 實際讀取的資料表是 CDC 資料表 **cdc .\<capture-instance>_CT**。  
  
8.  選取可有效處理處理需求的處理模式。 可能的選項包括：  
  
    -   **全部**：傳回目前 CDC 範圍中的變更，不含 [更新之前]  值。  
  
    -   **全部 (含舊值)** ：傳回目前 CDC 處理範圍中的變更，包括舊值 ([更新前]  )。 每個更新作業都有兩個資料列：一個包含更新之前的值，另一個則包含更新之後的值。  
  
    -   **淨**：只針對目前 CDC 處理範圍中修改的每個來源資料列傳回一項變更。 如果來源資料列更新了許多次，就會產生結合的變更 (例如，插入+更新會產生為單一更新，而更新+刪除則產生為單一刪除)。 在淨變更處理模式中工作時，您可以將變更分割成刪除、插入和更新輸出，並且以平行方式處理它們，因為單一來源資料列會出現在多個輸出中。  
  
    -   **淨 (含更新遮罩)** ：這種模式與一般的淨模式很相似，但還新增了名稱模式為 **__$\<資料行名稱>\__Changed** 的布林資料行，表示目前變更資料列中的變更資料行。  
  
    -   **淨 (含合併)** ：這種模式與一般的淨模式很相似，但是插入和更新作業會合併成單一合併作業 (UPSERT)。  
  
9. 選取針對目前 CDC 內容維護 CDC 狀態的 SSIS 字串封裝變數。 如需 CDC 狀態變數的詳細資訊，請參閱[定義狀態變數](../../integration-services/data-flow/define-a-state-variable.md)。  
  
10. 選取 [Include reprocessing indicator column (包含重新處理指標資料行)]  核取方塊即可建立名為 **__$reprocessing** 的特殊輸出資料行。 當 CDC 處理範圍與初始處理範圍 (對應至初始載入週期之 LSN 的範圍) 重疊，或者上一次執行發生錯誤之後重新處理 CDC 處理範圍時，這個資料行的值就是 **true**。 這個指標資料行可讓 SSIS 開發人員在重新處理變更時以不同的方式處理錯誤 (例如，可以忽略刪除不存在的資料列以及在重複索引鍵上失敗的插入等動作)。  
  
     如需詳細資訊，請參閱 [CDC 來源自訂屬性](../../integration-services/data-flow/cdc-source-custom-properties.md)。  
  
11. 若要更新外部及輸出資料行之間的對應，請按一下 **[資料行]** ，並在 **[外部資料行]** 清單中選取不同的資料行。  
  
12. (選擇性) 藉由刪除 [輸出資料行]  清單中的值，更新輸出資料行的值。  
  
13. 若要設定錯誤輸出，請按一下 **[錯誤輸出]** 。  
  
14. 您可以按一下 [預覽]  ，以檢視 CDC 來源擷取的最多 200 個資料列。  
  
15. 按一下 [確定]  。  
  
## <a name="see-also"></a>另請參閱  
 [CDC 來源編輯器 &#40;連線管理員頁面&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)   
 [CDC 來源編輯器 &#40;資料行頁面&#41;](../../integration-services/data-flow/cdc-source-editor-columns-page.md)   
 [CDC 來源編輯器 &#40;錯誤輸出頁面&#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
  
