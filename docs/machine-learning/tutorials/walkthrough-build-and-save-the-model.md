---
title: R 教學課程：建置及儲存模型
description: 此教學課程示範如何建置用於 SQL Server 資料庫內分析的 R 語言模型。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8ae0de4af29dd68e71300de52875044a8c2d64b4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730430"
---
# <a name="build-an-r-model-and-save-to-sql-server-walkthrough"></a>建置 R 模型並儲存至 SQL Server (逐步解說)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

在此步驟中，瞭解如何建立機器學習模型，並將模型儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 儲存模型之後，可以使用系統預存程序 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 或 [PREDICT (T-SQL) 函數](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)直接從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼進行呼叫。

## <a name="prerequisites"></a>Prerequisites

此步驟會假設您有以本逐步解說中先前步驟為基礎的進行中 R 工作階段。 它會使用在那些步驟中建立的連接字串和資料來源物件。 會使用下列工具和套件來執行指令碼。

+ Rgui.exe 來執行 R 命令
+ Management Studio 來執行 T-SQL
+ ROCR 套件
+ RODBC 套件

### <a name="create-a-stored-procedure-to-save-models"></a>建立預存程序來儲存模型

此步驟會使用預存程序，將定型的模型儲存至 SQL Server。 建立用來執行這項作業的預存程序，可讓工作變得更容易。

在 Management Studio 的查詢視窗中執行下列 T-SQL 程式碼，以建立預存程序。

```sql
USE [NYCTaxi_Sample]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO

IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PersistModel')
  DROP PROCEDURE PersistModel
GO

CREATE PROCEDURE [dbo].[PersistModel] @m nvarchar(max)
AS
BEGIN
    -- SET NOCOUNT ON added to prevent extra result sets from
    -- interfering with SELECT statements.
    SET NOCOUNT ON;
    insert into nyc_taxi_models (model) values (convert(varbinary(max),@m,2))
END
GO
```

> [!NOTE]
> 如果您收到錯誤，請確認您的登入具有建立物件的授權。 您可以執行類似下列的 T-SQL 陳述式，以授予建立物件的明確權限：`exec sp_addrolemember 'db_owner', '<user_name>'`。

## <a name="create-a-classification-model-using-rxlogit"></a>使用 rxLogit 建立分類模型

模型是二進位分類器，可預測計程車司機是否可能在特定車程收到小費。 您將使用在上一課中建立的資料來源，利用羅吉斯迴歸來定型小費分類器。

1. 呼叫 [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) 函數 (包含在 **RevoScaleR** 封裝中) 來建立羅吉斯迴歸模型。 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource));
    ```

    建置模型的呼叫包含在 system.time 函數中。 這可讓您取得建置模型所需的時間。

2. 在您建立模型之後，可以使用 `summary` 函數進行檢查，以及檢視係數。

    ```R
    summary(logitObj);
    ```

    **結果**
    
    ```R
     *Logistic Regression Results for: tipped ~ passenger_count + trip_distance + trip_time_in_secs +*
     direct_distance* 
     *Data: featureDataSource (RxSqlServerData Data Source)*
     *Dependent variable(s): tipped*
     *Total independent variables: 5*
     *Number of valid observations: 17068*
     *Number of missing observations: 0*
     *-2\*LogLikelihood: 23540.0602 (Residual deviance on 17063 degrees of freedom)*
     *Coefficients:*
     *Estimate Std. Error z value Pr(>|z|)*
     *(Intercept)       -2.509e-03  3.223e-02  -0.078  0.93793*
     *passenger_count   -5.753e-02  1.088e-02  -5.289 1.23e-07 \*\*\**
     *trip_distance     -3.896e-02  1.466e-02  -2.658  0.00786 \*\**
     *trip_time_in_secs  2.115e-04  4.336e-05   4.878 1.07e-06 \*\*\**
     *direct_distance    6.156e-02  2.076e-02   2.966  0.00302 \*\**
     *---*
     *Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1*
     *Condition number of final variance-covariance matrix: 48.3933*
     *Number of iterations: 4*
   ```

## <a name="use-the-logistic-regression-model-for-scoring"></a>使用羅吉斯迴歸模型進行評分

現在，已建立模型，您可以用來預測司機是否可能在特定車程收到小費。

1. 首先，使用 [RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata) 函數定義用於儲存評分結果的資料來源物件。

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + 為了簡化這個範例，羅吉斯迴歸模型的輸入是用來定型模型的相同功能資料來源 (`sql_feature_ds`)。  更常見的情況是，您可能會有一些要評分的新資料，也可能設定一些資料來進行測試與定型。
  
    + 預測結果將儲存在 _taxiscoreOutput_ 資料表中。 請注意，在您使用 rxSqlServerData 建立資料表時，並未定義其結構描述。 結構描述是從 rxPredict 的輸出取得。
  
    + 若要建立可儲存預測值的資料表，執行 rxSqlServer 資料函數的 SQL 登入必須具有資料庫中的 DDL 權限。 如果登入無法建立資料表，則陳述式會失敗。

2. 呼叫 [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) 函數來產生結果。

    ```R
    rxPredict(modelObject = logitObj,
        data = featureDataSource,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    如果陳述式成功，則需要一些時間來執行。 完成時，您可以開啟 SQL Server Management Studio，並確認資料表已建立，而且其中包含分數資料行和其他預期的輸出。

## <a name="plot-model-accuracy"></a>繪製模型的精確度

若要瞭解模型的精確度，您可以使用 [rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc) 函數來繪製接收者作業曲線。 因為 rxRoc 是支援遠端運算內容之 RevoScaleR 套件所提供的其中一個新函數，所以您有兩個選項︰

+ 您可以使用 rxRoc 函數在遠端電腦內容中執行繪圖，然後將繪圖傳回給本機用戶端。

+ 您也可以將資料匯入至 R 用戶端電腦，並使用其他 R 繪製函數來建立效能圖形。

在本節中，您將實驗這兩種技術。

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>在遠端 (SQL Server) 電腦內容中執行繪圖

1. 呼叫 rxRoc 函數，並提供稍早定義的資料做為輸入。

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    此呼叫會傳回用來計算 ROC 圖表的值。 標籤資料行是_獲得小費_，其中包含您嘗試要預測的實際結果，而_分數_資料行則具有預測。

2. 若要實際繪製圖表，您可以儲存 ROC 物件，然後使用繪圖函數繪製它。 圖形是建立於遠端計算內容上，並傳回您的 R 環境。

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    檢視圖形的方式是開啟 R 圖形裝置，或按一下 RStudio 中的 [繪製]  視窗。

    ![模型的 ROC 繪圖](media/rsql-e2e-rocplot.png "模型的 ROC 繪圖")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>使用 SQL Server 中的資料在本機計算內容建立繪圖

您可以在命令提示字元中執行 `rxGetComputeContext()`，以確認計算內容是本機的。 傳回值應為「RxLocalSeq 計算內容」。

1. 對於本機計算內容，此流程極為相同。 使用 [rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport) 函數，將指定的資料帶入本機 R 環境。

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. 使用本機記憶體中的資料，您可以載入 **ROCR** 封裝，並使用該封裝中的預測函數來建立一些新的預測。

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. 根據 `pred` 的輸出變數中所儲存的值，產生本機繪圖。

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![使用 R 繪製模型效能](media/rsql-e2e-performanceplot.png "使用 R 繪製模型效能")

> [!NOTE]
> 根據您使用的資料點數目而定，您的圖表看起來可能會與這些不同。

## <a name="deploy-the-model"></a>部署模型

在您建立模型並確認它的執行狀況良好之後，您可能會想要將它部署到組織中的使用者或人員可以使用模型的網站，或可能定期重新定型和重新校準模型。 此程式有時稱為*運作化*模型。 在 SQL Server 中，運作化是藉由在預存程序中內嵌 R 程式碼來達成。 因為程式碼位於程式中，所以可以從任何可連線到 SQL Server 的應用程式呼叫。

您必須將模型儲存至用於生產環境的資料庫，才能從外部應用程式呼叫模型。 定型的模型會以二進位形式儲存在 **varbinary(max)** 類型的單一資料行中。

典型的部署工作流程包含下列步驟：

1. 將模型序列化成十六進位字串
2. 將序列化物件傳輸至資料庫
3. 將模型儲存至 varbinary(max) 資料行

在本節中，您將瞭解如何使用預存程序來保存模型，並使其可用於預測。 本節中使用的預存程序為 PersistModel。 PersistModel 的定義是[必要條件](#prerequisites)。

1. 如果您尚未使用，請切換回本機 R 環境，將模型序列化，並將它儲存在變數中。

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. 使用 **RODBC** 開啟 ODBC 連線。 如果您已載入封裝，您可以省略 RODBC 的呼叫。

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

3. 在 SQL Server 上呼叫 PersistModel 預存程序，將序列化物件傳送至資料庫，並將模型的二進位標記法儲存在資料行中。 

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

4. 使用 Management Studio 驗證模型是否存在。 在 [物件總管] 中，以滑鼠右鍵按一下「nyc_taxi_models」  資料表，然後按一下 [選取前 1000 個資料列]  。 在 [結果] 中，您應該會在 [模型]  資料行中看到二進位標記法。

只需要 INSERT 陳述式，就可以將模型儲存至資料表。 不過，包裝在預存程序 (例如 *PersistModel*) 時，通常會比較容易。

## <a name="next-steps"></a>後續步驟

在接下來的最後一課，您將瞭解如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 針對儲存的模型執行評分。

> [!div class="nextstepaction"]
> [部署 R 模型並在 SQL 中使用](walkthrough-deploy-and-use-the-model.md)
