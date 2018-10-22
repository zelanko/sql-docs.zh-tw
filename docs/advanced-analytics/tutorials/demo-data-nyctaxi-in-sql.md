---
title: 下載 NYC 計程車示範資料和指令碼內嵌 R 和 Python （SQL Server 機器學習服務） |Microsoft Docs
description: 指示下載紐約市計程車資料的範例，並建立資料庫。 資料會在 SQL Server 教學課程示範如何內嵌 R 和 Python 中 SQL Server 預存程序和 T-SQL 函數。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/19/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 9359bb9a441551d16bc5de3f57f0158e56a98626
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2018
ms.locfileid: "49463035"
---
# <a name="nyc-taxi-demo-data-for-sql-server"></a>適用於 SQL Server 的 NYC 計程車示範資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章說明如何設定從公用資料所組成的範例資料庫[紐約市計程車和禮車委託](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)。 這項資料可在數個 R 和 Python 教學課程中的 SQL Server 中的資料庫內分析。 範例資料是公用的資料集的 1%。 在您系統上，將資料庫備份檔案是稍微超過 90 MB，提供資料表中的主要資料的 1.7 百萬個資料列。

若要完成此練習中，您應該具備[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017)或其他工具，可以還原資料庫備份檔案，並執行 T-SQL 查詢。

教學課程和快速入門使用此資料集包含下列項目：

+  [使用 SQL Server 中的 Python 模型訓練和評分](train-score-using-python-in-tsql.md)

## <a name="download-demo-database"></a>下載示範資料庫

範例資料庫是由 Microsoft 裝載的備份檔案。 立即當您按一下連結時，就會開始下載檔案。 

檔案大小大約是 90 MB。

1. 按一下  [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak)下載資料庫備份檔案。

2. 將檔案複製到 C:\Program files\Microsoft SQL Server\MSSQL 執行個體 name\MSSQL\Backup 資料夾中。

3. 在 Management Studio 中，以滑鼠右鍵按一下**資料庫**，然後選取**還原檔案和檔案群組**。

4. 請輸入*NYCTaxi_Sample*做為資料庫名稱。

5. 按一下 **從裝置**，然後開啟 選取備份檔案的 選取檔案 頁面。 按一下 **新增**選取 NYCTaxi_Sample.bak。

6. 選取 **還原**核取方塊，按一下 **確定**來還原資料庫。

## <a name="review-database-objects"></a>檢閱資料庫物件
   
確認資料庫物件上存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 您應該會看到資料庫、 資料表、 函數和預存程序。
  
   ![rsql_devtut_BrowseTables](media/rsql-devtut-browsetables.png "rsql_devtut_BrowseTables")

### <a name="objects-in-nyctaxisample-database"></a>NYCTaxi_Sample 資料庫中的物件

下表摘要說明在 NYC 計程車示範資料庫中建立的物件。

|**物件名稱**|**物件類型**|**說明**|
|----------|------------------------|---------------|
|**NYCTaxi_Sample** | [資料庫] |建立-db-tb-上傳-data.sql 指令碼建立。 建立資料庫和兩個資料表：<br /><br />dbo.nyctaxi_sample 資料表： 包含主要紐約市計程車資料集。 叢集資料行存放區索引會加入資料表，以提升儲存體和查詢效能。 NYC 計程車資料集的 1%樣本會插入此資料表。<br /><br />dbo.nyc_taxi_models 資料表： 用來保存定型的進階的分析模型。|
|**fnCalculateDistance** |純量值函式 | FnCalculateDistance.sql 指令碼建立。 計算上車與下車位置之間的直線距離。 此函式會在[建立資料特徵](sqldev-create-data-features-using-t-sql.md)，[定型及儲存模型](sqldev-train-and-save-a-model-using-t-sql.md)並[R 模型作業化](sqldev-operationalize-the-model.md)。|
|**fnEngineerFeatures** |資料表值函式 | FnEngineerFeatures.sql 指令碼建立。 建立新的資料特徵來訓練模型。 此函式會在[建立資料特徵](sqldev-create-data-features-using-t-sql.md)並[R 模型作業化](sqldev-operationalize-the-model.md)。|
|**PlotHistogram** |預存程序 | PlotHistogram.sql 指令碼建立。 呼叫 R 函數，以繪製變數的長條圖，然後傳回繪圖作為二進位物件。 這個預存程序會在[瀏覽及視覺化資料](sqldev-explore-and-visualize-the-data.md)。|
|**PlotInOutputFiles** |預存程序| PlotInOutputFiles.sql 指令碼建立。 建立使用 R 函數的圖形，並接著會將輸出儲存為本機 PDF 檔案。 這個預存程序會在[瀏覽及視覺化資料](sqldev-explore-and-visualize-the-data.md)。|
|**PersistModel** |預存程序 | PersistModel.sql 指令碼建立。 接受已序列化為 varbinary 資料類型，並將它寫入至指定資料表的模型。 |
|**PredictTip**  |預存程序 |PredictTip.sql 指令碼建立。 呼叫所定型的模型，來使用模型建立預測。 此預存程序接受查詢作為其輸入參數，並傳回包含輸入資料列分數的數值資料行。 這個預存程序會在[使 R 模型作業化](sqldev-operationalize-the-model.md)。|
|**PredictTipSingleMode**  |預存程序| PredictTipSingleMode.sql 指令碼建立。 呼叫所定型的模型，來使用模型建立預測。 此預存程序接受新的觀察值作為輸入，其個別特徵值會當作內嵌參數傳遞，並傳回值以預測新觀察值的結果。 這個預存程序會在[使 R 模型作業化](sqldev-operationalize-the-model.md)。|
|**TrainTipPredictionModel**  |預存程序|TrainTipPredictionModel.sql 指令碼建立。 藉由呼叫 R 封裝，可訓練羅吉斯迴歸模型。 此模型會預測已支付小費資料行的值，並使用隨機選取的 70%資料進行定型。 此預存程序會輸出已定型的模型，並儲存在資料表 nyc_taxi_models 中。 這個預存程序會在[定型及儲存模型](sqldev-train-and-save-a-model-using-t-sql.md)。|

## <a name="query-data-for-verification"></a>驗證查詢資料

驗證步驟中，執行查詢，以確認資料已上傳。

1. 在 [物件總管] 的資料庫，以滑鼠右鍵按一下**NYCTaxi_Sample**資料庫，然後開始新的查詢。

2. 執行一些簡單的查詢：

    ```sql
    SELECT TOP(10) * FROM dbo.nyctaxi_sample;
    SELECT COUNT(*) FROM dbo.nyctaxi_sample;
    ```
資料庫包含 1.7 百萬個資料列。

## <a name="next-steps"></a>後續步驟

NYC 計程車資料範例現在可供實際操作學習。

+ [了解在 SQL Server 中使用 R 的資料庫內分析](sqldev-in-database-r-for-sql-developers.md)