---
title: 教學課程的紐約市計程車示範資料
description: 建立包含紐約市計程車範例資料的資料庫。 此資料集會用於 SQL Server 機器學習服務的 R 和 Python 教學課程。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/31/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||>=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 2dab1d48ca2aa98e4a70a08bac492366f2632b79
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584953"
---
# <a name="nyc-taxi-demo-data-for-sql-server-python-and-r-tutorials"></a>SQL Server Python 和 R 教學課程的紐約市計程車示範資料
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

本文說明如何設定由[紐約市計程車和禮車委員會](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)公用資料所組成的範例資料庫。 此資料用於適用於 SQL Server 上資料庫內分析的數個 R 和 Python 教學課程。 為了更快速執行範例程式碼，我們建立了代表性的 1% 取樣資料。 在您的系統上，資料庫備份檔案會稍微超過 90MB，在主要資料表中提供一百七十萬個資料列。

若要完成此練習，您應該具備 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md?view=sql-server-2017&preserve-view=true) 或可還原資料庫備份檔案及執行 T-SQL 查詢的其他工具。

使用此資料集的教學課程和快速入門包括下列內容：

+ [了解在 SQL Server 中使用 R 的資料庫內分析](r-taxi-classification-introduction.md)
+ [了解在 SQL Server 中使用 Python 的資料庫內分析](python-taxi-classification-introduction.md)

## <a name="download-files"></a>下載檔案

範例資料庫是由 Microsoft 主控的 SQL Server 2016 BAK 檔案。 您可以在 SQL Server 2016 和更新版本上還原它。 按一下連結，就會立即開始下載檔案。 

檔案大小約為 90 MB。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
>[!NOTE]
>若要在 [SQL Server 巨量資料叢集](../../big-data-cluster/big-data-cluster-overview.md)上還原範例資料庫，請下載 [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak)，並遵循[將資料庫還原至 SQL Server 巨量資料叢集主要執行個體](../../big-data-cluster/data-ingestion-restore-database.md)中的指引。
::: moniker-end

::: moniker range=">=azuresqldb-mi-current||=sqlallproducts-allversions"
>[!NOTE]
>若要在 [Azure SQL 受控執行個體中的機器學習服務](/azure/azure-sql/managed-instance/machine-learning-services-overview)上還原範例資料庫，請遵循[快速入門：將資料庫還原至 Azure SQL 受控執行個體](/azure/azure-sql/managed-instance/restore-sample-database-quickstart)中的指示，使用紐約市計程車示範資料庫 .bak 檔案操作：[https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak)。
::: moniker-end

1. 按一下 [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) 下載資料庫備份檔案。

2. 將檔案複製到 C:\Program files\Microsoft SQL Server\MSSQL-instance-name\MSSQL\Backup 資料夾。

3. 在 Management Studio 中，以滑鼠右鍵按一下 [資料庫]，然後選取 [還原檔案和檔案群組]。

4. 輸入 NYCTaxi_Sample 作為資料庫名稱。

5. 按一下 [從裝置]，然後開啟檔案選取頁面來選取備份檔案。 按一下 [新增] 以選取 [NYCTaxi_Sample.bak]。

6. 選取 [還原] 核取方塊，然後按一下 [確定] 以還原資料庫。

## <a name="review-database-objects"></a>檢閱資料庫物件
   
使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 確認資料庫物件存在於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上。 您應該會看到資料庫、資料表、函式和預存程序。
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxi_sample-database"></a>NYCTaxi_Sample 資料庫中的物件

下表摘要說明在紐約市計程車示範資料庫中建立的物件。

|**物件名稱**|**物件類型**|**說明**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | [資料庫] | 建立資料庫和兩個資料表：<br /><br />dbo.nyctaxi_sample 資料表：包含主要紐約市計程車資料集。 叢集資料行存放區索引會加入資料表，以提升儲存體和查詢效能。 紐約市計程車資料集的 1% 樣本會插入此資料表。<br /><br />dbo.nyc_taxi_models 資料表：用來保存所定型的進階分析模型。|
|**fnCalculateDistance** |純量值函式 | 計算上車與下車位置之間的直線距離。 此函式用於[建立資料功能](r-taxi-classification-create-features.md)、[定型和儲存模型](r-taxi-classification-train-model.md)以及[讓 R 模型能夠運作](r-taxi-classification-deploy-model.md)。|
|**fnEngineerFeatures** |資料表值函式 | 建立用於模型定型的新資料功能。 此函式用於[建立資料功能](r-taxi-classification-create-features.md)以及[讓 R 模型能夠運作](r-taxi-classification-deploy-model.md)。|


預存程序是使用可在各種教學課程中找到的 R 和 Python 指令碼所建立。 下表摘要說明當您從各種課程執行指令碼時，可以選擇性地加入紐約市計程車示範資料庫中的預存程序。

|**預存程序**|**語言**|**說明**|
|-------------------------|------------|---------------|
|**RxPlotHistogram** |R | 呼叫 RevoScaleR rxHistogram 函式，以繪製變數的長條圖，然後傳回繪圖作為二進位物件。 這個預存程序用於[探索資料並將其視覺化](r-taxi-classification-explore-data.md)。|
|**RPlotRHist** |R| 使用 Hist 函式來建立圖形，然後將輸出儲存為本機 PDF 檔案。 這個預存程序用於[探索資料並將其視覺化](r-taxi-classification-explore-data.md)。|
|**RxTrainLogitModel**  |R| 藉由呼叫 R 套件以將羅吉斯迴歸模型定型。 此模型會預測已支付小費資料行的值，並使用隨機選取的 70%資料進行定型。 此預存程序會輸出已定型的模型，並儲存在資料表 nyc_taxi_models 中。 這個預存程序用於[定型和儲存模型](r-taxi-classification-train-model.md)。|
|**RxPredictBatchOutput**  |R | 呼叫所定型的模型，以使用該模型來建立預測。 此預存程序接受查詢作為其輸入參數，並傳回包含輸入資料列分數的數值資料行。 這個預存程序用於[預測潛在結果](r-taxi-classification-deploy-model.md)。|
|**RxPredictSingleRow**  |R| 呼叫所定型的模型，以使用該模型來建立預測。 此預存程序接受新的觀察值作為輸入，其個別特徵值會當作內嵌參數傳遞，並傳回值以預測新觀察值的結果。 這個預存程序用於[預測潛在結果](r-taxi-classification-deploy-model.md)。|

## <a name="query-the-data"></a>查詢資料

執行查詢以確認資料已上傳，作為驗證步驟。

1. 在 [物件總管] 的 [資料庫] 下，以滑鼠右鍵按一下 [NYCTaxi_Sample] 資料庫，然後開始新的查詢。

2. 執行一些簡單的查詢：

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
資料庫包含一百七十萬個資料列。

3. 資料庫內有包含資料集的 **nyctaxi_sample** 資料表。 此資料表已透過新增[資料行存放區索引](../../relational-databases/indexes/columnstore-indexes-overview.md)，針對集合式計算最佳化。 請執行此陳述式，在資料表上產生簡短摘要。

    ```sql
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
結果應該類似於下列螢幕擷取畫面中顯示的結果。

  ![資料表摘要資訊](media/nyctaxidatatablesummary.png "查詢結果")

## <a name="next-steps"></a>後續步驟

紐約市計程車範例資料現在可供實際操作學習之用。

+ [了解在 SQL Server 中使用 R 的資料庫內分析](r-taxi-classification-introduction.md)
+ [了解在 SQL Server 中使用 Python 的資料庫內分析](python-taxi-classification-introduction.md)