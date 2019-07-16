---
title: 查詢及修改使用 RevoScaleR-SQL Server Machine Learning 的 SQL Server 資料
description: 教學課程逐步解說如何查詢及修改 SQL Server 上使用 R 語言的資料。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 35583815be7c89707efcf9bb31488cd80e3836e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962181"
---
# <a name="query-and-modify-the-sql-server-data-sql-server-and-revoscaler-tutorial"></a>查詢及修改 SQL Server 資料 （SQL Server 和 RevoScaleR 教學課程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這一課是屬於[RevoScaleR 教學課程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

您可以在上一個課程中，載入將資料載入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在此步驟中，您就可以探索並將資料使用下列方法修改**RevoScaleR**:

> [!div class="checklist"]
> * 傳回變數的基本資訊
> * 從原始資料建立類別目錄資料

類別的資料，或是*因素變數*，適合用於探勘資料視覺效果。 您可以使用它們做為輸入長條圖若要了解哪些變數的資料看起來的樣子。

## <a name="query-for-columns-and-types"></a>資料行和類型的查詢

若要執行 R 指令碼中使用的 R IDE 或 RGui.exe。 

首先，取得一份資料行和其資料類型的清單。 您可以使用此函式[rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf)並指定您想要分析的資料來源。 版本而定**RevoScaleR**，您也可以使用[rxGetVarNames](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarnames)。 
  
```R
rxGetVarInfo(data = sqlFraudDS)
```

**結果**

```R
Var 1: custID, Type: integer
Var 2: gender, Type: integer
Var 3: state, Type: integer
Var 4: cardholder, Type: integer
Var 5: balance, Type: integer
Var 6: numTrans, Type: integer
Var 7: numIntlTrans, Type: integer
Var 8: creditLine, Type: integer
Var 9: fraudRisk, Type: integer
```

## <a name="create-categorical-data"></a>建立類別的資料

所有變數會都儲存為整數，但某些變數代表類別的資料，稱為*因素變數*例如，資料行*狀態*包含當做識別項之 50 州再加上哥倫比亞特區的數字。 為了讓您更輕鬆地了解資料，您將數字取代為各州縮寫的清單。

在此步驟中，您會建立包含縮寫的字串向量，並再將這些類別的值對應至原始的整數識別碼。 然後使用中的新變數*colInfo*引數，來指定此資料行視為因素。 每當您分析資料，或將它移，使用縮寫，以及資料行視為因素。

將資料行對應至縮寫，然後才使用它作為因數，實際上也能改善效能。 如需詳細資訊，請參閱 < [R 和資料最佳化](../r/r-and-data-optimization-r-services.md)。

1. 一開始先建立 R 變數*stateAbb*，以及定義要加入，，如下所示的字串向量。
  
    ```R
    stateAbb <- c("AK", "AL", "AR", "AZ", "CA", "CO", "CT", "DC",
        "DE", "FL", "GA", "HI","IA", "ID", "IL", "IN", "KS", "KY", "LA",
        "MA", "MD", "ME", "MI", "MN", "MO", "MS", "MT", "NB", "NC", "ND",
        "NH", "NJ", "NM", "NV", "NY", "OH", "OK", "OR", "PA", "RI","SC",
        "SD", "TN", "TX", "UT", "VA", "VT", "WA", "WI", "WV", "WY")
    ```

2. 接下來，建立名為 *ccColInfo*的資料行資訊物件，指定現有整數值對類別層級 (各州的縮寫) 的對應。
  
    此陳述式也會建立針對 gender 和 cardholder 的因素變數。
  
    ```R
    ccColInfo <- list(
    gender = list(
              type = "factor",
              levels = c("1", "2"),
              newLevels = c("Male", "Female")
              ),
    cardholder = list(
                  type = "factor",
                  levels = c("1", "2"),
                  newLevels = c("Principal", "Secondary")
                   ),
    state = list(
             type = "factor",
             levels = as.character(1:51),
             newLevels = stateAbb
             ),
    balance = list(type = "numeric")
    )
    ```
  
3. 若要建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會使用更新的資料，呼叫的資料來源**RxSqlServerData**函式和以前一樣，但新增*colInfo*引數。
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
    table = sqlFraudTable, colInfo = ccColInfo,
    rowsPerRead = sqlRowsPerRead)
    ```
  
    - 針對 *table* 參數，傳入變數 *sqlFraudTable*，其中包含您稍早建立的資料來源。
    - 針對 *colInfo* 參數，傳入 *ccColInfo* 變數，其中包含資料行資料類型和因素層級。

4.  您現在可以使用 **rxGetVarInfo** 函數檢視新資料來源中的變數。
  
    ```R
    rxGetVarInfo(data = sqlFraudDS)
    ```

    **結果**
    
    ```R
    Var 1: custID, Type: integer
    Var 2: gender  2 factor levels: Male Female
    Var 3: state   51 factor levels: AK AL AR AZ CA ... VT WA WI WV WY
    Var 4: cardholder  2 factor levels: Principal Secondary
    Var 5: balance, Type: integer
    Var 6: numTrans, Type: integer
    Var 7: numIntlTrans, Type: integer
    Var 8: creditLine, Type: integer
    Var 9: fraudRisk, Type: integer
    ```

現在您指定的三個變數 (*gender*、 *state*和 *cardholder*) 被視為因素。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [定義及使用計算內容](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)