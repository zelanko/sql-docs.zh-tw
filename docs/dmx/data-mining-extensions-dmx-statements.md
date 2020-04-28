---
title: 資料採礦延伸模組（DMX）語句參考 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a7a9c18599d13c4db510793a1d75c85bbb7a829
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68070858"
---
# <a name="data-mining-extensions-dmx-statements"></a>資料採礦延伸模組 (DMX) 陳述式
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在中[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]使用資料採礦模型包含下列主要工作：  
  
-   建立採礦結構與採礦模型  
  
-   處理採礦結構與採礦模型  
  
-   刪除或卸除採礦結構或採礦模型  
  
-   複製採礦模型  
  
-   瀏覽採礦模型  
  
-   針對採礦模型預測  
  
 您可以使用資料採礦延伸模組 (DMX) 陳述式，以程式來執行每一項工作。  
  
 建立採礦結構與採礦模型  
 使用 [[建立採礦結構 &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md)語句，將新的採礦結構新增至資料庫。 然後，您可以使用[ALTER 採礦結構 &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md)語句，將採礦模型加入至採礦結構。  
  
 使用 [[建立採礦模型 &#40;DMX&#41;](../dmx/create-mining-model-dmx.md)語句來建立新的採礦模型和相關聯的採礦結構。  
  
 處理採礦結構與採礦模型  
 使用[INSERT INTO &#40;DMX&#41;](../dmx/insert-into-dmx.md)語句來處理採礦結構和採礦模型。  
  
 刪除或卸除採礦結構或採礦模型  
 使用[DELETE &#40;DMX&#41;](../dmx/delete-dmx.md)語句，從「採礦模型」或「採礦結構」中移除所有定型的資料。 使用[DROP 採礦結構 &#40;dmx&#41;](../dmx/drop-mining-structure-dmx.md)或卸載[模型 &#40;dmx&#41;](../dmx/drop-mining-model-dmx.md)語句，以從資料庫完全移除採礦結構或採礦模型。  
  
 複製採礦模型  
 使用[SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md)語句，將現有的採礦模型結構複製到新的採礦模型，並使用相同的資料來定型新模型。  
  
 瀏覽採礦模型  
 使用[SELECT &#40;DMX&#41;](../dmx/select-dmx.md)語句，流覽資料採礦演算法在模型定型期間計算並儲存在資料採礦模型中的資訊。 與相似之[!INCLUDE[tsql](../includes/tsql-md.md)]處是，您可以使用數個子句搭配 SELECT 語句來擴充其功能。 這些子句包含[不同于\<model> 的模型>](../dmx/select-distinct-from-model-dmx.md) [ \<。案例](../dmx/select-from-model-cases-dmx.md)，[從\<模型>。SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)，[從\<模型>。內容](../dmx/select-from-model-content-dmx.md)和[從\<模型>。DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)。  
  
 針對採礦模型預測  
 請使用 SELECT 語句的[預測聯結](../dmx/select-from-model-prediction-join-dmx.md)子句來建立以現有的採礦模型為基礎的預測。  
  
 您也可以使用匯[入 &#40;dmx&#41;](../dmx/import-dmx.md)匯入和匯出模型，並[匯出 &#40;dmx&#41;](../dmx/export-dmx.md)語句。  
  
 這些工作分成兩個類別目錄：資料定義陳述式與資料操作陳述式，這會在下表中描述。  
  
|主題|描述|  
|-----------|-----------------|  
|[資料採礦延伸模組 &#40;DMX&#41; 資料定義陳述式](../dmx/dmx-statements-data-definition.md)|資料定義語言 (DDL) 的一部份。 用於定義新的採礦模型 (包括培訓)，或從資料庫卸除現有的採礦模型。|  
|[資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)|資料操作語言 (DML) 的一部份。 用於處理現有的採礦模型，包括瀏覽模型或建立預測。|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; Operator Reference &#40;的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41; 語法元素的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-syntax-elements.md)  
  
  
