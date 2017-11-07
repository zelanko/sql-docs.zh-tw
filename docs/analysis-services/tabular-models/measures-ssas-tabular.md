---
title: "量值 |Microsoft 文件"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27ec8f99-e9ef-44c9-a83f-f7c88e128ad3
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 38b7467cd4ad765d651ea0ebe4ad57c278c987a1
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="measures"></a>量值
  在表格式模型中，量值是透過報表用戶端內使用的 DAX 公式所建立的計算。 量值會以使用者在報表用戶端應用程式中選取的欄位、篩選及交叉分析篩選器為依據來計算。  
  
##  <a name="bkmk_understanding"></a> 優點  
 量值可以用標準彙總函式 (例如 AVERAGE、COUNT 或 SUM) 做為基礎，或者，您也可以使用 DAX 自行定義公式。 除了公式以外，每個量值都具備由量值資料類型定義的屬性，如名稱、資料表詳細資料、格式及小數位數。  
  
 若模型中已定義量值，使用者即可將其加入報表或樞紐分析表。 視檢視方塊與角色而定，量值會與其相關聯的資料表一起出現在欄位清單中，且可供模型中的所有使用者使用。 量值通常會在事實資料表中建立；不過，量值也可以獨立於其相關聯的資料表之外。  
  
 請務必了解導出資料行和量值的基本差異。 在導出資料行中，會使用公式來計算資料行中每一個資料列的值。 例如，在 FactSales 資料表中，名為 TotalProfit 的導出資料行含有下列公式，以計算 FactSales 資料表中每個資料列 (一個資料列一筆銷售) 總收益的值：  
  
```  
=[SalesAmount] - [TotalCost] - [ReturnAmount]  
```  
  
 導出資料行 TotalProfit 和任何其他資料行一樣，皆可在報表用戶端中使用。  
  
 而量值則是以使用者選取為依據，也就是樞紐分析表或報表中設定的篩選內容來計算值。 例如，FactSales 資料表中的量值是用下列公式建立的：  
  
```  
Sum of TotalProfit: =SUM([TotalProfit])  
```  
  
 某位使用 Excel 的銷售分析人員想知道某產品類別目錄的總收益。 每個產品類別目錄包含多項產品。 銷售分析人員選取 ProductCategoryName 資料行並將其加入至樞紐分析表的 [資料列標籤] 篩選視窗；每個產品類別目錄的資料列即會顯示在樞紐分析表中。 然後，使用者選取 TotalProfit 量值的總和。 量值會依預設加入 [值] 篩選視窗。 量值會計算總收益的總和並顯示每個產品類別目錄的結果。 接著，銷售分析人員即可使用交叉分析篩選器來篩選每個產品類別目錄的總收益總和，例如，加入 CalendarYear 做為交叉分析篩選器，依年度檢視每個產品類別的總收益總和。  
  
|ProductCategoryName|TotalProfit 總和|  
|-------------------------|------------------------|  
|音響產品|$2,731,061,308.69|  
|相機和攝影機|$620,623,675.75|  
|電腦|$392,999,044.59|  
|電視及錄影機|$946,989,702.51|  
|**總計**|**$4,691,673,731.53**|  
  
##  <a name="bkmk_def_mg"></a> Defining measures by using the measure grid  
 量值是在設計階段透過使用模型設計師中的量值方格而建立的。 每一個資料表都有量值方格。 根據預設，量值方格會顯示在模型設計師中的每一個資料表下方。 您也可以選擇不檢視特定資料表的量值方格。 若要切換資料表的量值方格顯示，請按一下 **[資料表]** 功能表，然後按一下 **[顯示量值方格]**。  
  
 在量值方格中，您可用下列方式建立量值：  
  
-   按一下量值方格中的空白資料格，然後在公式列中輸入 DAX 公式。 按 ENTER 完成公式，量值即會出現在量值方格中。  
  
-   若要使用標準彙總函式建立量值，請按一下資料行，然後按一下工具列上的 [自動加總] 按鈕 (∑)，再按一下標準彙總函式。 標準彙總包括：Sum、Average、Count、DistinctCount、Max、Min。 使用 [自動加總] 按鈕建立的量值一律會出現在量值方格資料行的下方。  
  
 依預設，使用自動加總時，量值的名稱會由相關聯的資料行名稱所定義，後面接著冒號和公式。 您可在公式列或 [屬性] 視窗的 **[量值名稱]** 屬性設定中變更名稱。 使用自訂公式建立量值時，您可在公式列中輸入名稱，後接冒號和公式，或者，您可在 [屬性] 視窗的 **[量值名稱]** 屬性設定中輸入名稱。  
  
 務必命名量值謹慎。 量值名稱會和相關聯的資料表一起出現在報表用戶端的欄位清單中。 KPI 也會根據基底量值來命名。 量值不得與模型中任何資料表的任何資料行名稱相同。  
  
> [!TIP]  
>  您可以將多個資料表中的量值群組到一個資料表中，其方式是建立空白資料表，然後將量值移到其中或是在其中建立新的量值。 請牢記，當您參考其他資料表中的資料行時，可能必須在 DAX 公式中包含資料表名稱。  
  
 若模型已定義檢視方塊，量值不會自動加入這些檢視方塊中。 您必須使用 [檢視方塊] 對話方塊，手動將量值加入檢視方塊中。 若要進一步了解，請參閱[檢視方塊](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)。  
  
##  <a name="bkmk_properties"></a> 量值屬性  
 每個量值都有定義的屬性。 您可在 [屬性] 視窗中，編輯量值屬性以及相關聯的資料行屬性。 量值具有下列屬性：  
  
|屬性|預設設定|說明|  
|--------------|---------------------|-----------------|  
|**說明**|空白|量值的說明。 報表用戶端中不會顯示量值說明。|  
|**格式**|在公式運算式中，自動從參考資料行的資料類型來判斷。|量值的格式。 例如，貨幣或百分比。|  
|**公式**|量值建立時，在公式列中輸入的公式。|量值的公式。|  
|**[量值名稱]**|若使用自動加總，量值名稱後面會接著資料行名稱和冒號。 若是輸入自訂公式，請輸入名稱，後面接著冒號，然後再輸入公式。|量值名稱就是報表用戶端欄位清單中顯示的名稱。|  
  
##  <a name="bkmk_KPI"></a> 使用 KPI 中的量值  
 KPI (關鍵效能指標) 是由「基底」值定義，而基底值是由「目標」值 (由量值或絕對值定義) 對應的量值來定義。 KPI 也包括 *「狀態」*(Status)，其為計算基底值和目標值之間的臨界值，且會以圖形格式顯示。 商務專業人士常常利用 KPI 來識別重要商務標準中的趨勢。  
  
 任何量值都可以做為 KPI 的基底量值。 若要建立 KPI，請在量值方格中，以滑鼠右鍵按一下量值，然後按一下 [建立 KPI]。 [關鍵效能指標] 對話方塊隨即出現，您即可在其中指定目標值 (由量值或絕對值來定義)，及定義狀態臨界值和圖形類型。 若要進一步了解，請參閱[Kpi](../../analysis-services/tabular-models/kpis-ssas-tabular.md)。  
  
##  <a name="bkmk_rel_tasks"></a> 相關工作  
  
|主題|Description|  
|-----------|-----------------|  
|[建立及管理量值](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md)|描述如何使用模型設計師中的量值方格，建立及管理量值。|  
  
## <a name="see-also"></a>另請參閱  
 [Kpi](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [建立及管理 Kpi](../../analysis-services/tabular-models/create-and-manage-kpis-ssas-tabular.md)   
 [導出資料行](../../analysis-services/tabular-models/ssas-calculated-columns.md)  
  
  

