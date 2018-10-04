---
title: 彙總函式參考 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: db6542ee-02d0-4073-90e6-cba8f9510fbb
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 7d3a6843ea643ac447e42a1d78f5f2e7b3bc09da
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48194114"
---
# <a name="aggregate-functions-reference-report-builder-and-ssrs"></a>彙總函式參考 (報表產生器及 SSRS)
  若要在報表中加入彙總值，您可以在運算式中使用內建彙總函式。 數值欄位的預設彙總函式是 SUM。 您可以編輯運算式，並使用不同的內建彙總函式或指定不同的範圍。 範圍會識別用於計算的資料集。  
  
 當報表處理器結合報表資料和報表配置時，將會評估每一個報表項目的運算式。 當您檢視報表的每一頁時，您會在轉譯的報表項目中看到每一個運算式的結果。  
  
 下表列出可以包含在運算式中的內建函數類別：  
  
-   [內建彙總函式](#CalculatingAggregates)  
  
-   [內建欄位、集合和彙總函式的限制](#Restrictions)  
  
-   [巢狀彙總的限制](#NestedRestrictions)  
  
-   [計算執行值](#CalculatingRunningValues)  
  
-   [擷取資料列計數](#RetrievingRowCounts)  
  
-   [從其他資料集查詢值](#LookupFunctions)  
  
-   [擷取與排序相依的值](#RetrievingPostsortValues)  
  
-   [擷取伺服器彙總](#RetrievingServerAggregates)  
  
-   [擷取遞迴層級](#RetrievingRecursiveLevel)  
  
-   [測試範圍](#TestingforScope)  
  
 若要決定函數的有效範圍，請參閱個別的函數參考主題。 如需詳細資訊和範例，請參閱[Expression Scope for Totals，Aggregates，and Built-in Collections&#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="CalculatingAggregates"></a> 內建彙總函式  
 下列內建函數會針對預設範圍或具名範圍，計算非 Null 數值資料集的摘要值。  
  
|**函數**|**說明**|  
|------------------|---------------------|  
|[Avg](report-builder-functions-avg-function.md)|傳回運算式指定的所有非 Null 數值的平均值 (在給定範圍中評估)。|  
|[計數](report-builder-functions-count-function.md)|傳回運算式指定的非 Null 值的計數 (在給定範圍的內容中評估)。|  
|[CountDistinct](report-builder-functions-countdistinct-function.md)|傳回運算式指定的所有非 Null 相異值的計數 (在給定範圍的內容中評估)。|  
|[Max](report-builder-functions-max-function.md)|傳回運算式指定的所有非 Null 數值的最大值 (在給定範圍的內容中)。 這個函數可用來指定圖表軸的最大值以控制刻度。|  
|[Min](report-builder-functions-min-function.md)|傳回運算式指定的所有非 Null 數值的最小值 (在給定範圍的內容中)。 這個函數可用來指定圖表軸的最小值以控制刻度。|  
|[Stdev 函數](report-builder-functions-stdev-function.md)|傳回運算式指定的所有非 Null 數值的標準差 (在給定範圍中評估)。|  
|[StDevP](report-builder-functions-stdevp-function.md)|傳回運算式指定的所有非 Null 數值的母體標準差 (在給定範圍的內容中評估)。|  
|[Sum](report-builder-functions-sum-function.md)|傳回運算式指定之所有非 Null 數值的總和 (在給定範圍中評估)。|  
|[Union](report-builder-functions-union-function.md)|傳回運算式所指定之 `SqlGeometry` 或 `SqlGeography` 類型的所有非 Null 空間資料值聯集 (在給定的範圍中評估)。|  
|[Var](report-builder-functions-var-function.md)|傳回運算式指定的所有非 Null 數值的變異數 (在給定範圍中評估)。|  
|[VarP](report-builder-functions-varp-function.md)|傳回運算式指定的所有非 Null 數值的母體擴展變異數 (在給定範圍的內容中評估)。|  
  
##  <a name="Restrictions"></a> 內建欄位、集合和彙總函式的限制  
 下表摘要列出您可以加入運算式之報表位置的限制，該運算式包含全域內建集合的參考。  
  
|報表中的位置|欄位|參數|ReportItems|PageNumber<br /><br /> TotalPages|DataSource<br /><br /> DataSet|變數|RenderFormat|  
|------------------------|------------|----------------|-----------------|-------------------------------|----------------------------|---------------|------------------|  
|頁首<br /><br /> 頁尾|是|是|最多一個<br /><br /> 附註 1|是|是|是|是|  
|本文|是<br /><br /> 附註 2|是|只有目前範圍或包含範圍內的項目<br /><br /> 附註 3|否|是|是|是|  
|報表參數|否|只有清單中稍早的參數<br /><br /> 附註 4|否|否|否|否|否|  
|欄位|是|是|否|否|否|否|否|  
|查詢參數|否|是|否|否|否|否|否|  
|群組運算式|是|是|否|否|是|否|否|  
|排序運算式|是|是|否|否|是|是<br /><br /> 附註 5|否|  
|篩選運算式|是|是|否|否|是|是<br /><br /> 附註 6|否|  
|程式碼|否|是<br /><br /> 附註 7|否|否|否|否|否|  
|報表語言|否|是|否|否|否|否|否|  
|變數|是|是|否|否|是|目前範圍或包含的範圍|否|  
|彙總|是|是|只有在頁首和頁尾|只有在報表項目彙總內|是|否|否|  
|查閱函數|是|是|是|否|是|否|否|  
  
-   **附註 1：** ReportItems 必須存在於轉譯的報表頁面中，否則其值會是 Null。 如果報表項目的可見性取決於評估為 False 的運算式，則表示報表項目不存在於頁面上。  
  
-   **附註 2。** 如果欄位參考用於群組範圍中，而且欄位參考未包含在群組運算式中，則表示未定義該欄位的值，除非此範圍內只有一個值。 若要指定值，請使用 First 或 Last 及群組範圍。  
  
-   **附註 3。** 包含 ReportItems 之參考的運算式可以針對相同群組範圍或包含的群組範圍內的其他 ReportItems 指定值。  
  
-   **附註 4。** 之前參數的屬性值可能為 null。  
  
-   **附註 5。** 僅限成員排序。 無法在資料區排序運算式內使用。  
  
-   **附註 6。** 僅限成員篩選。 無法在資料區或資料集篩選運算式內使用。  
  
-   **附註 7。** 處理程式碼區塊之前沒有初始化參數集合，所以無法使用方法來控制初始化的參數。  
  
-   **附註 8。** 除了 Count 與 CountDistinct 以外的所有彙總之資料類型，所有的值都必須是相同的資料類型或 null。  
  
##  <a name="NestedRestrictions"></a> 巢狀彙總的限制  
 下表摘要列出彙總函式可以將其他彙總函式指定為巢狀彙總的限制。  
  
|內容|RunningValue|RowNumber|第一個<br /><br /> 最後一個|Previous|Sum 和其他 Presort 函數|ReportItem 彙總|查閱函數|彙總函式|  
|-------------|------------------|---------------|--------------------|--------------|-------------------------------------|---------------------------|----------------------|------------------------|  
|執行中的值|否|否|否|否|是|否|是|否|  
|第一個<br /><br /> 最後一個|否|否|否|否|是|否|否|否|  
|Previous|是|是|是|否|是|否|是|否|  
|Sum 和其他 Presort 函數|否|否|否|否|是|否|是|否|  
|ReportItem 彙總|否|否|否|否|否|否|否|否|  
|查閱函數|是|是<br /><br /> 附註 1|是<br /><br /> 附註 1|是<br /><br /> 附註 1|是<br /><br /> 附註 1|是<br /><br /> 附註 1|否|否|  
|彙總函式|否|否|否|否|否|否|否|否|  
  
-   **附註 1：** 如果查閱函數未包含在彙總內，則只有查閱函數的 *Source* 運算式中才允許彙總函式。 查閱函數的 *Destination* 或 *Result* 運算式內不允許彙總函式。  
  
##  <a name="CalculatingRunningValues"></a> 計算執行值  
 下列的內建函數會計算資料集的執行值。 `RowNumber` 與 `RunningValue` 類似，會傳回累加包含範圍內每個資料列的計數執行值。 這些函數的範圍參數必須指定包含範圍，這個範圍控制何時重新開始計數。  
  
|**函數**|**說明**|  
|------------------|---------------------|  
|[RowNumber](report-builder-functions-rownumber-function.md)|傳回指定範圍中資料列數的執行計數。 `RowNumber`函數開始重新計數為 1，不是 0。|  
|[RunningValue](report-builder-functions-runningvalue-function.md)|傳回運算式指定的所有非 Null 數值的執行彙總 (在給定範圍中評估)。|  
  
##  <a name="RetrievingRowCounts"></a> 擷取資料列計數  
 下列的內建函數會計算給定範圍中的資料列數。 這個函數可用來計算所有資料列的數目，包括具有 Null 值的資料列。  
  
|**函數**|**說明**|  
|------------------|---------------------|  
|[CountRows](report-builder-functions-countrows-function.md)|傳回指定之範圍中的資料列數目，包括具有 Null 值的資料列。|  
  
##  <a name="LookupFunctions"></a> 從其他資料集查詢值  
 下列查閱函數會從指定的資料集擷取值。  
  
|**函數**|**說明**|  
|------------------|---------------------|  
|[Lookup 函數](report-builder-functions-lookup-function.md)|從指定之運算式的資料集傳回值。|  
|[LookupSet 函式](report-builder-functions-lookupset-function.md)|從指定之運算式的資料集傳回一組值。|  
|[Multilookup 函式](report-builder-functions-multilookup-function.md)|從包含名稱/值組的資料集傳回第一組符合某一組名稱的值。|  
  
##  <a name="RetrievingPostsortValues"></a> 擷取與排序相依的值  
 下列的內建函數會傳回給定範圍內的第一個、最後一個或上一個值。 這些函數會視資料值的排序次序而定。 舉例而言，這些函數可用來尋找頁面上的第一個和最後一個值，以建立字典樣式的頁首。 使用`Previous`來比較特定範圍內的前一個資料列的值的一個資料列中的值，例如，若要尋找資料表中的年份值的百分比年。  
  
|**函數**|**說明**|  
|------------------|---------------------|  
|[第一個](report-builder-functions-first-function.md)|傳回所指定運算式給定範圍中的第一個值。|  
|[最後一個](report-builder-functions-last-function.md)|傳回所指定運算式給定範圍中的最後一個值。|  
|[[上一步]](report-builder-functions-previous-function.md)|傳回某個項目在指定之範圍內上一個執行個體的值或指定的彙總值。|  
  
##  <a name="RetrievingServerAggregates"></a> 擷取伺服器彙總  
 下列的內建函數將從資料提供者擷取自訂彙總。 例如，您可以使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源類型擷取在資料來源伺服器上計算的彙總，以用於群組頁首。  
  
|**函數**|**說明**|  
|------------------|---------------------|  
|[Aggregate](report-builder-functions-aggregate-function.md)|傳回指定之運算式的自訂彙總，由資料提供者定義。|  
  
##  <a name="TestingforScope"></a> 測試範圍  
 下列的內建函數會測試報表項目目前的內容，查看是否為特定範圍的成員。  
  
|函數|描述|  
|--------------|-----------------|  
|[InScope](report-builder-functions-inscope-function.md)|指出目前項目的執行個體是否在指定的範圍內。|  
  
##  <a name="RetrievingRecursiveLevel"></a> 擷取遞迴層級  
 下列的內建函數會在系統處理遞迴階層時，擷取目前的層級。 使用這個函式的結果`Padding`控制遞迴群組視覺階層的縮排層級的文字方塊中的屬性。 如需詳細資訊，請參閱[建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
|函數|描述|  
|--------------|-----------------|  
|[Level](report-builder-functions-level-function.md)|傳回遞迴階層中之目前所在的層級。|  
  
## <a name="see-also"></a>另請參閱  
 [在報表中的運算式會使用&#40;報表產生器及 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Expression Scope for Totals，Aggregates，and Built-in Collections&#40;報表產生器及 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
