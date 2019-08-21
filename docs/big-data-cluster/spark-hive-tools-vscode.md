---
title: 在 SQL Server 巨量資料叢集上搭配適用於 VS Code 的 Spark & Hive Tools 執行 Spark 作業
titleSuffix: SQL Server big data clusters
description: 在 SQL Server 巨量資料叢集上搭配適用於 Visual Studio Code 的 Spark & Hive Tools 提交 Spark 作業。
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b09a5febe9bc67f04d70c4d5b7850ef26ebac750
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653736"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-cluster-in-visual-studio-code"></a>在 Visual Studio Code 中於 SQL Server 巨量資料叢集上提交 Spark 作業

了解如何使用適用於 Visual Studio Code 的 Spark & Hive Tools 來建立及提交適用於 Apache Spark 的 PySpark 指令碼。首先我們將會描述如何在 Visual Studio Code 中安裝 Spark & Hive Tools，然後便會逐步解說向 Spark 提交作業的方法。  

您可以在 Visual Studio Code 所支援的平台上安裝 Spark & Hive Tools，這包括 Windows、Linux 及 macOS。 您可以在下面找到不同平台的先決條件。


## <a name="prerequisites"></a>必要條件

若要完成此文章中的步驟，將會需要下列項目：

- SQL Server 巨量資料叢集。 請參閱 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions)。
- [Visual Studio Code](https://code.visualstudio.com/) \(英文\)。
- [Mono](https://www.mono-project.com/docs/getting-started/install/) \(英文\)。 只有 Linux 和 macOS 才需要 Mono。
- [針對 Visual Studio Code 設定 PySpark 互動式環境](https://docs.microsoft.com/azure/hdinsight/set-up-pyspark-interactive-environment) \(部分機器翻譯\)。
- 名為**SQLBDCexample**的本機目錄。  本文使用**C:\SQLBDC\SQLBDCexample**。

## <a name="install-spark--hive-tools"></a>安裝 Spark & Hive Tools

在您具備先決條件之後，便可以安裝適用於 Visual Studio Code 的 Spark & Hive Tools。  完成下列步驟來安裝 Spark & Hive Tools：

1. 開啟 Visual Studio Code。

2. 從功能表列，瀏覽至 [檢視] > [擴充功能]。

3. 在搜尋方塊中，輸入 **Spark & Hive**。

4. 從搜尋結果中選取 [Spark & Hive Tools]，然後選取 [安裝]。  

   ![安裝擴充功能](./media/spark-hive-tools-vscode/extension.png)

5. 視需要重新載入。

## <a name="open-work-folder"></a>開啟工作資料夾

完成下列步驟來在 Visual Studio Code 中開啟工作資料夾並建立檔案：

1. 從功能表列, 流覽至  > [檔案] [**開啟資料夾 ...** ]C:\SQLBDC\SQLBDCexample, 然後選取 [**選取資料夾**] 按鈕。  >  該資料夾會出現在左側的 [檔案總管] 檢視中。

2. 從 [ **Explorer** ] 視圖中, 選取資料夾**SQLBDCexample**, 然後在 [工作] 資料夾旁**新增**[檔案] 圖示。

   ![新增檔案](./media/spark-hive-tools-vscode/new-file.png)

3. 以 `.py` (Spark 指令碼) 副檔名來為新檔案命名。  此範例會使用 **HelloWorld.py**。
4. 將下列程式碼複製並貼到該指令檔：
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

## <a name="link-a-sql-server-big-data-cluster"></a>連結 SQL Server 巨量資料叢集

在您可以從 Visual Studio Code 將指令碼提交至叢集之前，您必須連結 SQL Server 巨量資料叢集。

1. 從功能表列，瀏覽至 [檢視] > [命令選擇區]，然後輸入 **Spark / Hive:Link a Cluster**。

   ![連結叢集命令](./media/spark-hive-tools-vscode/link-cluster-command.png)

2. 針對已連結的叢集類型選取 [SQL Server 巨量資料]。

3. 輸入 SQL Server 巨量資料端點。

4. 輸入 SQL Server 巨量資料叢集使用者名稱。

5. 輸入使用者管理員的密碼。

6. 設定叢集的顯示名稱 (選擇性)。

7. 列出叢集，檢閱 [輸出] 檢視以確認。

## <a name="list-clusters"></a>列出叢集

1. 從功能表列，瀏覽至 [檢視] > [命令選擇區]，然後輸入 **Spark / Hive:List Cluster**。

2. 檢閱 [輸出] 檢視。  該檢視將會顯示已連結的叢集。

    ![設定預設叢集設定](./media/spark-hive-tools-vscode/list-cluster-result.png)

## <a name="set-default-cluster"></a>設定預設叢集

1. 重新開啟稍[早](#open-work-folder)建立的資料夾**SQLBDCexample** (如果已關閉)。  

2. 選取[先前](#open-work-folder)所建立的 **HelloWorld.py** 檔案，它將會在指令碼編輯器中開啟。

3. 如果您尚未連結叢集，請先這麼做。

4. 以滑鼠右鍵按一下腳本編輯器, 然後選取**Spark/Hive:設定 預設**叢集。   

5. 選取某個叢集作為目前指令檔的預設叢集。 工具會自動更新設定檔 **.VSCode\settings.json**。 

   ![設定預設叢集設定](./media/spark-hive-tools-vscode/set-default-cluster-configuration.png)

## <a name="submit-interactive-pyspark-queries"></a>提交互動式 PySpark 查詢

您可以遵循下列步驟來提交互動式 PySpark 查詢：

1. 重新開啟稍[早](#open-work-folder)建立的資料夾**SQLBDCexample** (如果已關閉)。  

2. 選取[先前](#open-work-folder)所建立的 **HelloWorld.py** 檔案，它將會在指令碼編輯器中開啟。

3. 如果您尚未連結叢集，請先這麼做。

4. 選擇所有程式碼, 並以滑鼠右鍵按一下腳本編輯器, **然後選取 [Spark:PySpark Interactive** ] 以提交查詢, 或使用快速鍵**Ctrl + Alt + I**。

   ![[PySpark 互動式] 內容功能表](./media/spark-hive-tools-vscode/pyspark-interactive-right-click.png)

5. 如果您尚未指定預設叢集，請選取叢集。 幾分鐘後，[Python 互動式] 結果便會出現在新的索引標籤中。此工具也可以讓您使用內容功能表來提交程式碼區塊，而非整個指令檔。 

   ![PySpark 互動式 Python 互動式視窗](./media/spark-hive-tools-vscode/pyspark-interactive-python-interactive-window.png) 

6. 輸入 **"%%info"** ，然後按 **Shift + Enter** 以檢視作業資訊。 (選擇性)

   ![檢視作業資訊](./media/spark-hive-tools-vscode/pyspark-interactive-view-job-information.png)

   > [!NOTE] 
   >
   > 在設定中取消選取 [已啟用 Python 擴充功能] (預設為選取) 時，已提交的 [PySpark 互動式] 結果將會使用舊的視窗。
   >
   > ![PySpark 互動式 Python 擴充功能已停用](./media/spark-hive-tools-vscode/pyspark-interactive-python-extension-disabled.png)


## <a name="submit-pyspark-batch-job"></a>提交 PySpark 批次工作

1. 重新開啟稍[早](#open-work-folder)建立的資料夾**SQLBDCexample** (如果已關閉)。  

2. 選取[先前](#open-work-folder)所建立的 **HelloWorld.py** 檔案，它將會在指令碼編輯器中開啟。

3. 如果您尚未連結叢集，請先這麼做。

4. 以滑鼠右鍵按一下腳本編輯器, 然後選取 **[Spark:PySpark 批**次], 或使用快速鍵**Ctrl + Alt + H**。 

5. 如果您尚未指定預設叢集，請選取叢集。 在您提交 Python 作業之後，提交記錄便會出現在 Visual Studio Code 的 [輸出] 視窗中。 同時也會顯示 **Spark UI URL** 和 **Yarn UI URL**。 您可以在網頁瀏覽器中開啟該 URL 來追蹤作業狀態。

   ![提交 Python 作業結果](./media/spark-hive-tools-vscode/submit-pythonjob-result.png) 

## <a name="apache-livy-configuration"></a>Apache Livy 設定

支援 [Apache Livy](https://livy.incubator.apache.org/) \(英文\) 設定，且可以在工作區資料夾中的 **.VSCode\settings.json** 設定它。 目前 Livy 設定僅支援 Python 指令碼。 如需詳細資料，請參閱 [Livy 讀我檔案](https://github.com/cloudera/livy/blob/master/README.rst )。

### <a id="triggerlivyconf"></a>**如何觸發 Livy 設定**

#### <a name="method-1"></a>方法 1

1. 從功能表列，瀏覽至 [檔案] > [喜好設定] > [設定]。  
2. 在 [搜尋設定] 文字方塊中，輸入 **HDInsight Job Sumission:Livy Conf**。  
3. 選取 [在 settings.json 中編輯] 以取得相關的搜尋結果。

#### <a name="method-2"></a>方法 2

提交檔案。請注意，系統會自動將 `.vscode` 資料夾加入工作資料夾。 您可以按一下 `.vscode\settings.json` 來找到 Livy 設定。

+ 專案設定：

    ![Livy 設定](./media/spark-hive-tools-vscode/hdi-livyconfig.png)

>[!NOTE]
>針對 **driverMomory** 和 **executorMomry** 設定，請搭配單位設定值，例如 1g 或 1024m。 

### <a name="supported-livy-configurations"></a>支援的 Livy 設定

#### <a name="post-batches"></a>POST /batches

**要求本文**

| name | description | type |
| :- | :- | :- |
| 檔案 | 包含要執行之應用程式的檔案 | 路徑 (必要) |
| proxyUser | 執行作業時要模擬的使用者 | string |
| className | 應用程式 Java/Spark 主要類別 | string |
| args | 適用於應用程式的命令列引數 | 字串清單 |
| jars | 要用於此工作階段的 jars | 字串清單 |
| pyFiles | 要用於此工作階段的 Python 檔案 | 字串清單 |
| files | 要用於此工作階段的檔案 | 字串清單 |
| driverMemory | 要用於驅動程式程序的記憶體數量 | string |
| driverCores | 要用於驅動程式程序的核心數目 | ssNoversion |
| executorMemory | 要用於每個執行程式程序的記憶體數量 | string |
| executorCores | 要用於每個執行程式的核心數目 | ssNoversion |
| numExecutors | 要針對此工作階段啟動的執行程式數目 | ssNoversion |
| archives | 要用於此工作階段的封存 | 字串清單 |
| queue | 提交至的 YARN 佇列名稱 | string |
| name | 此工作階段的名稱 | string |
| conf | Spark 設定屬性 | key=val 的對應 |

#### <a name="response-body"></a>回應本文

建立的批次物件。

| name | description | type |
| :- | :- | :- |
| id | 工作階段識別碼 | ssNoversion |
| appId | 此工作階段的應用程式識別碼 | String |
| appInfo | 詳細的應用程式資訊 | key=val 的對應 |
| log | 記錄行 | 字串清單 |
| state | 批次狀態 | string |

>[!NOTE]
>提交指令碼時，已指派的 Livy 設定將會顯示在 [輸出] 窗格中。

## <a name="additional-features"></a>其他功能

適用於 Visual Studio Code 的 Spark & Hive 支援下列功能：

- **IntelliSense 自動完成**。 會針對關鍵字、方法、變數等快顯的建議。 不同的圖示代表不同類型的物件。

    ![適用於 Visual Studio Code 的 Spark & Hive Tools IntelliSense 物件類型](./media/spark-hive-tools-vscode/hdinsight-for-vscode-auto-complete-objects.png)
- **IntelliSense 錯誤標記**。 語言服務會為 Hive 指令碼的編輯錯誤加上底線。     
- **語法醒目提示**。 語言服務會使用不同的色彩來區分變數、關鍵字、資料類型、函式等。 

    ![適用於 Visual Studio Code 的 Spark & Hive Tools 語法醒目提示](./media/spark-hive-tools-vscode/hdinsight-for-vscode-syntax-highlights.png)

## <a name="unlink-cluster"></a>將叢集取消連結

1. 從功能表列，瀏覽至 [檢視] > [命令選擇區]，然後輸入 **Spark / Hive:Unlink a Cluster**。  

2. 選取要取消連結的叢集。  

3. 檢閱 [輸出] 檢視以確認。  

## <a name="next-steps"></a>後續步驟
如需 SQL Server big data cluster 和相關案例的詳細資訊, [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions)請參閱。
