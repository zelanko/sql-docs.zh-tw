---
title: "在 DirectQuery 模式 （SSAS 表格式） 中定義資料分割 |Microsoft 文件"
ms.custom: 
ms.date: 07/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5f179ba9-6efb-46ae-90e5-945bbfddb719
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 88079b80a84e692ca07695f718c161f626093cec
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="define-partitions-in-directquery-models"></a>在 DirectQuery 模式中定義分割區
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]本節說明如何將資料分割用於 DirectQuery 模型中。 如需表格式模型中之資料分割的更一般資訊，請參閱 [資料分割 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/partitions-ssas-tabular.md)。  
  
> [!NOTE]  
>  雖然資料表可以有多個分割區，但在 DirectQuery 模式中，只有其中之一可指定用於執行查詢。 單一分割區需求適用於所有相容性等級的 DirectQuery 模型。  
  
## <a name="using-partitions-in-directquery-mode"></a>在 DirectQuery 模式中使用資料分割  
 您必須針對每一個資料表指定當做 DirectQuery 資料來源使用的單一資料分割。  如果有多個資料分割，當您將模型切換為啟用 DirectQuery 模式時，根據預設，資料表中建立的第一個資料分割會標示為 DirectQuery 資料分割。 可以在稍後透過使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的資料分割管理員來變更此設定。  
  
 為什麼在 DirectQuery 模式下只允許單一資料分割？  
  
 在表格式模型中 (就如同 OLAP 模型一樣)，資料表的資料分割是由 SQL 查詢所定義。 建立資料分割定義的開發人員會負責確保資料分割不會重疊。 Analysis Services 不會檢查記錄是屬於一個資料分割還是多個資料分割。  
  
 快取表格式模型中資料分割有相同的行為。 如果您使用記憶體中的模型，在存取快取時，會對每個資料分割評估 DAX 公式，並且合併結果。 但是當表格式模型使用 DirectQuery 模式時，無法評估多個資料分割、合併結果，以及將其轉換為 SQL 陳述式以傳送到關聯式資料存放區。 這樣做可能會導致無法接受的效能損失，以及在彙總結果時可能發生的不精確性。  
  
 因此，對於在 DirectQuery 模式中回答的查詢，伺服器會使用已標示為主要資料分割的單一資料分割來存取 DirectQuery，稱為「DirectQuery 資料分割」。  在這個分割區定義中指定的 SQL 查詢，會定義一組完整的資料，用來回答 DirectQuery 模式中的查詢。  
  
 如果您未明確定義資料分割，則引擎只是發出 SQL 查詢至整個關聯式資料來源、執行 DAX 公式規定的任何以集合為基礎的作業，並且傳回查詢結果。  
  
  
## <a name="change-a-directquery-partition"></a>變更 DirectQuery 分割區  
 因為資料表中只有一個資料分割可以指定為 DirectQuery 資料分割，所以根據預設，Analysis Services 會使用資料表中建立的第一個資料分割。 在模型專案撰寫期間，您可以藉由使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的 [資料分割管理員] 對話方塊來變更 DirectQuery 資料分割。 如果是部署的模型，您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]來變更 DirectQuery 資料分割。  
  
#### <a name="change-the-directquery-partition-for-a-tabular-model-project"></a>變更表格式模型專案的 DirectQuery 資料分割  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，於模型設計師中按一下包含分割資料表的資料表 (標籤)。  
  
2.  按一下 **[資料表]** 功能表，然後按一下 **[資料分割]**。  
  
3.  在 [資料分割管理員] 中，作為目前直接查詢資料分割的資料分割是由資料分割名稱上的前置詞 **(DirectQuery)** 所表示。  
  
     從 [資料分割] 清單中選取其他資料分割，然後按一下 [設為 DirectQuery]。 選取目前的 DirectQuery 資料分割時，[設為 DirectQuery] 按鈕不會啟用，而且在模型尚未啟用直接查詢模式時，看不到此按鈕。  
  
4.  如果需要，請變更處理選項，然後按一下 [確定]。  
  
#### <a name="change-the-directquery-partition-for-a-deployed-tabular-model"></a>變更已部署的表格式模型的 DirectQuery 資料分割  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的物件總管中，開啟模型資料庫。  
  
2.  展開 [資料表] 節點，然後以滑鼠右鍵按一下資料分割資料表，再選取 [資料分割]。  
  
     指定用於 DirectQuery 模式的資料分割在資料分割名稱上具有前置詞 (DirectQuery)。  
  
3.  若要變更為其他資料分割，請按一下 [直接查詢] 工具列圖示以開啟 [設定 DirectQuery 資料分割] 對話方塊。 在尚未啟用直接查詢的模型上，無法使用 DirectQuery 工具列圖示。  
  
4.  從 [資料分割名稱] 下拉式清單中選擇其他資料分割，然後視需要變更該資料分割的處理選項。  
  
## <a name="partitions-in-cached-models-and-in-directquery-models"></a>快取模型和 DirectQuery 模型中的資料分割  
 當您設定 DirectQuery 資料分割時，您必須為此資料分割指定處理選項。  
  
 DirectQuery 資料分割有兩個處理選項。 若要設定這個屬性，請在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中使用 [資料分割管理員]，然後選取 [處理選項] 屬性。 下表列出這個屬性的值，並描述當每個值在連接字串上結合 DirectQueryUsage 屬性使用時的影響：  
  
|[連接字串] 屬性|[處理選項] 屬性|注意|  
|------------------------------------|------------------------------------|-----------|  
|DirectQuery|永不處理這個資料分割|當模型使用僅限 DirectQuery 時，不需要進行處理。<br /><br /> 在混合模型中，您可以將 DirectQuery 資料分割設定為永遠不會處理。 例如，如果您正在對一個非常大的資料集進行操作，並且不想要將完整結果新增至快取，則可以指定 DirectQuery 資料分割包含資料表中所有其他資料分割結果的聯集，然後永遠不處理聯集。 傳送至關聯式資料來源的查詢不會受到影響，並且對快取資料執行的查詢會合併來自其他資料分割的資料。|  
|DataView=Sample<br /><br /> 適用於表格式模型使用範例資料檢視|允許處理資料分割|如果模型使用範例資料，您可以處理資料表，在模型設計期間傳回提供視覺提示的篩選資料集。|  
|DirectQueryUsage=InMemory With DirectQuery<br /><br /> 適用於在記憶體中和 DirectQuery 模式組合中執行的表格式 1100 或1103 模型|允許處理資料分割|如果模型使用混合模式，記憶體中和 DirectQuery 資料來源的查詢應該使用相同的分割區。|  
  
## <a name="see-also"></a>另請參閱  
 [資料分割 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/partitions-ssas-tabular.md)  
  
  
