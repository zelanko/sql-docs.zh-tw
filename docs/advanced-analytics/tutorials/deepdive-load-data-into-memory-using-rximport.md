---
title: "資料載入記憶體使用 rxImport （SQL 與 R 深入探討） |Microsoft 文件"
ms.custom: 
ms.date: 12/14/2017
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
dev_langs: R
ms.assetid: 47a42e9a-05a0-4a50-871d-de73253cf070
caps.latest.revision: "14"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 4c68d7e358ec9d02e68aaa5b0fef708414a11b41
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="load-data-into-memory-using-rximport-sql-and-r-deep-dive"></a>將資料載入至記憶體使用 rxImport （SQL 與 R 深入探討）

本文是資料科學深入探討教學課程中，有關如何使用一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

[RxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport)函式可將資料從資料來源移至資料框架中工作階段記憶體或磁碟上 XDF 檔案。 如果您未指定檔案作為目的地，系統會將資料放入記憶體作為資料框架。

在此步驟中，了解如何取得從資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然後使用**rxImport**感興趣的資料放在本機檔案的函式。 這樣一來，您就可以在本機計算內容中重複分析資料，而不必重新查詢資料庫。

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>從 SQL Server 擷取資料的子集，為本機記憶體

您已決定您想要檢查只有更詳細的高風險每個人。 中的來源資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]很大，所以您想要取得高風險的客戶資訊。 您接著該資料載入本機工作站的記憶體中的資料框架。

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

3. 呼叫此函式[rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport)來讀取的資料至資料框架，在本機的 R 工作階段中。

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    如果作業成功，您應該會看到與下列類似的狀態訊息:"Rows Read: 35，總計資料列處理： 35，時間總計區塊： 0.036 秒 」

4. 既然高風險的觀察值已在記憶體中的資料框架中，您可以使用各種不同的 R 函數來操作資料框架。 比方說，您可以依其風險評分，客戶，並列印一份高風險的客戶。

    ```R
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]
    row.names(orderedHighRisk) <- NULL
    head(orderedHighRisk)
    ```

**結果**

*ccFraudLogitScore   state gender cardholder balance numTrans numIntlTrans creditLine ccFraudProb1*

*9.786345    SD   Male  Principal   23456       25            5 75   0.99994382*

*9.433040    FL Female  Principal   20629       24           28 75   0.99992003*

*8.556785    NY Female  Principal   19064       82           53 43   0.99980784*

*8.188668    AZ Female  Principal   19948       29            0 75   0.99972235*

*7.551699    NY Female  Principal   11051       95            0 75   0.99947516*

*7.335080    NV   Male  Principal   21566        4            6  75   0.9993482*

## <a name="more-about-rximport"></a>進一步了解 rxImport

您不僅可以使用 **rxImport** 來移動資料，也在讀取過程中轉換資料。 例如，您可以指定固定寬度資料行的字元數、提供變數的描述、設定因素層級資料行，甚至建立要在匯入後使用的新層級。

**RxImport**函式將變數的名稱指派給資料行匯入過程中，但您可以使用，表示新的變數名稱*colInfo*參數或變更資料類型使用*colClasses*參數。

藉由在 *transforms* 參數中指定其他運算，您可以對所讀取的每個資料區塊執行基本處理。

## <a name="next-step"></a>下一步

[使用 rxDataStep 建立新的 SQL Server 資料表](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)

## <a name="previous-step"></a>上一個步驟

[使用 R 轉換資料](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

