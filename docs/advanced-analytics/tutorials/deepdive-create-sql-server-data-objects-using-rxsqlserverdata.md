---
title: 建立 SQL Server 資料物件使用 RxSqlServerData （SQL 與 R 深入探討） |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e15c3e7c13c1be4f524c25bb1cec6da3c8e20c7e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-and-r-deep-dive"></a>建立使用 RxSqlServerData （SQL 與 R 深入探討） 的 SQL Server 資料物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是資料科學深入探討教學課程中，有關如何使用一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

現在您已建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫，而且擁有處理資料的必要權限。 在此步驟中，您可以建立可讓您處理資料的 R 中的某些物件。

## <a name="create-the-sql-server-data-objects"></a>建立 SQL Server 資料物件

在此步驟中，您可以使用函式從**RevoScaleR**封裝建立和擴展這兩個資料表。 一個資料表是用於定型模型，另一個資料表是用於計分。 這兩個資料表包含模擬的信用卡詐騙資料。

若要建立遠端資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]電腦，請呼叫**RxSqlServerData**函式。

> [!TIP]
> 如果您是使用 R Tools for Visual Studio，請從工具列中選取 [R Tools]，然後按一下 [視窗] 查看用於偵錯以及檢視 R 變數的選項。

### <a name="create-the-training-data-table"></a>建立定型資料的資料表

1. R 變數中儲存資料庫連接字串。 以下是有效的 ODBC 連接字串，適用於 SQL Server 的兩個範例： 使用 SQL 登入，而另一個用於 Windows 整合式驗證。

    **SQL 登入**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name; Database=DeepDive;Uid=user_name;Pwd=password"
    ```

    **Windows 驗證**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
    ```

    請務必視需要修改執行個體名稱、資料庫名稱、使用者名稱和密碼。
  
2. 指定您想要建立的資料表名稱，並將它儲存在 R 變數中。
  
    ```R
    sqlFraudTable <- "ccFraudSmall"
    ```
  
    因為已將執行個體和資料庫名稱指定為連接字串的一部分，所以當您合併兩個變數時，新資料表的「完整」名稱會變成 _instance.database.schema.ccFraudSmall_。
  
3.  具現化資料來源物件之前，請加入一行，指定額外的參數 *rowsPerRead*。  *rowsPerRead* 參數可控制每個批次讀取的資料列數目。
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    雖然這是選擇性參數，但對於處理記憶體使用量和有效率的計算而言很重要。  增強的分析函數中，大部分[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]處理區塊中的資料和儲存中繼結果，傳回最後一個計算在所有的資料已讀取。
  
    如果此參數的值太大，資料存取可能會變慢，因為您沒有足夠的記憶體，可有效率地處理這類大型資料區塊。  在某些系統上，如果 *rowsPerRead* 的值太小，效能可能會變慢。 因此，我們建議您試驗這項設定您的系統上使用大型資料集時。
  
    本逐步解說中，使用所定義的預設批次程序大小[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]來控制每個區塊中的資料列數目的執行個體。 將值儲存在變數中`sqlRowsPerRead`。
  
4.  最後，定義新的資料來源物件的變數，並將先前定義 RxSqlServerData 建構函式引數傳遞。 請注意，這只會建立資料來源物件，並不會在其中填入資料。
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

#### <a name="to-create-the-scoring-data-table"></a>建立計分資料表

使用相同的步驟，建立資料表所在的計分的資料，使用相同的程序。

1. 建立新的 R 變數 *sqlScoreTable*，來儲存用於計分的資料表名稱。
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. 提供做為引數至 RxSqlServerData 函式來定義第二個資料來源物件，該變數*sqlScoreDS*。
  
    ```R
    sqlScoreDS \<- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

因為您已經為 R 工作空間中的變數定義連接字串與其他參數，很容易就能建立新的資料來源，針對不同的資料表、 檢視或查詢。

> [!NOTE]
> 此函數會使用不同的引數來定義比整份資料表的查詢為基礎的資料來源為基礎的資料來源。 這是因為 SQL Server database engine 必須以不同的方式準備查詢。 稍後在本教學課程中，您會學習如何建立 SQL 查詢為基礎的資料來源物件。

## <a name="load-data-into-sql-tables-using-r"></a>資料載入至使用 R 的 SQL 資料表

現在您已建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，您可以使用適當的 **Rx** 函數將資料載入其中。

**RevoScaleR**封裝包含支援許多不同的資料來源函式： 文字資料，使用[RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata)來產生資料來源物件。 還有其他函數，可從 Hadoop 資料、ODBC 資料等建立資料來源物件。

> [!NOTE]
> 這個區段中，您必須擁有**執行 DDL**資料庫的權限。

### <a name="load-data-into-the-training-table"></a>定型資料表將資料載入

1. 建立 R 變數， *ccFraudCsv*，並指派給此變數包含的範例資料的 CSV 檔案的檔案路徑。
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    請注意在呼叫**rxGetOption**，這 GET 方法與相關聯[rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions)中**RevoScaleR**。 使用此公用程式來設定和清單選項與本機和遠端計算內容，例如預設共用的目錄或要在計算中使用的處理器 （核心） 數目。
    
    這個特定的呼叫會取得從正確的程式庫，不論執行您的程式碼範例。 例如，嘗試在 SQL Server 和開發電腦上執行函數，並查看路徑的差異。
  
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
  
3. 此時，您可能想要暫停的時刻，並檢視您的資料庫中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  請重新整理資料庫中的資料表清單。
  
    您所見，雖然 R 資料物件已建立本機工作區中，已建立資料表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。 此外，任何資料已經從不載入文字檔案放入 R 變數中。
  
4. 現在，呼叫 [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 函數，將資料插入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
  
    如果連接字串沒有任何問題，則在短暫暫停之後，您應該會看到類似如下的結果：
  
      *Total Rows written: 10000, Total time: 0.466*

      *Rows Read: 10000, Total Rows Processed: 10000, Total Chunk Time: 0.577 seconds*
  
5. 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]重新整理資料表清單。 若要確認每個變數具有正確的資料類型及匯入成功，您也可以以滑鼠右鍵按一下資料表中的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]選取**選取前 1000 個資料列**。

### <a name="load-data-into-the-scoring-table"></a>計分的資料表將資料載入

1. 重複步驟以載入資料集用於計分到資料庫。
  
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
  
    - 如果資料表已經存在，而且您不使用*覆寫*選項，而不會截斷插入結果。
  
同樣地，如果連線成功，您應該會看到一則訊息，指出完成以及將資料寫入資料表所需的時間︰

*Total Rows written: 10000, Total time: 0.384*

*Rows Read: 10000, Total Rows Processed: 10000, Total Chunk Time: 0.456 seconds*

## <a name="more-about-rxdatastep"></a>進一步了解 rxDataStep

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)是強大的函數可以在 R 資料框架上執行多個轉換。 您也可以將資料轉換成目的地所需的表示法使用 rxDataStep： 在此情況下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

（選擇性） 使用的 R 函數的引數中的資料，指定轉換**rxDataStep**。 稍後在本教學課程將提供這些作業的範例。

## <a name="next-step"></a>下一步

[查詢及修改 SQL Server 資料](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)

## <a name="previous-step"></a>上一個步驟

[使用 SQL Server 資料使用 R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
