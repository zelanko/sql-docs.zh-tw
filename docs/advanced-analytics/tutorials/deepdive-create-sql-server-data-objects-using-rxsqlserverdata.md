---
title: 建立使用 RevoScaleR RxSqlServerData-SQL Server Machine Learning 的 SQL Server 資料物件
description: 教學課程逐步解說如何建立 SQL Server 上使用 R 語言的資料物件。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 45643dbcdc2876fe0794ddb731abe6334537169c
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510355"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-server-and-revoscaler-tutorial"></a>SQL Server 資料使用 RxSqlServerData 建立物件 （SQL Server 和 RevoScaleR 教學課程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這一課是屬於[RevoScaleR 教學課程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

兩個是建立資料庫的接續： 加入資料表和載入資料。 如果是 DBA 建立資料庫和登入[第一課](deepdive-work-with-sql-server-data-using-r.md)中，您可以新增資料表使用的 R IDE，例如 RStudio 或之類的內建工具**Rgui**。

從 R，連接到 SQL Server，並使用**RevoScaleR**函式來執行下列工作：

> [!div class="checklist"]
> * 建立訓練資料和預測資料表
> * 從本機的.csv 檔案載入資料的資料表

範例資料是模擬的信用卡詐騙資料 （ccFraud 資料集），分割成定型和計分資料集。 資料檔案包含在**RevoScaleR**。

使用 R IDE 或**Rgui**完成這些所。 請務必使用這個位置，請參閱 R 可執行檔：C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 (任一 Rgui.exe 如果您正在使用該工具或指向 C:\Program Files\Microsoft\R Client\R_SERVER R IDE)。 擁有[R 用戶端工作站](../r/set-up-a-data-science-client.md)這些可執行檔會被視為本教學課程的必要條件。

## <a name="create-the-training-data-table"></a>建立定型資料表

1. 在 R 變數中儲存的資料庫連接字串。 以下是適用於 SQL Server 的兩個有效 ODBC 連接字串範例： 一個使用 SQL 登入，一個用於 Windows 整合式驗證。 

   請務必修改伺服器名稱、 使用者名稱和適當的密碼。

    **SQL 登入**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=<server-name>; Database=RevoDeepDive;Uid=<user_name>;Pwd=<password>"
    ```

    **Windows 驗證**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=<server-name>;Database=RevoDeepDive;Trusted_Connection=True"
    ```

2. 指定您想要建立的資料表名稱，並將它儲存在 R 變數中。
  
    ```R
    sqlFraudTable <- "ccFraudSmall"
    ```
  
    伺服器執行個體和資料庫名稱會指定為一部分的連接字串，當您合併兩個變數，因為*完整*新的資料表名稱會變成*instance.database.schema.ccFraudSmall*。
  
3.  （選擇性） 指定*rowsPerRead*來控制在每個批次中讀取多少個資料列。
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    雖然這個參數是選擇性的則將其設定會導致更有效率的計算。 增強型分析函數中的大部分**RevoScaleR**並**MicrosoftML**處理區塊中的資料。 *RowsPerRead*參數會決定每個區塊中的資料列數目。
  
    您可能需要嘗試此設定可找到適當的平衡。 如果值太大，資料存取可能會變慢，如果沒有足夠的記憶體來處理該大小的區塊中的資料。 相反地，在某些系統中，如果值*rowsPerRead*太小，效能可以也變慢。
  
    做為初始的值，使用 database engine 執行個體所定義的預設批次程序大小控制每個區塊 （5,000 個資料列） 中的資料列數目。 將該值儲存在變數*sqlRowsPerRead*。
  
4.  定義新的資料來源物件的變數，並將傳遞至先前定義的引數**RxSqlServerData**建構函式。 請注意，這只會建立資料來源物件，並不會在其中填入資料。 載入資料是個別的步驟。
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

## <a name="create-the-scoring-data-table"></a>建立計分資料表

使用相同的步驟，建立保存計分資料使用相同的程序的資料表。

1. 建立新的 R 變數 *sqlScoreTable*，來儲存用於計分的資料表名稱。
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. 提供該變數作為 **RxSqlServerData** 函數的引數，以定義第二個資料來源物件 *sqlScoreDS*。
  
    ```R
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

因為您已作為 R 工作區中的變數定義的連接字串和其他參數，您可以代表不同的資料表、 檢視或查詢的新資料來源的重複使用它。

> [!NOTE]
> 此函數會使用不同的引數來定義比整個資料表，以查詢為基礎的資料來源為基礎的資料來源。 這是因為 SQL Server database engine 必須以不同的方式準備查詢。 稍後在本教學課程中，您將了解如何建立以 SQL 查詢為基礎的資料來源物件。

## <a name="load-data-into-sql-tables-using-r"></a>將資料載入使用 R 的 SQL 資料表

現在您已建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，您可以使用適當的 **Rx** 函數將資料載入其中。

**RevoScaleR**套件包含特定資料來源類型的函數。 針對文字資料，使用[RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata)來產生資料來源物件。 還有其他函數，可從 Hadoop 資料、ODBC 資料等建立資料來源物件。

> [!NOTE]
> 在本節中，您必須擁有**執行 DDL**資料庫的權限。

### <a name="load-data-into-the-training-table"></a>將資料載入定型資料表

1. 建立 R 變數*ccFraudCsv*，並指派給變數包含的範例資料的 CSV 檔案的檔案路徑。 此資料集所提供的**RevoScaleR**。 「 SampleDataDir 」 上是一個關鍵字**rxGetOption**函式。
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    請注意在呼叫**rxGetOption**，其 GET 方法相關聯[rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions)中**RevoScaleR**。 使用此公用程式來設定並與本機和遠端計算內容，例如預設共用的目錄或在計算中使用的處理器 （核心） 數目相關的清單選項。
    
    這個特定的呼叫會取得從正確的程式庫，無論您在其中執行程式碼範例。 例如，嘗試在 SQL Server 和開發電腦上執行函數，並查看路徑的差異。
  
2. 定義一個變數來儲存新的資料，並使用 **RxTextData** 函數來指定文字資料來源。
  
    ```R
    inTextData <- RxTextData(file = ccFraudCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer",
        "fraudRisk" = "integer"))
    ```
  
    引數 *colClasses* 很重要。 您可以使用此引數，指出要指派給從文字檔載入之每個資料行的資料類型。 在此範例中，所有資料行都會當作文字來處理，除了具名資料行之外，該資料行會當作整數來處理。
  
3. 此時，您可能想要暫停的時間，並檢視您的資料庫[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 請重新整理資料庫中的資料表清單。
  
    您所見，雖然 R 資料物件已建立本機工作區中，已建立資料表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。 此外，任何資料已不載入從文字檔 R 變數。
  
4. 將資料插入呼叫函式[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)函式。
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
    
    如果連接字串沒有任何問題，則在短暫暫停之後，您應該會看到類似如下的結果：
  
    *寫入的資料列總數：10000，總時間：0.466* *讀取的資料列：10000，總處理的資料列：10000 的 total Chunk Time:0.577 秒*
  
5. 重新整理資料表清單。 若要確認每個變數具有正確的資料類型，且已成功匯入，您也可以以滑鼠右鍵按一下資料表中的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然後選取**選取前 1000 個資料列**。

### <a name="load-data-into-the-scoring-table"></a>將資料載入計分資料表

1. 重複步驟來載入資料集用於計分的資料庫。
  
    一開始先提供來源檔案的路徑。
  
    ```R
    ccScoreCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudScoreSmall.csv")
    ```
  
2. 使用 **RxTextData** 函數來取得資料，並將它儲存在變數 *inTextData*中。
  
    ```R
    inTextData <- RxTextData(file = ccScoreCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer"))
    ```
  
3.  呼叫 **rxDataStep** 函數，以新的結構描述和資料覆寫目前的資料表。
  
    ```R
    rxDataStep(inData = inTextData, sqlScoreDS, overwrite = TRUE)
    ```
  
    - *InData* 引數會定義要使用的資料來源。
  
    - *OutFile* 引數會指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的資料表，這是您要儲存資料的位置。
  
    - 如果資料表已存在，而且您不使用*覆寫*選項時，結果會插入而不會截斷。
  
同樣地，如果連線成功，您應該會看到一則訊息，指出完成以及將資料寫入資料表所需的時間︰

*寫入的資料列總數：10000，總時間：0.384*
*讀取的資料列：10000，總處理的資料列：10000 的 total Chunk Time:0.456 秒*

## <a name="more-about-rxdatastep"></a>進一步了解 rxDataStep

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)是強大的函數，可對 R 資料框架執行多個轉換。 您也可以將資料轉換成目的地所需的表示法使用 rxDataStep： 在此情況下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

（選擇性），您可以在資料上，指定轉換的引數中使用 R 函數**rxDataStep**。 本教學課程稍後會提供這些作業的範例。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [查詢及修改 SQL Server 資料](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)