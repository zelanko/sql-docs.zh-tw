---
title: "步驟 3：瀏覽及視覺化資料 | Microsoft Docs"
ms.custom: 
ms.date: 05/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-python
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dfb80fcd3241b22f0ac72c2cf4cd8a18d1add857
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="step-3-explore-and-visualize-the-data"></a>步驟 3：瀏覽及視覺化資料

開發資料科學方案通常會包含大量資料瀏覽和資料視覺化。 在此步驟中，將探索範例資料，並產生一些繪圖。 稍後，您將學習如何序列化圖形物件，在 [Python]，然後將那些物件還原序列化，以進行繪圖。

> [!NOTE]
> 本逐步解說示範只有二元分類工作。您可以隨意地嘗試建立其他兩個機器學習工作、 迴歸和多級分類不同的模型。

## <a name="review-the-data"></a>檢閱資料

在原始資料集中，計程車識別碼和車程記錄會提供在不同的檔案中。 不過，為了更輕鬆地使用範例資料，已根據 _medallion_、 _hack_license_和 _pickup_datetime_資料行來聯結兩個原始資料集。  也會對記錄進行抽樣，只取得 1% 的原始記錄數目。 產生的向下取樣資料集有 1,703,957 個資料列和 23 個資料行。

**計程車識別碼**

- _medallion_ 資料行代表計程車的唯一識別碼。
- _hack_license_ 資料行包含計程車司機駕照號碼 (匿名)。

**車程和小費記錄**

- 每筆車程記錄都會包含上車和下車位置與時間，以及車程距離。
- 每筆費用記錄都會包括付款資訊，例如付款類型、總付款金額和小費金額。
- 最後三個資料行可以用於各種機器學習工作。  _tip_amount_ 資料行包含連續數值，而且可以當成 **label** 資料行來進行迴歸分析。 _tipped_ 資料行只有是/否值，並且用於二元分類。 _tip_class_ 資料行有多個 **類別標籤** ，因此可以當成多類別分類工作的標籤使用。
- 使用這些商務規則，用於 label 資料行的值都是根據 _tip_amount_ 資料行︰
  
    |衍生的資料行名稱|規則|
    |-|-|
     |tipped|If tip_amount > 0, tipped = 1, otherwise tipped = 0|
    |tip_class|Class 0: tip_amount = $0<br /><br />Class 1: tip_amount > $0 and tip_amount <= $5<br /><br />Class 2: tip_amount > $5 and tip_amount <= $10<br /><br />Class 3: tip_amount > $10 and tip_amount <= $20<br /><br />Class 4: tip_amount > $20|

## <a name="create-plots-using-python-in-t-sql"></a>建立 T-SQL 中使用 Python 的繪圖

由於視覺效果是這種功能強大的工具來了解在極端值與資料的分佈，Python 提供許多封裝將資料視覺化。 **Matplotlib**模組是常用的程式庫包含許多函數，可建立長條圖、 散佈圖、 方塊繪圖和其他資料瀏覽圖形。

在本節中，您將學習如何使用預存程序的繪圖使用。 想要儲存`plot`Python 物件當做**varbinary**資料類型，並儲存在伺服器上產生的繪圖。

### <a name="storing-plots-as-varbinary-data-type"></a>將繪圖儲存為 varbinary 資料類型

**Revoscalepy**隨附於 SQL Server 2017 機器學習服務模組包含類似於 RevoScaleR 封裝中的 R 程式庫的程式庫。 在此範例中，您將使用 Python 相當於`rxHistogram`要繪製的長條圖的資料[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢。 若要讓您更輕鬆，您會將它包裝在預存程序， _PlotHistogram_。

預存程序會傳回已序列化的 Python`figure`物件做為資料流**varbinary**資料。 您無法直接管理，檢視的二進位資料，但是您可以使用用戶端上的 Python 程式碼，以還原序列化，並檢視數字，並再儲存在用戶端電腦的映像檔案。

### <a name="create-the-stored-procedure-plotspython"></a>建立預存程序 Plots_Python

1.  在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，開啟新**查詢**視窗。

2.  選取逐步解說的資料庫，然後使用此陳述式建立程序。 必要時，請務必修改程式碼來使用正確的資料表名稱。
  
    ```SQL
    
    CREATE PROCEDURE [dbo].[SerializePlots]
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
**注意：**

- 變數`@query`定義的查詢文字 (`'SELECT tipped FROM nyctaxi_sample'`)，為指令碼輸入變數的引數傳遞給 Python 程式碼區塊`@input_data_1`。
- Python 指令碼是相當簡單： **matplotlib** `figure`物件可用來讓色階分佈圖和散佈圖，這些物件會接著使用序列化`pickle`程式庫。
- Python 圖形物件序列化為 Python**熊**輸出資料框架。

### <a name="output-varbinary-data-to-viewable-graphics-file"></a>可檢視的圖形檔的輸出 varbinary 資料

1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中，執行下列陳述式：
  
    ```
    EXEC [dbo].[SerializePlots]
    ```
  
    **結果**
  
    *繪圖*
    *0xFFD8FFE000104A4649...* 
     *0xFFD8FFE000104A4649...* 
     *0xFFD8FFE000104A4649...* 
     *0xFFD8FFE000104A4649...*

  
2.  用戶端在電腦上，執行下列 Python 程式碼，並取代伺服器名稱、 資料庫名稱及適當的認證。
  
    **SQL server 驗證：**
    
        ```python
        import pyodbc
        import pickle
        import os
        cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSOWRD}')
        cursor = cnxn.cursor()
        cursor.execute("EXECUTE [dbo].[SerializePlots]")
        tables = cursor.fetchall()
        for i in range(0, len(tables)):
            fig = pickle.loads(tables[i][0])
            fig.savefig(str(i)+'.png')
        print("The plots are saved in directory: ",os.getcwd())
        ```  
    **Windows 驗證：**

        ```python
        import pyodbc
        import pickle
        import os
        cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER={SERVER_NAME};DATABASE={DB_NAME};Trusted_Connection=yes;')
        cursor = cnxn.cursor()
        cursor.execute("EXECUTE [dbo].[SerializePlots]")
        tables = cursor.fetchall()
        for i in range(0, len(tables)):
            fig = pickle.loads(tables[i][0])
            fig.savefig(str(i)+'.png')
        print("The plots are saved in directory: ",os.getcwd())
        ```

    > [!NOTE]
    > 請確定 Python 版本用戶端和伺服器上相同。 此外，請確定您在您的用戶端 （例如 matplotlib) 使用的 Python 程式庫是相對於安裝在伺服器上的程式庫之相同或更高版本。


3.  如果連線成功時，您會看到以下的結果
  
    *會儲存在目錄中的繪圖： xxxx*
  
4.  Python 的工作目錄中，將會建立輸出檔案。 若要檢視繪圖，只要開啟 Python 工作目錄。 下圖顯示在用戶端電腦上儲存範例圖。
  
    ![提示量 vs 價位量](media/sqldev-python-sample-plot.png "提示量 vs 價位數量") 

## <a name="next-step"></a>下一個步驟

[步驟 4︰使用 T-SQL 建立資料特徵](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>上一個步驟

[步驟 2︰使用 PowerShell 將資料匯入 SQL Server](sqldev-py2-import-data-to-sql-server-using-powershell.md)

## <a name="see-also"></a>另請參閱

[使用 Python 的機器學習服務](../python/sql-server-python-services.md)

