---
title: "效能案例研究 (R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0e902312-ad9c-480d-b82f-b871cd1052d9
caps.latest.revision: 8
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 6
---
# 效能案例研究 (R Services)

為了示範在前面幾節提供的指導方針的效果，執行任何測試使用的飛行資料集的資料表。 

## 測試和範例資料

有六個資料表，但使用 10m 每個資料表中的資料列︰

| 資料表名稱 | Description |
| ---------- | ----------- |
| _航空公司_ | 從原始 xdf 檔案使用的資料轉換 *rxDataStep*。 |
| _airlineWithIntCol_ | *DayOfWeek* 轉換成整數，而不是字串。 也會加入 *rowNum* 資料行。 |
| _airlineWithIndex_ | 相同的資料 *airlineWithIntCol* 資料表，但有一個叢集的索引，使用 *rowNum* 資料行。 |
| _airlineWithPageComp_ | 相同的資料 *airlineWithIndex* 資料表，但已啟用的頁面壓縮。 也會將兩個資料行，加入 *CRSDepHour* 和 *05*, ，它會計算從 *CRSDepTime* 和 *ArrDelay*。 |
| _airlineWithRowComp_ | 相同的資料 *airlineWithIndex* 資料表，但已啟用的資料列壓縮。 也會將兩個資料行，加入 *CRSDepHour* 和 *05* 它會計算從 *CRSDepTime* 和 *ArrDelay*。 
| _airlineColumnar_ | 具有單一叢集索引的單欄式存放區。 此資料表中填入中設定已清除的 csv 檔案。 |

用來執行這一節，以及用於測試的範例資料的連結中所述的測試指令碼位於 [https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)。

每個測試執行六次，第一次執行 （執行時，冷） 的時間已卸除。 若要允許非經常性的極端值，其餘的五個執行的最長時間也已卸除。 用來計算每個測試的平均經過的執行階段原本是四個剩餘的回合的平均值。 每個測試之前產生 R 記憶體回收。 值 *rowsPerRead* 每項測試已設定為 500000。

## 當使用壓縮和單欄式存放區資料表的資料大小

使用壓縮和單欄式資料表，減少資料大小的結果如下︰

| 資料表名稱 | 資料列 | 已保留 | 資料 | index_size | 未使用 | %儲存 （保留） |
| ---------- | ---- | -------- | ---- | ---------- | ------ | ------------------- |
| airlineWithIndex | 10000000 | 2978816 KB | 2972160 KB | 6128 KB | 528 KB | 0 |
| airlineWithPageComp | 10000000 | 625784 KB | 623744 KB | 1352 KB | 了 688 KB | 79% |
| airlineWithRowComp | 10000000 | 1262520 KB | 1258880 KB | 2552 KB | 1088 KB | 58% |
| airlineColumnar | 9999999 | 201992 KB | 201624 KB | n/a | 368 KB | 93% |

## 使用 vs 的整數。在公式中的字串

在此實驗中， `rxLinMod` 航空公司表中使用 (其中 *DayOfWeek* 是一個字串) 和 *airlineWithIndex* (其中 *DayOfWeek* 是整數)。 第一種情況， `colInfo` 用來指定因素層級 (`Monday`, ，`Tuesday`, ，...)。 第二個，如 `colInfo` 未指定。 在這兩種情況下，使用相同的公式。 所使用的公式是 `ArrDelay ~ CRSDepTime + DayOfWeek`。 下列的結果會清楚地顯示使用整數 vs 字串的好處︰

| 資料表名稱 | 測試名稱 | 平均時間 |
| ---------- | --------- | ------------ |
| 航空公司 | FactorCol | 10.72 |
| airlineWithIntCol | IntCol | 3.4475 |

## 使用壓縮

在此實驗中， `rxLinMod` 使用 *airlineWithIndex*, ，*airlineWithPageComp*, ，和 *airlineWithRowComp* 資料表。 所有資料表都使用相同的公式和查詢。 

| 資料表名稱 | 測試名稱 | numTasks | 平均時間 |
| ---------- | --------- | -------- | ------------ |
| airlineWithIndex | NoCompression | 1 | 5.6775 |
| &nbsp; | &nbsp; | 4 | 5.1775 |
| airlineWithPageComp | PageCompression | 1 | 6.7875 |
| &nbsp; | &nbsp; | 4 | 5.3225 |
| airlineWithRowComp | RowCompression | 1 | 6.1325 |
| &nbsp; | &nbsp; | 4 | 5.2375 |

請注意，單獨的壓縮 (*numTasks* 設為 1，) 似乎不在此範例中，幫助，增加的 CPU 處理壓縮會減少 IO 時間補償。 不過，在測試執行時以平行方式藉由設定 *numTasks* 為 4，減少的平均時間。 較大的資料集，可能會更明顯地壓縮的效果。 壓縮會取決於資料集和值，因此實驗可能需要判斷效果壓縮對您的資料集。

## 避免轉換函式

在此實驗中， `rxLinMod` airlineWithIndex 資料表及未使用的轉換函式搭配使用。  

| 測試名稱 | 平均時間 |
| --------- | ------------ |
| WithTransformation | 5.1675 |
| WithoutTransformation | 4.7 |

請注意，沒有時間改進時不使用轉換函式 （使用預先計算並保存在資料表的資料行）。 如果有許多的多個轉換和資料集很大 （> 100 萬），就會大很多省下的。

## 使用單欄式存放區

在此實驗中， `rxLinMod` airlineWithIndex 和 airlineColumnar 資料表搭配使用而不使用任何轉換。 結果會指出單欄式存放區可以執行效能優於資料列存放區。 會有較大的資料集 （> 100 萬） 上的效能顯著的差異。  

| 資料表名稱 | 測試名稱 |平均時間 |
| ---------- | --------- | ------------ |
| airlineWithIndex | 資料列存放區 | 4.67 |
| airlineColumnar | ColStore | 4.555 |

## Cube 參數的效果

在此實驗中， `rxLinMod` 航空公司表使用其中 `DayOfWeek` 會儲存為字串。 所使用的公式是 `ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime`。 結果清楚地顯示，使用 `cube` 參數有助於效能。 

| 測試名稱 | Cube 參數 | numTasks | 平均時間 | 一個資料列的預測 (ArrDelay_Pred) |
| --------- | -------------- | -------- | ------------ | ------------------------------- |
| CubeArgEffect | `cube = F` | 1 | 91.0725 | 9.959204 |
| &nbsp; | &nbsp; | 4 | 44.09 | 9.959204 |
| &nbsp; | `cube = T` | 1 | 21.1125 | 9.959204 |
| &nbsp; | &nbsp; | 4 | 8.08 | 9.959204 |

## RxDTree 的 maxDepth 的效果

在此實驗中， `rxDTree` airlineColumnar 資料表搭配使用。 數個不同的值，如 *maxDepth* 用來示範如何影響執行的階段的複雜性。 隨著深度增加，以指數方式增加的節點總數，已耗用時間會大幅增加。 這項測試 *numTasks* 已設為 4。

| 測試名稱 | maxDepth | 平均時間 |
| --------- | -------- | ------------ |
| TreeDepthEffect | 1 | 10.1975 |
| &nbsp; | 2 | 13.2575 |
| &nbsp; | 4 | 19.27 |
| &nbsp; | 8 | 45.5775 |
| &nbsp; | 16 | 339.54 |

## 電源選項的效果

在此實驗中， `rxLinMod` airlineWithIntCol 表 Windows 已設定為平衡以及高效能的電源選項時使用。 所有測試， *numTasks* 已設為 1。 測試已執行過 6 次，且已執行兩次下這兩個電源選項] 以使用平衡 」 電源選項會呈現結果的變化。 結果顯示的數字是更一致且高效能的電源選項更快。 

__高效能__ 電源選項︰

| 測試名稱 | 執行 # | 經過時間 | 平均時間 |
| --------- | ----- | ------------ | ------------ |
| IntCol | 1 | 3.57 秒 | &nbsp; |
| &nbsp; | 2 | 3.45 秒 | &nbsp; |
| &nbsp; | 3 | 3.45 秒 | &nbsp; |
| &nbsp; | 4 | 3.55 秒 | &nbsp; |
| &nbsp; | 5 | 3.55 秒 | &nbsp; |
| &nbsp; | 6 | 3.45 秒 | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.475 |
| &nbsp; | 1 | 3.45 秒 | &nbsp; |
| &nbsp; | 2 | 3.53 秒 | &nbsp; |
| &nbsp; | 3 | 3.63 秒 | &nbsp; |
| &nbsp; | 4 | 3.49 秒 | &nbsp; |
| &nbsp; | 5 | 3.54 秒 | &nbsp; |
| &nbsp; | 6 | 3.47 秒 | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.5075 |

__平衡__ 電源選項︰

| 測試名稱 | 執行 # | 經過時間 | 平均時間 |
| --------- | ----- | ------------ | ------------ |
| IntCol | 1 | 3.89 秒 | &nbsp; |
| &nbsp; | 2 | 4.15 秒 | &nbsp; |
| &nbsp; | 3 | 3.77 秒 | &nbsp; |
| &nbsp; | 4 | 5 秒 | &nbsp; |
| &nbsp; | 5 | 3.92 秒 | &nbsp; |
| &nbsp; | 6 | 3.8 秒 | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.91 |
| &nbsp; | 1 | 3.82 秒 | &nbsp; |
| &nbsp; | 2 | 3.84 秒 | &nbsp; |
| &nbsp; | 3 | 3.86 秒 | &nbsp; |
| &nbsp; | 4 | 4.07 秒 | &nbsp; |
| &nbsp; | 5 | 4.86 秒 | &nbsp; |
| &nbsp; | 6 | 3.75 秒 | &nbsp; |
| &nbsp; | &nbsp; | &nbsp; | 3.88 |

## 使用預存的模型的預測

在此實驗中，會建立模型，並將其儲存至資料庫中。 然後會從資料庫和建立使用記憶體 （本機計算內容） 中的一個資料列的資料框架的預測載入預存的模型。 訓練、 儲存和載入模型和預測所花費的時間如下所示。 這顯然是更快的方法來進行預測。 測試結果會顯示將儲存模型及載入模型，並預測所花費的時間。 

| 資料表名稱 | 測試名稱 | 平均回應時間 （定型模型） | 儲存負載模型的時機 |
| ---------- | --------- | ----- | ----- |
| 航空公司 | SaveModel | 21.59 | 2.08 | 
| &nbsp; | LoadModelAndPredict | &nbsp; |  2.09 （包含要預測的時間） |


## 效能疑難排解

本節中使用測試會產生輸出檔的每次執行使用 *reportProgress* 參數，傳遞至測試，以值 `3`。 主控台輸出導向到輸出目錄中的檔案。 輸出檔包含有關在 IO、 轉換時間和運算時間所花費的時間。 這些時間是適用於疑難排解和診斷。 測試指令碼處理這些想出的平均時間透過執行各種不同的執行時間。 這些測試指令碼和技巧也可以用於疑難排解問題，在使用 rx 分析函式時您 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 例如，以下顯示範例的時間執行。 感興趣的主要執行時間是總時間 （IO 時間） 的讀取和轉換 （負擔在設定程序來計算） 的時間。

    Running IntCol Test. Using airlineWithIntCol table.  
        run  1  took  3.66  seconds  
        run  2  took  3.44  seconds  
        run  3  took  3.44  seconds  
        run  4  took  3.44  seconds  
        run  5  took  3.45  seconds  
        run  6  took  3.75  seconds  

    Average Time:  3.4425  
                    metric   time    pct 
    1           Total time 3.4425 100.00 
    2 Overall compute time 2.8512  82.82 
    3      Total read time 2.5378  73.72 
    4      Transition time 0.5913  17.18 
    5    Total non IO time 0.3134   9.10 
 
 ## 另請參閱
 [SQL Server R 服務效能微調的指南](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 [R 服務的 SQL Server 組態](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [R 和資料最佳化](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)