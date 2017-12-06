---
title: "使用 R 的資料轉換 |Microsoft 文件"
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
ms.assetid: 0327e788-94cc-4a47-933b-7c5c027b9208
caps.latest.revision: "19"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ebc10cd4169f48956ab6b9a770b46c1c11cad6f3
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="transform-data-using-r"></a>使用 R 的資料轉換

**RevoScaleR** 套件提供適用於在各種分析階段轉換資料的多個函數：

- **rxDataStep** 可用來建立及轉換資料子集。

- **rxImport** 支援在將資料匯入 XDF 檔案或記憶體內資料框架，或是從中匯入資料時，對資料進行轉換。

- **rxSummary**、 **rxCube**、 **rxLinMod**和 **rxLogit** 函數雖然不是專為資料移動所設計，但全部都支援資料轉換。

在本節中，您將了解如何使用這些函數。 讓我們開始與 rxDataStep。

## <a name="use-rxdatastep-to-transform-variables"></a>使用 rxDataStep 轉換變數

RxDataStep 函式一次，從一個資料來源中讀取和寫入到另一個處理資料的一個區塊。 您可以指定要轉換的資料行、要載入的轉換等等。

為了讓此範例更有趣，您將使用另一個 R 套件中的函數來轉換資料。  **boot** 套件是其中一個「建議」的套件；也就是說， **boot** 會隨附於每個 R 版本，但未在啟動時自動載入。 因此，您搭配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]執行個體上，應該已提供此套件。

從 **boot** 套件，您將使用 `inv.logit`函數，它會計算 logit 的反函數。 換句話說， `inv.logit` 函數會將 logit 轉換回 [0,1] 刻度的機率。

> [!TIP] 
> 若要取得在這個標尺的預測另一種方式是以設定*類型*參數**回應**rxPredict 原始呼叫中。

1. 一開始先建立一個資料來源以保存資料表 *ccScoreOutput*的資料。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. 再加入另一個資料來源以保存資料表 ccScoreOutput2 的資料。
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    在新的資料表中，您會從先前的 *ccScoreOutput* 資料表取得所有變數，再加上新建立的變數。
  
3. 將計算內容設定為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 使用函式 rxSqlServerTableExists 來檢查是否輸出資料表*ccScoreOutput2*已經存在;，而且如果是，使用函式 rxSqlServerDropTable 以便刪除的資料表。
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")
    ```
  
5. 呼叫 rxDataStep 函式，並在清單中指定所需的轉換。
  
    ```R
    rxDataStep(inData = sqlOutScoreDS,
        outFile = sqlOutScoreDS2,
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),
        transformPackages = "boot",
        overwrite = TRUE)
    ```

    當您定義要套用至每個資料行的轉換時，您也可以指定執行轉換所需的任何其他 R 套件。  如需您可以執行的轉換類型的詳細資訊，請參閱  [Transforming 和內嵌資料](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-transform)
  
6. 呼叫 rxGetVarInfo 變數的摘要檢視中新的資料集。
  
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

請注意，因素變數已寫入資料表 *ccScoreOutput2* 作為字元資料。  若要使用這些變數作為後續分析的因素，請使用參數 *colInfo* 來指定層級。

## <a name="next-step"></a>下一個步驟

[將資料載入至使用 rxImport 記憶體](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)

## <a name="previous-step"></a>上一個步驟

[建立和執行 R 指令碼](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
