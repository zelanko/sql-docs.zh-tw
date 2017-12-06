---
title: "使用 R 將 SQL Server 資料視覺化 (資料科學深入探討) | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 05/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 10def0b3-9b09-4df9-b8aa-69516f7d7659
caps.latest.revision: "14"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fa42e69f1e376dc528b3385ca3c4be38fea4710b
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="visualize-sql-server-data-using-r"></a>使用 R 將 SQL Server 資料視覺化

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中的增強套件包含的多個函數，已針對延展性和平行處理功能進行最佳化。 這些函數通常都使用 *rx* 或 *Rx*做為字首。

在此逐步解說中，您將使用 **rxHistogram** 函數，依性別檢視 _creditLine_ 資料行中的值分佈。

## <a name="visualize-data-using-rxhistogram"></a>使用 rxHistogram 資料視覺化

1. 使用下列 R 程式碼呼叫 rxHistogram 函式，並傳遞公式和資料來源。 您可以先在本機執行此作業，查看預期的結果及所需時間。
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    就內部而言，rxHistogram 呼叫 rxCube 函式，其隨附於**RevoScaleR**封裝。 RxCube 函式會輸出包含一個資料行在公式中，指定每個變數的單一清單 （或資料框架） 再加上計算資料行。
    
2. 現在，設定計算內容至遠端 SQL Server 電腦，然後再次執行 rxHistogram。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
 
3. 結果會完全相同，因為您使用相同的資料來源；不過，計算是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上執行。  然後，系統會將結果傳回到您的本機工作站以進行繪製。
   
![長條圖結果](media/rsql-sue-histogramresults.jpg "長條圖結果")

4. 您也可以呼叫 rxCube 函式，並將結果傳遞給 R 繪圖函式。  例如，下列範例會使用 rxCube 來計算平均值*fraudRisk*每個組合*numTrans*和*numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    若要指定用來計算群組平均值的群組，請使用 `F()` 標記法。 在此範例中， `F(numTrans):F(numIntlTrans)` 指出應將 _numTrans_ 和 _numIntlTrans_ 變數中的整數視為類別目錄變數，且每個整數值代表一個層級。
  
    由於資料來源 *sqlFraudDS* 已經新增低層級和高層級 (使用 *colInfo* 參數)，因此長條圖中會自動使用這些層級。
  
5. 預設為 rxCube 的傳回值*rxCube 物件*，用來表示交叉資料表。 不過，您可以使用 **rxResultsDF** 函數，將結果轉換成資料框架，以輕鬆用於 R 標準繪圖函數中。
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    > [!TIP]
    > 
    > 請注意 rxCube 函式包含選擇性引數， *returnDataFrame* = TRUE，您可以使用來將結果直接轉換至資料框架。 例如：
    >   
    > `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
    >   
    > 不過，rxResultsDF 的輸出會比較簡單，並保留來源資料行的名稱。
  
6. 最後，執行下列程式碼來建立使用熱門地圖`levelplot`函數從**斜格紋**隨附於所有的 R 散發的封裝。
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **結果**
  
    ![散佈圖結果](media/rsql-sue-scatterplotresults.jpg "散佈圖結果")
  
即使只是透過這個快速的分析，您都可以看出詐騙的風險會隨著交易數目和國際交易數目增加而提高。

有關 rxCube 函式和交叉資料表的一般詳細資訊，請參閱[資料摘要](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-summaries)。

## <a name="next-step"></a>下一個步驟

[建立模型](../../advanced-analytics/tutorials/deepdive-create-models.md)

## <a name="previous-step"></a>上一個步驟

[第 2 課︰建立及執行 R 指令碼](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)


