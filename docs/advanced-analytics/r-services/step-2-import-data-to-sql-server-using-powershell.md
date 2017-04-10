---
title: "步驟 2︰使用 PowerShell 將資料匯入 SQL Server (資料庫內進階分析教學課程) | Microsoft Docs"
ms.custom: ""
ms.date: "08/05/2016"
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
  - "TSQL"
ms.assetid: 3c5b5145-fa57-455a-b153-0400fc062dc0
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 步驟 2︰使用 PowerShell 將資料匯入 SQL Server (資料庫內進階分析教學課程)
在此步驟中，您將執行其中一個下載的指令碼，建立本逐步解說所需的資料庫物件。 此指令碼也會建立您將會使用的大部分預存程序，並將範例資料上傳至您指定的資料庫資料表。  
  
## 執行指令碼來建立 SQL 物件  
在下載的檔案中，您應該會看到 PowerShell 指令碼。 為了準備本逐步解說的環境，您將執行此指令碼。  
  
指令碼所執行的動作包括：  
  
-   如果尚未安裝，請安裝 SQL Native Client 和 SQL 命令列公用程式。 使用 **bcp** 將資料大量載入資料庫時，需要這些公用程式。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上建立資料庫和資料表，並將資料大量插入資料表。  
  
-   建立多個 SQL 函數與預存程序。  
  
#### 執行指令碼  
1.  以系統管理員身分開啟 PowerShell 命令提示字元，然後執行下列命令。  
  
    ```  
    .\RunSQL_SQL_Walkthrough.ps1  
    ```  
  
    系統會提示您輸入下列資訊：  
  
    -   [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 安裝所在之 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體的名稱或位址  
  
    -   執行個體上之帳戶的使用者名稱和密碼。 您使用的帳戶必須能夠建立資料庫、建立資料表和預存程序，以及將資料上傳至資料表。  
  
    -   您剛才下載之範例資料檔案的路徑和檔案名稱。 例如：  
  
        `C:\tempRSQL\nyctaxi1pct.csv`  
  
2.  在此步驟中，也會修改所有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼，以您提供作為指令碼輸入的資料庫名稱和使用者名稱取代預留位置。  
  
    請花幾分鐘檢閱指令碼所建立的預存程序和函數。  
  
    |||  
    |-|-|  
    |**SQL 指令碼檔案名稱**|**函數**|  
    |create-db-tb-upload-data.sql|建立資料庫和兩個資料表：<br /><br />nyctaxi_sample︰包含主要紐約市計程車資料集。 叢集資料行存放區索引會加入資料表，以提升儲存體和查詢效能。 紐約市計程車資料集的 1% 樣本會插入此資料表。<br /><br />nyc_taxi_models︰用來保存所定型的進階分析模型。|  
    |fnCalculateDistance.sql|建立純量值函式，以計算上車與下車位置之間的直線距離|  
    |fnEngineerFeatures.sql|建立資料表值函式，以建立用於定型模型的新資料特徵|  
    |PersistModel.sql|建立可呼叫以儲存模型的預存程序。 此預存程序接受已序列化為 varbinary 資料類型的模型，並將其寫入指定的資料表。|  
    |PredictTipBatchMode.sql|建立呼叫所定型之模型的預存程序，以使用該模型來建立預測。 此預存程序接受查詢作為其輸入參數，並傳回包含輸入資料列分數的數值資料行。|  
    |PredictTipSingleMode.sql|建立呼叫所定型之模型的預存程序，以使用該模型來建立預測。 此預存程序接受新的觀察值作為輸入，其個別特徵值會當作內嵌參數傳遞，並傳回值以預測新觀察值的結果。|  
  
    在本逐步解說後半部，您將建立一些額外的預存程序：  
  
    |||  
    |-|-|  
    |**SQL 指令碼檔案名稱**|**函數**|  
    |PlotHistogram.sql|建立預存程序進行資料瀏覽。 此預存程序會呼叫 R 函數，以繪製變數的長條圖，然後傳回繪圖作為二進位物件。|  
    |PlotInOutputFiles.sql|建立預存程序進行資料瀏覽。 此預存程序使用 R 函數來建立圖形，然後將輸出儲存為本機 PDF 檔案。|  
    |TrainTipPredictionModel.sql|藉由呼叫 R 套件來建立預存程序，以將羅吉斯迴歸模型定型。 此模型會預測已支付小費資料行的值，並使用隨機選取的 70%資料進行定型。 此預存程序會輸出已定型的模型，並儲存在資料表 nyc_taxi_models 中。|  
  
3.  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 及您指定的登入，登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，確認您可以看到已建立的資料庫、資料表、函數和預存程序。  
  
    ![rsql_devtut_BrowseTables](../../advanced-analytics/r-services/media/rsql-devtut-browsetables.PNG "rsql_devtut_BrowseTables")  
  
    > [!NOTE]  
    > 如果資料庫物件已存在，就無法再次建立。  
    >   
    > 如果資料表已存在，則會附加而不是覆寫資料。 因此，請務必捨棄任何現有的物件，再執行指令碼。  
  
## 下一個步驟  
[步驟 3：瀏覽及視覺化資料](../../advanced-analytics/r-services/step-3-explore-and-visualize-the-data-in-database-advanced-analytics-tutorial.md)  
  
## 上一個步驟  
[步驟 1︰下載範例資料](../../advanced-analytics/r-services/step-1-download-the-sample-data-in-database-advanced-analytics-tutorial.md)  
  
## 另請參閱  
[適用於 SQL 開發人員的資料庫內進階分析 &#40;教學課程&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[SQL Server R Services 教學課程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
