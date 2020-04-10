---
title: 建立、匯出 Spark ML 模型：MLeap
titleSuffix: SQL Server Big Data Clusters
description: 使用 PySpark 搭配 SQL Server 巨量資料叢集上的 Spark 來定型和建立機器學習模型。 使用 MLeap 匯出，然後在 SQL Server 中使用 JAVA 為模型評分。
author: RogPodge
ms.author: roliu
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9d51cc4164cbb40ff647cad337240e689696b449
ms.sourcegitcommit: 1124b91a3b1a3d30424ae0fec04cfaa4b1f361b6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/01/2020
ms.locfileid: "80531119"
---
# <a name="create-export-and-score-spark-machine-learning-models-on-big-data-clusters-2019"></a>在 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 上建立、匯出及評分 Spark 機器學習模型

以下範例示範如何使用 [Spark ML](https://spark.apache.org/docs/latest/ml-guide.html)建立模型、將模型匯出至 [MLeap](http://mleap-docs.combust.ml/)，以及在 SQL Server 中使用其 [Java 語言延伸模組](../language-extensions/language-extensions-overview.md)為模型評分。 此作業會在 SQL Server 2019 巨量資料叢集的內容中完成。

下圖說明此範例中所執行的工作：

![使用 Spark 定型分數匯出](./media/spark-create-machine-learning-model/train-score-export-with-spark.png)

## <a name="prerequisites"></a>Prerequisites

這個範例的所有檔案都位於 [https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml) \(英文\)。

若要執行範例，您也必須具備下列必要條件：

- [SQL Server 巨量資料叢集](deploy-get-started.md)

- [巨量資料工具](deploy-big-data-tools.md)
   - **kubectl**
   - **curl**
   - **Azure Data Studio**

## <a name="model-training-with-spark-ml"></a>使用 Spark ML 將模型定型

此範例會使用普查資料 (**AdultCensusIncome.csv**) 來建立 Spark ML 管線模型。

1. 使用 [mleap_sql_test/setup.sh](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mleap_sql_test/setup.sh) 檔案從網際網路下載資料集，然後放在您 SQL Server 巨量資料叢集的 HDFS 中。 這可讓 Spark 能夠存取資料集。

1. 然後請下載範例筆記本 [train_score_export_ml_models_with_spark.ipynb](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb)。 從 PowerShell 或 Bash 命令列，執行下列命令來下載筆記本：

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb"
   ```

   此筆記本包含具有此範例區段之必要命令的儲存格。

1. 在 Azure Data Studio 中開啟筆記本，並執行每個程式碼區塊。 如需使用筆記本的詳細資訊，請參閱[如何搭配 SQL Server 使用筆記本](../azure-data-studio/notebooks-guidance.md)。

資料會先讀入 Spark 並分割成定型和測試資料集。 然後程式碼會使用定型資料將管線模型定型。 最後，它會將模型匯出至 MLeap 組合。

> [!TIP]
> 您也可以在 [mleap_sql_test/mleap_pyspark.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mleap_sql_test/mleap_pyspark.py) 檔案中，查看或執行與這些步驟有關的 Python 程式碼。

## <a name="model-scoring-with-sql-server"></a>使用 SQL Server 進行模型評分

現在 Spark ML 管線模型已經是通用序列化 [MLeap 組合](http://mleap-docs.combust.ml/core-concepts/mleap-bundles.html) 格式，因此您可以在沒有 Spark 的情況下使用 JAVA 為模型評分。

此範例使用 SQL Server 中的 [JAVA 語言延伸模組](../language-extensions/language-extensions-overview.md)。 若要為 SQL Server 中的模型評分，您需要先建置可將模型載入到 JAVA 並加以評分的 JAVA 應用程式。 您可以在 [mssql-mleap-app folder](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mssql-mleap-app) 中找到此 JAVA 應用程式的範例程式碼。

建置範例之後，您可以使用 Transact-SQL 呼叫 JAVA 應用程式，並搭配資料庫資料表為模型評分。 您可以在 [mleap_sql_test/mleap_sql_tests.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mleap_sql_test/mleap_sql_tests.py) 來源檔案中看到此情況。

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[如何在 Kubernetes 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-guidance.md)
