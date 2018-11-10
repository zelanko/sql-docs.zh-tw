---
title: 課程 1 的瀏覽和使用 Python 和 T-SQL (SQL Server Machine Learning) 將資料視覺化 |Microsoft Docs
description: 教學課程示範如何內嵌 Python 中 SQL Server 預存程序和 T-SQL 函數
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: cf14409cdb321d2f52196e0793ea092ab9ba2430
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2018
ms.locfileid: "51030975"
---
# <a name="explore-and-visualize-the-data"></a>瀏覽及視覺化資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是教學課程中，部分[適用於 SQL 開發人員的資料庫內 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

在此步驟中，您可以探索範例資料，並產生一些繪圖。 稍後，您會了解如何序列化圖形物件，在 Python 中，然後還原序列化的物件，以進行繪圖。

## <a name="review-the-data"></a>檢閱資料

首先，花點時間瀏覽資料結構描述，因為我們已進行一些變更，以方便使用的 NYC 計程車資料

+ 原始資料集的計程車識別碼和車程記錄用於不同的檔案。 我們已加入兩個原始資料集的資料行_medallion_， _hack_license_，並_pickup_datetime_。  
+ 原始資料集跨越許多檔案，並已相當大。 我們已 downsampled，只取得 1%的原始記錄數目。 目前資料表有 1,703,957 個資料列和 23 的資料行。

**計程車識別碼**

_Medallion_資料行代表計程車的唯一識別碼。

_Hack_license_資料行包含計程車司機駕照號碼 （匿名）。

**車程和小費記錄**

每筆車程記錄都會包含上車和下車位置與時間，以及車程距離。

每筆費用記錄都會包括付款資訊，例如付款類型、總付款金額和小費金額。

最後三個資料行可以用於各種機器學習工作。  _tip_amount_ 資料行包含連續數值，而且可以當成 **label** 資料行來進行迴歸分析。 _tipped_ 資料行只有是/否值，並且用於二元分類。 _tip_class_ 資料行有多個 **類別標籤** ，因此可以當成多類別分類工作的標籤使用。

用於標籤資料行的值都以`tip_amount`資料行中，使用這些商務規則：

+ 標籤資料行`tipped`有可能的值 0 和 1

    如果`tip_amount`> 0， `tipped` = 1，否則為`tipped`= 0

+ 標籤資料行`tip_class`有可能的類別值 0 到 4 之間

    類別 0: `tip_amount` = $0

    類別 1: `tip_amount` > $0 和`tip_amount`< = 美金 5
    
    類別 2: `tip_amount` > $5 和`tip_amount`< = 美金 10
    
    課程 3: `tip_amount` > $10 和`tip_amount`< = 美金 20
    
    類別 4: `tip_amount` > $20

## <a name="create-plots-using-python-in-t-sql"></a>建立在 T-SQL 中使用 Python 的繪圖

開發資料科學方案通常會包含大量資料瀏覽和資料視覺化。 由於視覺效果是這類強大的工具來了解資料和極端值的分佈，Python 會提供許多套件，以視覺化方式呈現資料。 **Matplotlib**模組是其中一個更熱門的程式庫，針對視覺效果，且包含許多函數，可建立長條圖、 散佈圖、 方塊繪圖和其他資料瀏覽圖形。

在本節中，您已了解如何搭配使用預存程序的繪圖。 而是開啟伺服器上的映像，您將 Python 物件儲存`plot`作為**varbinary**資料，然後寫入，到檔案，可以是共用或其他地方檢視。

### <a name="create-a-plot-as-varbinary-data"></a>建立繪圖做為 varbinary 資料

預存程序會傳回序列化的 Python`figure`當做資料流的物件**varbinary**資料。 您無法直接檢視的二進位資料，但是您可以使用用戶端上的 Python 程式碼，以還原序列化，並檢視圖表，並再儲存映像檔，用戶端電腦上。

1. 建立預存程序**PyPlotMatplotlib**，如果 PowerShell 指令碼已未。

    - 變數`@query`定義的查詢文字`SELECT tipped FROM nyctaxi_sample`，為指令碼輸入變數的引數傳遞給 Python 程式碼區塊`@input_data_1`。
    - 是相當簡單的 Python 指令碼： **matplotlib** `figure`物件用來讓色階分佈圖和散佈圖，以及這些物件接著會序列化使用`pickle`程式庫。
    - Python 圖形物件會序列化成**pandas**輸出資料框架。
  
    ```SQL
    DROP PROCEDURE IF EXISTS PyPlotMatplotlib;
    GO

    CREATE PROCEDURE [dbo].[PyPlotMatplotlib]
    AS
    BEGIN
      SET NOCOUNT ON;
      DECLARE @query nvarchar(max) =
      N'SELECT cast(tipped as int) as tipped, tip_amount, fare_amount FROM [dbo].[nyctaxi_sample]'
      EXECUTE sp_execute_external_script
      @language = N'Python',
      @script = N'
    import matplotlib
    matplotlib.use("Agg")
    import matplotlib.pyplot as plt
    import pandas as pd
    import pickle

    fig_handle = plt.figure()
    plt.hist(InputDataSet.tipped)
    plt.xlabel("Tipped")
    plt.ylabel("Counts")
    plt.title("Histogram, Tipped")
    plot0 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.hist(InputDataSet.tip_amount)
    plt.xlabel("Tip amount ($)")
    plt.ylabel("Counts")
    plt.title("Histogram, Tip amount")
    plot1 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.hist(InputDataSet.fare_amount)
    plt.xlabel("Fare amount ($)")
    plt.ylabel("Counts")
    plt.title("Histogram, Fare amount")
    plot2 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    plt.scatter( InputDataSet.fare_amount, InputDataSet.tip_amount)
    plt.xlabel("Fare Amount ($)")
    plt.ylabel("Tip Amount ($)")
    plt.title("Tip amount by Fare amount")
    plot3 = pd.DataFrame(data =[pickle.dumps(fig_handle)], columns =["plot"])
    plt.clf()

    OutputDataSet = plot0.append(plot1, ignore_index=True).append(plot2, ignore_index=True).append(plot3, ignore_index=True)
    ',
    @input_data_1 = @query
    WITH RESULT SETS ((plot varbinary(max)))
    END
    GO
    ```

2. 現在執行預存程序來產生繪圖硬式編碼為輸入的查詢將資料從沒有引數。

    ```
    EXEC [dbo].[PyPlotMatplotlib]
    ```

3. 結果應該類似這樣：
  
    ```
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. 從[Python 用戶端](../python/setup-python-client-tools-sql.md)，您現在可以連線到 SQL Server 執行個體產生的二進位繪圖物件，並檢視繪圖。 

    若要這樣做，請執行下列 Python 程式碼，取代伺服器名稱、 資料庫名稱和適當的認證。 請確定 Python 版本的用戶端和伺服器上相同。 也請確定您的用戶端 （例如 matplotlib) 上的 Python 程式庫的相同或更高版本，相對於安裝在伺服器上的程式庫。
  
    **使用 SQL Server 驗證：**
    
    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSWORD}')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

    **使用 Windows 驗證：**

    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};Trusted_Connection=True;')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

5.  如果連線成功，您應該會看到類似下列訊息：
  
    *繪圖儲存在目錄： xxxx*
  
6.  Python 工作目錄中，會建立輸出檔。 若要檢視繪圖，找出 Python 工作目錄，並開啟檔案。 下圖顯示儲存在用戶端電腦上的繪圖。
  
    ![小費金額 vs 費用金額](media/sqldev-python-sample-plot.png "小費金額 vs 費用金額") 

## <a name="next-step"></a>下一步

[使用 T-SQL 建立資料特徵](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>上一個步驟

[下載的 NYC 計程車資料集](demo-data-nyctaxi-in-sql.md)

