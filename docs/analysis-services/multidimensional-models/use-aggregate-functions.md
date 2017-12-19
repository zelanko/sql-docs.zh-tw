---
title: "使用彙總函式 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: aggregate functions [Analysis Services]
ms.assetid: c42166ef-b75c-45f4-859c-09a3e9617664
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 7a146e6be066f8669757d15f5fe76ac67c5c172b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="use-aggregate-functions"></a>使用彙總函式
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]當維度用來配量的量值時，量值是一起該維度包含的階層彙總。 而總和行為則視指定給量值的彙總函式而定 對於大多數包含數值資料的量值而言，彙總函式是 **Sum**。 量值的值會依據所使用的階層層級而加總為不同的數量。  
  
 在 Analysis Services 中，您建立的每個量值都有一個彙總函數可以決定量值的作業。 預先定義的彙總類型包括 **Sum**、**Min**、**Max**、**Count****Distinct Count** 及更多其他特殊函數。 或者，您如需透過複雜或自訂的公式執行彙總，可以建置 MDX 計算，而不使用預先建置的彙總函數。 例如，若您要定義百分比值的量值，可以在 MDX 中使用導出量值。 請參閱 [CREATE MEMBER 陳述式 &#40;MDX&#41;](../../mdx/mdx-data-definition-create-member.md)。  
  
 由 [Cube 精靈] 建立的量值，會在定義量值時，為其指派彙總類型。 若來源資料行包含數值資料，彙總類型一律為 **Sum**。 無論來源資料行的資料類型為何，一律會指派**Sum** 。 例如，若是使用 [Cube 精靈] 建立量值，並將其從事實資料表提取到所有資料行，則即使來源為日期時間資料行，所得量值的彙總類型都會是 **Sum**。 對於精靈所建立的量值，請務必檢查預先指派的彙總方法，以確認彙總函數的適用性。  
  
 您可以使用 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] 或 MDX 指派或變更任一個 Cube 定義的彙總方法。 如需進一步指示，請參閱[在多維度模型中建立量值和量值群組](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)或 [Aggregate &#40;MDX&#41;](../../mdx/aggregate-mdx.md)。  
  
##  <a name="AggFunction"></a> 彙總函式  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供多種函數可以彙總量值群組中所含維度的量值。 彙總函式的「加總性」決定如何在 Cube 的所有維度中來彙總量值。 彙總函式分成三個加總性層級：  
  
 加法  
 此為加總量值，也稱為完全加總量值，可將包含該量值的量值群組中，所包含的所有維度加以彙總，而且沒有限制。  
  
 局部加總  
 局部加總量值可將包含該量值的量值群組中，所包含的部分而非全部維度加以彙總。 例如，可將地理維度中代表存貨可用數量的量值加以彙總，以產生所有倉庫可用的總數量，但不能將時間維度的量值加以彙總，因為該量值代表可用數量的定期快照集。 彙總時間維度的量值可能會產生不正確的結果。 如需詳細資訊，請參閱 [定義局部加總行為](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md) 。  
  
 非加法  
 非加總量值無法將包含該量值的量值群組中，所包含的任何維度加以彙總。 反之，必須在代表量值的 Cube 中，個別計算每一個資料格的量值。 例如，傳回百分比的導出量值 (例如獲利率) 無法從任何維度的子成員之百分比值彙總而得。  
  
 下表列出 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的彙總函式，並描述函數的加總性和預期輸出。  
  
|彙總函式|加總性|傳回值|  
|--------------------------|----------------|--------------------|  
|**Sum**|加法|針對所有子成員，計算值的總和。 這是預設的彙總函式。|  
|**Count**|加法|擷取所有子成員的計數。|  
|**Min**|局部加總|擷取所有子成員的最低值。|  
|**Max**|局部加總|擷取所有子成員的最高值。|  
|**DistinctCount**|非加法|擷取所有唯一子成員的計數。 如需詳細資訊，請參閱下一節中的 [About Distinct Count measure](../../analysis-services/multidimensional-models/use-aggregate-functions.md#bkmk_distinct) (關於相異計數量值)。|  
|**無**|非加法|不執行彙總，而且針對包含該量值的量值群組，直接從事實資料表提供維度中分葉與非分葉成員的所有值。 如果無法從成員的事實資料表讀取任何值，該成員的值就會設定為 Null。|  
|**ByAccount**|局部加總|針對帳戶維度中的成員，依據指派給帳戶類型的彙總函式來計算彙總。 如果量值群組中沒有帳戶類型維度，則視為 **None** 彙總函式。<br /><br /> 如需帳戶維度的詳細資訊，請參閱 [建立父子式類型維度的財務帳戶](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)。|  
|**AverageOfChildren**|局部加總|針對所有非空白的子成員，計算值的平均。|  
|**FirstChild**|局部加總|擷取第一個子成員的值。|  
|**LastChild**|局部加總|擷取最後一個子成員的值。|  
|**FirstNonEmpty**|局部加總|擷取第一個非空白之子成員的值。|  
|**LastNonEmpty**|局部加總|擷取最後一個非空白之子成員的值。|  
  
##  <a name="bkmk_distinct"></a> About Distinct Count measure  
 具有 **彙總函式** 屬性值 **Distinct Count** 的量值稱為相異計數量值。 相異計數量值可用來統計事實資料表中某維度之最低層級成員的出現次數。 因為當成員出現多次時，此計數便會不同，所以只會計算一次。 相異計數量值只會用在專用的量值群組中。 最佳做法是將相異計數量值放入設計師內建的專用量值群組，以最佳化效能。  
  
 相異計數量值通常是用來針對維度的每一個成員判斷，另一個維度有多少相異的最低層級成員共用事實資料表中的資料列； 例如在 Sales Cube 中，針對每一個客戶及客戶群組判斷，已經購買了多少數量的相異產品？ (也就是說，對於客戶維度的每一個成員而言，產品維度中有多少相異的最低層級成員共用事實資料表中的資料列？)或者在 Internet Site Visits Cube 中，針對每一個網站造訪者及網站造訪者群組判斷，此網際網路網站上造訪過的相異網頁數目。 (也就是說，對於網站造訪者維度的每一個成員而言，網頁維度中有多少相異的最低層級成員共用事實資料表中的資料列？)在每一個範例中，第二個維度的最低層級成員是由相異計數量值所統計。  
  
 此分析種類不需要限制為兩個維度； 事實上，相異計數量值可由 Cube 中的任何維度組合 (包括含有已計算成員的維度) 加以區隔及切割。  
  
 計算成員的相異計數量值是以事實資料表中的外部索引鍵資料行為根據  (也就是說，此量值的**來源資料行**屬性會識別此資料行。)這個資料行會聯結可識別相異計數量值所計算之成員的維度資料表資料行。  
  
## <a name="see-also"></a>請參閱  
 [量值和量值群組](../../analysis-services/multidimensional-models/measures-and-measure-groups.md)   
 [MDX 函數參考 &#40;MDX &#41;](../../mdx/mdx-function-reference-mdx.md)   
 [定義局部加總行為](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md)  
  
  
