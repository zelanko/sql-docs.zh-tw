---
title: 建立 R 模型，並儲存至 SQL Server |Microsoft 文件
ms.custom: ''
ms.date: 07/14/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 69b374c1-2042-4861-8f8b-204a6297c0db
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 71ad6a35d28a3d7975f03e6b7e7589ffee4e18ca
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2018
---
# <a name="build-an-r-model-and-save-to-sql-server"></a>建立 R 模型，並儲存至 SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在此步驟中，您將學習如何建立機器學習模型，並將儲存在模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

## <a name="create-a-classification-model-using-rxlogit"></a>建立使用 rxLogit 分類模型

您所建立的模型是預測計程車驅動程式是否有可能取得特定的賽車的提示，或不二元分類器。 您將使用您建立定型提示分類器中上, 一課使用羅吉斯迴歸的資料來源。

1. 呼叫 [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) 函數 (包含在 **RevoScaleR** 封裝中) 來建立羅吉斯迴歸模型。 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = sql_feature_ds));
    ```

    建置模型的呼叫包含在 system.time 函數中。 這可讓您取得建置模型所需的時間。

2. 建立模型之後，您可以檢查它使用`summary`函式，並檢視係數。

    ```R
    summary(logitObj);
    ```

     *結果*

     *羅吉斯迴歸結果： 傾斜 ~ passenger_count + trip_distance + trip_time_in_secs +* direct_distance *   <br/>*資料： featureDataSource （RxSqlServerData 資料來源）*
     <br/>*Dependent variable(s)： 傾斜*
     <br/>*總計的獨立變數： 5*
     <br/>*有效的觀察值的數目： 17068*
     <br/>*遺失的觀察值的數目： 0*
     <br/>*-2\*LogLikelihood: 23540.0602 （17063 自由度上剩餘的差）*
     <br/>*係數：*
     <br/>*Estimate Std.錯誤 z 值 Pr (> | z |)*
     <br/>*(Intercept)       -2.509e-03  3.223e-02  -0.078  0.93793*
     <br/>*passenger_count   -5.753e-02  1.088e-02  -5.289 1.23e-07 \*\*\**
     <br/>*trip_distance     -3.896e-02  1.466e-02  -2.658  0.00786 \*\**
     <br/>*trip_time_in_secs  2.115e-04  4.336e-05   4.878 1.07e-06 \*\*\**
     <br/>*direct_distance    6.156e-02  2.076e-02   2.966  0.00302 \*\**
     <br/>*---*
     <br/>*Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’0.1 ‘ ’ 1*
     <br/>*條件的最後一個差異共變數矩陣數目： 48.3933*
     <br/>*Number of iterations: 4*

## <a name="use-the-logistic-regression-model-for-scoring"></a>使用羅吉斯迴歸模型進行評分

現在，已建立模型，您可以用來預測司機是否可能在特定車程收到小費。

1. 首先，使用[RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata)函式定義在資料來源物件來儲存計分 resul

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + 若要簡化此範例中，羅吉斯迴歸模型的輸入是相同的功能資料來源 (`sql_feature_ds`)，您用來定型模型。  更常見的情況是，您可能會有一些要評分的新資料，也可能設定一些資料來進行測試與定型。
  
    + 預測結果會儲存在資料表中， _taxiscoreOutput_。 請注意當您建立使用 rxSqlServerData 時，未定義此資料表的結構描述。 結構描述被取自 rxPredict 輸出。
  
    + 若要建立儲存的預測的值的資料表，執行 rxSqlServer 資料函式的 SQL 登入必須具有資料庫中的 DDL 權限。 如果登入無法建立資料表，則陳述式會失敗。

2. 呼叫 [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) 函數來產生結果。

    ```R
    rxPredict(modelObject = logitObj,
        data = sql_feature_ds,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    如果陳述式會成功，則應該需要一些時間才能執行。 完成時，您可以開啟 SQL Server Management Studio，並確認已建立資料表，和它包含分數資料行和其他預期的輸出。

## <a name="plot-model-accuracy"></a>繪製模型的精確度

若要取得之模型的精確度的概念，您可以使用[rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc)繪製接收器操作曲線的函式。 因為 rxRoc 是 RevoScaleR 封裝所提供的新函數的其中一個支援遠端計算內容，有兩個選項：

+ 您可以使用 rxRoc 函式來執行遠端計算內容中的繪圖，然後傳回至本機用戶端的 繪圖。

+ 您也可以將資料匯入至 R 用戶端電腦，並使用其他 R 繪製函數來建立效能圖形。

在本節中，您將實驗這兩種技術。

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>在遠端 (SQL Server) 電腦內容中執行繪圖

1. 呼叫函式 rxRoc，並提供做為輸入先前定義的資料。

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    這個呼叫會傳回計算 ROC 圖表中使用的值。 標籤資料行_傾斜_，其中包含您嘗試預測，實際的結果時_分數_資料行的預測。

2. 實際繪製圖表，可儲存 ROC 物件或將它與拖曳`plot`函式。 圖形是遠端計算內容上，建立並傳回給您的 R 環境。

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    R 的圖形裝置，或按一下 [檢視圖形**繪製**RStudio] 視窗。

    ![模型的 ROC 繪圖](media/rsql-e2e-rocplot.png "模型的 ROC 繪圖")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>使用 SQL Server 中的資料在本機計算內容建立繪圖

1. 本機計算內容中，處理程序是非常類似。 您使用[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport)函式，將指定的資料帶入您本機的 R 環境。

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. 您使用的資料在本機記憶體中，載入**ROCR**封裝，並使用該套件的預測函式建立一些新的預測。

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. 產生的輸出變數中儲存的值為基礎的本機圖`pred`。

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

您已建立模型，並確定它已順利執行之後，您可能想將它部署至網站，讓使用者或組織中的人員進行使用模型，或可能是重新定型，並校準以規則為基礎的模型。 此程序有時稱為*運用*模型。

因為[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]可讓您叫用 R 模型使用[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序，所以可以輕鬆地在用戶端應用程式中使用 R。

不過，您必須將模型儲存至用於生產環境的資料庫，才能從外部應用程式呼叫模型。 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中，所定型模型會以二進位形式儲存在 **varbinary(max)**類型的單一資料行中。

因此，將定型模型從 R 移至 SQL Server 包含下列步驟：

+ 將模型序列化成十六進位字串

+ 將序列化物件傳輸至資料庫

+ 將模型儲存至 varbinary(max) 資料行

在本節中，您將學會如何保存模型，以及如何呼叫它來進行預測。

1. 切換回本機的 R 環境中，如果您還沒有使用它，序列化模型，並將它儲存在變數中。

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. 開啟 ODBC 連接使用**RODBC**。

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

    如果您已經載入的封裝，您可以省略 RODBC 的呼叫。

3. 呼叫預存程序建立 PowerShell 指令碼，在資料庫中的資料行中儲存模型的二進位表示法。

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

    只需要 INSERT 陳述式，就可以將模型儲存至資料表。 但是，所以更容易，這類包裝在預存程序中，當_PersistModel_。

    > [!NOTE]
    > 如果您收到錯誤，例如"的 EXECUTE 權限遭拒的物件 PersistModel 」，請確定您的登入具有權限。 您可以執行這樣的 T-SQL 陳述式來授與的明確權限只預存程序： `GRANT EXECUTE ON [dbo].[PersistModel] TO <user_name>`

4. 建立模型，並儲存在資料庫中，您可以直接從呼叫之後[!INCLUDE[tsql](../../includes/tsql-md.md)]程式碼，使用系統預存程序， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

    不過，您經常使用的任何模型，很容易將輸入的查詢和模型，與其他參數，呼叫包裝在自訂預存程序。

    以下是一個這類預存程序的完整程式碼。 我們建議您建立要更輕鬆地管理與更新您的 R 模型，在這種預存程序[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

    ```tsql
    CREATE PROCEDURE [dbo].[PersistModel]  @m nvarchar(max)
    AS
    BEGIN
      SET NOCOUNT ON;
      INSERT INTO nyc_taxi_models (model) values (convert(varbinary(max),@m,2))
    END
    ```

  > [!NOTE]
  > 使用**SET NOCOUNT ON**干擾 SELECT 陳述式的子句，以避免額外的結果設定。


在下一個和最後一課，您會學到如何執行 不要儲存的模型使用計分[!INCLUDE[tsql](../../includes/tsql-md.md)]。

## <a name="next-lesson"></a>下一課

[部署 R 模型，並在 SQL 中使用](walkthrough-deploy-and-use-the-model.md)

## <a name="previous-lesson"></a>上一課

[建立使用 R 和 SQL 資料功能](walkthrough-create-data-features.md)

