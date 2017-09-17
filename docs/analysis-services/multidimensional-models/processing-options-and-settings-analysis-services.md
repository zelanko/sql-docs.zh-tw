---
title: "處理選項和設定 (Analysis Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- process data option [Analysis Services]
- processing objects [Analysis Services]
- unprocess option [Analysis Services]
- process full option [Analysis Services]
- process index option [Analysis Services]
- process structure option [Analysis Services]
- process incremental option [Analysis Services]
- process update option [Analysis Services]
- process clear structure option [Analysis Services]
- process default option [Analysis Services]
ms.assetid: 2e858c74-ad3e-45f1-8745-efe2c0c3a7fa
caps.latest.revision: 48
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a4540adcf485554cff6c909dedf4d53585336ae6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="processing-options-and-settings-analysis-services"></a>處理選項和設定 (Analysis Services)
  當您在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中處理物件時，您可以選取處理選項來控制每個物件發生的處理類型。 每一個物件可用的處理類型各不相同，且會依據因上次處理之後物件所發生的變更來決定。 如果您讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 自動選取處理方法，它將使用的方法是能夠使物件在最短時間內回到完整處理狀態。  
  
 處理設定可讓您控制所處理的物件，以及用來處理這些物件的方法。 有些處理設定主要是用在批次處理作業。 如需批次處理的詳細資訊，請參閱[批次處理 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md)。  
  
> [!NOTE]  
>  本主題適用於多維度和資料採礦方案。 如需表格式解決方案的資訊，請參閱[處理資料庫、資料表或資料分割 &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)。  
  
## <a name="processing-options"></a>處理選項  
 下表描述 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中可用的處理方法，並識別支援每一個方法的物件。  
  
|模式|適用於|說明|  
|----------|----------------|-----------------|  
|**處理預設**|Cube、資料庫、維度、量值群組、採礦模型、採礦結構和分割區。|偵測資料庫物件的處理狀態，並且執行必要的處理，以便將尚未處理或部分處理的物件傳遞為完整處理的狀態。 如果您變更資料繫結，[處理預設] 將針對受影響的物件執行 [完整處理]。|  
|**完整處理**|Cube、資料庫、維度、量值群組、採礦模型、採礦結構和分割區。|處理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件及其包含的所有物件。 對已處理過的物件執行完整處理時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會先卸除該物件中的所有資料，然後再處理該物件。 當物件有結構變更時，例如加入、刪除或重新命名了屬性階層，就需要這種處理。|  
|**處理清除**|Cube、資料庫、維度、量值群組、採礦模型、採礦結構和分割區。|卸除所指定之物件中的資料和任何較低層級的構成物件。 卸除資料之後，不會重新載入它。|  
|**處理資料**|維度、Cube、量值群組和分割區。|只處理資料而不建立彙總或索引。 如果資料分割中有資料，將先卸除後再用來源資料重新填入資料分割。|  
|**處理加入**|維度、量值群組和分割區<br /><br /> 注意：[處理加入] 無法用於 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中的維度處理，但是您可以撰寫 XMLA 指令碼來執行這個動作。|針對維度，加入新的成員，並更新維度屬性標題與描述。<br /><br /> 針對量值群組和分割區，加入新的、可用的事實資料，且只處理相關的分割區。|  
|**處理更新**|維度|強制重新讀取資料和更新維度屬性。 相關資料分割上的彈性彙總和索引將被卸除。|  
|**處理索引**|Cube、維度、量值群組和分割區|為所有已處理的分割區建立或重建索引和彙總。 若是尚未處理的物件，此選項會產生錯誤。<br /><br /> 如果您關閉 [延遲處理]，則需要使用此選項處理。|  
|**處理結構**|Cube 和採礦結構|如果 Cube 已取消處理， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 將視需要來處理 Cube 的所有維度。 然後， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 只會建立 Cube 定義。 如果將這個選項套用到採礦結構，它會用來源資料擴展採礦結構。 這個選項和完整處理選項的差異在於，這個選項不會向下反覆處理採礦模型自身。|  
|**處理清除結構**|採礦結構|從採礦結構中移除所有定型資料。|  
  
## <a name="processing-settings"></a>處理設定  
 下表描述建立處理作業時可用的處理設定。  
  
|處理選項|說明|選項值|  
|-----------------------|-----------------|------------------|  
|**Parallel**|用於批次處理。 此設定會造成 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 將處理工作分出，以便在單一交易內平行執行。 如果失敗，結果就是回復所有變更。 您可以明確設定平行工作的最大數目，或讓伺服器決定最佳散發方式。 [平行] 選項在加速處理方面很有用。||  
|**循序 (交易模式)**|控制處理作業的執行行為。 有兩個選項可以使用。<br /><br /> 當您使用 [一筆交易] 處理時，所有變更會在處理作業成功之後才獲得認可。 也就是說，所有受到特定處理作業影響的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件都會保持為可供查詢使用，直到認可處理為止。 這會使物件暫時無法使用。 使用 [個別交易] 會讓受到處理作業中某個處理序影響的所有物件在該處理序一成功後，就無法供查詢使用。|**一筆交易**。 處理作業會以交易的形式來執行。 如果處理作業內的所有處理序都執行成功，處理作業所作的所有變更便會得到認可。 如果有一個處理序失敗，處理作業所作的所有變更就會回復。 [一筆交易] 是預設值。<br /><br /> **個別交易**。 處理作業中的每個處理序都是以獨立作業的形式執行。 如果其中一個處理序失敗，只會回復該處理序，處理作業會繼續進行。 每個作業都會在作業結束時認可所有處理序變更。|  
|**回寫資料表選項**|控制處理進行期間回寫資料表的處理方式。 此選項適用於 Cube 中的回寫分割區。|**使用現有的**。 使用現有的回寫資料表。 這是預設值。<br /><br /> **建立**： 建立新的回寫資料表，如果資料表已存在，就會造成處理序失敗。<br /><br /> **永遠建立**。 即使已經有回寫資料表存在，還是會建立新的回寫資料表。 將刪除及取代現有的資料表。|  
|**處理受影響的物件**|控制處理作業的物件範圍。 受影響的物件是由物件相依性來定義。 例如，分割區相依於可決定彙總的維度，但維度並未相依於分割區。 [False] 是預設值。|**False**。 作業會處理作業中已明確命名的物件以及所有相依物件。 例如，如果處理作業只包含維度， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 只會處理作業中明確識別的物件。 如果處理作業包含分割區，則分割區處理會自動叫用受影響維度的處理。<br /><br /> **True**。 作業會處理作業中明確命名的物件、所有相依物件，以及所有受到正在處理之物件影響的物件，而不會變更受影響物件的狀態。 例如，如果處理作業只包含維度，對於目前處於已處理狀態的分割區， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 也會處理所有受到維度處理影響的分割區。 目前處於尚未處理狀態的受影響分割區則不予處理。 然而，由於分割區相依於維度，因此，如果處理作業只包含分割區，則即使維度目前處於尚未處理的狀態，分割區處理還是會自動叫用受影響維度的處理。|  
|**維度索引鍵錯誤**|決定在處理期間發生錯誤時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所採取的動作。 選取 [使用自訂錯誤組態] 時，可以選取下列動作的值，來控制錯誤處理行為。<br /><br /> 當您選取 [使用預設錯誤組態] 時，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用為各個正在處理的物件而設定的錯誤組態。 如果物件設定為使用預設組態設定， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用為各個選項列出的預設值。||  
||**索引鍵錯誤動作**。 如果記錄中沒有索引鍵值，會選取發生下列其中一種動作：|**轉換為未知**。 索引鍵會解譯為未知成員。 這是預設值。<br /><br /> **捨棄記錄**。 記錄會被捨棄。|  
||**處理錯誤限制**。 選取其中一個選項來控制處理的錯誤數目：|**忽略錯誤計數**。 這個選項將使處理不管錯誤數目有多少都能繼續進行。<br /><br /> **發生錯誤時停止**。 使用這個選項，您可以控制其他兩個設定。 [錯誤數目] 可讓您將處理發生的錯誤限制在特定錯誤數目之內。 [發生錯誤時的動作] 可讓您決定到達 [錯誤數目] 時所要採取的動作。 您可以選取 [停止處理]，讓處理作業失敗並回復任何變更，也可以選取 [停止記錄]，讓處理能夠繼續進行而不記錄錯誤。 [發生錯誤時停止] 是在 [錯誤數目] 設定為 **0**，且 [發生錯誤時的動作] 設定為 [停止處理] 時的預設值。|  
||在下列錯誤情況中， 您可以設定選項值，來控制特定的錯誤處理行為。<br /><br /> 當您選取 [使用預設錯誤組態] 時，Analysis Services 會使用為各個正在處理的物件而設定的錯誤組態。 如果物件設定為使用預設組態設定，Analysis Services 會使用為各個選項列出的預設值。|**找不到索引鍵**。 在索引鍵值存在於分割區中，但不存在於對應維度時發生。 預設設定為 [報告並繼續]。 其他設定為 [忽略錯誤] 和 [報告並停止]。<br /><br /> **重複的索引鍵**。 當維度中存在一個以上的索引鍵值時發生。 預設設定為 [忽略錯誤]。 其他設定為 [報告並繼續] 和 [報告並停止]。<br /><br /> **Null 索引鍵已轉換為未知**。 當索引鍵值為 Null，且 [索引鍵錯誤動作] 設定為 [轉換為未知] 時發生。 預設設定為 [忽略錯誤]。 其他設定為 [報告並繼續] 和 [報告並停止]。<br /><br /> **不允許 Null 索引鍵**。 當 [索引鍵錯誤動作] 設定為 [捨棄記錄] 時發生。 預設設定為 [報告並繼續]。 其他設定為 [忽略錯誤] 和 [報告並停止]。|  
  
## <a name="see-also"></a>另請參閱  
 [處理多維度模型 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
