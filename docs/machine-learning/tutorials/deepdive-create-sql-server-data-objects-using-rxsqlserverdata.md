---
title: 建立 RxSqlServerData 物件
description: RevoScaleR 教學課程 2：如何在 SQL Server 上使用 R 語言建立資料物件。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4bd3b33e7549d0b0e9d4fabb9b873b51a1fce418
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116941"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-server-and-revoscaler-tutorial"></a>使用 RxSqlServerData 建立 SQL Server 資料物件 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

此教學課程是 [RevoScaleR 教學課程系列](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的第 2 個，該系列說明如何搭配 SQL Server 使用 [RevoScaleR 函式](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) \(英文\)。

此教學課程接續資料庫建立：新增資料表及載入資料。 如果 DBA 在[教學課程二](deepdive-work-with-sql-server-data-using-r.md)中建立資料庫並登入，您可以使用 R IDE (例如 RStudio) 或內建工具 (例如 **Rgui**) 來新增資料表。

從 R 連線到 SQL Server，並且使用 **RevoScaleR** 函式來執行下列工作：

> [!div class="checklist"]
> * 建立資料表以定型資料和預測
> * 載入具有資料 (來自本機 .csv 檔案) 的資料表

範例資料是模擬的信用卡詐騙資料 (ccFraud 資料集)，會分割成定型和評分資料集。 資料檔案包含在 **RevoScaleR** 中。

使用 R IDE 或 **Rgui** 來完成這些工作。 請務必使用在以下位置找到的 R 可執行檔：C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 (如果您使用 Rgui.exe 則為該工具，或者如果是 R IDE 則指向 C:\Program Files\Microsoft\R Client\R_SERVER)。 讓 [R 用戶端工作站](../r/set-up-a-data-science-client.md)具有這些可執行檔，是本教學課程的必要條件。

## <a name="create-the-training-data-table"></a>建立定型資料表

1. 在 R 變數中儲存資料庫連接字串。 以下是適用於 SQL Server 的兩個有效 ODBC 連接字串範例︰一個使用 SQL 登入，一個適用於 Windows 整合式驗證。 

   請務必視需要修改伺服器名稱、使用者名稱和密碼。

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
  
    因為已將伺服器執行個體和資料庫名稱指定為連接字串的一部分，所以當您合併兩個變數時，新資料表的「完整」  名稱會變成 instance.database.schema.ccFraudSmall  。
  
3.  選擇性指定 rowsPerRead  ，以控制每個批次中讀取的資料列數目。
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    雖然這個參數是選擇性的，但是設定它可以讓計算更有效率。 **RevoScaleR** 和 **MicrosoftML** 中的大部分增強型分析函式會以區塊形式處理資料。 rowsPerRead  參數會決定每個區塊中的資料列數目。
  
    您可能需要實驗此設定，以找出正確的平衡。 如果值太大，而沒有足夠記憶體可以該大小的區塊形式處理資料，則資料存取可能會變慢。 相反地，在某些系統上，如果 rowsPerRead  的值太小，效能也會變慢。
  
    作為初始值，使用資料庫引擎執行個體所定義的預設批次處理大小，來控制每個區塊中的資料列數目 (5000 個資料列)。 將該值儲存在 sqlRowsPerRead  變數中。
  
4.  為新的資料來源物件定義一個變數，並將先前定義的引數傳遞至 **RxSqlServerData** 建構函式。 請注意，這只會建立資料來源物件，並不會在其中填入資料。 載入資料是個別的步驟。
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

## <a name="create-the-scoring-data-table"></a>建立評分資料表

使用相同的步驟，以相同的程序建立保存評分資料的資料表。

1. 建立新的 R 變數 *sqlScoreTable*，來儲存用於計分的資料表名稱。
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. 提供該變數作為 **RxSqlServerData** 函數的引數，以定義第二個資料來源物件 *sqlScoreDS*。
  
    ```R
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

因為您已經將連接字串和其他參數定義為 R 工作區中的變數，所以您可以針對代表不同資料表、檢視或查詢的新資料來源重複使用它。

> [!NOTE]
> 函式會使用不同的引數，以整個資料表為基礎定義資料來源，而不是以查詢為基礎定義資料來源。 這是因為 SQL Server 資料庫引擎必須以不同的方式來準備查詢。 稍後在本教學課程中，您將了解如何建立以 SQL 查詢為基礎的資料來源物件。

## <a name="load-data-into-sql-tables-using-r"></a>使用 R 將資料載入 SQL 資料表

現在您已建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，您可以使用適當的 **Rx** 函數將資料載入其中。

**RevoScaleR** 套件包含資料來源類型特有的函式。 若為文字資料，請使用 [RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata) 來產生資料來源物件。 還有其他函數，可從 Hadoop 資料、ODBC 資料等建立資料來源物件。

> [!NOTE]
> 在本節中，您必須具有資料庫的**執行 DDL** 權限。

### <a name="load-data-into-the-training-table"></a>將資料載入定型資料表

1. 建立 R 變數 ccFraudCsv  ，並將 CSV 檔案 (包含範例資料) 的檔案路徑指派給變數。 **RevoScaleR** 提供此資料集。 "SampleDataDir" 是 **rxGetOption** 函式上的關鍵字。
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    請注意對 **rxGetOption** 的呼叫，這是與 **RevoScaleR** 中 [rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions) 相關聯的 GET 方法。 使用此公用程式來設定及列出與本機和遠端計算內容相關的選項，例如預設共用目錄，或用於計算的處理器 (核心) 數目。
    
    此特定呼叫會從正確的程式庫取得範例，無論您是在哪裡執行程式碼。 例如，嘗試在 SQL Server 和開發電腦上執行函數，並查看路徑的差異。
  
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
  
3. 此時，您可能想要暫停一下，並檢視 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的資料庫。 請重新整理資料庫中的資料表清單。
  
    如您所見，雖然已在本機工作區中建立 R 資料物件，但尚未在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中建立資料表。 此外，也沒有任何資料從文字檔載入至 R 變數。
  
4. 藉由呼叫 [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 函式來插入資料。
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
    
    如果連接字串沒有任何問題，則在短暫暫停之後，您應該會看到類似如下的結果：
  
    *寫入的資料列總數：10000，總時間：0.466* *讀取的資料列:10000，已處理的資料列總數：10000，總區塊時間：0.577 秒*
  
5. 重新整理資料表清單。 若要確認每個變數具有正確的資料類型且已順利匯入，您也可以使用滑鼠右鍵按一下 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的資料表，然後選取 [選取前 1000 個資料列]  。

### <a name="load-data-into-the-scoring-table"></a>將資料載入評分資料表

1. 重複步驟，將用於評分的資料集載入資料庫。
  
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
  
    - 如果資料表已存在，而且您未使用 overwrite  選項，就會插入而不會截斷結果。
  
同樣地，如果連線成功，您應該會看到一則訊息，指出完成以及將資料寫入資料表所需的時間︰

*寫入的資料列總數：10000，總時間：0.384*
*讀取的資料列：10000，已處理的資料列總數：10000，總區塊時間：0.456 秒*

## <a name="more-about-rxdatastep"></a>進一步了解 rxDataStep

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 是功能強大的函式，可以在 R 資料框架上執行多個轉換。 您也可以使用 rxDataStep，將資料轉換成目的地所需的表示法：在此案例中為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

您可以選擇性地使用引數中的 R 函式來 **rxDataStep**，以指定資料的轉換。 本教學課程稍後會提供這些作業的範例。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [查詢及修改 SQL Server 資料](../../machine-learning/tutorials/deepdive-query-and-modify-the-sql-server-data.md)