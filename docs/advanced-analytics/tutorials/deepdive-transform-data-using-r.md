---
title: "轉換資料使用 R （SQL 與 R 深入探討） |Microsoft 文件"
ms.date: 12/24/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.assetid: 0327e788-94cc-4a47-933b-7c5c027b9208
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: d3dbda505155cb8da1f192b2dc36a6889938ccde
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="transform-data-using-r-sql-and-r-deep-dive"></a>使用 R （SQL 與 R 深入探討） 轉換的資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是資料科學深入探討教學課程中，有關如何使用一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

**RevoScaleR** 套件提供適用於在各種分析階段轉換資料的多個函數：

- **rxDataStep** 可用來建立及轉換資料子集。

- **rxImport** 支援在將資料匯入 XDF 檔案或記憶體內資料框架，或是從中匯入資料時，對資料進行轉換。

- **rxSummary**、 **rxCube**、 **rxLinMod**和 **rxLogit** 函數雖然不是專為資料移動所設計，但全部都支援資料轉換。

在本節中，您會學習如何使用這些函式。 讓我們開始[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)。

## <a name="use-rxdatastep-to-transform-variables"></a>使用 rxDataStep 轉換變數

**rxDataStep** 函數會一次處理一個資料區塊，從一個資料來源讀取並寫入另一個資料來源。 您可以指定要轉換的資料行、要載入的轉換等等。

若要讓此範例的有趣，讓我們使用來自另一個的 R 封裝函數來轉換資料。  **boot** 套件是其中一個「建議」的套件；也就是說， **boot** 會隨附於每個 R 版本，但未在啟動時自動載入。 因此，您搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]執行個體上，應該已提供此套件。

從**開機**封裝，請使用此函式`inv.logit`，它會計算 logit 的反向。 換句話說， `inv.logit` 函數會將 logit 轉換回 [0,1] 刻度的機率。

> [!TIP] 
> 若要取得在這個標尺的預測另一種方式是以設定*類型*參數**回應**rxPredict 原始呼叫中。

1. 開始建立資料來源，以便保存資料的目的地資料表中，為`ccScoreOutput`。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. 加入另一個資料來源，以保存資料的資料表`ccScoreOutput2`。
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    在新的資料表中，儲存從先前的所有變數`ccScoreOutput`資料表，再加上新建立的變數。
  
3. 將計算內容設定為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 使用函數**rxSqlServerTableExists**來檢查是否輸出資料表`ccScoreOutput2`已經存在，而且如果是，使用此函式**rxSqlServerDropTable**以便刪除的資料表。
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")
    ```
  
5. 呼叫 **rxDataStep** 函數，然後從清單中指定所需的轉換。
  
    ```R
    rxDataStep(inData = sqlOutScoreDS,
        outFile = sqlOutScoreDS2,
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),
        transformPackages = "boot",
        overwrite = TRUE)
    ```

    當您定義要套用至每個資料行的轉換時，您也可以指定執行轉換所需的任何其他 R 套件。  如需您可以執行的轉換類型的詳細資訊，請參閱[如何轉換和子集資料使用 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform)。
  
6. 呼叫 **rxGetVarInfo** 檢視新資料集裡的變數摘要。
  
    ```R
    rxGetVarInfo(sqlOutScoreDS2)
    ```

    **結果**
    
    *Var 1: ccFraudLogitScore, Type: numeric*
    
    *Var 2: state, Type: character*
    
    *Var 3: gender, Type: character*
    
    *Var 4: cardholder, Type: character*
    
    *Var 5: balance, Type: integer*
    
    *Var 6: numTrans, Type: integer*
    
    *Var 7: numIntlTrans, Type: integer*
    
    *Var 8: creditLine, Type: integer*
    
    *Var 9: ccFraudProb, Type: numeric*

會保留原始的 logit 分數，但新增了新的資料行 *ccFraudProb*，在其中 logit 分數以介於 0 和 1 之間的值代表。

請注意，資料表已寫入因數變數`ccScoreOutput2`為字元資料。 若要使用這些變數作為後續分析的因素，請使用參數 *colInfo* 來指定層級。

## <a name="next-step"></a>下一步

[使用 rxImport 將資料載入記憶體](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)

## <a name="previous-step"></a>上一個步驟

[建立及執行 R 指令碼](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
