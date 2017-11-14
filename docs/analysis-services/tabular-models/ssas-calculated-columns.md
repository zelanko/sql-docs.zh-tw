---
title: "導出資料行 (SSAS 表格式) |Microsoft 文件"
ms.custom: 
ms.date: 10/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e1011278-556d-4984-b01d-a37f8a33b304
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: dd20fe12af6f1dcaf378d737961bc2ba354aabe5
ms.openlocfilehash: 3c36cd3b55617c7ca6c20c244a9488227a2f6ff5
ms.contentlocale: zh-tw
ms.lasthandoff: 10/04/2017

---
# <a name="calculated-columns"></a>導出資料行
  導出資料行，在表格式模型中，可讓您將新資料加入至模型。 您可以建立定義資料行之資料列層級值的 DAX 公式，而不是將值貼上或匯入至資料行中。 然後就可以像是其他任何資料行一樣，在報表、樞紐分析表或樞紐分析圖中使用導出資料行。  
 
  
  
##  <a name="bkmk_understanding"></a> 優點  
 導出資料行中的公式與 Excel 中的公式非常類似。 然而與 Excel 不同的是，您不能為資料表中不同的資料列建立不同的公式，DAX 公式會自動套用到整個資料行。  
  
 當資料行包含公式時，會針對每個資料列計算其值。 當您輸入有效的公式時，即會計算資料行的結果。 資料行值日後將視需要進行重新計算，例如當基礎資料重新整理之時。  
  
 您可以根據量值及其他導出資料行，建立導出資料行。 例如，您可以建立一個導出資料行，以便從文字字串中擷取數字，然後將該數字使用在另一個導出資料行中。  
  
 導出資料行會以現有資料表中的資料為基礎，或透過 DAX 公式建立。 例如，您可以選擇串連值、執行加法、擷取子字串，或比較其他欄位中的值。 若要加入導出資料行，模型中至少必須有一個資料表。  
  
 此範例示範導出資料行中的簡單公式：  
  
```  
=EOMONTH([StartDate],0])  
  
```  
  
 此公式從 StartDate 資料行中擷取月份。 接著再計算資料表中每個資料列的月底值。 第二個參數是指定在 StartDate 當月之前或之後的月數，本例為 0 即表示同一個月份。 例如，若 StartDate 資料行的值為 6/1/2001，則導出資料行的值將是 6/30/2001。  
  
##  <a name="bkmk_naming"></a> Naming a calculated column  
 根據預設，新的導出資料行會加入至資料表中其他資料行的右邊，而且將自動為這類資料行指派預設名稱 **CalculatedColumn1**、 **CalculatedColumn2**，依此類推。 您也可以在資料行上按一下滑鼠右鍵，然後按一下插入資料行，在兩個現有的資料行之間建立新資料行。 您可以按一下再拖曳，來重新排列相同資料表中的資料行，也可以在建立資料行之後，重新命名資料行；但是，您應該注意下列有關變更導出資料行的限制：  
  
-   每個資料行名稱在資料表中都必須是唯一的。  
  
-   在相同的模型中，請避免使用已經用於量值的名稱。 雖然量值和導出資料行可能使用相同的名稱，但是如果這些名稱不是唯一的，可能會發生計算錯誤。 為避免不小心叫用量值，如果指的是資料行，請務必使用完整的資料行參考。  
  
-   當您重新命名導出資料行時，必須手動更新依賴此資料行的所有公式。 只要您不是處於手動更新模式，公式的結果都會自動更新。 不過，這項作業可能需要花一些時間。  
  
-   資料行的名稱中不能使用某些字元。 如需詳細資訊，請參閱 [DAX 語法參考](http://msdn.microsoft.com/en-us/098630f4-7d1d-467e-976c-99b2279430d5)中的＜命名需求＞。  
  
##  <a name="bkmk_perf"></a> Performance of calculated columns  
 導出資料行的公式可能會比量值所使用的公式更耗費資源。 其中一個原因是：導出資料行的結果永遠是針對資料表中的每個資料列計算，而量值僅針對報表、樞紐分析表或樞紐分析圖中所用篩選定義的資料格計算。 例如，包含一百萬個資料列的資料表所擁有的導出資料行永遠都會有一百萬個結果，在效能上也會有對應的影響。 但是，樞紐分析表通常會套用資料列和資料行標題來篩選資料，因此，只會針對樞紐分析表內每一個資料格中的資料子集來計算量值。  
  
 公式通常與該公式中參考之物件具有相依性，例如評估值的其他資料行或運算式。 舉例來說，以另一個資料行做為根據的導出資料行或是包含具有資料行參考之運算式的計算，必須等到評估另一個資料行的結果之後，才會評估出結果。 預設情況下，活頁簿會啟用自動重新整理，因此在更新值或重新整理公式時，任何這類相依性都有可能影響效能。  
  
 為了避免當您在建立導出資料行時發生效能問題，請遵循以下指導方針：  
  
-   分多個步驟建立公式並將結果儲存到資料行，讓您能夠驗證結果及評估效能，而不要建立包含許多複雜相依性的單一公式。  
  
-   修改資料通常需要重新計算導出資料行。 您可以將重新計算模式設定為手動來防止重新計算；不過，如果導出資料行中有任何不正確的值，則該資料行將呈灰色，直到您重新整理與重新計算資料為止。  
  
-   如果您變更或刪除資料表之間的關聯性，使用這些資料表中之資料行的公式將會變成無效。  
  
-   如果您建立包含循環相依性或自我參考相依性的公式，將會發生錯誤。  
  
##  <a name="bkmk_rel_tasks"></a> Related tasks  
  
|主題|Description|  
|-----------|-----------------|  
|[建立導出資料行](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md)|此主題中的工作描述如何將新導出資料行加入至資料表。|  
  
## <a name="see-also"></a>另請參閱  
 [資料表和資料行](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [量值](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [計算](../../analysis-services/tabular-models/calculations-ssas-tabular.md)  
  
  

