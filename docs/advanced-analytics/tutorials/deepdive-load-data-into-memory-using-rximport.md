---
title: "資料載入記憶體使用 rxImport |Microsoft 文件"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 47a42e9a-05a0-4a50-871d-de73253cf070
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bfea2db1797638da671cb59ffc4cd4954d145199
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="load-data-into-memory-using-rximport"></a>使用 rxImport 將資料載入記憶體

您可以使用 **rxImport** 函數，將資料來源中的資料移至 R 工作階段記憶體中的資料框架，或移至磁碟上的 XDF 檔案。 如果您未指定檔案作為目的地，系統會將資料放入記憶體作為資料框架。

在此步驟中，您將學習如何將資料從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，然後使用 rxImport 函式將感興趣的資料放入本機檔案。 這樣一來，您就可以在本機計算內容中重複分析資料，而不必重新查詢資料庫。

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>將資料子集從 SQL Server 擷取到本機記憶體

您已決定只要更詳細地查看高風險的人員。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的來源資料表很大，因此您只會取得高風險客戶的相關資訊，並將該資訊載入本機工作站記憶體內的資料框架。

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

3. 您使用函數 **rxImport** 來實際將資料載入至本機 R 工作階段中的資料框架。

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    如果作業成功，您應該會看到狀態訊息︰Rows Read: 35, Total Rows Processed: 35, Total Chunk Time: 0.036 seconds

4. 既然您在記憶體內的資料框架中已有高風險的觀察值，您可以使用各種 R 函數來操作資料框架。 例如，您可以依其客戶的風險分數來排序客戶，並列印具有最高風險的客戶。

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

您可以使用 rxImport 不只是要移動資料，但要轉換的過程中讀取的資料。 例如，您可以指定固定寬度資料行的字元數、提供變數的描述、設定因素層級資料行，甚至建立要在匯入後使用的新層級。

RxImport 函式將變數的名稱指派給資料行匯入過程中，但您可以使用，表示新的變數名稱*colInfo*參數，而且您可以變更資料類型使用*colClasses*參數。

藉由在 *transforms* 參數中指定其他運算，您可以對所讀取的每個資料區塊執行基本處理。

## <a name="next-step"></a>下一個步驟

[建立新的 SQL Server 資料表，使用 rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)

## <a name="previous-step"></a>上一個步驟

[使用 R 的資料轉換](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

## <a name="see-also"></a>另請參閱

[機器學習教學課程](../../advanced-analytics/tutorials/machine-learning-services-tutorials.md)


