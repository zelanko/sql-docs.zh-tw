---
title: 建立 R 模型，並儲存至 SQL Server （逐步解說）-SQL Server Machine Learning
description: 本教學課程示範如何建置用於 SQL Server 資料庫內分析的 R 語言模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b02b1e0298af6fbb96ba5ddd8d5a18dc8e154598
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645477"
---
# <a name="build-an-r-model-and-save-to-sql-server-walkthrough"></a>建立 R 模型，並儲存至 SQL Server （逐步解說）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在此步驟中，了解如何建置機器學習模型，並儲存在模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 儲存模型，您可以呼叫它直接從[!INCLUDE[tsql](../../includes/tsql-md.md)]程式碼，使用系統預存程序[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)或[PREDICT (T-SQL) 函式](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)。

## <a name="prerequisites"></a>先決條件

這個步驟會假設根據先前在本逐步解說的步驟進行中的 R 工作階段。 它會使用連接字串和資料來源中建立的物件執行這些步驟。 下列工具和套件來執行指令碼。

+ 若要執行 R 命令的 Rgui.exe
+ Management Studio 來執行 T-SQL
+ ROCR 封裝
+ RODBC 套件

### <a name="create-a-stored-procedure-to-save-models"></a>建立預存程序，將模型儲存

此步驟會用來將定型的模型儲存至 SQL Server 預存程序。 建立預存程序來執行這項作業，可讓工作更容易。

在 Management Studio 中建立預存程序的查詢視窗中執行下列 T-SQL 程式碼。

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
> 如果您收到錯誤，請確定您的登入已建立物件的權限。 您可以授與明確的權限來執行如下的 T-SQL 陳述式建立物件： `exec sp_addrolemember 'db_owner', '<user_name>'`。

## <a name="create-a-classification-model-using-rxlogit"></a>建立分類模型使用 rxLogit

此模型是預測計程車司機是否可能獲得在特定車程小費的二元分類器。 您將使用羅吉斯迴歸，來定型小費分類器上, 一課建立的資料來源。

1. 呼叫 [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) 函數 (包含在 **RevoScaleR** 封裝中) 來建立羅吉斯迴歸模型。 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource));
    ```

    建置模型的呼叫包含在 system.time 函數中。 這可讓您取得建置模型所需的時間。

2. 建立模型之後，您可以檢查它使用`summary`函式，以及檢視係數。

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

1. 首先，使用[RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata)函式來定義資料來源物件來儲存評分結果。

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + 為了簡化此範例中，羅吉斯迴歸模型的輸入是相同的功能資料來源 (`sql_feature_ds`)，您用來定型模型。  更常見的情況是，您可能會有一些要評分的新資料，也可能設定一些資料來進行測試與定型。
  
    + 預測結果會儲存在資料表中， _taxiscoreOutput_。 請注意當您使用 rxSqlServerData 建立它時，未定義此資料表的結構描述。 結構描述被取自 rxPredict 輸出。
  
    + 若要建立可儲存預測的值的資料表，執行 rxSqlServer 資料函式的 SQL 登入必須具有資料庫中的 DDL 權限。 如果登入無法建立資料表，則陳述式會失敗。

2. 呼叫 [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) 函數來產生結果。

    ```R
    rxPredict(modelObject = logitObj,
        data = featureDataSource,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    如果此陳述式成功，會花費一些時間才能執行。 完成時，您可以開啟 SQL Server Management Studio，並確認已建立資料表，而且它包含分數資料行和其他預期的輸出。

## <a name="plot-model-accuracy"></a>繪製模型的精確度

若要了解模型的精確度，您可以使用[rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc)函數來繪製接收者作業曲線。 因為 rxRoc 是 RevoScaleR 封裝所提供的新函數的其中一個支援遠端計算內容，您有兩個選項：

+ 若要在遠端計算內容中執行繪圖，然後將繪圖傳回給您的本機用戶端，您可以使用 rxRoc 函式。

+ 您也可以將資料匯入至 R 用戶端電腦，並使用其他 R 繪製函數來建立效能圖形。

在本節中，您將體驗這兩種技巧。

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>在遠端 (SQL Server) 電腦內容中執行繪圖

1. 呼叫函式 rxRoc，並提供稍早定義做為輸入的資料。

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    這個呼叫會傳回用來計算 ROC 圖的值。 標籤資料行_tipped_，其中包含實際的結果，您想要預測，而_分數_資料行的預測。

2. 若要實際繪製圖表，您可以儲存 ROC 物件，然後將它繪製繪圖函式。 圖形會在遠端計算內容上建立，並傳回給 R 環境。

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    開啟 R 圖形裝置，或按一下 檢視圖形**繪製**在 RStudio 中的視窗。

    ![模型的 ROC 繪圖](media/rsql-e2e-rocplot.png "模型的 ROC 繪圖")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>使用 SQL Server 中的資料在本機計算內容建立繪圖

您可以確認執行本機計算內容是`rxGetComputeContext()`在命令提示字元。 傳回的值應該是 「 RxLocalSeq 計算內容 」。

1. 針對本機計算內容中，程序是非常類似。 您使用[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport)函式，將指定的資料帶入本機 R 環境。

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. 您使用的資料在本機記憶體中，載入**ROCR**套件，並使用該套件從預測函數來建立一些新的預測。

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. 產生本機的繪圖，並根據輸出變數中儲存的值`pred`。

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![使用 R 繪製的模型效能](media/rsql-e2e-performanceplot.png "使用 R 繪製的模型效能")

> [!NOTE]
> 您的圖表看起來可能不同於這些項目，根據您所使用的資料點數目。

## <a name="deploy-the-model"></a>部署模型

在您建置模型並確定它的運作狀況良好之後，您可能要將它部署至網站，其中使用者或組織中的人員可以將使用此模型，或可能是重新定型以及隨處可見以規則為基礎的模型。 此程序有時稱為*另尋高就*模型。 在 SQL Server 中，運算化之後，即可將 R 程式碼內嵌在預存程序。 因為程式碼所在的程序，它可以從任何可以連線到 SQL Server 的應用程式呼叫它。

您可以從外部應用程式呼叫模型之前，您必須將模型儲存至用於生產環境資料庫中。 定型的模型會儲存在類型的單一資料行中的二進位格式**varbinary （max)**。

一般部署工作流程包含下列步驟：

1. 將模型序列化成十六進位字串
2. 傳輸資料庫到序列化的物件
3. 將模型儲存在 varbinary （max） 資料行

在本節中，了解如何保存模型，並使其可供預測使用預存程序。 在本節中所用的預存程序是 PersistModel。 PersistModel 的定義位於[必要條件](#prerequisites)。

1. 切換回本機 R 環境中，如果您不已使用它，序列化模型，並將它儲存在變數中。

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. 開啟 ODBC 連接使用**RODBC**。 如果您已經載入的封裝，您可以省略 RODBC 的呼叫。

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

3. 呼叫 PersistModel 預存程序在 SQL Server 上 transmite 序列化資料庫物件和儲存模型的二進位表示法的資料行。 

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

4. 使用 Management Studio，若要確認模型存在。 在 [物件總管] 中，以滑鼠右鍵按一下**nyc_taxi_models**資料表，然後按一下**選取前 1000 個資料列**。 在結果中，您應該會看到中的二進位表示法**模型**資料行。

只需要 INSERT 陳述式，就可以將模型儲存至資料表。 不過，通常會更容易，例如包裝在預存程序中，當*PersistModel*。

## <a name="next-steps"></a>後續步驟

在下一個和最後一課中，了解如何執行評分已儲存的模型使用[!INCLUDE[tsql](../../includes/tsql-md.md)]。

> [!div class="nextstepaction"]
> [部署 R 模型，然後在 SQL 中使用](walkthrough-deploy-and-use-the-model.md)
