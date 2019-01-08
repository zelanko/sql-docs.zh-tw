---
title: 將資料載入到記憶體中使用 RevoScaleR rxImport-SQL Server Machine Learning
description: 教學課程逐步解說如何將 SQL Server 上使用 R 語言的資料。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f1a2cfd889fd8ff594b5ead48a9bd391955158f8
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645189"
---
# <a name="load-data-into-memory-using-rximport-sql-server-and-revoscaler-tutorial"></a>將資料載入記憶體使用 rximport 將 （SQL Server 和 RevoScaleR 教學課程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這一課是屬於[RevoScaleR 教學課程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

[RxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport)函式可用來從資料來源移動資料，到工作階段記憶體中的資料框架或 XDF 檔案在磁碟上。 如果您未指定檔案作為目的地，系統會將資料放入記憶體作為資料框架。

在此步驟中，了解如何將資料從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然後使用**rxImport**感興趣的資料放入本機檔案的函式。 這樣一來，您就可以在本機計算內容中重複分析資料，而不必重新查詢資料庫。

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>從 SQL Server 擷取資料的子集，至本機記憶體

您已決定您想要檢查只有高風險的人員在更多詳細資料。 中的來源資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]很大，因此您想要取得高風險的客戶的相關資訊。 然後，您會將該資料載入本機工作站的記憶體中的資料框架。

1. 將計算內容重設為您的本機工作站。

    ```R
    rxSetComputeContext("local")
    ```

2. 建立新 SQL Server 資料來源物件，並在 *sqlQuery* 參數中提供有效的 SQL 陳述式。 這個範例會取得具有最高風險分數的觀察值子集。 這樣一來，只有您真正需要的資料才會放在本機記憶體中。

    ```R
    sqlServerProbDS \<- RxSqlServerData(
        sqlQuery = paste("SELECT * FROM ccScoreOutput2",
        "WHERE (ccFraudProb > .99)"),
        connectionString = sqlConnString)
    ```

3. 呼叫函式[rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport)來將資料讀入資料框架，在本機 R 工作階段中。

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    如果作業成功，您應該會看到與下列類似的狀態訊息：「 讀取的資料列：35，total 處理的資料列：35 的 total Chunk Time:0.036 seconds"

4. 既然高風險的觀察值已在記憶體中的資料框架中，您可以使用各種 R 函數來操作資料框架。 比方說，您可以依其風險評分中，客戶，並列印一份最高風險的客戶。

    ```R
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]
    row.names(orderedHighRisk) <- NULL
    head(orderedHighRisk)
    ```

**結果**

```R
ccFraudLogitScore   state gender cardholder balance numTrans numIntlTrans creditLine ccFraudProb1
9.786345    SD   Male  Principal   23456       25            5 75   0.99994382
9.433040    FL Female  Principal   20629       24           28 75   0.99992003
8.556785    NY Female  Principal   19064       82           53 43   0.99980784
8.188668    AZ Female  Principal   19948       29            0 75   0.99972235
7.551699    NY Female  Principal   11051       95            0 75   0.99947516
7.335080    NV   Male  Principal   21566        4            6  75   0.9993482
```

## <a name="more-about-rximport"></a>進一步了解 rxImport

您不僅可以使用 **rxImport** 來移動資料，也在讀取過程中轉換資料。 例如，您可以指定固定寬度資料行的字元數、提供變數的描述、設定因素層級資料行，甚至建立要在匯入後使用的新層級。

**RxImport**函式匯入過程中，將變數名稱指派給資料行，但您可以藉由指定新的變數名稱*colInfo*參數或變更資料類型使用*colClasses*參數。

藉由在 *transforms* 參數中指定其他運算，您可以對所讀取的每個資料區塊執行基本處理。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 rxDataStep 建立新的 SQL Server 資料表](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)