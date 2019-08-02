---
title: 第1課使用 Python 和 T-sql 探索資料並加以視覺化
description: 示範如何在 SQL Server 預存程式和 T-sql 函數中內嵌 Python 的教學課程
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6ee82de1431a6bc21596505dc4b008b817b35830
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714698"
---
# <a name="explore-and-visualize-the-data"></a>探索資料並加以視覺化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文屬於[適用于 SQL 開發人員的資料庫內 Python 分析](sqldev-in-database-python-for-sql-developers.md)教學課程的一部分。 

在此步驟中, 您將探索範例資料並產生一些繪圖。 稍後, 您將瞭解如何在 Python 中序列化繪圖物件, 然後將這些物件還原序列化, 並製作繪圖。

## <a name="review-the-data"></a>檢查資料

首先, 請花一點時間流覽資料結構描述, 因為我們進行了一些變更, 讓您更輕鬆地使用 NYC 計程車資料

+ 原始資料集會針對計程車識別碼和旅程記錄使用不同的檔案。 我們已聯結_medallion_、 _hack_license_和_pickup_datetime_資料行上的兩個原始資料集。  
+ 原始資料集跨越許多檔案, 而且相當大。 我們已 downsampled, 只會取得原始記錄數目的 1%。 目前的資料表具有1703957個數據列和23個數據行。

**計程車識別碼**

_Medallion_資料行代表計程車的唯一識別碼。

_Hack_license_資料行包含計程車駕駛的授權號碼 (匿名)。

**車程和小費記錄**

每筆車程記錄都會包含上車和下車位置與時間，以及車程距離。

每筆費用記錄都會包括付款資訊，例如付款類型、總付款金額和小費金額。

最後三個資料行可以用於各種機器學習工作。  _tip_amount_ 資料行包含連續數值，而且可以當成 **label** 資料行來進行迴歸分析。 _tipped_ 資料行只有是/否值，並且用於二元分類。 _tip_class_ 資料行有多個 **類別標籤** ，因此可以當成多類別分類工作的標籤使用。

標籤資料行所使用的值都是以下列`tip_amount`商務規則為基礎:

+ 標籤`tipped`資料行的可能值為0和1

    如果`tip_amount` > 0, `tipped` = 1, 則`tipped`為, 否則為 = 0

+ 標籤`tip_class`資料行有可能的類別值0-4

    類別 0: `tip_amount` = $0

    類別 1: `tip_amount` > $0 和`tip_amount` < = $5
    
    類別 2: `tip_amount` > $5 和`tip_amount` < = $10
    
    類別 3: `tip_amount` > $10 和`tip_amount` < = $20
    
    類別 4: `tip_amount` > $20

## <a name="create-plots-using-python-in-t-sql"></a>在 T-sql 中使用 Python 建立繪圖

開發資料科學方案通常會包含大量資料瀏覽和資料視覺化。 因為視覺效果是用來瞭解資料和極端值分佈的強大工具, 所以 Python 提供許多可將資料視覺化的套件。 **Matplotlib**模組是視覺效果較熱門的程式庫, 其中包含許多用來建立長條圖、散佈圖、盒狀圖和其他資料流覽圖形的功能。

在本節中, 您將瞭解如何使用預存程式來處理繪圖。 您不需要在伺服器上開啟映射, 而是將 Python 物件`plot`儲存為**Varbinary**資料, 然後將它寫入可在其他地方共用或查看的檔案。

### <a name="create-a-plot-as-varbinary-data"></a>建立繪圖做為 Varbinary 資料

預存程式會傳回序列化的`figure` Python 物件當做**Varbinary**資料的資料流程。 您無法直接查看二進位資料, 但是您可以在用戶端上使用 Python 程式碼來還原序列化和觀看圖形, 然後將影像檔案儲存在用戶端電腦上。

1. 建立預存程式**PyPlotMatplotlib**(如果 PowerShell 腳本尚未這麼做)。

    - 變數`@query`會定義查詢文字`SELECT tipped FROM nyctaxi_sample`, 並將它傳遞至 Python 程式碼區塊做為腳本輸入變數`@input_data_1`的引數。
    - Python 腳本相當簡單: **matplotlib** `figure`物件是用來建立長條圖和散佈圖, 然後使用`pickle`程式庫將這些物件序列化。
    - Python 繪圖物件會序列化為輸出的**pandas**資料框架。
  
    ```sql
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

2. 現在, 請執行不含引數的預存程式, 以從硬式編碼為輸入查詢的資料產生繪圖。

    ```sql
    EXEC [dbo].[PyPlotMatplotlib]
    ```

3. 結果應該如下所示:
  
    ```sql
    plot
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    0xFFD8FFE000104A4649...
    ```

  
4. 從[Python 用戶端](../python/setup-python-client-tools-sql.md), 您現在可以連接到產生二進位繪圖物件的 SQL Server 實例, 並查看繪圖。 

    若要這麼做, 請執行下列 Python 程式碼, 並適當地取代伺服器名稱、資料庫名稱和認證。 請確定用戶端和伺服器上的 Python 版本相同。 此外, 也請確定您用戶端上的 Python 程式庫 (例如 matplotlib) 與伺服器上所安裝程式庫的版本相同或更高。
  
    **使用 SQL Server 驗證:**
    
    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER=SQL Server;SERVER={SERVER_NAME};DATABASE={DB_NAME};UID={USER_NAME};PWD={PASSWORD}')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

    **使用 Windows 驗證:**

    ```python
    %matplotlib notebook
    import pyodbc
    import pickle
    import os
    cnxn = pyodbc.connect('DRIVER=SQL Server;SERVER={SERVER_NAME};DATABASE={DB_NAME};Trusted_Connection=True;')
    cursor = cnxn.cursor()
    cursor.execute("EXECUTE [dbo].[PyPlotMatplotlib]")
    tables = cursor.fetchall()
    for i in range(0, len(tables)):
        fig = pickle.loads(tables[i][0])
        fig.savefig(str(i)+'.png')
    print("The plots are saved in directory: ",os.getcwd())
    ```

5.  如果連線成功, 您應該會看到如下的訊息:
  
    *繪圖會儲存在目錄: xxxx 中*
  
6.  輸出檔案會建立在 Python 工作目錄中。 若要查看繪圖, 請找出 Python 工作目錄, 然後開啟檔案。 下圖顯示在用戶端電腦上儲存的繪圖。
  
    ![秘訣數量與費用金額](media/sqldev-python-sample-plot.png "秘訣數量與費用金額") 

## <a name="next-step"></a>下一步

[使用 T-SQL 建立資料特徵](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="previous-step"></a>上一個步驟

[下載 NYC 計程車資料集](demo-data-nyctaxi-in-sql.md)

