---
title: 錯誤組態 （採礦結構對話方塊） (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.miningstructuredialog.general.f1
ms.assetid: d9aa028b-bad9-49c7-a81c-c2150e4dd481
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e8973d9dd6fb5d96afc9cf66ded4b894f0dfe6df
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081365"
---
# <a name="error-configuration-mining-structure-dialog-box-analysis-services---multidimensional-data"></a>錯誤組態 (採礦結構對話方塊) (Analysis Services - 多維度資料)
  在 **SQL Server Management Studio** 中，使用 **[採礦結構屬性]** 對話方塊的 **[錯誤組態]** 頁面，即可設定 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料庫中採礦結構的錯誤組態屬性。  
  
## <a name="options"></a>選項。  
 **使用預設錯誤組態**  
 選取即可針對處理作業中的物件使用預設錯誤組態。  
  
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
 當錯誤數目超出 [錯誤數目] 中的值時，請選擇採取下列動作之一：  
  
-   **[停止處理]** 會結束處理作業。  
  
-   **[停止記錄]** 會停止記錄錯誤，但仍繼續處理作業。  
  
 **找不到索引鍵**  
 當處理物件時找不到索引鍵時，請指定採取下列動作之一：  
  
-   **[忽略錯誤]** 會忽略錯誤  
  
-   **[報告並繼續]** 會報告錯誤，並繼續處理作業  
  
-   **[報告並停止]** 會報告錯誤並停止處理作業。  
  
 **重複的索引鍵**  
 處理物件時如果找到重複索引鍵，請指定採取下列動作之一：  
  
-   **[忽略錯誤]** 會忽略錯誤  
  
-   **[報告並繼續]** 會報告錯誤，並繼續處理作業  
  
-   **[報告並停止]** 會報告錯誤並停止處理作業。  
  
 **Null 索引鍵已轉換為未知**  
 指定處理物件時，若有 Null 成員索引鍵加入未知成員中，要採取下列其中一項動作。  
  
-   **[忽略錯誤]** 會忽略錯誤  
  
-   **[報告並繼續]** 會報告錯誤，並繼續處理作業  
  
-   **[報告並停止]** 會報告錯誤並停止處理作業。  
  
 **不允許 Null 索引鍵**  
 指定處理物件時，若在不允許 Null 索引鍵的情況下找到 Null 索引鍵，要採取下列其中一項動作。  
  
-   **[忽略錯誤]** 會忽略錯誤  
  
-   **[報告並繼續]** 會報告錯誤，並繼續處理作業  
  
-   **[報告並停止]** 會報告錯誤並停止處理作業。  
  
 **錯誤記錄路徑**  
 輸入錯誤記錄檔的完整路徑和檔案名稱。  
  
## <a name="see-also"></a>另請參閱  
 [採礦結構屬性 對話方塊&#40;Analysis Services-資料採礦&#41;](mining-structure-properties-dialog-analysis-services-data-mining.md)   
 [一般&#40;採礦結構對話方塊&#41; &#40;Analysis Services-資料採礦&#41;](general-mining-structure-dialog-box-analysis-services-data-mining.md)  
  
  
