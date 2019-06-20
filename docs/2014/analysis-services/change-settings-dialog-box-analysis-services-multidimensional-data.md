---
title: 變更設定對話方塊 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.process.batchsettingsdialog.f1
ms.assetid: 0041e042-d7ce-48f9-a690-a6dc65471ff3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 43dfc1dca2e60fe2f5e467556ee36c3add1a9da3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088244"
---
# <a name="change-settings-dialog-box-analysis-services---multidimensional-data"></a>變更設定對話方塊 (Analysis Services - 多維度資料)
  使用 **和** 中的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] [變更設定] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 對話方塊，即可變更 **[處理]** 對話方塊所列出之物件的處理設定。 您可以在 **[處理]** 對話方塊中按一下 **[變更設定]** ，以顯示 **[變更設定]** 對話方塊。  
  
> [!NOTE]  
>  對於 [處理]  對話方塊中列出的物件，此對話方塊所指定的設定會覆寫從 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫繼承的預設值。  
  
## <a name="options"></a>選項  
 **處理選項**  
 使用此索引標籤即可針對處理作業，修改處理順序、回寫資料表以及受影響的物件等相關設定。 索引標籤包含下列選項：  
  
 **Parallel**  
 按一下以平行處理物件。  
  
 **平行工作數上限**  
 選取處理作業平行執行的工作數上限，或選擇 [讓伺服器決定]  ，即可讓 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 選取最佳的平行工作數。  
  
 **循序**  
 按一下即可循序處理物件。  
  
 **交易模式**  
 選擇循序處理物件時使用的交易模式：  
  
-   **[一筆交易]** 會在相同交易中處理所有物件。  
  
-   **[個別交易]** 會在個別交易中處理所有物件，包括相依物件。  
  
> [!NOTE]  
>  只有選取 [循序]  時才會啟用此選項。  
  
 **回寫資料表選項**  
 選擇用來管理回寫資料表的選項：  
  
-   **[建立]** 會建立回寫資料表 (如果不存在)。 如果回寫資料表已存在，則會發生錯誤。  
  
-   **[永遠建立]** 會建立不存在的回寫資料表，如果已存在，則會覆寫現有的回寫資料表。  
  
-   **[使用現有的]** 會使用現有的回寫資料表 (如果存在)。 如果回寫資料表不存在，則會發生錯誤。  
  
 **處理受影響的物件**  
 選取即可包含並處理相依於處理作業所包含物件的物件。  
  
 **維度索引鍵錯誤**  
 使用此索引標籤即可修改處理作業錯誤組態的相關設定。 索引標籤包含下列選項：  
  
 **使用預設錯誤組態**  
 選取即可針對處理作業中的物件使用預設錯誤組態。  
  
 **使用自訂錯誤組態**  
 選取即可為處理作業中的物件定義錯誤組態。  
  
 **索引鍵錯誤動作**  
 在處理期間發現無法查閱的新索引鍵時，請選擇下列其中一個發生的動作：  
  
-   **[轉換為未知]** 會將該記錄的資訊彙總至未知成員。  
  
-   **[捨棄記錄]** 會將該記錄的資訊排除在物件的處理範圍以外。  
  
 **忽略錯誤計數**  
 按一下即可忽略處理時發生的錯誤。  
  
 **發生錯誤時停止**  
 按一下即可在錯誤發生時停止處理。 此選項會啟用 **[錯誤數目]** 和 **[發生錯誤時的動作]** 選項。  
  
 **錯誤數目**  
 輸入處理停止之前所忽略的錯誤數目。  
  
 **發生錯誤時要執行的動作**  
 當錯誤數目超出 [錯誤數目]  中的值時，請選擇採取下列動作之一：  
  
-   **[停止處理]** 會結束處理作業。  
  
-   **[停止記錄]** 會停止記錄錯誤，但仍繼續處理作業。  
  
 **找不到索引鍵**  
 當處理物件時找不到索引鍵時，請指定採取下列動作之一：  
  
-   **[忽略錯誤]** 會忽略錯誤。  
  
-   **[報告並繼續]** 會報告錯誤並繼續處理作業。  
  
-   **[報告並停止]** 會報告錯誤並停止處理作業。  
  
 **重複的索引鍵**  
 處理物件時如果找到重複索引鍵，請指定採取下列動作之一：  
  
-   **[忽略錯誤]** 會忽略錯誤。  
  
-   **[報告並繼續]** 會報告錯誤並繼續處理作業。  
  
-   **[報告並停止]** 會報告錯誤並停止處理作業。  
  
 **Null 索引鍵已轉換為未知**  
 指定處理物件時，若有 Null 成員索引鍵加入未知成員中，要採取下列其中一項動作：  
  
-   **[忽略錯誤]** 會忽略錯誤。  
  
-   **[報告並繼續]** 會報告錯誤並繼續處理作業。  
  
-   **[報告並停止]** 會報告錯誤並停止處理作業。  
  
 **不允許 Null 索引鍵**  
 指定處理物件時，若在不允許 Null 索引鍵的情況下找到 Null 索引鍵，要採取下列其中一項動作：  
  
-   **[忽略錯誤]** 會忽略錯誤。  
  
-   **[報告並繼續]** 會報告錯誤並繼續處理作業。  
  
-   **[報告並停止]** 會報告錯誤並停止處理作業。  
  
 **錯誤記錄路徑**  
 輸入錯誤記錄檔的完整路徑和檔案名稱。  
  
 **瀏覽**  
 按一下即可開啟 [開啟]  對話方塊，並選取錯誤記錄檔的完整路徑和檔案名稱。  
  
 **處理受影響的物件**  
 按一下即可處理相依於 [處理]  對話方塊中所選取物件的物件。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services Designers and Dialog Boxes&#40;多維度資料&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [處理序 對話方塊&#40;Analysis Services-多維度資料&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  
