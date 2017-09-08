---
title: "更新-SQL Server 文件 Advanced Analytics |Microsoft 文件"
description: "顯示更新的內容，如需 Microsoft SQL server 的進階分析中最近變更過的文件的程式碼片段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/17/2017
ms.author: genemi
ms.workload: advanced-analytics
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 79f979ecda1ff0851978d19ef28fa3cf909f9a43
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>新增和更新最近： SQL Server 的進階分析



Microsoft 幾乎每天都會在其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文件網站上更新一些現有文章。 本文會顯示最近更新文章的摘錄。 可能也會列出新文章的連結。

本文是透過定期重新執行的程式所產生。 摘錄中偶爾會出現示不完整的格式，或顯示為來自來源文章的 Markdown。 影像永遠不會顯示在這裡。

新的更新會報告下列日期範圍和主旨：



- 更新日期範圍：&nbsp;**2017 年 5 月 23 日** &nbsp; -至- &nbsp; **2017 年 7 月 17 日**
- *主旨區域：* &nbsp; **Advanced Analytics for SQL Server**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近建立的新文章

下列連結會跳至最近新增的新文章。


1. [外部指令碼執行的一般問題](common-issues-external-script-execution.md)
2. [取得機器學習的疑難排解資料收集](data-collection-ml-troubleshooting-process.md)
3. [SQL Server Python 教學課程](tutorials/sql-server-python-tutorials.md)
4. [SQL Server R 教學課程](tutorials/sql-server-r-tutorials.md)




&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新文章的壓縮清單

此壓縮清單提供所有更新文章的連結，並將列於＜摘要＞一節。



&nbsp;

## <a name="updated-articles-with-excerpts"></a>更新文章與摘要

本節會顯示從最近發生大規模更新的文章所收集的更新摘錄。

此處顯示的摘錄不同於其適當語意內容。 此外，有時摘錄也與實際文件四周的重要 Markdown 語法不同。 因此，這些摘錄僅適用於一般指導方針。 摘錄只能讓您知道您感興趣的項目，是否值得花時間按一下並瀏覽實際文章。

由於這些和其他原因，請勿從這些摘錄中複製程式碼，而且不要將任何文字摘錄視為確切事實。 相反地，請瀏覽實際文章。



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-introducing-revoscalepypythonwhat-is-revoscalepymd"></a>1.&nbsp;[簡介 revoscalepy](python/what-is-revoscalepy.md)

*Updated: 2017-06-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 112.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 cab7330ac9944508aaa360e00cbc2e866455776d 33f4e0e2421fa79fc11931dc7f29bff4432c6f5a  (PR=2171  ,  Filename=what-is-revoscalepy.md  ,  Dirpath=docs\advanced-analytics\python\  ,  MergeCommitSha40=7d2dbe0bdc4cbd05f11eacf938b35a9c35ace2e7) -->



**使用 MicrosoftML revoscalepy**


MicrosoftML Python 的功能整合在一起的計算內容和 revoscalepy 中所提供的資料來源。 因此，您無法使用 MicrosoftML 演算法來定義和 Python 中定型模型，並使用在本機或 SQl Server 計算內容中執行 Python 程式碼的 revoscalepy 函式。

只需匯入您的 Python 程式碼中的模組，然後參考您需要個別的函式。

```
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

**需求**


若要在 SQL Server 中執行 Python 程式碼，您必須已安裝 SQL Server 2017 和功能**機器學習服務**，並啟用 Python 語言。 舊版的 SQL Server 不支援 Python 整合。

> [!NOTE]
> Python 的開放原始碼散發套件不支援 SQL Server 計算內容。 不過，如果您要發佈和取用從 Windows 的 Python 應用程式，您可以安裝 Microsoft Machine Learning 伺服器而不需要安裝 SQL Server。 如需詳細資訊，請參閱 [建立獨立 R 伺服器../r/create-a-standalone-r-server.md)

**取得更多說明**





&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-step-5-train-and-save-a-model-using-t-sqltutorialssqldev-py5-train-and-save-a-model-using-t-sqlmd"></a>2.&nbsp;[步驟 5： 定型和儲存模型使用 T-SQL](tutorials/sqldev-py5-train-and-save-a-model-using-t-sql.md)

*更新日期︰ 2017年-06-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 121.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5c1cbe92282b96105ffdb69efa803f58dc0ac7e2 e4077a2154a90de468c435efa5b2225125d5b0e7  (PR=1904  ,  Filename=sqldev-py5-train-and-save-a-model-using-t-sql.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=dbf91e0d6f8257227cfe8ac6d13c484d0a566f57) -->



1. 在 [！包含 [s../../includes/ssmanstudio-md.md)]，開啟新的查詢視窗，然後執行下列陳述式來建立預存程序_TrainTipPredictionModelRxPy_。  此模型會根據您剛才準備好定型資料。 因為預存程序已經包含輸入資料的定義，您不必提供輸入的查詢。

    ```SQL
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelRxPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelRxPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script 
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    import pandas
    from revoscalepy.functions.RxLogit import rx_logit_ex
    
    ## Create a logistic regression model using rx_logit_ex function from revoscalepy package
    logitObj = rx_logit_ex("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
    ## Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    ```



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-step-6-operationalize-the-modeltutorialssqldev-py6-operationalize-the-modelmd"></a>3.&nbsp;[步驟 6： 實施模型](tutorials/sqldev-py6-operationalize-the-model.md)

*更新日期︰ 2017年-06-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_2) | [下一步](#TitleNum_4))

<!-- Source markdown line 236.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1eb50ac902d4e80bafb1dd7fdf8f607dcdf0d33f 57d5abdc6119db1ecd81587d625054a5bbfb5fc8  (PR=1904  ,  Filename=sqldev-py6-operationalize-the-model.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=dbf91e0d6f8257227cfe8ac6d13c484d0a566f57) -->



以下是執行計分使用預存程序的定義**revoscalepy**模型。

```
CREATE PROCEDURE [dbo].[PredictTipSingleModeRxPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
    SELECT * FROM [dbo].[fnEngineerFeatures-- 
      @passenger_count,
      @trip_distance,
      @trip_time_in_secs,
      @pickup_latitude,
      @pickup_longitude,
      @dropoff_latitude,
      @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      from revoscalepy.functions.RxPredict import rx_predict_ex;
```




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-use-python-with-revoscalepy-to-create-a-modeltutorialsuse-python-revoscalepy-to-create-modelmd"></a>4.&nbsp;[Revoscalepy 與建立模型的使用 Python](tutorials/use-python-revoscalepy-to-create-model.md)

*更新日期︰ 2017年-06-21* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([先前](#TitleNum_3))

<!-- Source markdown line 119.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0886939f86fe12d7ff7b339689a02c7fc75e0786 23dd469349a05d535063aab3c14aec152ed2cd7b  (PR=2141  ,  Filename=use-python-revoscalepy-to-create-model.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=76839e39427e24688609353b8708d59fee772d28) -->



**檢閱的程式碼**


讓我們檢閱的程式碼，並反白顯示某些主要的步驟。

**定義資料來源，並計算內容**


這是很重要的一部分使用**revoscalepy**和其相關的 R 封裝**RevoScaleR**。 資料來源與不同的計算內容。 _資料來源_定義您的程式碼中使用的資料。 _計算內容_定義執行程式碼。

> [!NOTE]
> 發行前版本，可能會受限於 RevoScaleR 中支援某些資料來源類型的支援。 如需最新版本中所包含的函式的詳細資訊，請參閱 [什麼是 revoscalepy../python/what-is-revoscalepy.md)。

整體處理序來建立和使用資料來源，並計算內容，如下所示：

1. 建立 Python 變數，例如_sqlQuery_和_connectionString_，定義來源和您想要使用的資料。 將這些變數來傳遞**RxSqlServerData**建構函式來實作**資料來源物件**名為_dataSource_。
2. 使用建立的計算內容物件**RxInSqlServer**建構函式。 在此範例中，您可以傳遞定義前面，假設您將會當成計算內容使用的相同 SQL Server 執行個體上的資料相同的連接字串。 不過，在資料來源和計算內容可能會在不同伺服器上。 產生**計算內容物件**名為_computeContext_。
3. 選擇 使用中的計算內容。 根據預設，作業會於本機執行，這表示，如果您未指定不同的計算內容、 將資料來源擷取資料和模型調整將會執行目前的 Python 環境中。

    在 RevoScaleR，您也可以使用此函式`rxSetComputeContext`計算內容之間切換。 此函式尚未實作中的預覽版本**revoscalepy**，但是您可以指定做為引數的計算內容**rx_lin_mod_ex**。





<a name="similars2"/>

&nbsp;

## <a name="similar-articles"></a>類似的文章

本節會在 GitHub 儲存機制中，列出與其他主題區中最近更新的文章十分相似的文章：[MicrosoftDocs/**sql-docs-pr**](https://github.com/microsoftdocs/sql-docs-pr/)。

<!--  20170717-1101  -->

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>具有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (4+4)：**SQL 進階分析**文件](../advanced-analytics/new-updated-advanced-analytics.md)
- [新文章 + 更新文章 (2+0)：**SQL Analysis Services** 文件](../analysis-services/new-updated-analysis-services.md)
- [新文章 + 更新文章 (1+2)：**連線到 SQL** 文件](../connect/new-updated-connect.md)
- [新文章 + 更新文章 (6+0)：**SQL 資料庫引擎**文件](../database-engine/new-updated-database-engine.md)
- [新文章 + 更新文章 (13+2)：**Linux for SQL** 文件](../linux/new-updated-linux.md)
- [新文章 + 更新文章 (1+0)：**SQL Master Data Services (MDS)** 文件](../master-data-services/new-updated-master-data-services.md)
- [新文章 + 更新文章 (1+0)：**SQL ODBC (開放式資料庫連接)** 文件](../odbc/new-updated-odbc.md)
- [新文章 + 更新文章 (8+4)：**SQL 關聯式資料庫**文件](../relational-databases/new-updated-relational-databases.md)
- [新文章 + 更新文章 (2+2)：**Microsoft SQL Server** 文件](../sql-server/new-updated-sql-server.md)
- [新文章 + 更新文章 (0+1)：**SQL Server Management Studio (SSMS)** 文件](../ssms/new-updated-ssms.md)
- [新文章 + 更新文章 (1+0)：**Transact-SQL** 文件](../t-sql/new-updated-t-sql.md)
- [新文章 + 更新文章 (1+0)：**SQL 工具**文件](../tools/new-updated-tools.md)


#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>沒有新文章或最近更新文章的主題區

- [新文章 + 更新文章 (0+0)：**ActiveX Data Objects (ADO) for SQL** 文件](../ado/new-updated-ado.md)
- [新文章 + 更新文章 (0+0)：**Data Quality Services for SQL** 文件](../data-quality-services/new-updated-data-quality-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 資料採礦延伸模組 (DMX)** 文件](../dmx/new-updated-dmx.md)
- [新文章 + 更新文章 (0+0)：**SQL Integration Services** 文件](../integration-services/new-updated-integration-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 多維度運算式 (MDX)** 文件](../mdx/new-updated-mdx.md)
- [新文章 + 更新文章 (0+0)：**PowerShell for SQL** 文件](../powershell/new-updated-powershell.md)
- [新文章 + 更新文章 (0+0)：**SQL Reporting Services** 文件](../reporting-services/new-updated-reporting-services.md)
- [新文章 + 更新文章 (0+0)：**SQL 範例**文件](../sample/new-updated-sample.md)
- [新文章 + 更新文章 (0+0)：**SQL Server Data Tools (SSDT)** 文件](../ssdt/new-updated-ssdt.md)
- [新文章 + 更新文章 (0+0)：**SQL Server 移轉小幫手 (SSMA)** 文件](../ssma/new-updated-ssma.md)
- [新文章 + 更新文章 (0+0)：**XQuery for SQL** 文件](../xquery/new-updated-xquery.md)


&nbsp;


