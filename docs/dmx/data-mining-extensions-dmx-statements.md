---
description: 資料採礦延伸模組 (DMX) 陳述式參考
title: 資料採礦延伸模組 (DMX) 語句參考 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ce95adec18bd17dce45fdc988b6db92d66383c74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414094"
---
# <a name="data-mining-extensions-dmx-statements"></a>資料採礦延伸模組 (DMX) 陳述式
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  使用中的資料採礦模型 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 牽涉到下列主要工作：  
  
-   建立採礦結構與採礦模型  
  
-   處理採礦結構與採礦模型  
  
-   刪除或卸除採礦結構或採礦模型  
  
-   複製採礦模型  
  
-   瀏覽採礦模型  
  
-   針對採礦模型預測  
  
 您可以使用資料採礦延伸模組 (DMX) 陳述式，以程式來執行每一項工作。  
  
 建立採礦結構與採礦模型  
 使用 [CREATE 挖掘 structure &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md) 語句，將新的採礦結構新增至資料庫。 然後，您可以使用 [ALTER 採礦結構 &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md) 語句，將採礦模型加入至採礦結構。  
  
 使用 [CREATE BUILD model &#40;DMX&#41;](../dmx/create-mining-model-dmx.md) 語句來建立新的採礦模型和相關聯的採礦結構。  
  
 處理採礦結構與採礦模型  
 使用 [INSERT INTO &#40;DMX&#41;](../dmx/insert-into-dmx.md) 語句來處理採礦結構和採礦模型。  
  
 刪除或卸除採礦結構或採礦模型  
 使用 [DELETE &#40;DMX&#41;](../dmx/delete-dmx.md) 語句，從採礦模型或採礦結構中移除所有定型的資料。 使用 [drop &#40;dmx&#41;的採礦結構 ](../dmx/drop-mining-structure-dmx.md) ，或卸載 [&#40;dmx&#41;語句的採礦模型 ](../dmx/drop-mining-model-dmx.md) ，以從資料庫完全移除採礦結構或採礦模型。  
  
 複製採礦模型  
 您可以使用 [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md) 語句，將現有的採礦模型的結構複製到新的採礦模型，以及使用相同的資料來訓練新模型。  
  
 瀏覽採礦模型  
 使用 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md) 語句，流覽資料採礦演算法在模型定型期間計算和儲存在資料採礦模型中的資訊。 與不同的 [!INCLUDE[tsql](../includes/tsql-md.md)] 是，您可以使用數個子句搭配 SELECT 語句來擴充其功能。 這些子句包括 from 的[ \<model> DISTINCT](../dmx/select-distinct-from-model-dmx.md) [ \<model> 。案例](../dmx/select-from-model-cases-dmx.md)，[從 \<model> 。SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)，[從 \<model> 。內容](../dmx/select-from-model-content-dmx.md)和[來源 \<model> 。DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)。  
  
 針對採礦模型預測  
 您可以使用 SELECT 語句的 [預測聯結](../dmx/select-from-model-prediction-join-dmx.md) 子句，建立以現有的採礦模型為基礎的預測。  
  
 您也可以使用匯 [入 &#40;dmx&#41;](../dmx/import-dmx.md) 匯入和匯出模型，並 [匯出 &#40;DMX&#41;](../dmx/export-dmx.md) 語句。  
  
 這些工作分成兩個類別目錄：資料定義陳述式與資料操作陳述式，這會在下表中描述。  
  
|主題|描述|  
|-----------|-----------------|  
|[資料採礦延伸模組 &#40;DMX&#41; 資料定義陳述式](../dmx/dmx-statements-data-definition.md)|資料定義語言 (DDL) 的一部份。 用於定義新的採礦模型 (包括培訓)，或從資料庫卸除現有的採礦模型。|  
|[資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)|資料操作語言 (DML) 的一部份。 用於處理現有的採礦模型，包括瀏覽模型或建立預測。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)  
  
  
