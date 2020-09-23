---
title: 使用 rxImport 載入資料
description: 了解如何從 SQL Server 取得資料，然後使用 rxImport 函式將感興趣的資料放入本機檔案。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7c31650525934b14bf31135264d9b86c52d85119
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179919"
---
# <a name="load-data-into-memory-using-rximport-sql-server-and-revoscaler-tutorial"></a>使用 rxImport 將資料載入記憶體 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

此教學課程是 [RevoScaleR 教學課程系列](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的第 10 個，該系列說明如何搭配 SQL Server 使用 [RevoScaleR 函式](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) \(英文\)。

在此教學課程中，您將了解如何從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 取得資料，然後使用 **rxImport** 函式將感興趣的資料放入本機檔案。 這樣一來，您就可以在本機計算內容中重複分析資料，而不必重新查詢資料庫。

您可以使用 [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) 函式，將資料來源中的資料移至工作階段記憶體中的資料框架，或移至磁碟上的 XDF 檔案。 如果您未指定檔案作為目的地，系統會將資料放入記憶體作為資料框架。

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>將資料子集從 SQL Server 擷取到本機記憶體

您已決定只要更詳細地查看高風險的人員。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的來源資料表很大，因此您只想取得高風險客戶的相關資訊， 然後將該資料載入到本機工作站記憶體中的資料框架。

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

3. 呼叫 [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) 函式來將資料讀取到本機 R 工作階段中的資料框架。

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    如果作業成功，您應該會看到如下的狀態訊息：「讀取的資料列：35，已處理的資料列總數：35，總區塊時間：0.036 秒」

4. 現在高風險觀察是在記憶體內部資料框架中，您可以使用各種 R 函式來操作資料框架。 例如，您可以依客戶的風險分數來排序客戶，並列印具有最高風險的客戶清單。

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

**rxImport** 函式會在匯入程序中將變數名稱指派給資料行，但您可以使用 colInfo  參數表示新的變數名稱，或使用 colClasses  參數變更資料類型。

藉由在 *transforms* 參數中指定其他運算，您可以對所讀取的每個資料區塊執行基本處理。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 rxDataStep 建立新的 SQL Server 資料表](../../machine-learning/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)