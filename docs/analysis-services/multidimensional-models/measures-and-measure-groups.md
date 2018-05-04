---
title: 量值和量值群組 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 171ee494ad3d4b89ab923b4b2f0a769da0d7012c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="measures-and-measure-groups"></a>量值和量值群組
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Cube 包含「量值群組」中的「量值」、商務邏輯，以及可以在求取量值所提供之數值資料的值時提供內容的維度集合。 量值和量值群組均為 Cube 的重要元件。 Cube 的存在至少須具備其中一項元件。  
  
 本主題描述 [量值](#bkmk_measure) 和 [量值群組](#bkmk_mg)。 它也包含下表，表內有連結可供取得建立及設定量值和量值群組的程序步驟。  
  
|**連結**|**說明**|  
|--------------|---------------------|  
|[多維度模型中建立量值和量值群組](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)|您有數種方法可以用來建立量值和量值群組。|  
|[設定量值屬性](../../analysis-services/multidimensional-models/configure-measure-properties.md)|若是使用 [Cube 精靈] 啟動您的 Cube 時，您必須變更彙總方法、套用資料格式、設定是否要在用戶端應用程式中顯示量值，或可能需要在彙總值之前，先新增量值運算式來操作資料。|  
|[設定量值群組屬性](../../analysis-services/multidimensional-models/configure-measure-group-properties.md)|在多維度模型中，量值群組等於來源資料倉儲中的事實資料表。 量值群組的屬性可讓您指定在量值群組層級之快取行為、儲存體及處理指示詞的整體運作方式。 磁碟分割設定有部分取決於您對量值群組物件設定的屬性。|  
|[使用彙總函式](../../analysis-services/multidimensional-models/use-aggregate-functions.md)|了解可以指派給量值的彙總方法。|  
|[定義局部加總行為](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md)|局部加總行為是指對於某些維度有效，但對其他維度無效的彙總。 常見範例為銀行帳戶餘額。 您可能只想要依客戶及地區彙總餘額，而不需要依時間。 例如，您不想要加總同一帳戶連續數日期間的餘額。 若要定義局部加總行為，請使用 [加入商業智慧精靈]。|  
|[連結量值群組](../../analysis-services/multidimensional-models/linked-measure-groups.md)|重新安排現有的量值群組中在同一資料庫或不同 Analysis Services 資料庫中之其他 Cube 中的用途。|  
  
##  <a name="bkmk_measure"></a> 量值  
 量值代表包含可彙總之可量化資料 (通常是數值) 的資料行。 量值代表組織活動的某些層面，可以貨幣表示 (例如營收、獲利或成本)，或以計數表示 (庫存量、員工數、客戶數或訂單數)，或以結合商務邏輯之更複雜的計算方式表示。  
  
 每個 Cube 至少須有一個量值，但大部分 Cube 都有許多量值，有時數量可達數百。 從結構來說，量值通常會對應到事實資料表中的來源資料行，再由資料行提供用以載入量值的值。 或者，您也可以使用 MDX 定義量值。  
  
 量值取決於內容，並會在查詢中所含之維度成員所指定的內容中，對數值資料作業。 例如，計算「轉售商銷售」的量值由 **Sum** 運算子執行，其會將查詢中所含之每個維度成員的銷售金額加總。 無論查詢指定個別的產品、彙總成一個類別，或是依時間或地理位置切割，量值所衍生的作業對查詢中所含的維度而言，都必須有效。  
  
 在此範例中，「轉售商銷售」會彙總成「銷售領域」階層的各種層級。  
  
 ![樞紐分析表與量值和維度叫出](../../analysis-services/multidimensional-models/media/ssas-keyconcepts-pivot1-measures-dimensions.png "具有量值和維度叫出樞紐分析表")  
  
 當事實資料表中所含的數值來源資料，也包含查詢中所用之維度資料表的指標時，量值會產生有效的結果。 在轉售商銷售的範例中，每個資料列除了儲存銷售金額之外，也會儲存對產品資料表、日期資料表中或銷售領域資料表的指標，如此才能正確地解析包含這些維度成員的查詢。  
  
 若量值與查詢中所用的維度無關會如何？ 一般而言，Analysis Services 會顯示的預設量值，而所有成員的該值皆相同。 在此範例中，「網際網路銷售」(計算客戶使用線上型錄直接下單的銷售) 與銷售組織無關。  
  
 ![顯示重複的樞紐分析表的量值](../../analysis-services/multidimensional-models/media/ssas-unrelatedmeasure.PNG "樞紐分析表顯示重複的量值")  
  
 若要降低用戶端應用程式發生這些行為的機率，可以在相同的資料庫中建立多個 Cube 或檢視方塊，並確認每個 Cube 或檢視方塊只包含相關的物件。 您必須檢查量值群組 (對應至事實資料表) 與維度之間的關聯性。  
  
##  <a name="bkmk_mg"></a> 量值群組  
 在 Cube 中，量值是根據它們的基礎事實資料表分組成量值群組。 量值群組是用來建立維度與量值的關聯。 量值群組也會用於與其彙總行為具有相異計數的量值； 將每一個相異計數量值放入其本身的量值群組時，會最佳化彙總處理。  
  
 簡單的 <xref:Microsoft.AnalysisServices.MeasureGroup> 物件由群組名稱、儲存模式及處理模式等基本資訊組成。 其同時包含其構成部分：量值、維度，以及組成量值群組組合的資料分割。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的 cube](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)   
 [多維度模型中建立量值和量值群組](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)  
  
  
