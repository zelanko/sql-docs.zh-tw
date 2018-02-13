---
title: "彙總轉換 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.aggregatetrans.f1
- sql13.dts.designer.aggregationtransformation.aggregations.f1
- sql13.dts.designer.aggregationtransformation.advanced.f1
helpviewer_keywords:
- IsBig property
- aggregate functions [Integration Services]
- Aggregate transformation [Integration Services]
- large data, SSIS transformations
ms.assetid: 2871cf2a-fbd3-41ba-807d-26ffff960e81
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7262db9da133a2aa6f82f501e8dab3228de16efb
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/13/2018
---
# <a name="aggregate-transformation"></a>彙總轉換
  「彙總」轉換會將彙總函式 (例如 Average) 套用至資料行值，並將結果複製到轉換輸出。 除了彙總函式外，該轉換還提供 GROUP BY 子句，讓您用來指定要彙總的群組。  
  
## <a name="operations"></a>作業  
 「彙總」轉換支援下列作業。  
  
|作業|描述|  
|---------------|-----------------|  
|群組依據|將資料集分割成群組。 任何資料類型的資料行都可用於群組。 如需詳細資訊，請參閱 [GROUP BY &#40;Transact-SQL&#41;](../../../t-sql/queries/select-group-by-transact-sql.md)。|  
|SUM|加總資料行中的值。 只能加總具有數值資料類型的資料行。 如需詳細資訊，請參閱 [SUM &#40;Transact-SQL&#41;](../../../t-sql/functions/sum-transact-sql.md)。|  
|平均值|傳回資料行中資料行值的平均。 只能平均具有數值資料類型的資料行。 如需詳細資訊，請參閱 [AVG &#40;Transact-SQL&#41;](../../../t-sql/functions/avg-transact-sql.md)。|  
|Count|傳回群組中的項目數。 如需詳細資訊，請參閱 [COUNT &#40;Transact-SQL&#41;](../../../t-sql/functions/count-transact-sql.md)。|  
|計算相異|傳回群組中唯一非 Null 值的數目。|  
|最小值|傳回群組中的最小值。 如需詳細資訊，請參閱 [MIN &#40;Transact-SQL&#41;](../../../t-sql/functions/min-transact-sql.md)。 與 Transact-SQL MIN 函數的不同之處，在於此作業只適用於數值、日期和時間資料類型。|  
|最大值|傳回群組中的最大值。 如需詳細資訊，請參閱 [MAX &#40;Transact-SQL&#41;](../../../t-sql/functions/max-transact-sql.md)。 與 Transact-SQL MAX 函數的不同之處，在於此作業只適用於數值、日期和時間資料類型。|  
  
 「彙總」轉換處理 Null 值的方式，與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 關聯式 Database Engine 的處理方式相同。 此行為是在 SQL-92 標準中所定義。 適用的規則如下：  
  
-   在 GROUP BY 子句中，處理 Null 的方式與處理其他資料行值的方式相同。 若群組資料行內包含了多個 Null 值，Null 值將放入單一群組內。  
  
-   在 COUNT (資料行名稱) 與 COUNT (DISTINCT 資料行名稱) 函數中，會忽略 Null 值，且結果會排除具名資料行中包含 Null 值的資料列。  
  
-   在 COUNT (*) 函數中，會計算所有資料列，包括含有 Null 值的資料列在內。  
  
## <a name="big-numbers-in-aggregates"></a>彙總中的大數值  
 資料行可能包含因為過大數值或有效位數需求而需要特殊考量的數值。 「彙總」轉換包含 IsBig 屬性，您可以在輸出資料行上設定該屬性，以叫用大型數值或高有效位數數值的特殊處理。 如果資料行值可能超過 40 億，或需要比浮點資料類型更高的有效位數，則 IsBig 應設定為 1。  
  
 將 IsBig 屬性設定為 1，會對彙總轉換的輸出有下列影響：  
  
-   使用 DT_R8 資料類型，而非 DT_R4 資料類型。  
  
-   計數結果會以 DT_UI8 資料類型儲存。  
  
-   相異計數結果會以 DT_UI4 資料類型儲存。  
  
> [!NOTE]  
>  您無法在 GROUP BY、Maximum 或 Minimum 作業所使用的資料行上，將 IsBig 設定為 1。  
  
## <a name="performance-considerations"></a>效能考量  
 「彙總」轉換包含一組屬性，可讓您用來增強轉換的效能。  
  
-   當執行 [群組依據] 作業時，請設定元件的 Keys 或 KeysScale 屬性和元件輸出。 您可以使用 Keys，指定轉換預期要處理的確切索引鍵數目。 (在此內容中，Keys 會參考預期要從 [群組依據] 作業產生的群組數)。您可以使用 KeysScale，指定索引鍵的近似數目。 當您為 Keys 或 KeyScale 指定適當值時，您將會提高效能，因為轉換能夠針對轉換所快取的資料來配置足夠的記憶體。  
  
-   當執行 [相異計數] 作業時，請設定元件的 CountDistinctKeys 或 CountDistinctScale 屬性。 您可以使用 CountDistinctKeys，為相異計數作業指定轉換預期要處理的確切索引鍵數目。 (在此內容中，CountDistinctKeys 會參考預期要從 [相異計數] 作業產生的相異值數目)。您可以使用 CountDistinctScale，為相異計數作業指定索引鍵的近似數目。 當您為 CountDistinctKeys 或 CountDistinctScale 指定適當值時，您將會提高效能，因為轉換能夠針對轉換所快取的資料來配置足夠的記憶體。  
  
## <a name="aggregate-transformation-configuration"></a>彙總轉換組態  
 您可以在轉換、輸出和資料行層級設定「彙總」轉換。  
  
-   在轉換層級上，您可以藉由指定下列值來設定「彙總」轉換的效能：  
  
    -   預期要從 **[群組依據]** 作業產生的群組數。  
  
    -   預期要從 **[相異計數]** 作業產生的相異值數目。  
  
    -   記憶體於彙總期間可以擴充的百分比。  
  
     「彙總」轉換也可以設定為在除數的值為零時產生警告，而非發生失敗。  
  
-   在輸出層級上，您可以藉由指定預期要從 **[群組依據]** 作業產生的群組數來設定「彙總」轉換的效能。 「彙總」轉換支援多個輸出，且每個輸出能以不同的方式設定。  
  
-   在資料行層級上，您可以指定下列其中一個值：  
  
    -   資料行執行的彙總。  
  
    -   彙總的比較選項。  
  
 您也可以藉由指定下列值來設定「彙總」轉換的效能：  
  
-   預期資料行上要從 **[群組依據]** 作業產生的群組數。  
  
-   預期資料行上要從 **[相異計數]** 作業產生的相異值數目。  
  
 如果資料行包含大型數值或是有效位數很高的數值，您也可以將識別欄位指定為 IsBig。  
  
 「彙總」轉換是非同步的，這表示它不會以逐列的方式取用和發行資料， 而是會取用整個資料列集、執行其群組和彙總，然後發行結果。  
  
 這個轉換不會通過任何資料行，但是會在資料流程中為其所發行的資料建立新的資料行。 只有套用彙總函式的輸入資料行，或是轉換用於群組的輸入資料行，才會複製到轉換輸出。 例如，「彙總」轉換輸入可能有三個資料行： **CountryRegion**、 **City**和 **Population**。 轉換會依 **CountryRegion** 資料行來分組，並將 Sum 函數套用至 **Population** 資料行。 因此，輸出不會包含 **City** 資料行。  
  
 您也可以將多個輸出加入「彙總」轉換，並將每個彙總導向不同的輸出。 例如，如果「彙總」轉換套用 Sum 和 Average 函數，則每個彙總可以導向至不同的輸出。  
  
 您可以將多個彙總套用至單一輸入資料行。 例如，如果您要計算名為 **Sales**之輸入資料行的總和與平均值，可以將轉換設定為套用 Sum 和 Average 函數至 **Sales** 資料行。  
  
 「彙總」轉換有一個輸入，以及一個或多個輸出。 它不支援錯誤輸出。  
  
 您可以透過 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 **[進階編輯器]** 對話方塊會反映能以程式設計的方式設定之屬性。 如需有關可以在 **[進階編輯器]** 對話方塊中或以程式設計方式設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [通用屬性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [轉換自訂屬性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 如需有關如何設定屬性的詳細資訊，請按下列其中一個主題：  
  
-   [使用彙總轉換來彙總資料集中的值](../../../integration-services/data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
-   [設定資料流程元件的屬性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [排序合併和合併聯結轉換的資料](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-tasks"></a>相關工作  
 [使用彙總轉換來彙總資料集中的值](../../../integration-services/data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
## <a name="aggregate-transformation-editor-aggregations-tab"></a>彙總轉換編輯器 (彙總索引標籤)
  使用 [彙總轉換編輯器] 對話方塊的 [彙總] 索引標籤，即可指定彙總的資料行與彙總屬性。 您可以套用多個彙總。 此轉換不會產生錯誤輸出。  
  
> [!NOTE]  
>  索引鍵計數、索引鍵小數位數、相異索引鍵計數和相異索引鍵小數位數的選項，若是指定在 [進階] 索引標籤上，就會套用至元件層級；若是指定在 [彙總] 索引標籤的進階畫面上，則會套用至輸出層級；若是指定在 [彙總] 索引標籤底端的資料行清單中，則會套用至資料行層級。  
>   
>  在彙總轉換中， **[索引鍵]** 和 **[索引鍵小數位數]** 會參考預期要從 **[群組依據]** 作業產生的群組數。 **[計算相異索引鍵]** 和 **[計算相異小數位數]** 會參考預期要從 **[相異計數]** 作業產生的相異值數目。  
  
### <a name="options"></a>選項。  
 **進階 / 基本**  
 顯示或隱藏設定多個輸出之多個彙總的選項。 依預設，會隱藏 [進階] 選項。  
  
 **彙總名稱**  
 在 [進階] 顯示中，輸入彙總的易記名稱。  
  
 **群組依據資料行**  
 在 [進階] 顯示中，使用 [可用的輸入資料行] 清單選取要群組的資料行，如下所述。  
  
 **索引鍵小數位數**  
 在 [進階] 顯示中，選擇性地指定彙總可以寫入的大約索引鍵數目。 根據預設，此選項的值為 **[未指定]**。 如果 [索引鍵小數位數] 和 [索引鍵] 屬性都有設定，會優先使用 [索引鍵]。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|[未指定]|不使用 [索引鍵小數位數] 屬性。|  
|低|彙總可寫入大約 500,000 個索引鍵。|  
|中|彙總可寫入大約 5,000,000 個索引鍵。|  
|高|彙總可寫入超過 25,000,000 個索引鍵。|  
  
 **[索引鍵]**  
 在 [進階] 顯示中，選擇性地指定彙總可以寫入的確切索引鍵數目。 如果 [索引鍵小數位數] 和 [索引鍵] 都有指定，會優先使用 [索引鍵]。  
  
 **可用的輸入資料行**  
 使用此資料表中的核取方塊，從可用的輸入資料行清單中選取。  
  
 **輸入資料行**  
 從可用的輸入資料行清單中選取。  
  
 **輸出別名**  
 輸入每個資料行的別名。 預設是輸入資料行的名稱；但是，您可以選擇任何唯一的、描述性名稱。  
  
 **運算**  
 使用下表作為指南，從可用的作業清單中選擇。  
  
|作業|描述|  
|---------------|-----------------|  
|**GroupBy**|將資料集分割成群組。 具有任何資料類型的資料行可用於分組。 如需詳細資訊，請參閱 GROUP BY。|  
|**Sum**|加總資料行中的值。 只能加總具有數值資料類型的資料行。 如需詳細資訊，請參閱 SUM。|  
|**平均值**|傳回資料行中資料行值的平均。 只能平均具有數值資料類型的資料行。 如需詳細資訊，請參閱 AVG。|  
|**Count**|傳回群組中的項目數。 如需詳細資訊，請參閱 COUNT。|  
|**CountDistinct**|傳回群組中唯一非 Null 值的數目。 如需詳細資訊，請參閱 COUNT 和 Distinct。|  
|**最小值**|傳回群組中的最小值。 限制為數值資料類型。|  
|**最大值**|傳回群組中的最大值。 限制為數值資料類型。|  
  
 **比較旗標**  
 如果您選擇 [群組依據]，請使用核取方塊來控制轉換執行比較的方式。 如需字串比較選項的資訊，請參閱 [比較字串資料](../../../integration-services/data-flow/comparing-string-data.md)。  
  
 **Count Distinct Scale**  
 可選擇性地指定彙總可寫入之相異值的近似數目。 根據預設，此選項的值為 **[未指定]**。 如果 [CountDistinctScale] 和 [CountDistinctKeys] 都有指定，會優先使用 [CountDistinctKeys]。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|[未指定]|不使用 **CountDistinctScale** 屬性。|  
|低|彙總可寫入大約 500,000 個相異值。|  
|中|彙總可寫入大約 5,000,000 個相異值。|  
|高|彙總可寫入超過 25,000,000 個相異值。|  
  
 **Count Distinct Keys**  
 可選擇性地指定彙總可寫入之相異值的確實數目。 如果 [CountDistinctScale] 和 [CountDistinctKeys] 都有指定，會優先使用 [CountDistinctKeys]。  
  
## <a name="aggregate-transformation-editor-advanced-tab"></a>彙總轉換編輯器 (進階索引標籤)
  使用 **[彙總轉換編輯器]** 對話方塊的 **[進階]** 索引標籤，即可設定元件屬性、指定彙總，以及設定輸入和輸出資料行的屬性。  
  
> [!NOTE]  
>  索引鍵計數、索引鍵小數位數、相異索引鍵計數和相異索引鍵小數位數的選項，若是指定在 [進階] 索引標籤上，就會套用至元件層級；若是指定在 [彙總] 索引標籤的進階畫面上，則會套用至輸出層級；若是指定在 [彙總] 索引標籤底端的資料行清單中，則會套用至資料行層級。  
>   
>  在彙總轉換中， **[索引鍵]** 和 **[索引鍵小數位數]** 會參考預期要從 **[群組依據]** 作業產生的群組數。 **[計算相異索引鍵]** 和 **[計算相異小數位數]** 會參考預期要從 **[相異計數]** 作業產生的相異值數目。  
  
### <a name="options"></a>選項。  
 **[索引鍵小數位數]**  
 選擇性地指定彙總預期的近似索引鍵數目。 轉換時會使用此資訊來最佳化初始快取大小。 根據預設，此選項的值為 **[未指定]**。 如果 **[索引鍵小數位數]** 和 **[索引鍵數目]** 都有指定，會優先使用 **[索引鍵數目]** 。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|[未指定]|不使用 **[索引鍵小數位數]** 屬性。|  
|低|彙總可寫入大約 500,000 個索引鍵。|  
|中|彙總可寫入大約 5,000,000 個索引鍵。|  
|高|彙總可寫入超過 25,000,000 個索引鍵。|  
  
 **[索引鍵數目]**  
 選擇性地指定彙總預期的確實索引鍵數目。 轉換時會使用此資訊來最佳化初始快取大小。 如果 **[索引鍵小數位數]** 和 **[索引鍵數目]** 都有指定，會優先使用 **[索引鍵數目]** 。  
  
 **[計算相異小數位數]**  
 可選擇性地指定彙總可寫入之相異值的近似數目。 根據預設，此選項的值為 **[未指定]**。 如果 **[計算相異小數位數]** 和 **[計算相異索引鍵]** 都有指定，會優先使用 **[計算相異索引鍵]** 。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|[未指定]|不使用 CountDistinctScale 屬性。|  
|低|彙總可寫入大約 500,000 個相異值。|  
|中|彙總可寫入大約 5,000,000 個相異值。|  
|高|彙總可寫入超過 25,000,000 個相異值。|  
  
 **[計算相異索引鍵]**  
 可選擇性地指定彙總可寫入之相異值的確實數目。 如果 **[計算相異小數位數]** 和 **[計算相異索引鍵]** 都有指定，會優先使用 **[計算相異索引鍵]** 。  
  
 **自動擴充因數**  
 使用介於 1 到 100 之間的值，指定記憶體於彙總期間可以擴充的百分比。 根據預設，此選項的值為 **25%**。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 轉換](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
