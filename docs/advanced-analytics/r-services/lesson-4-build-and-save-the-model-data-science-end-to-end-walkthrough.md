---
title: "第 4 課︰建立和儲存模型 (資料科學端對端逐步解說) | Microsoft Docs"
ms.custom: ""
ms.date: "11/22/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 69b374c1-2042-4861-8f8b-204a6297c0db
caps.latest.revision: 20
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 18
---
# 第 4 課︰建立和儲存模型 (資料科學端對端逐步解說)
在這一課，您將了解如何建立機器學習模型，並將模型儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="creating-a-classification-model"></a>建立分類模型  
您將建立的模型是二進位分類器，可預測計程車司機是否可能在特定車程收到小費。 您將使用在上一課中建立的資料來源 `featureDataSource,` ，利用羅吉斯迴歸來定型小費分類器。  
  
以下是您將在模型中使用的函數︰  
  
-   passenger_count  
  
-   trip_distance  
  
-   trip_time_in_secs  
  
-   direct_distance  

### <a name="create-the-model-using-rxlogit"></a>使用 rxLogit 建立模型  
1.  呼叫 *rxLogit* 函數 (包含在 **RevoScaleR** 封裝中) 來建立羅吉斯迴歸模型。  
  
    ```R  
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource))    
    ```  
  
2.  在您建立模型之後，想要使用 `summary` 函數進行檢查，以及檢視係數。  
  
    ```  
    summary(logitObj)  
    ```  

     *結果*

     *Logistic Regression Results for: tipped ~ passenger_count + trip_distance + trip_time_in_secs +*  
     *direct_distance*  
     *Data: featureDataSource (RxSqlServerData Data Source)*  
     *Dependent variable(s): tipped*  
     *Total independent variables: 5*   
     *Number of valid observations: 17068*  
     *Number of missing observations: 0*   
     *-2\*LogLikelihood: 23540.0602 (Residual deviance on 17063 degrees of freedom)*  
     *Coefficients:*  
     *Estimate Std.Error z value Pr(>|z|)*   
     *(Intercept)       -2.509e-03  3.223e-02  -0.078  0.93793*   
     *passenger_count   -5.753e-02  1.088e-02  -5.289 1.23e-07 \*\*\**  
     *trip_distance     -3.896e-02  1.466e-02  -2.658  0.00786 \*\**   
     *trip_time_in_secs  2.115e-04  4.336e-05   4.878 1.07e-06 \*\*\**  
     *direct_distance    6.156e-02  2.076e-02   2.966  0.00302 \*\**   
     *---*  
     *Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’0.1 ‘ ’ 1*  
     *Condition number of final variance-covariance matrix: 48.3933*   
     *Number of iterations: 4*  
  
### <a name="use-the-logistic-regression-model-for-scoring"></a>使用羅吉斯迴歸模型進行評分  
現在，已建立模型，您可以用來預測司機是否可能在特定車程收到小費。  
  
1.  首先，定義要用於儲存評分結果的資料物件  
  
    ```R  
    scoredOutput <- RxSqlServerData(  
      connectionString = connStr,  
      table = "taxiScoreOutput"  )  
    ```  
    + 為了簡化這個範例，羅吉斯迴歸模型的輸入是用來定型模型的相同 `featureDataSource` 。  更常見的情況是，您可能會有一些要評分的新資料，也可能設定一些資料來進行測試與定型。  
  
    + 預測結果會儲存在 _taxiscoreOutput_資料表中。 請注意，您在使用 `rxSqlServerData`建立此資料表時未定義其結構描述，而是取自 *中的* scoredOutput `rxPredict`物件輸出。  
  
    + 若要建立可儲存預測值的資料表，執行 `rxSqlServer` 資料函數的 SQL 登入必須具有資料庫中的 DDL 權限。 如果登入無法建立資料表，則陳述式會失敗。  
  
2.  呼叫 *rxPredict* 函數來產生結果。  
  
    ```R  
    rxPredict(modelObject = logitObj, data = featureDataSource, outData = scoredOutput,   
                       predVarNames = "Score", type = "response",   
                       writeModelVars = TRUE, overwrite = TRUE)  
    ```  

  
## <a name="plotting-model-accuracy"></a>繪製模型的精確度  
若要了解模型的精確度，您可以使用 *rxRocCurve* 函數來繪製接收者作業曲線。 因為 *rxRocCurve* 是支援遠端運算內容之 RevoScaleR 封裝所提供的其中一個新函數，所以您有兩個選項：  
  
+ 您可以使用 `rxRocCurve` 函數在遠端電腦內容中執行繪圖，然後將繪圖傳回給本機用戶端。
+ 您也可以將資料匯入至 R 用戶端電腦，並使用其他 R 繪製函數來建立效能圖形。  
  
在本節中，您將使用這兩種技術。  
  
### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>在遠端 (SQL Server) 電腦內容中執行繪圖  
  
1.  呼叫 *rxRocCurve* 函數，並提供稍早定義的資料做為輸入。  
  
    ```R  
    rxRocCurve( "tipped", "Score", scoredOutput)  
    ```  
  
    請注意，您也必須指定輕觸的標籤資料行 (您嘗試預測的變數) 以及可儲存預測的資料行名稱 (_Score_)。  
  
2.  開啟 R 圖形裝置，或按一下 RStudio 中的 [繪製] 視窗，來檢視所產生的圖形。  
  
    ![ROC plot for the model](../../advanced-analytics/r-services/media/rsql-e2e-rocplot.png "ROC plot for the model")  

    圖形是建立於遠端計算內容上，然後傳回您的 R 環境。   
    
### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>使用 SQL Server 中的資料在本機計算內容建立繪圖  
  
1.  使用 *rxImport* 函數，將指定的資料帶入本機 R 環境。  
  
    ```R  
    scoredOutput = rxImport(scoredOutput)  
    ```  
  
2.  將資料載入至本機記憶體之後，接著可呼叫 **ROCR** 程式庫來建立一些預測，以及產生繪圖。  
  
    ```R  
    library('ROCR')  
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped)  
  
    acc.perf = performance(pred, measure = 'acc')  
    plot(acc.perf)  
    ind = which.max( slot(acc.perf, 'y.values')[[1]] )  
    acc = slot(acc.perf, 'y.values')[[1]][ind]  
    cutoff = slot(acc.perf, 'x.values')[[1]][ind]  
    ```  
  
3.  在這兩種情況下，會產生下列繪圖。  
  
    ![plotting model performance using R](../../advanced-analytics/r-services/media/rsql-e2e-performanceplot.png "plotting model performance using R")  
  
## <a name="deploying-a-model"></a>部署模型  

在您建置模型且確認其運作狀況良好之後，可能想要讓模型能夠*運作*。 因為 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可讓您使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序來叫用 R 模型，所以在用戶端應用程式中使用 R 極為簡單。  
  
不過，您必須將模型儲存至用於生產環境的資料庫，才能從外部應用程式呼叫模型。 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中，所定型模型會以二進位形式儲存在 **varbinary(max)**類型的單一資料行中。

因此，將定型模型從 R 移至 SQL Server 包含下列步驟：  
  
+ 將模型序列化成十六進位字串
+ 將序列化物件傳輸至資料庫
+ 將模型儲存至 varbinary(max) 資料行  
  
在本節中，您將了解如何保存模型，以及如何呼叫它來進行預測。  
  
### <a name="serialize-the-model"></a>序列化模型  
  
+  在本機 R 環境中，序列化模型，並將它儲存在變數中。  
  
    ```R  
    modelbin <- serialize(logitObj, NULL)  
    modelbinstr=paste(modelbin, collapse="")  
    ```  
  
    *serialize* 函數包含於 R **base** 封裝中，並提供簡單低階介面來序列化至連接。 如需詳細資訊，請參閱 [http://www.inside-r.org/r-doc/base/serialize](http://www.inside-r.org/r-doc/base/serialize)。  
  
### <a name="move-the-model-to-sql-server"></a>將模型移至 SQL Server

+ 開啟 ODBC 連接並呼叫預存程序，以將模型的二進位表示法儲存在資料庫的資料行中。 
  
    ```R  
    library(RODBC)  
    conn <- odbcDriverConnect(connStr )  
  
    # persist model by calling a stored procedure from SQL  
    q<-paste("EXEC PersistModel @m='", modelbinstr,"'", sep="")  
    sqlQuery (conn, q)    
    ```  

只需要 INSERT 陳述式，就可以將模型儲存至資料表。 不過，為了讓它更為簡單，我們在此處使用了 _PersistModel_ 預存程序。 
 
以下是供參考之預存程序的完整程式碼︰  
  
```tsql  
CREATE PROCEDURE [dbo].[PersistModel]  @m nvarchar(max)  
AS  
BEGIN  
        -- SET NOCOUNT ON added to prevent extra result sets from  
        -- interfering with SELECT statements.  
        SET NOCOUNT ON;  
        insert into nyc_taxi_models (model) values (convert(varbinary(max),@m,2))  
END   
```  
> [!TIP] 建議您建立 Helper 函數 (如這個預存程序)，來簡化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中 R 模型的管理和更新。  
  
  
### <a name="invoke-the-saved-model"></a>叫用儲存的模型  
在您將模型儲存至資料庫之後，可以使用 [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 系統預存程序直接從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼進行呼叫。  
  
例如，若要產生預測，您只需要連接到資料庫，並執行預存程序，以使用所儲存的模型作為輸入，以及一些輸入資料。  
  
不過，如果您有一個經常使用的模型，很容易就可以在自訂預存程序中包裝輸入查詢、模型呼叫和任何其他參數。  
  
在下一課，您將了解如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]針對儲存的模型執行評分。  
  
## <a name="next-lesson"></a>下一課  
[第 5 課︰部署和使用模型 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/lesson-5-deploy-and-use-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>上一課  
[第 3 課︰建立資料特徵 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)  
  
  
  
