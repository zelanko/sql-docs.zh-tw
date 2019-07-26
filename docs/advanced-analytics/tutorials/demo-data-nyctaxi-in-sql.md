---
title: 下載適用于 embedded R 和 Python 的 NYC 計程車示範資料和腳本
description: 下載紐約計程車範例資料和建立資料庫的指示。 資料用於 SQL Server Python 和 R 語言教學課程, 示範如何在 SQL Server 預存程式和 T-sql 函數中內嵌腳本。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/31/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5d5d74090713666a2da6058d9eccee1e33e4d7cb
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469748"
---
# <a name="nyc-taxi-demo-data-for-sql-server-python-and-r-tutorials"></a>SQL Server Python 和 R 教學課程的 NYC 計程車示範資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文說明如何設定包含紐約[計程車和禮車委員會](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)之公用資料的範例資料庫。 此資料用於數個 R 和 Python 教學課程, 用於 SQL Server 上的資料庫內分析。 為了讓範例程式碼執行得更快, 我們為數據建立了代表性的 1% 取樣。 在您的系統上, 資料庫備份檔案會稍微超過 90 MB, 並在主要資料表中提供1700000個數據列。

若要完成此練習, 您應該有[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)或另一個可還原資料庫備份檔案並執行 t-SQL 查詢的工具。

使用此資料集的教學課程和快速入門包括下列各項:

+ [瞭解在 SQL Server 中使用 R 的資料庫內分析](sqldev-in-database-r-for-sql-developers.md)
+ [瞭解在 SQL Server 中使用 Python 的資料庫內分析](sqldev-in-database-python-for-sql-developers.md)

## <a name="download-files"></a>下載檔案

範例資料庫是由 Microsoft 主控的 SQL Server 2016 .BAK 檔案。 您可以在 SQL Server 2016 和更新版本上還原它。 當您按一下連結時, 就會立即開始下載檔案。 

檔案大小大約是 90 MB。

1. 按一下 [ [NYCTaxi_Sample](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak) ] 以下載資料庫備份檔案。

2. 將檔案複製到 C:\Program files\Microsoft SQL Server\MSSQL-instance-name\MSSQL\Backup 資料夾。

3. 在 Management Studio 中, 以滑鼠右鍵按一下 [**資料庫**], 然後選取 [**還原檔案和檔案群組**]。

4. 輸入*NYCTaxi_Sample*做為資料庫名稱。

5. 按一下 [**從裝置**], 然後開啟 [檔案選取] 頁面來選取備份檔案。 按一下 [**新增**] 以選取 [NYCTaxi_Sample]。

6. 選取 [**還原**] 核取方塊, 然後按一下 **[確定]** 以還原資料庫。

## <a name="review-database-objects"></a>審查資料庫物件
   
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]確認資料庫物件存在於實例上。 您應該會看到資料庫、資料表、函數和預存程式。
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxisample-database"></a>NYCTaxi_Sample 資料庫中的物件

下表摘要說明在 NYC 計程車示範資料庫中建立的物件。

|**物件名稱**|**物件類型**|**說明**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | database | 建立資料庫和兩個資料表：<br /><br />nyctaxi_sample 資料表:包含主要 NYC 計程車資料集。 叢集資料行存放區索引會加入資料表，以提升儲存體和查詢效能。 NYC 計程車資料集的 1% 樣本會插入此資料表中。<br /><br />dbo. nyc _taxi_models table:用來保存已定型的先進分析模型。|
|**fnCalculateDistance** |純量值函式 | 計算 pickup 和下車位置之間的直線距離。 此函式用於[建立資料特徵](sqldev-create-data-features-using-t-sql.md)、[定型和儲存模型](sqldev-train-and-save-a-model-using-t-sql.md), 以及[讓 R 模型](sqldev-operationalize-the-model.md)。|
|**fnEngineerFeatures** |資料表值函式 | 建立用於模型定型的新資料功能。 此函式用於[建立資料特徵](sqldev-create-data-features-using-t-sql.md)和[讓 R 模型](sqldev-operationalize-the-model.md)。|


預存程式是使用在各種教學課程中找到的 R 和 Python 腳本所建立。 下表摘要說明當您從各種課程執行腳本時, 可以選擇性地加入 NYC 計程車示範資料庫中的預存程式。

|**預存程式**|**語言**|**描述**|
|-------------------------|------------|---------------|
|**RxPlotHistogram** |R | 呼叫 RevoScaleR rxHistogram 函式以繪製變數的長條圖, 然後將繪圖當做二進位物件傳回。 這個預存程式是用來[流覽資料並將其視覺化](sqldev-explore-and-visualize-the-data.md)。|
|**RPlotRHist** |R| 使用歷程函式建立圖形, 並將輸出儲存為本機 PDF 檔案。 這個預存程式是用來[流覽資料並將其視覺化](sqldev-explore-and-visualize-the-data.md)。|
|**RxTrainLogitModel**  |R| 藉由呼叫 R 封裝來訓練羅吉斯回歸模型。 此模型會預測已支付小費資料行的值，並使用隨機選取的 70%資料進行定型。 此預存程序會輸出已定型的模型，並儲存在資料表 nyc_taxi_models 中。 這個預存程式用於[定型和儲存模型](sqldev-train-and-save-a-model-using-t-sql.md)。|
|**RxPredictBatchOutput**  |R | 呼叫定型的模型, 以使用模型建立預測。 此預存程序接受查詢作為其輸入參數，並傳回包含輸入資料列分數的數值資料行。 這個預存程式是用來[預測潛在的結果](sqldev-operationalize-the-model.md)。|
|**RxPredictSingleRow**  |R| 呼叫定型的模型, 以使用模型建立預測。 此預存程序接受新的觀察值作為輸入，其個別特徵值會當作內嵌參數傳遞，並傳回值以預測新觀察值的結果。 這個預存程式是用來[預測潛在的結果](sqldev-operationalize-the-model.md)。|

## <a name="query-the-data"></a>查詢資料

執行查詢以確認資料已上傳, 做為驗證步驟。

1. 在物件總管的 [資料庫] 底下, 以滑鼠右鍵按一下 [ **NYCTaxi_Sample** ] 資料庫, 然後開始新的查詢。

2. 執行一些簡單的查詢:

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
資料庫包含1700000個數據列。

3. 在資料庫中, 是包含資料集的**nyctaxi_sample**資料表。 資料表已針對以集合為基礎的計算進行優化, 並加入資料行存放區[索引](../../relational-databases/indexes/columnstore-indexes-overview.md)。 執行此語句, 以產生資料表的快速摘要。

    ```sql
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
結果應該類似于下列螢幕擷取畫面中顯示的結果。

  ![資料表摘要資訊](media/nyctaxidatatablesummary.png "查詢結果")

## <a name="next-steps"></a>後續步驟

NYC 計程車範例資料現在可供實際操作學習之用。

+ [瞭解在 SQL Server 中使用 R 的資料庫內分析](sqldev-in-database-r-for-sql-developers.md)
+ [瞭解在 SQL Server 中使用 Python 的資料庫內分析](sqldev-in-database-python-for-sql-developers.md)