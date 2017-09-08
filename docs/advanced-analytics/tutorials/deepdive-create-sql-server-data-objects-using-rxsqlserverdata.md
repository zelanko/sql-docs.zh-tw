---
title: "使用 RxSqlServerData 建立 SQL Server 資料物件 | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: bcf5f7ff-795b-4815-b163-bcddd496efce
caps.latest.revision: 18
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a1da660f019ca7665735c3d9aeb352a37214924
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata"></a>使用 RxSqlServerData 建立 SQL Server 資料物件

現在您已建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫並具有使用資料的必要權限，您將在 R 中建立物件，以便讓您在伺服器和工作站上使用資料。

## <a name="create-the-sql-server-data-objects"></a>建立 SQL Server 資料物件

在此步驟中，您將使用 R 建立並填入兩個資料表。 這兩個資料表包含模擬的信用卡詐騙資料。 一個資料表是用於定型模型，另一個資料表是用於計分。

為了在遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上建立資料表，您將使用 **RxSqlServerData** RevoScaleR **套件中提供的** 函數。

> [!TIP]
> 如果您是使用 R Tools for Visual Studio，請從工具列中選取 [R Tools]，然後按一下 [視窗] 查看用於偵錯以及檢視 R 變數的選項。

### <a name="create-the-training-data-table"></a>建立定型資料的資料表

1. 在 R 變數中提供您的資料庫連接字串。 我們在這裡提供適用於 SQL Server 的兩個有效 ODBC 連接字串範例︰一個使用 SQL 登入，一個適用於 Windows 整合式驗證 (建議)。

    **使用 SQL 登入**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name; Database=DeepDive;Uid=user_name;Pwd=password"
    ```

    **使用 Windows 驗證**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
    ```

    請務必視需要修改執行個體名稱、資料庫名稱、使用者名稱和密碼。
  
2. 指定您想要建立的資料表名稱，並將它儲存在 R 變數中。
  
    ```R
    sqlFraudTable <- "ccFraudSmall"
    ```
  
    因為已將執行個體和資料庫名稱指定為連接字串的一部分，所以當您合併兩個變數時，新資料表的「完整」名稱會變成 _instance.database.schema.ccFraudSmall_.。
  
3.  具現化資料來源物件之前，請加入一行，指定額外的參數 *rowsPerRead*。  *rowsPerRead* 參數可控制每個批次讀取的資料列數目。
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    雖然這是選擇性參數，但對於處理記憶體使用量和有效率的計算而言很重要。  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中的大多數增強型分析函數會分區塊處理資料並累積中繼結果，然後在讀取所有資料之後，傳回最終計算結果。
  
    如果此參數的值太大，資料存取可能會變慢，因為您沒有足夠的記憶體，可有效率地處理這類大型資料區塊。  在某些系統上，如果 *rowsPerRead* 的值太小，效能可能會變慢。
  
    在本逐步解說中，您將使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體所定義的批次處理大小，來控制每個區塊中的資料列數目，並將該值儲存在 *sqlRowsPerRead*變數中。  當您使用大型資料集時，建議您在系統上試驗這項設定。
  
4.  最後，定義新的資料來源物件的變數，並將先前定義 RxSqlServerData 建構函式引數傳遞。 請注意，這只會建立資料來源物件，並不會在其中填入資料。
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

#### <a name="to-create-the-scoring-data-table"></a>建立計分資料表

您將會使用相同的程序，來建立保存計分資料的資料表。

1. 建立新的 R 變數 *sqlScoreTable*，來儲存用於計分的資料表名稱。
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. 提供做為引數至 RxSqlServerData 函式來定義第二個資料來源物件，該變數*sqlScoreDS*。
  
    ```R
    sqlScoreDS \<- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

因為您已定義連接字串和其他參數作為 R 工作區中的變數，所以可以輕鬆地建立不同資料表、檢視或查詢的新資料來源；只要指定不同的資料表名稱即可。

稍後在本教學課程中，您將了解如何建立以 SQL 查詢為基礎的資料來源物件。

## <a name="load-data-into-sql-tables-using-r"></a>使用 R 將資料載入 SQL 資料表

現在您已建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，您可以使用適當的 **Rx** 函數將資料載入其中。

**RevoScaleR**封裝包含支援許多不同的資料來源函式： 文字資料，您將使用 RxTextData 來產生資料來源物件。 還有其他函數，可從 Hadoop 資料、ODBC 資料等建立資料來源物件。

> [!NOTE]
> 在本節中，您必須具有資料庫的「執行 DDL」權限。

### <a name="load-data-into-the-training-table"></a>定型資料表將資料載入

1. 建立 R 變數， *ccFraudCsv*，並指派給此變數包含的範例資料的 CSV 檔案的檔案路徑。
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    請注意公用程式函數 **rxGetOption**。 此函數隨附於 **RevoScaleR** 套件中，可協助您設定及管理與本機和遠端計算內容相關的選項，例如預設共用目錄、用於計算的處理器 (核心) 數目等等。這個呼叫是很有用，因為它會從正確的程式庫，不論執行您的程式碼取得這些範例。 例如，嘗試在 SQL Server 和開發電腦上執行函數，並查看路徑的差異。
  
2. 定義變數，以儲存新的資料，並使用指定的文字資料來源的 RxTextData 函式。
  
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
  
    如您所見，雖然已在本機工作區中建立 R 資料物件，但尚未在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中建立資料表。 此外，任何資料已經從不載入文字檔案放入 R 變數中。
  
4. 現在，呼叫 **rxDataStep** 函數，將資料插入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
  
    如果連接字串沒有任何問題，則在短暫暫停之後，您應該會看到類似如下的結果：
  
      *Total Rows written: 10000, Total time: 0.466*

      *Rows Read: 10000, Total Rows Processed: 10000, Total Chunk Time: 0.577 seconds*
  
5. 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]重新整理資料表清單。 若要確認每個變數具有正確的資料類型及匯入成功，您也可以以滑鼠右鍵按一下資料表中的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]選取**選取前 1000 個資料列**。

### <a name="load-data-into-the-scoring-table"></a>計分的資料表將資料載入

1. 您將遵循相同的步驟，將用於計分的資料集載入資料庫。
  
    一開始先提供來源檔案的路徑。
  
    ```R
    ccScoreCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudScoreSmall.csv")
    ```
  
2. 若要取得的資料，並將它儲存在變數中，使用 RxTextData 函式*inTextData*。
  
    ```R
    inTextData <- RxTextData(file = ccScoreCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer"))
    ```
  
3.  呼叫 rxDataStep 函式，以新的結構描述和資料覆寫目前的資料表。
  
    ```R
    rxDataStep(inData = inTextData, sqlScoreDS, overwrite = TRUE)
    ```
  
    - *InData* 引數會定義要使用的資料來源。
  
    - *OutFile* 引數會指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的資料表，這是您要儲存資料的位置。
  
    - 如果資料表已存在，而且您未使用 *overwrite* 選項，就會插入而不會截斷結果。
  
同樣地，如果連線成功，您應該會看到一則訊息，指出完成以及將資料寫入資料表所需的時間︰

*Total Rows written: 10000, Total time: 0.384*

*Rows Read: 10000, Total Rows Processed: 10000, Total Chunk Time: 0.456 seconds*

## <a name="more-about-rxdatastep"></a>進一步了解 rxDataStep

**RxDataStep**是強大的函數可在將資料轉換成目的地所需的表示法的 R 資料框架上執行多個轉換。 在本例中，目的地是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

您也可以在資料上，指定轉換在 rxDataStep 引數中使用 R 函式。 您會看到這些作業稍後的範例。

## <a name="next-step"></a>下一個步驟

[查詢及修改 SQL Server 資料](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)

## <a name="previous-step"></a>上一個步驟

[使用 SQL Server 資料使用 R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)


