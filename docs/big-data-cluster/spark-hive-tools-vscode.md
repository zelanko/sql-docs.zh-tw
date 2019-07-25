---
title: 在 SQL Server big data cluster 上使用 Spark & Hive 工具執行 Spark 作業 VS Code
titleSuffix: SQL Server big data clusters
description: 使用 Spark & Hive 工具提交 spark 作業, 以在 SQL Server big data cluster 上 Visual Studio Code。
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4458666792d7f4629b4e1820e98e2dbb9901c2b6
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68425978"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-cluster-in-visual-studio-code"></a>在 Visual Studio Code 的 SQL Server big data cluster 上提交 Spark 作業

瞭解如何使用 Spark & Hive 工具來 Visual Studio Code 建立和提交適用于 Apache Spark 的 PySpark 腳本, 首先我們會說明如何在 Visual Studio Code 中安裝 Spark & Hive 工具, 然後逐步解說如何將作業提交至 Spark。  

Spark & Hive 工具可以安裝在 Visual Studio Code 支援的平臺上, 包括 Windows、Linux 和 macOS。 您可以在下面找到不同平臺的必要條件。


## <a name="prerequisites"></a>先決條件

若要完成本文中的步驟, 需要下列專案:

- SQL Server big data 叢集。 請參閱[SQL Server big data](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions)叢集。
- [Visual Studio Code](https://code.visualstudio.com/)。
- [Mono](https://www.mono-project.com/docs/getting-started/install/)。 只有 Linux 和 macOS 才需要 Mono。
- [設定 Visual Studio Code 的 PySpark 互動式環境](https://docs.microsoft.com/azure/hdinsight/set-up-pyspark-interactive-environment)。
- 名為**hdexample 已**的本機目錄。  本文使用**C:\HD\HDexample**。

## <a name="install-spark--hive-tools"></a>安裝 Spark & Hive 工具

完成必要條件之後, 您可以為 Visual Studio Code 安裝 Spark & Hive 工具。  請完成下列步驟以安裝 Spark & Hive 工具:

1. 開啟 Visual Studio Code。

2. 從功能表列, 流覽至 [**視圖** > **延伸**模組]。

3. 在 [搜尋] 方塊中, 輸入**Spark & Hive**。

4. 從搜尋結果中選取 [ **Spark & Hive 工具**], 然後選取 [**安裝**]。  

   ![安裝延伸模組](./media/spark-hive-tools-vscode/extension.png)

5. 視需要重載。

## <a name="open-work-folder"></a>開啟工作資料夾

完成下列步驟以開啟工作資料夾, 並在 Visual Studio Code 中建立檔案:

1. 從功能表列, 流覽至  > [檔案] [**開啟資料夾 ...** ]C:\HD\HDexample, 然後選取 [**選取資料夾**] 按鈕。   >  資料夾會出現在左側的**Explorer**視圖中。

2. 從 [ **Explorer** ] 視圖中, 選取資料夾**hdexample 已**, 然後在 [工作] 資料夾旁**新增**[檔案] 圖示。

   ![新增檔案](./media/spark-hive-tools-vscode/new-file.png)

3. 將新`.py`檔案命名為 (Spark 腳本) 副檔名。  這個範例會使用**HelloWorld.py**。
4. 複製下列程式碼並貼到腳本檔案中:
   ```python
    import sys
    from operator import add
    from pyspark.sql import SparkSession, Row
    
    spark = SparkSession\
        .builder\
        .appName("PythonWordCount")\
        .getOrCreate()
    
    data = [Row(col1='pyspark and spark', col2=1), Row(col1='pyspark', col2=2), Row(col1='spark vs hadoop', col2=2), Row(col1='spark', col2=2), Row(col1='hadoop', col2=2)]
    df = spark.createDataFrame(data)
    lines = df.rdd.map(lambda r: r[0])

    counters = lines.flatMap(lambda x: x.split(' ')) \
        .map(lambda x: (x, 1)) \
        .reduceByKey(add)
    
    output = counters.collect()
    sortedCollection = sorted(output, key = lambda r: r[1], reverse = True)
    
    for (word, count) in sortedCollection:
        print("%s: %i" % (word, count))
   ```

## <a name="link-a-sql-server-big-data-cluster"></a>連結 SQL Server big data 叢集

您必須先連結 SQL Server big data 叢集, 才能從 Visual Studio Code 將腳本提交至您的叢集。

1. 從功能表列中, 流覽  > 至 [流覽] [**命令**選擇區 ... **], 然後輸入 Spark/Hive:連結叢集**。

   ![連結叢集命令](./media/spark-hive-tools-vscode/link-cluster-command.png)

2. 選取連結的叢集類型**SQL Server Big Data**。

3. 輸入 SQL Server Big Data 端點。

4. 輸入 SQL Server Big Data 叢集使用者名稱。

5. 輸入使用者管理員的密碼。

6. 設定叢集的顯示名稱 (選擇性)。

7. 列出叢集, 檢查**輸出**視圖以進行驗證。

## <a name="list-clusters"></a>列出叢集

1. 從功能表列中, 流覽  > 至 [流覽] [**命令**選擇區 ... **], 然後輸入 Spark/Hive:列出叢集**。

2. 查看**輸出**視圖。  此視圖會顯示您的連結的叢集。

    ![設定預設叢集配置](./media/spark-hive-tools-vscode/list-cluster-result.png)

## <a name="set-default-cluster"></a>設定預設叢集

1. 重新開啟稍[早](#open-work-folder)建立的資料夾**hdexample 已**(如果已關閉)。  

2. 選取稍[早](#open-work-folder)建立的檔案**HelloWorld.py** , 它會在腳本編輯器中開啟。

3. 連結叢集 (如果您還沒這麼做)。

4. 以滑鼠右鍵按一下腳本編輯器, 然後選取**Spark/Hive:設定 預設**叢集。   

5. 選取叢集作為目前腳本檔案的預設叢集。 這些工具會自動更新設定檔 **。VSCode\settings.json**。 

   ![設定預設叢集配置](./media/spark-hive-tools-vscode/set-default-cluster-configuration.png)

## <a name="submit-interactive-pyspark-queries"></a>提交互動式 PySpark 查詢

您可以遵循下列步驟來提交互動式 PySpark 查詢:

1. 重新開啟稍[早](#open-work-folder)建立的資料夾**hdexample 已**(如果已關閉)。  

2. 選取稍[早](#open-work-folder)建立的檔案**HelloWorld.py** , 它會在腳本編輯器中開啟。

3. 連結叢集 (如果您還沒這麼做)。

4. 選擇所有程式碼, 並以滑鼠右鍵按一下腳本編輯器, **然後選取 [Spark:PySpark Interactive** ] 以提交查詢, 或使用快速鍵**Ctrl + Alt + I**。

   ![pyspark 互動式操作功能表](./media/spark-hive-tools-vscode/pyspark-interactive-right-click.png)

5. 如果您尚未指定預設叢集, 請選取叢集。 幾分鐘後, **Python 互動式**結果會出現在新的索引標籤中。這些工具也可讓您使用內容功能表來提交程式碼區塊, 而不是整個腳本檔案。 

   ![pyspark 互動式 python 互動式視窗](./media/spark-hive-tools-vscode/pyspark-interactive-python-interactive-window.png) 

6. 輸入 **"%% info"** , 然後按**Shift + enter**以查看作業資訊。 (選擇性)

   ![查看作業資訊](./media/spark-hive-tools-vscode/pyspark-interactive-view-job-information.png)

   > [!NOTE] 
   >
   > 在設定中取消選取 [**啟用 Python 延伸**模組] (預設設定為 [已核取]) 時, 提交的 pyspark 互動結果將使用舊的視窗。
   >
   > ![pyspark 互動式 python 延伸模組已停用](./media/spark-hive-tools-vscode/pyspark-interactive-python-extension-disabled.png)


## <a name="submit-pyspark-batch-job"></a>提交 PySpark 批次作業

1. 重新開啟稍[早](#open-work-folder)建立的資料夾**hdexample 已**(如果已關閉)。  

2. 選取稍[早](#open-work-folder)建立的檔案**HelloWorld.py** , 它會在腳本編輯器中開啟。

3. 連結叢集 (如果您還沒這麼做)。

4. 以滑鼠右鍵按一下腳本編輯器, 然後選取 **[Spark:PySpark 批**次], 或使用快速鍵**Ctrl + Alt + H**。 

5. 如果您尚未指定預設叢集, 請選取叢集。 提交 Python 作業之後, 提交記錄會出現在 Visual Studio Code 的 [**輸出**] 視窗中。 [ **SPARK UI url** ] 和 [ **Yarn UI url** ] 也會顯示。 您可以在網頁瀏覽器中開啟 URL, 以追蹤作業狀態。

   ![提交 Python 作業結果](./media/spark-hive-tools-vscode/submit-pythonjob-result.png) 

## <a name="apache-livy-configuration"></a>Apache Livy 設定

支援[Apache Livy](https://livy.incubator.apache.org/)設定, 它可以在上設定 **。** [工作空間] 資料夾中的 VSCode\settings.json。 目前, Livy 設定只支援 Python 腳本。 如需詳細資訊, 請參閱[LIVY 讀我檔案](https://github.com/cloudera/livy/blob/master/README.rst )。

### <a id="triggerlivyconf"></a>**如何觸發 Livy 設定**

#### <a name="method-1"></a>方法 1

1.  > 從功能表列, 流覽至 [檔案**喜好** > **設定**]。  
2. 在 [**搜尋設定**] 文字方塊中 **, 輸入 HDInsight Job Sumission:Livy 會議**。  
3. **在 [設定] 中**選取 [編輯], 以取得相關的搜尋結果。

#### <a name="method-2"></a>方法 2

提交檔案, 請注意`.vscode` , 資料夾會自動新增至工作資料夾。 您可以按一下`.vscode\settings.json`來尋找 Livy 設定。

+ 專案設定:

    ![Livy 設定](./media/spark-hive-tools-vscode/hdi-livyconfig.png)

>[!NOTE]
>針對 settings **driverMomory**和**executorMomry**, 將值設定為 unit, 例如1g 或1024m。 

### <a name="supported-livy-configurations"></a>支援的 Livy 設定

#### <a name="post-batches"></a>張貼/batches

**要求本文**

| name | description | type |
| :- | :- | :- |
| 檔案 | 包含要執行之應用程式的檔案 | 路徑 (必要) |
| proxyUser | 執行作業時要模擬的使用者 | string |
| className | 應用程式 JAVA/Spark 主要類別 | string |
| 引數 | 應用程式的命令列引數 | 字串清單 |
| jar | 要在此會話中使用的 jar | 字串清單 |
| pyFiles | 要在此會話中使用的 Python 檔案 | 字串清單 |
| files | 要在此會話中使用的檔案 | 字串清單 |
| driverMemory | 要用於驅動程式進程的記憶體數量 | string |
| driverCores | 要用於驅動程式進程的核心數目 | ssNoversion |
| executorMemory | 每個執行程式進程所使用的記憶體數量 | string |
| executorCores | 要用於每個執行程式的核心數目 | ssNoversion |
| numExecutors | 要為此會話啟動的執行程式數目 | ssNoversion |
| 封存 | 要在此會話中使用的封存 | 字串清單 |
| queue | 已提交的 YARN 佇列名稱 | string |
| name | 此會話的名稱 | string |
| conf | Spark 設定屬性 | Key = val 的對應 |

#### <a name="response-body"></a>回應主體

建立的批次物件。

| name | description | type |
| :- | :- | :- |
| id | 會話識別碼 | ssNoversion |
| 標識 | 此會話的應用程式識別碼 | String |
| appInfo | 詳細的應用程式資訊 | Key = val 的對應 |
| 日誌 | 記錄行 | 字串清單 |
| state | 批次狀態 | string |

>[!NOTE]
>指派的 Livy 設定會在提交腳本時顯示在 [輸出] 窗格中。

## <a name="additional-features"></a>其他功能

適用于 Visual Studio Code 的 Spark & Hive 支援下列功能:

- **IntelliSense 自動完成**。 關鍵字、方法、變數等等的快顯建議。 不同的圖示代表不同類型的物件。

    ![適用于 Visual Studio Code IntelliSense 物件類型的 Spark & Hive 工具](./media/spark-hive-tools-vscode/hdinsight-for-vscode-auto-complete-objects.png)
- **IntelliSense 錯誤標記**。 語言服務會將 Hive 腳本的編輯錯誤加上底線。     
- **語法**反白顯示。 語言服務會使用不同的色彩來區分變數、關鍵字、資料類型、函數等等。 

    ![適用于 Visual Studio Code 語法重點的 Spark & Hive 工具](./media/spark-hive-tools-vscode/hdinsight-for-vscode-syntax-highlights.png)

## <a name="unlink-cluster"></a>取消連結叢集

1. 從功能表列中, 流覽  > 至 [流覽] [命令選擇區 **...** ] **, 然後輸入 Spark/Hive:取消連結叢集**。  

2. 選取要取消連結的叢集。  

3. 檢查**輸出**視圖以進行驗證。  

## <a name="next-steps"></a>後續步驟
如需 SQL Server big data cluster 和相關案例的詳細資訊, 請參閱[SQL Server big data](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions)叢集。
