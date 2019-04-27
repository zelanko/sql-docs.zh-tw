---
title: CDC 來源編輯器 （連線管理員頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.connection.f1
ms.assetid: 304e6717-e160-4a7b-a06f-32182449fef8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d0e421d6ba1aaf69c04a450d8d93ff1ddf385935
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62771774"
---
# <a name="cdc-source-editor-connection-manager-page"></a>CDC 來源編輯器 (連接管理員頁面)
  使用 [CDC 來源編輯器] 對話方塊的 [連線管理員] 頁面，即可針對 CDC 來源從中讀取變更資料列的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 資料庫 (CDC 資料庫) 選取 ADO.NET 連線管理員。 一旦選取 CDC 資料庫之後，您就必須在資料庫中選取擷取的資料表。  
  
 如需 CDC 來源的詳細資訊，請參閱 [CDC 來源](data-flow/cdc-source.md)。  
  
## <a name="task-list"></a>工作清單  
 **若要開啟 CDC 來源編輯器的連接管理員頁面**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，開啟具有 CDC 來源的 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 封裝。  
  
2.  在 [資料流程] 索引標籤中，按兩下 CDC 來源。  
  
3.  在 [CDC 來源編輯器] 中，按一下 [連線管理員]。  
  
## <a name="options"></a>選項。  
 **ADO.NET 連接管理員**  
 從清單中選取現有的連接管理員，或按一下 [新增] 建立新的連接。 此連接必須指向啟用 CDC 而且包含選取之變更資料表的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫。  
  
 **新增**  
 按一下 **[新增]**。 [設定 ADO.NET 連線管理員編輯器] 對話方塊隨即開啟，讓您能夠建立新的連線管理員。  
  
 **CDC 資料表**  
 選取 CDC 來源資料表，其中包含您想要讀取並饋送至下游 SSIS 元件進行處理的擷取變更。  
  
 **擷取執行個體**  
 選取或輸入包含要讀取之 CDC 資料表的 CDC 擷取執行個體名稱。  
  
 擷取的來源資料表可以具有一個或兩個擷取執行個體，以便透過結構描述變更處理資料表定義的流暢轉換。 如果針對所擷取的來源資料表定義了多個擷取執行個體，請在此選取您想要使用的擷取執行個體。 [schema].[table] 資料表的預設擷取執行個體名稱是 \<結構描述>_\<資料表>，但是使用中的實際擷取執行個體名稱可能有所不同。 實際讀取的資料表是 CDC 資料表 **cdc .\<capture-instance>_CT**。  
  
 **CDC 處理模式**  
 選取可有效處理處理需求的處理模式。 可能的選項包括：  
  
-   **全部**：傳回目前 CDC 範圍中的變更，不含 [更新之前] 值。  
  
-   **全部 (含舊值)**：傳回目前 CDC 處理範圍中的變更，包括舊值 ([更新前])。 每個更新作業都有兩個資料列：一個包含更新之前的值，另一個則包含更新之後的值。  
  
-   **淨**：只針對目前 CDC 處理範圍中修改的每個來源資料列傳回一項變更。 如果來源資料列更新了許多次，就會產生結合的變更 (例如，插入+更新會產生為單一更新，而更新+刪除則產生為單一刪除)。 在淨變更處理模式中工作時，您可以將變更分割成刪除、插入和更新輸出，並且以平行方式處理它們，因為單一來源資料列會出現在多個輸出中。  
  
-   **淨 (含更新遮罩)**：這種模式與一般的淨模式很相似，但還新增了名稱模式為 **__$\<資料行名稱>\__Changed** 的布林資料行，表示目前變更資料列中的變更資料行。  
  
-   **淨 (含合併)**：這種模式與一般的淨模式很相似，但是插入和更新作業會合併成單一合併作業 (UPSERT)。  
  
> [!NOTE]  
>  對於所有淨變更選項而言，來源資料表必須具有主索引鍵或唯一索引。 如果資料表沒有主索引鍵或唯一索引，您就必須使用 [全部] 選項。  
  
 **包含 CDC 狀態的變數**  
 選取針對目前 CDC 內容維護 CDC 狀態的 SSIS 字串封裝變數。 如需 CDC 狀態變數的詳細資訊，請參閱 [定義狀態變數](data-flow/define-a-state-variable.md)。  
  
 **包含重新處理指標資料行**  
 選取此核取方塊即可建立名為 **__$reprocessing**的特殊輸出資料行。  
  
 當 CDC 處理範圍與初始處理範圍 (對應至初始載入週期之 LSN 的範圍) 重疊，或者上一次執行發生錯誤之後重新處理 CDC 處理範圍時，這個資料行的值就是 **true** 。 這個指標資料行可讓 SSIS 開發人員在重新處理變更時以不同的方式處理錯誤 (例如，可以忽略刪除不存在的資料列以及在重複索引鍵上失敗的插入等動作)。  
  
 如需詳細資訊，請參閱 [CDC 來源自訂屬性](data-flow/cdc-source-custom-properties.md)。  
  
## <a name="see-also"></a>另請參閱  
 [CDC 來源編輯器 &#40;資料行頁面&#41;](../../2014/integration-services/cdc-source-editor-columns-page.md)   
 [CDC 來源編輯器 &#40;錯誤輸出頁面&#41;](../../2014/integration-services/cdc-source-editor-error-output-page.md)  
  
  
