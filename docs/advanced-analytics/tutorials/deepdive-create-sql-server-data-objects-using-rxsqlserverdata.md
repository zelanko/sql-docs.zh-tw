---
title: 使用 RevoScaleR RxSqlServerData 建立 SQL Server 資料物件
description: 有關如何在 SQL Server 上使用 R 語言建立資料物件的教學課程逐步解說。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 403f71b4c04d4017094fb7de85ae5de36bcb2c68
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714904"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-server-and-revoscaler-tutorial"></a>使用 RxSqlServerData 建立 SQL Server 資料物件 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

這一課是[RevoScaleR 教學](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)課程的一部分, 說明如何搭配 SQL Server 使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。

第二課是資料庫建立的接續: 加入資料表和載入資料。 如果 DBA 在第[一課](deepdive-work-with-sql-server-data-using-r.md)建立資料庫並登入, 您可以使用 R IDE (例如 RStudio) 或內建工具 (例如**rgui.exe**) 來新增資料表。

從 R, 連接到 SQL Server 並使用**RevoScaleR**函式來執行下列工作:

> [!div class="checklist"]
> * 建立定型資料和預測的資料表
> * 使用來自本機 .csv 檔案的資料載入資料表

範例資料是模擬的信用卡詐騙資料 (Ccfraud.xdf 資料集), 會分割成定型和評分資料集。 資料檔案包含在**RevoScaleR**中。

使用 R IDE 或**rgui.exe**來完成這些變成。 請務必使用在此位置找到的 R 可執行檔:C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 (如果您使用該工具, 則為 Rgui.exe, 或指向 C:\Program Files\Microsoft\R Client\R_SERVER 的 R IDE)。 具有這些可執行檔的[R 用戶端工作站](../r/set-up-a-data-science-client.md)會被視為本教學課程的先決條件。

## <a name="create-the-training-data-table"></a>建立定型資料表

1. 將資料庫連接字串儲存在 R 變數中。 以下是 SQL Server 的有效 ODBC 連接字串的兩個範例: 一個使用 SQL 登入, 另一個用於 Windows 整合式驗證。 

   請務必適當地修改伺服器名稱、使用者名稱和密碼。

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
  
    由於伺服器實例和資料庫名稱已指定為連接字串的一部分, 因此當您結合這兩個變數時, 新資料表的*完整*名稱會變成*ccFraudSmall*。
  
3.  選擇性地指定*rowsPerRead* , 以控制每個批次中讀取的資料列數目。
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    雖然此參數是選擇性的, 但設定它可能會導致更有效率的計算。 **RevoScaleR**和**MicrosoftML**中的大多數增強型分析函數會以區塊處理資料。 *RowsPerRead*參數會決定每個區塊中的資料列數目。
  
    您可能需要試驗此設定, 以找出正確的平衡。 如果值太大, 如果記憶體不足, 無法以該大小的區塊來處理資料, 則資料存取可能會變慢。 相反地, 在某些系統上, 如果*rowsPerRead*的值太小, 效能也會變慢。
  
    作為初始值, 使用 database engine 實例所定義的預設批次進程大小來控制每個區塊中的資料列數目 (5000 個數據列)。 將該值儲存在變數*sqlrowsperread 中*中。
  
4.  為新的資料來源物件定義變數, 並將先前定義的引數傳遞給**RxSqlServerData**的函式。 請注意，這只會建立資料來源物件，並不會在其中填入資料。 載入資料是個別的步驟。
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

## <a name="create-the-scoring-data-table"></a>建立計分資料表

使用相同的步驟, 使用相同的程式來建立保存計分資料的資料表。

1. 建立新的 R 變數 *sqlScoreTable*，來儲存用於計分的資料表名稱。
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. 提供該變數作為 **RxSqlServerData** 函數的引數，以定義第二個資料來源物件 *sqlScoreDS*。
  
    ```R
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

因為您已經將連接字串和其他參數定義為 R 工作區中的變數, 所以您可以針對代表不同資料表、views 或查詢的新資料來源重複使用它。

> [!NOTE]
> 函式會使用不同的引數來定義以整個資料表為基礎的資料來源, 而不是以查詢為基礎的資料來源。 這是因為 SQL Server 資料庫引擎必須以不同的方式來準備查詢。 稍後在本教學課程中, 您將瞭解如何建立以 SQL 查詢為基礎的資料來源物件。

## <a name="load-data-into-sql-tables-using-r"></a>使用 R 將資料載入 SQL 資料表

現在您已建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，您可以使用適當的 **Rx** 函數將資料載入其中。

**RevoScaleR**封裝包含資料來源類型特有的函數。 若為文字資料, 請使用[RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata)來產生資料來源物件。 還有其他函數，可從 Hadoop 資料、ODBC 資料等建立資料來源物件。

> [!NOTE]
> 在此區段中, 您必須擁有資料庫的「**執行 DDL** 」許可權。

### <a name="load-data-into-the-training-table"></a>將資料載入定型資料表

1. 建立 R 變數*ccFraudCsv*, 並將包含範例資料之 CSV 檔案的檔案路徑指派給變數。 此資料集是在**RevoScaleR**中提供。 "SampleDataDir" 是**rxGetOption**函數上的關鍵字。
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    請注意**rxGetOption**的呼叫, 這是與**RevoScaleR**中的[rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions)相關聯的 GET 方法。 使用此公用程式來設定和列出與本機和遠端計算內容相關的選項, 例如預設共用目錄, 或用於計算的處理器 (核心) 數目。
    
    此特定呼叫會從正確的程式庫取得範例, 而不論您執行程式碼的位置為何。 例如，嘗試在 SQL Server 和開發電腦上執行函數，並查看路徑的差異。
  
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
  
3. 此時, 您可能會想要暫停一段時間, 並在中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]查看您的資料庫。 請重新整理資料庫中的資料表清單。
  
    您可以看到, 雖然已在本機工作區中建立 R 資料物件, 但尚未在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫中建立資料表。 此外, 也沒有任何資料從文字檔載入至 R 變數。
  
4. 藉由呼叫函數[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)函數來插入資料。
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
    
    如果連接字串沒有任何問題，則在短暫暫停之後，您應該會看到類似如下的結果：
  
    *寫入的資料列總數:10000, 總時間:已*讀取 0.466 *個數據列:10000, 已處理的資料列總數:10000, 總區塊時間:0.577 秒*
  
5. 重新整理資料表清單。 若要確認每個變數都具有正確的資料類型且已成功匯入, 您也可以在中的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]資料表上按一下滑鼠右鍵, 然後選取 [**選取前 1000**個數據列]。

### <a name="load-data-into-the-scoring-table"></a>將資料載入評分表

1. 重複這些步驟, 將用於計分的資料集載入資料庫。
  
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
  
    - 如果資料表已經存在, 而且您未使用 [*覆寫*] 選項, 就會插入結果而不截斷。
  
同樣地，如果連線成功，您應該會看到一則訊息，指出完成以及將資料寫入資料表所需的時間︰

*寫入的資料列總數:10000, 總時間:已*讀取 0.384
個數據列 *:10000, 已處理的資料列總數:10000, 總區塊時間:0.456 秒*

## <a name="more-about-rxdatastep"></a>進一步了解 rxDataStep

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)是功能強大的函式, 可以在 R 資料框架上執行多個轉換。 您也可以使用 rxDataStep, 將資料轉換成目的地所需的標記法: 在此案例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中為。

(選擇性) 您可以在**rxDataStep**的引數中使用 R 函數, 指定資料的轉換。 本教學課程稍後會提供這些作業的範例。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [查詢及修改 SQL Server 資料](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)