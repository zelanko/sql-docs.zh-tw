---
title: 使用 RevoScaleR rxImport 將資料載入記憶體中
description: 有關如何在 SQL Server 上使用 R 語言載入資料的教學課程逐步解說。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 6e7e986b3d0ebd21527d730cb5b4bd5fa60d1c4f
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469737"
---
# <a name="load-data-into-memory-using-rximport-sql-server-and-revoscaler-tutorial"></a>使用 rxImport 將資料載入記憶體 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

這一課是[RevoScaleR 教學](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)課程的一部分, 說明如何搭配 SQL Server 使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。

[RxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport)函數可以用來將資料來源中的資料移動到會話記憶體中的資料框架, 或移至磁片上的 XDF 檔案。 如果您未指定檔案作為目的地，系統會將資料放入記憶體作為資料框架。

在此步驟中, 您將瞭解如何從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]取得資料, 然後使用**rxImport**函數將感興趣的資料放入本機檔案。 這樣一來，您就可以在本機計算內容中重複分析資料，而不必重新查詢資料庫。

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>將資料子集從 SQL Server 解壓縮至本機記憶體

您已決定只想要更詳細地檢查高風險的人員。 中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的來源資料表很大, 因此您只想取得高風險客戶的相關資訊。 然後將該資料載入到本機工作站記憶體中的資料框架。

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

3. 呼叫函式[rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) , 將資料讀取至本機 R 會話中的資料框架。

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    如果作業成功, 您應該會看到如下的狀態訊息:「讀取的資料列:35, 已處理的資料列總數:35, 總區塊時間:0.036 秒」

4. 現在, 高風險觀察會在記憶體內部資料框架中, 您可以使用各種 R 函數來運算元據框架。 例如, 您可以依其風險分數訂購客戶, 並列印會造成最高風險的客戶清單。

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

**RxImport**函數會在匯入過程中將變數名稱指派給資料行, 但您可以使用*colInfo*參數來表示新的變數名稱, 或使用*colClasses*參數來變更資料類型。

藉由在 *transforms* 參數中指定其他運算，您可以對所讀取的每個資料區塊執行基本處理。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 rxDataStep 建立新的 SQL Server 資料表](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)