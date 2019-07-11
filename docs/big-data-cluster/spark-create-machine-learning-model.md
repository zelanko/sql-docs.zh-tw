---
title: 建立和匯出 Spark 機器學習服務模型與 MLeap
titleSuffix: SQL Server big data clusters
description: 使用 PySpark 來訓練及 SQL Server 的巨量資料叢集 （預覽） 上建立 Spark 機器學習服務模型。 使用匯出 MLeap，然後評分 SQL Server 中的 java 模型。
author: lgongmsft
ms.author: lgong
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aa4c31eca725e8e662937259f078cf00a3441915
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727381"
---
# <a name="create-export-and-score-spark-machine-learning-models-on-sql-server-big-data-clusters"></a>建立、 匯出和 Spark 機器學習模型進行評分上 SQL Server 的巨量資料叢集

下列範例示範如何使用建置模型[Spark ML](https://spark.apache.org/docs/latest/ml-guide.html)，匯出模型，才能[MLeap](http://mleap-docs.combust.ml/)，及評分的模型中使用的 SQL Server 及其[Java 語言擴充功能](../language-extensions/language-extensions-overview.md)。 這是 SQL Server 2019 巨量資料叢集的內容。

下圖說明此範例中執行的工作：

![訓練與 spark 的分數匯出](./media/spark-create-machine-learning-model/train-score-export-with-spark.png)

## <a name="prerequisites"></a>先決條件

此範例的所有檔案都都位於[ https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml ](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml)。

若要執行範例時，您也必須具有下列必要條件：

- A[巨量資料的 SQL Server 叢集](deploy-get-started.md)

- [巨量資料工具](deploy-big-data-tools.md)
   - **kubectl**
   - **curl**
   - **Azure Data Studio**

## <a name="model-training-with-spark-ml"></a>使用 Spark ML 模型訓練

對於此範例中，人口普查資料 (**AdultCensusIncome.csv**) 用來建立 Spark ML 管線模型。

1. 使用[mleap_sql_test/setup.sh](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/setup.sh)從網際網路下載的資料集，並將它放在 HDFS 中，在您的 SQL Server 巨量資料叢集的檔案。 這可讓 spark 能夠存取。

1. 然後，請下載範例 notebook [train_score_export_ml_models_with_spark.ipynb](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb)。 從 PowerShell 或 bash 命令列中，執行下列命令來下載 notebook:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb"
   ```

   此 notebook 會包含具有所需的命令，此區段的範例資料格。

1. 在 Azure 資料 Studio 中，開啟 notebook，並執行每個程式碼區塊。 如需有關使用 notebook 的詳細資訊，請參閱[如何在 SQL Server 2019 預覽中使用 notebook](notebooks-guidance.md)。

第一次讀取到 Spark 資料並分割成定型集和測試資料集。 然後程式碼使用訓練資料管線模型定型。 最後，它會將模型匯出至 MLeap 套件組合。

> [!TIP]
> 您也可以檢閱或執行 Python 程式碼中的 「 筆記本之外的這些步驟相關聯[mleap_sql_test/mleap_pyspark.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_pyspark.py)檔案。

## <a name="model-scoring-with-sql-server"></a>模型評分與 SQL Server

現在，Spark ML 管線模型在常見的序列化[MLeap 配套](http://mleap-docs.combust.ml/core-concepts/mleap-bundles.html)格式，您可以評分模型在 Java 中的沒有顯示 Spark。 

這個範例會使用[Java 語言擴充功能](../language-extensions/language-extensions-overview.md)SQL Server 中。 若要在 SQL Server 中，評分模型，必須先建置 Java 應用程式，可以將模型載入 Java 評分。 您可以尋找此 Java 應用程式中的範例程式碼[mssql mleap-應用程式資料夾](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mssql-mleap-app)。

建立範例之後, 您可以使用 TRANSACT-SQL 來呼叫的 Java 應用程式，及評分的模型與資料庫資料表。 您可以在下列[mleap_sql_test/mleap_sql_tests.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_sql_tests.py)原始程式檔。

## <a name="next-steps"></a>後續步驟

如需有關巨量資料叢集的詳細資訊，請參閱[如何部署 SQL Server 的巨量資料叢集的 Kubernetes 上](deployment-guidance.md)
