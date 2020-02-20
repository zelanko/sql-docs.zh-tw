---
title: 彙總函式參考 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: db6542ee-02d0-4073-90e6-cba8f9510fbb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 243f895c22621c3f83fab38a5bab47d1f7b7b490
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "68893764"
---
# <a name="report-builder-functions---aggregate-functions-reference"></a>報表產生器函式 - 彙總函式參考
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
  
 若要決定函數的有效範圍，請參閱個別的函數參考主題。 如需詳細資訊和範例，請參閱 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="CalculatingAggregates"></a> 內建彙總函式  
 下列內建函數會針對預設範圍或具名範圍，計算非 Null 數值資料集的摘要值。  
  
|**Function**|**說明**|  
|------------------|---------------------|  
|[Avg](../../reporting-services/report-design/report-builder-functions-avg-function.md)|傳回運算式指定的所有非 Null 數值的平均值 (在給定範圍中評估)。|  
|[Count](../../reporting-services/report-design/report-builder-functions-count-function.md)|傳回運算式指定的非 Null 值的計數 (在給定範圍的內容中評估)。|  
|[CountDistinct](../../reporting-services/report-design/report-builder-functions-countdistinct-function.md)|傳回運算式指定的所有非 Null 相異值的計數 (在給定範圍的內容中評估)。|  
|[Max](../../reporting-services/report-design/report-builder-functions-max-function.md)|傳回運算式指定的所有非 Null 數值的最大值 (在給定範圍的內容中)。 這個函數可用來指定圖表軸的最大值以控制刻度。|  
|[Min](../../reporting-services/report-design/report-builder-functions-min-function.md)|傳回運算式指定的所有非 Null 數值的最小值 (在給定範圍的內容中)。 這個函數可用來指定圖表軸的最小值以控制刻度。|  
|[StDev](../../reporting-services/report-design/report-builder-functions-stdev-function.md)|傳回運算式指定的所有非 Null 數值的標準差 (在給定範圍中評估)。|  
|[StDevP](../../reporting-services/report-design/report-builder-functions-stdevp-function.md)|傳回運算式指定的所有非 Null 數值的母體標準差 (在給定範圍的內容中評估)。|  
|[Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md)|傳回運算式指定之所有非 Null 數值的總和 (在給定範圍中評估)。|  
|[Union](../../reporting-services/report-design/report-builder-functions-union-function.md)|傳回運算式所指定之 **SqlGeometry** 或 **SqlGeography** 類型的所有非 Null 空間資料值聯集 (在給定的範圍中評估)。|  
|[Var](../../reporting-services/report-design/report-builder-functions-var-function.md)|傳回運算式指定的所有非 Null 數值的變異數 (在給定範圍中評估)。|  
|[VarP](../../reporting-services/report-design/report-builder-functions-varp-function.md)|傳回運算式指定的所有非 Null 數值的母體擴展變異數 (在給定範圍的內容中評估)。|  
  
 ![搭配 [回到頁首] 連結使用的箭頭圖示](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "與 [回到頁首] 連結搭配使用的箭頭圖示")[回到頁首]  
  
##  <a name="Restrictions"></a> 內建欄位、集合和彙總函式的限制  
 下表摘要列出您可以加入運算式之報表位置的限制，該運算式包含全域內建集合的參考。  
  
|報表中的位置|欄位|參數|ReportItems|PageNumber<br /><br /> TotalPages|DataSource<br /><br /> DataSet|變數|RenderFormat|  
|------------------------|------------|----------------|-----------------|-------------------------------|----------------------------|---------------|------------------|  
|頁首<br /><br /> 頁尾|是|是|最多一個<br /><br /> 附註 1|是|是|是|是|  
|body|是<br /><br /> 附註 2|是|只有目前範圍或包含範圍內的項目<br /><br /> 附註 3|否|是|是|是|  
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
  
 ![搭配 [回到頁首] 連結使用的箭頭圖示](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "與 [回到頁首] 連結搭配使用的箭頭圖示")[回到頁首]  
  
##  <a name="NestedRestrictions"></a> 巢狀彙總的限制  
 下表摘要列出彙總函式可以將其他彙總函式指定為巢狀彙總的限制。  
  
|Context|RunningValue|RowNumber|First<br /><br /> Last|Previous|Sum 和其他 Presort 函數|ReportItem 彙總|查閱函數|彙總函式|  
|-------------|------------------|---------------|--------------------|--------------|-------------------------------------|---------------------------|----------------------|------------------------|  
|執行中的值|否|否|否|否|是|否|是|否|  
|First<br /><br /> Last|否|否|否|否|是|否|否|否|  
|Previous|是|是|是|否|是|否|是|否|  
|Sum 和其他 Presort 函數|否|否|否|否|是|否|是|否|  
|ReportItem 彙總|否|否|否|否|否|否|否|否|  
|查閱函數|是|是<br /><br /> 附註 1|是<br /><br /> 附註 1|是<br /><br /> 附註 1|是<br /><br /> 附註 1|是<br /><br /> 附註 1|否|否|  
|彙總函式|否|否|否|否|否|否|否|否|  
  
-   **附註 1：** 如果查閱函數未包含在彙總內，則只有查閱函數的 *Source* 運算式中才允許彙總函式。 查閱函數的 *Destination* 或 *Result* 運算式內不允許彙總函式。  
  
 ![搭配 [回到頁首] 連結使用的箭頭圖示](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "與 [回到頁首] 連結搭配使用的箭頭圖示")[回到頁首]  
  
##  <a name="CalculatingRunningValues"></a> 計算執行值  
 下列的內建函數會計算資料集的執行值。 **RowNumber** 與 **RunningValue** 類似，會傳回累加包含範圍內每個資料列的計數執行值。 這些函數的範圍參數必須指定包含範圍，這個範圍控制何時重新開始計數。  
  
|**Function**|**說明**|  
|------------------|---------------------|  
|[RowNumber](../../reporting-services/report-design/report-builder-functions-rownumber-function.md)|傳回指定範圍中資料列數的執行計數。 **RowNumber** 函數從 1 開始重新計數，而不是 0。|  
|[RunningValue](../../reporting-services/report-design/report-builder-functions-runningvalue-function.md)|傳回運算式指定的所有非 Null 數值的執行彙總 (在給定範圍中評估)。|  
  
 ![搭配 [回到頁首] 連結使用的箭頭圖示](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "與 [回到頁首] 連結搭配使用的箭頭圖示")[回到頁首]  
  
##  <a name="RetrievingRowCounts"></a> 擷取資料列計數  
 下列的內建函數會計算給定範圍中的資料列數。 這個函數可用來計算所有資料列的數目，包括具有 Null 值的資料列。  
  
|**Function**|**說明**|  
|------------------|---------------------|  
|[CountRows](../../reporting-services/report-design/report-builder-functions-countrows-function.md)|傳回指定之範圍中的資料列數目，包括具有 Null 值的資料列。|  
  
 ![搭配 [回到頁首] 連結使用的箭頭圖示](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "與 [回到頁首] 連結搭配使用的箭頭圖示")[回到頁首]  
  
##  <a name="LookupFunctions"></a> 從其他資料集查詢值  
 下列查閱函數會從指定的資料集擷取值。  
  
|**Function**|**說明**|  
|------------------|---------------------|  
|[Lookup 函數](../../reporting-services/report-design/report-builder-functions-lookup-function.md)|從指定之運算式的資料集傳回值。|  
|[LookupSet 函式](../../reporting-services/report-design/report-builder-functions-lookupset-function.md)|從指定之運算式的資料集傳回一組值。|  
|[Multilookup 函式](../../reporting-services/report-design/report-builder-functions-multilookup-function.md)|從包含名稱/值組的資料集傳回第一組符合某一組名稱的值。|  
  
 ![搭配 [回到頁首] 連結使用的箭頭圖示](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "與 [回到頁首] 連結搭配使用的箭頭圖示")[回到頁首]  
  
##  <a name="RetrievingPostsortValues"></a> 擷取與排序相依的值  
 下列的內建函數會傳回給定範圍內的第一個、最後一個或上一個值。 這些函數會視資料值的排序次序而定。 舉例而言，這些函數可用來尋找頁面上的第一個和最後一個值，以建立字典樣式的頁首。 **Previous** 可用來比較特定範圍內一個資料列的值與上一個資料列的值，以在資料表中找出年的成長百分比。  
  
|**Function**|**說明**|  
|------------------|---------------------|  
|[第一個](../../reporting-services/report-design/report-builder-functions-first-function.md)|傳回所指定運算式給定範圍中的第一個值。|  
|[最後一個](../../reporting-services/report-design/report-builder-functions-last-function.md)|傳回所指定運算式給定範圍中的最後一個值。|  
|[[上一步]](../../reporting-services/report-design/report-builder-functions-previous-function.md)|傳回某個項目在指定之範圍內上一個執行個體的值或指定的彙總值。|  
  
 ![搭配 [回到頁首] 連結使用的箭頭圖示](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "與 [回到頁首] 連結搭配使用的箭頭圖示")[回到頁首]  
  
##  <a name="RetrievingServerAggregates"></a> 擷取伺服器彙總  
 下列的內建函數將從資料提供者擷取自訂彙總。 例如，您可以使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源類型擷取在資料來源伺服器上計算的彙總，以用於群組頁首。  
  
|**Function**|**說明**|  
|------------------|---------------------|  
|[彙總](../../reporting-services/report-design/report-builder-functions-aggregate-function.md)|傳回指定之運算式的自訂彙總，由資料提供者定義。|  
  
 ![搭配 [回到頁首] 連結使用的箭頭圖示](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "與 [回到頁首] 連結搭配使用的箭頭圖示")[回到頁首]  
  
##  <a name="TestingforScope"></a> 測試範圍  
 下列的內建函數會測試報表項目目前的內容，查看是否為特定範圍的成員。  
  
|函式|描述|  
|--------------|-----------------|  
|[InScope](../../reporting-services/report-design/report-builder-functions-inscope-function.md)|指出目前項目的執行個體是否在指定的範圍內。|  
  
 ![搭配 [回到頁首] 連結使用的箭頭圖示](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "與 [回到頁首] 連結搭配使用的箭頭圖示")[回到頁首]  
  
##  <a name="RetrievingRecursiveLevel"></a> 擷取遞迴層級  
 下列的內建函數會在系統處理遞迴階層時，擷取目前的層級。 在文字方塊中以 **Padding** 屬性使用此函數的結果，即可控制遞迴群組視覺階層的縮排層級。 如需詳細資訊，請參閱[建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
|函式|描述|  
|--------------|-----------------|  
|[Level](../../reporting-services/report-design/report-builder-functions-level-function.md)|傳回遞迴階層中之目前所在的層級。|  
  
 ![搭配 [回到頁首] 連結使用的箭頭圖示](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "與 [回到頁首] 連結搭配使用的箭頭圖示")[回到頁首]  
  
## <a name="see-also"></a>另請參閱  
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
