---
title: "定義資料來源檢視 (Analysis Services) |Microsoft 文件"
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
- names [Analysis Services], data source views
- name matching criteria [Analysis Services]
- Data Source View Wizard
- data source views [Analysis Services], creating
ms.assetid: 0bae4ee4-1742-40e9-bebe-17c788854484
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3aae9714c37d9bd4272add2829d4cdef8f2d9c9d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="defining-a-data-source-view-analysis-services"></a>定義資料來源檢視 (Analysis Services)
  資料來源檢視包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多維度資料庫物件 (也就是 Cube、維度和採礦結構) 所使用之結構描述的邏輯模型。 資料來源檢視就是統一維度模型 (UDM) 和採礦結構所使用之結構描述元素的中繼資料定義，並以 XML 格式儲存。 資料來源檢視：  
  
-   包含代表從一個或多個基礎資料來源選取之物件的中繼資料，或用來產生基礎關聯式資料存放區的中繼資料 (如果您是遵循由上而下產生結構描述的方法)。  
  
-   可建立在一個或多個資料來源上，讓您定義用來整合多個來源中資料的多維度和資料採礦物件。  
  
-   包含不存在於基礎資料來源中，而存在於基礎資料來源以外地方的關聯性、主索引鍵、物件名稱、導出資料行和查詢。  
  
-   無法讓用戶端應用程式看到或查詢。  
  
 DSV 是多維度模型的必要元件。 大部分 Analysis Services 開發人員在模型設計階段的早期建立 DSV，根據提供基礎資料的外部關聯式資料庫至少產生一個 DSV。 不過，您也可以在後期建立 DSV，在建立維度和 Cube 之後產生結構描述和基礎資料庫結構。 這第二個方法有時稱為由上而下設計，而且經常用於建立原型和分析模型。 當您使用這個方法時，您可以使用 [結構描述產生精靈] 根據 Analysis Services 專案或資料庫中定義的 OLAP 物件，來建立基礎資料來源檢視和資料來源物件。 不論如何及何時建立 DSV，每個模型必須先有一個 DSV，您才能進行處理。  
  
 本主題包含下列各節：  
  
 [資料來源檢視構成要素](#bkmk_dsvdef)  
  
 [使用 [資料來源檢視精靈] 建立 DSV](#bkmk_startWiz)  
  
 [指定關聯性的名稱比對準則](#bkmk_NameMatch)  
  
 [加入次要資料來源](#bkmk_secondaryDS)  
  
##  <a name="bkmk_dsvdef"></a> 資料來源檢視構成要素  
 資料來源檢視包含下列項目：  
  
-   名稱和描述。  
  
-   擷取自一或多個資料來源 (最多包含整個結構描述) 之結構描述的任何子集定義包含下列內容：  
  
    -   資料表名稱。  
  
    -   資料行名稱。  
  
    -   資料類型。  
  
    -   Null 屬性。  
  
    -   資料行長度。  
  
    -   主索引鍵。  
  
    -   主索引鍵 - 外部索引鍵關聯性。  
  
-   來自基礎資料來源之結構描述的註解，包括下列內容：  
  
    -   資料表、檢視和資料行的易記名稱。  
  
    -   從一或多個資料來源傳回資料行的具名查詢 (顯示為結構描述中的資料表)。  
  
    -   從資料來源傳回資料行的具名計算 (顯示為資料表或檢視中的資料行)。  
  
    -   邏輯主索引鍵 (如果基礎資料表中未定義主索引鍵，或是檢視或具名查詢中未包含主索引鍵，便需要邏輯主索引鍵)。  
  
    -   資料表、檢視和具名查詢之間的邏輯主索引鍵 - 外部索引鍵關聯性。  
  
##  <a name="bkmk_startWiz"></a> 使用 [資料來源檢視精靈] 建立 DSV  
 若要建立 DSV，請從 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的 [方案總管] 中執行 [資料來源檢視精靈]。  
  
> [!NOTE]  
>  或者，您可以先建構維度和 Cube，然後使用 [結構描述產生] 精靈產生模型的 DSV。 如需詳細資訊，請參閱[結構描述產生精靈 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/schema-generation-wizard-analysis-services.md)。  
  
1.  在方案總管中，以滑鼠右鍵按一下 [資料來源檢視] 資料夾，然後按一下 [新增資料來源檢視]。  
  
2.  指定新的或現有的資料來源物件，以提供連接資訊給外部關聯式資料庫 (在精靈中只能選取一個資料來源)。  
  
3.  在相同的頁面上，按一下 **[進階]** 選取特定結構描述、套用篩選或排除資料表關聯性資訊。  
  
     **選擇結構描述**  
  
     如果是包含多個結構描述的極大型資料來源，您可以在不含空格的逗號分隔清單中選取要使用的結構描述。  
  
     **擷取關聯性**  
  
     您可以清除 [進階資料來源檢視選項] 對話方塊中的 **[擷取關聯性]** 核取方塊，刻意省略資料表關聯性資訊，以便在資料來源檢視設計工具中手動建立資料表關聯性。  
  
4.  **篩選可用的物件**  
  
     若可用的物件清單中含有大量物件，您可套用簡單的篩選並指定字串為選取準則，以縮減清單。 例如，若您輸入 **dbo** 並按一下 **[篩選]** 按鈕，則只有以 "dbo" 開頭的項目會顯示在 **[可用的物件]** 清單中。 篩選也可以是部分字串 (例如 "sal" 會傳回 sales 和 salary)，但不能包括多個字串或運算子。  
  
5.  如果是未定義資料表關聯性的關聯式資料來源， **[名稱比對]** 頁面會出現，讓您可以選取適當的名稱比對方法。 如需詳細資訊，請參閱本主題中的＜ [指定關聯性的名稱比對準則](#bkmk_NameMatch) ＞一節。  
  
##  <a name="bkmk_secondaryDS"></a> 加入次要資料來源  
 當您定義包含多個資料來源中資料表、檢視或資料行的資料來源檢視時，您加入到此資料來源檢視之物件所來自的第一個資料來源會指定為主要資料來源 (在定義主要資料來源之後就不能變更)。 在根據單一資料來源中的物件定義資料來源檢視之後，可以加入其他資料來源中的物件。  
  
 如果 OLAP 處理或資料採礦查詢需要在單一查詢中使用多個資料來源中的資料，則主要資料來源必須支援使用 **OpenRowset**的遠端查詢。 一般來說，這會是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源。 例如，如果您設計一個 OLAP 維度，其中包含繫結至多個資料來源中資料行的屬性，則在處理期間， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 將會建構 **OpenRowset** 查詢來擴展這個維度。 但是，如果可以擴展 OLAP 物件，或是從單一資料來源解析資料採礦查詢，將不會建構 **OpenRowset** 查詢。 在某些情況下，您或許可以定屬性之間的屬性關聯性，如此便不需要 **OpenRowset** 查詢。 如需屬性關聯性的詳細資訊，請參閱 [屬性關聯性](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)、 [在資料來源檢視中加入或移除資料表或檢視 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md) 和 [定義屬性關聯性](../../analysis-services/multidimensional-models/attribute-relationships-define.md)的 [方案總管] 中執行 [資料來源檢視精靈]。  
  
 若要從次要資料來源新增資料表及資料行，請按兩下 [方案總管] 中的 DSV，以在資料來源檢視設計工具中開啟 DSV，然後使用 [新增/移除資料表] 對話方塊，以包含專案中定義之其他資料來源的物件。 如需詳細資訊，請參閱 [在資料來源檢視中加入或移除資料表或檢視 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)的 [方案總管] 中執行 [資料來源檢視精靈]。  
  
##  <a name="bkmk_NameMatch"></a> 指定關聯性的名稱比對準則  
 當您建立 DSV 時，會依據資料來源中的外部索引鍵條件約束，來建立資料表之間的關聯性。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 引擎必須要有這些關聯性，才能建構適當的 OLAP 處理和資料採礦查詢。 不過，有時候含有多個資料表的資料來源並沒有外部索引鍵條件約束。 如果資料來源沒有任何外部索引鍵條件約束，則「資料來源檢視精靈」會提示您定義您希望精靈嘗試比對不同資料表中資料行名稱的方式。  
  
> [!NOTE]  
>  只有在基礎資料來源中未偵測到任何外部索引鍵關聯性時，才會提示您提供名稱比對準則。 如果有偵測到外部索引鍵關聯性，則會使用偵測到的關聯性，而且您必須手動定義您想要包含在 DSV 中的其他任何關聯性，包括邏輯主索引鍵。 如需詳細資訊，請參閱[在資料來源檢視中定義邏輯關聯性 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-logical-relationships-in-a-data-source-view-analysis-services.md) 和[在資料來源檢視中定義邏輯主索引鍵 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-logical-primary-keys-in-a-data-source-view-analysis-services.md)。  
  
 [資料來源檢視精靈] 會使用您的回應來比對資料行名稱，並在 DSV 中建立不同資料表之間的關聯性。 您可以指定下表所列出的任何一個準則。  
  
|名稱比對準則|說明|  
|----------------------------|-----------------|  
|**與主索引鍵的名稱相同**|來源資料表中的外部索引鍵資料行名稱與目的地資料表中的主索引鍵資料行名稱相同。 例如，外部索引鍵資料行 `Order.CustomerID` 與主索引鍵資料行 `Customer.CustomerID`相同。|  
|**與目的地資料表的名稱相同**|來源資料表中的外部索引鍵資料行名稱與目的地資料表的名稱相同。 例如，外部索引鍵資料行 `Order.Customer` 與主索引鍵資料行 `Customer.CustomerID`相同。|  
|**目的地資料表名稱 + 主索引鍵名稱**|來源資料表中的外部索引鍵資料行名稱與以主索引鍵資料行名稱串連的目的地資料表名稱相同。 允許空格或底線分隔符號。 例如，下列外部-主索引鍵配對全部相符：<br /><br /> `Order.CustomerID` 和 `Customer.ID`<br /><br /> `Order.Customer ID` 和 `Customer.ID`<br /><br /> `Order.Customer_ID` 和 `Customer.ID`|  
  
 您選取的準則會變更 DSV 的 **[NameMatchingCriteria]** 屬性設定。 這個設定會決定精靈加入相關資料表的方式。 若您利用資料來源檢視設計工具來變更資料來源檢視，此規格會決定設計工具如何比對資料行，以建立 DSV 中資料表間的關聯性。 您可以在資料來源檢視設計工具中變更 **[NameMatchingCriteria]** 屬性設定。 如需詳細資訊，請參閱[變更資料來源檢視的屬性 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md)。  
  
> [!NOTE]  
>  完成 [資料來源檢視精靈] 之後，您可以在資料來源檢視設計工具的結構描述窗格中加入或移除關聯性。 如需詳細資訊，請參閱[在資料來源檢視中定義邏輯關聯性 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-logical-relationships-in-a-data-source-view-analysis-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [在資料來源檢視中加入或移除資料表或檢視 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)   
 [定義邏輯主索引鍵中的資料來源檢視 &#40;Analysis Services &#41;](../../analysis-services/multidimensional-models/define-logical-primary-keys-in-a-data-source-view-analysis-services.md)   
 [在資料來源檢視 &#40; 中定義具名的計算Analysis Services &#41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)   
 [在資料來源檢視 &#40; 中定義具名的查詢Analysis Services &#41;](../../analysis-services/multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)   
 [取代的資料表或資料來源檢視 &#40; 中的具名的查詢Analysis Services &#41;](../../analysis-services/multidimensional-models/replace-a-table-or-a-named-query-in-a-data-source-view-analysis-services.md)   
 [在資料來源檢視設計工具 &#40; 中使用圖表Analysis Services &#41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)   
 [瀏覽資料來源檢視 &#40; 中的資料Analysis Services &#41;](../../analysis-services/multidimensional-models/explore-data-in-a-data-source-view-analysis-services.md)   
 [刪除資料來源檢視 &#40;Analysis Services &#41;](../../analysis-services/multidimensional-models/delete-a-data-source-view-analysis-services.md)   
 [在資料來源檢視中重新整理結構描述 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/refresh-the-schema-in-a-data-source-view-analysis-services.md)  
  
  

